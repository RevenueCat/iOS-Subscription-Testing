# Testing Free Trials and Other Introductory Offers

Since free trials are a type of introductory offer, most subscription app developers use this feature even if they don’t realize it.

The most important thing here is to make sure your app only presents introductory offers to users that are eligible for them.

One thing to note is that once an account has redeemed an introductory offer, that account is no longer eligible for introductory offers for any product within the same subscription group. So if you test a free trial, that offer will no longer be available to that account (there doesn’t seem to be a way to reset this other than to create a fresh sandbox account).

Ideally your app should check introductory offer eligibility and hide “Free Trial” and other offer-related messaging when the user is not eligible. However, getting this wrong is a frequent cause for rejection, so err on the side of making everyone eligible instead of everyone ineligible.

## References

[Apple: Testing Introductory Offers](https://developer.apple.com/documentation/storekit/in-app_purchase/testing_introductory_offers)

[Apple: Implementing Introductory Offers in Your App](https://developer.apple.com/documentation/storekit/in-app_purchase/subscriptions_and_offers/implementing_introductory_offers_in_your_app)


___________________________________________________________________
_If you see anything that needs to be fixed or have anything to add, please submit a pull request!_