---
layout: post
title:      "Deleting Ruby Objects with Associated Child Objects"
date:       2018-02-18 15:03:24 +0000
permalink:  deleting_ruby_objects_with_associated_child_objects
---


Deleting a Ruby object is usually a simple process.  However, it gets complicated if that object has a child object(s) that belongs to that parent object.

The deletion process could potentially orphan those child objects.  Without their parent associations, applying certain methods that depend on those associations may no longer work and throw an error.

1. delete the child components first
2. delete parent components last

For example, we have these models:

```
class Post
     has_many :comments

end

class Comments
     belongs_to :post

end
```

An simple and effective way to delete an instance of a post is:

1) Delete the child objects first with .destroy

`@post.comments.destroy`

2) After all child objects are deleted, then the parent object can be deleted with .destroy

`@post.destroy`

Putting this together in a controller:

```
class PostsController < ApplicationController

     def destroy
          @post.comments.destroy
          @post.destroy
     end

end
```

If this were done in the reverse order (i.e. by destroying the parent object first), then its children without any other parents, will be orphaned since the parent object no longer exists.  Those child components may have to be deleted by other means or associated with another parent object.
 
.**destroy vs. .delete**

Both methods are used to remove records, however there are subtle differences between the two.  According to the rubyonrails.org documentation, "no callbacks are executed" on .delete. Delete merely executes a SQL query on the database without any other ActiveRecord tasks. .delete does not delete children objects.  With .destroy, there are ActiveRecord callbacks which performs some validation and examines dependencies.  

Another key difference, .destroy will destroy the parent object and its children.  **.destroy should not be used if other parent objects still depend on those children objects.**
