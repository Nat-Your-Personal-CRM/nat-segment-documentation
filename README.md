# 💫 Segment < > Nat.app Documentation 



---
Nat.app Destination
---

[Nat.app](https://nat.app?utm_source=segmentio&utm_medium=docs&utm_campaign=partners) is a CRM tool for founders and sales people that makes it easy to stay in touch with users and find product market fit.

We're actively maintaining this integration. For any issues with the destination, please [reach out to us](mailto:segment@nat.app).


## Getting Started
How to get set up.

1. From your Segment UI's Destinations page click on "Add Destination".
2. Search for "Nat.app" within the Destinations Catalog and confirm the Source you'd like to connect to.
3. Drop in the "API Key" into your Segment Settings UI which you can find from your [Nat.app's settings page](https://contacts.nat.app/settings).




## Identify

Here is an example of how a Segment Identify call would look like: 

```js
analytics.identify('userId123', {
  email: 'john.doe@example.com'
});
```

Identify calls are sent to Nat.app as an `identify` event. 

**Those are the only events this integration accepts and they need to contain an `email` and a `timestamp`to be accepted**.  

Every `identify` event that contains an email will be added as an interaction to the timeline of the contact it is associated with. There can only be one event generated per day per contact, so as to keep our *closeness indicator* accurate.

Additionally, they can also include a `url` that will be added as a description to the event in the user's timeline. 


Here is an example of an `identify` even that has been added to a timeline:
![timeline example](https://mcusercontent.com/452ee2a3b01a8ea6c6b8f57d6/images/4136c810-d9f2-4dd4-909b-652c60f53fea.png)

### Accepted data format
We accept multiple types of data format, so as to make the integration as easy as possible. Let's start with the recommended format: 

#### Recommended format - with traits & page
The user email is stored in `traits` and the url in `page`.
``` 
{
"type": "identify",
"timestamp": "2020-05-31T17:55:47.263Z",
"traits": {
    "email": "peter@initech.com"
  },
"page": {
      "url": "xxxxx"
    }
}
```
#### Alternative formats
Additionally, we also accept other formats that we created to satisfy specific customer needs. Please reach out to segment@nat.app if you need a custom format.

*Example 1 - Without traits or url information*

        {
      "timestamp": "2020-05-31T17:55:47.263Z",
      "type": "identify",
      "email": "test@example.org"
    }
*Example 2 - With event information but without traits*      
In this case, the `event`will replace the `url` in the app.
   

    {
      "timestamp": "2020-05-31T17:55:47.263Z",
      "type": "identify",
      "email": "test@example.org",
      "event": "User logged in",
        
      },
    }
    


### Required & Optional data
**Required: email & timestamp**
If the integration can't identify an `email` and a `timestamp`, an error will be returned. Please follow the recommended format.

**Optional: url**
A description data point is optional and needs to be called `url`. It will be added in the timeline as shown in the image above. If there is no `url`, a standard message will be added to the timeline instead.


