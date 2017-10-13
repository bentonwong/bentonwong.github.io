---
layout: post
title:      "Using Glassdoor's API for your Rails App"
date:       2017-10-13 21:12:46 +0000
permalink:  using_glassdoors_api_for_your_rails_app
---


The job search website Glassdoor (http://www.glassdoor.com) has an developer's API program (https://www.glassdoor.com/developer/index.htm) is a wonderful tool for getting intelligence on jobs and companies.

I am currently working on an Rails app that creates company objects populated by data from Glassdoor's Company API.  Although Glassdoor's documentation, instructions on formatting of the API request are relatively straight forward, there were configuration issues that did require some additional research.  Below is a guide to easily set up an Glassdoor employer API search.

**Step 1: Request an API keys**

After successfully registering, record the unique GLASSDOOR PARNTER ID and GLASSDOOR KEY values provided.

**Step 2: Add your API keys into a secret file**

After installing the [Figaro gem](https://github.com/laserlemon/figaro) to help hide the secret values, I added the keys into my config/application.yml file.  Here is an example:

```
GLASSDOOR_PARTNER_ID: 000000
GLASSDOOR_KEY: xxxxXxXXXx0
```

**Step 3: Query the Glassdoor API**

After studying the Glassdoor API documentation, I was able to successfully query the api from a controller here:
```
def glassdoor_search
  begin
     @resp = Faraday.get "http://api.glassdoor.com/api/api.htm?" do |req|
                  req.params['v'] = 1
                  req.params['format'] = "json"
                  req.params['t.p'] = ENV["GLASSDOOR_PARTNER_ID"]
                  req.params['t.k'] = ENV["GLASSDOOR_KEY"]
                  req.params['userip'] = request.remote_ip
                  req.params['useragent'] = request.env['HTTP_USER_AGENT']
                  req.params['q'] = params[:query]
                  req.params['action'] = "employers"
      end

      if @resp.success?
                  body = JSON.parse(@resp.body)
                  companies = body["response"]["employers"]
                  @exact_match = companies.select {|company| company["exactMatch"] == true}.first
                  Company.create! name: @exact_match["name"], industry: @exact_match["industry"], website:                                                   @exact_match["website"], overall_rating: @exact_match["overallRating"], square_logo:                                                         @exact_match["squareLogo"], ceo_name: @exact_match["ceo"]["name"]
                  render json: @exact_match
      else
                  @error = body["meta"["errorDetail"]]
      end
      rescue Faraday::TimeoutError
      @error = "There was a timeout. Please try again."
  end

end
```
To initiate the API call, you can send a POST request to this specific controller action and pass the desired employer as part of its params. For example, in my application, I have a button in my show.html.erb page where I set the 'query' params as the employer's name to initiate the API request for this particular company.
```
<div style="float:left;">
  <%= button_to "Get Company Info from Glassdoor", search_path(query: @company.name), method: :post %>
 </div>
```

IMPORTANT: Glassdoor's API has many required fields, including providing the client's or user's ip address and agent.  Using "request.env['HTTP_USER_AGENT'] and "request.remote_ip" respectively, when setting the above query parameters will return those required values in Ruby.

After that, the data comes through which can be saved into a response variable (such as @resp) and can be parsed as JSON data.

Because there may be companies with similar names, Glassdoor will likely return other close matches.  In the response data, which the API returns as an array of hash objects, you can filter for "true" on the exactMatch key provided by Glassdoor.

Happy coding!
