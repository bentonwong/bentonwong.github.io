---
layout: post
title:      "Using JavaScript Events To Communicate Between Two Distant React Components"
date:       2018-02-01 18:17:35 +0000
permalink:  using_javascript_events_to_communicate_between_two_distant_react_components
---


Simple communication between two React components that do not share the same parent and are distant cousins can be quite complex if using Redux dispatch to update the store or state. This strategy sends data all the way up to the common parent component and then have re-renders trickle down to all relevant components.  It can be a very roundabout way to get two distant React components to communicate with one another.

**Alternative Approach: Using An Event Listener on the Receiving Component**

What if one component just wants to trigger a callback function (little or no data exchange) of a distant component without going through Redux?  A good use case is where a modal pop-up appears above the page to confirm an action, and upon confirming that action, the modal disappears and the background page needs to immediately update to reflect that modal pop-up confirmation.  If the background page had a helper function to refresh that page, then it can be hooked up to an event listener which would trigger it as a callback to refresh that background page like this:
```
class CustomerProfile extends Component {

        componentDidMount() {
           ...
           document.addEventListener('updateTotal', () => {
                 this.refreshCustomerInfoPage();
            });
         }

        refreshCustomerInfoPage() {
        ...
        }

        render() {
        ...
        }
}
```
In the above example, this recipient component is listening for an event once the component is mounted.  However, this event listener is waiting to hear a custom event so that the component knows that an event is directed only to it.  Other standard events (e.g. click, keydown, submit) produce too much noise and are not unique enough to provide a distinguishable signal.

**Setting Up a Custom Event On the Broadcasting Component**

A custom event can be set up easily on the sender component using .dispatchEvent() and new CustomEvent like this:

```
var confirmUpdateEvent = new CustomEvent("updateTotal", {
  detail: {
             message: "update total due to modal confirmation"
  },
             bubbles: true,
             cancelable: true
  });

document.querySelector(".modal .btn-primary").dispatchEvent(confirmUpdateEvent);
```

**How the Code Works**

Above, a new custom event is created with new CustomEvent using a unique name.  The resulting custom event is passed as an argument into .dispatchEvent(). It will dispatch an event called 'updateTotal' when an event occurs on a specific page element (e.g. a button click).  .querySelector() returns the page element for that specific modal button.  Having chained that element to .dispatchEvent(), clicking on this button will broadcast the 'updateTotal'event.

Given that the underlying CustomerProfile component is still mounted with an active event listener, it will pick up 'updateTotal' event, triggering the refreshCustomerInfoPage() function to refresh its data, thus updating the data on that page.

**Dismounting the Event Listener**

To prevent the callback from being triggered when the page is no longer being rendered, the listener for that event should be removed when the recipient component is unmounted:

```
componentWillUnmount() {
         document.removeEventListener('updatePoints');
 }
```
.removeEventListener() works very well for this purpose.
