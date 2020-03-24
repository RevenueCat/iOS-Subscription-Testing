# Testing Free Trials and Other Introductory Offers

Since free trials are a form of introductory offer, most subscription app developers do use this feature even if they don’t realize it.

As Apple mentions, the primary thing to test here is that your app presents introductory offers only to users that are eligible for the offer.

One thing to note is that once an account has used an introductory offer, that account is no longer eligible to use an introductory offer for any product within the same subscription group. So if you test a free trial, that free trial will no longer be available again to that account (there doesn’t seem to be a way to reset this other than to create a fresh sandbox account).

In our experience, for purposes of app review it's sufficient to always assume the user is "eligible" for the free trial since that will be the correct state for the vast majority of users. 

## References

[Apple: Testing Introductory Offers](https://developer.apple.com/documentation/storekit/in-app_purchase/testing_introductory_offers)

[Apple: Implementing Introductory Offers in Your App](https://developer.apple.com/documentation/storekit/in-app_purchase/subscriptions_and_offers/implementing_introductory_offers_in_your_app)

_If you see anything that needs to be fixed, or have anything to add, please submit a pull request!_