# Sandbox Testing

To test in the developer sandbox, the app has to be built as a developer build in Xcode. Developers often use this to quickly test on-device during the development process, but you can also provision devices and distribute developer builds to QA and other internal testers without having to go through TestFlight and their beta app review. To prevent apps from being distributed widely outside the App Store, Apple limits device provisioning to 100 per device type (iPhone, iPad, Apple Watch, Apple TV, and Mac) for a total of 500 devices.

Testing in the developer sandbox requires a sandbox account. Apple’s [documentation](https://help.apple.com/app-store-connect/#/dev8b997bee1) on this is good and will hopefully stay up to date. You can also automatically generate sandbox accounts with [Fastlane](https://github.com/fastlane/fastlane/blob/master/spaceship/docs/AppStoreConnect.md#testers). 

To sign in with your new sandbox account for the first time, you must attempt to make a purchase in a developer build of your app. Once you have logged into a sandbox account using this method, you can then go to the Settings app, tap “iTunes & App Store”, then scroll to the bottom to the Sandbox Account section. Here you can log in and out of different sandbox accounts for testing. If you accidentally use a sandbox account on the production App Store, that account will no longer work in the sandbox. When in doubt, create a fresh sandbox account and retest.

(The Sandbox Account section of the Settings app was introduced in iOS 12. When testing on iOS 11 or before, you’ll need to sign out of your production App Store account, then sign in with a test account when prompted within the app.)

Although they should work independently, we've noticed that if your device is logged in with a production account and a sandbox account simultaneously, sandbox purchases don't work. If possible, we recommend signing in only to your sandbox account on test devices. 

### Sandbox Reliability

The developer sandbox is notoriously unreliable. It’s unclear whether Apple intentionally degrades performance of the developer sandbox to mimic issues that might arise in production, or if Apple uses the developer sandbox as their own sandbox and accidentally breaks it frequently. Either way, keep in mind that even if your code is working as expected, things will sometimes go awry with the developer sandbox. When this happens, it’s a great opportunity to look for ways to handle unexpected errors.

That said, **never assume an issue will magically fix itself when you launch in production**. There are certain known sandbox quirks that are documented in this guide, but you should still be able to fully test purchases end to end in sandbox before shipping your app.

## Subscription Duration in the Developer Sandbox

Subscription length has been significantly shortened for testing purposes. This allows developers to quickly test multiple renewals and expirations.

| Actual Subscription Duration  | Sandbox Duration |
| --- | --- |
3 days | 2 minutes
1 week | 3 minutes
1 month | 5 minutes
2 months | 10 minutes
3 months | 15 minutes
6 months | 30 minutes
1 year | 1 hour

(The 3-day duration isn’t documented anywhere but can be found by looking at sandbox transactions.)

The subscription will automatically renew up to 6 times per account. The actual number of renewals is random. After at most 6 renewals, the subscription will automatically stop renewing. These renewals happen automatically whether the app is open or not, just like renewals on the App Store. Unlike on the App Store, there’s no option to unsubscribe or get a refund, so there’s no way to directly test those scenarios. There’s also no way to test subscription management.

Each automatic renewal is added to the payment queue. The transaction (or transactions, depending on how much time has passed) is processed the next time the app is opened. Make sure you close the app and reopen it to see the updated receipt. If you’re refreshing the receipts server-side, these additional transactions should be visible in the receipt.

## Billing Issues in Sandbox

When testing sandbox subscriptions, Apple will randomly generate billing issues as a test of your app's error handling capabalities. These will only occur for renewals, so you'll always be able to make an initial purchase.

## Testing Procedures

**Testing renewals and expiration:**

1. Subscribe to a monthly subscription.
2. Close the app and set a 20-minute timer.
3. After 20 minutes, launch the app again to make sure your app is still in the subscribed state.
4. Close the app and set another 20-minute timer.
5. After 20 more minutes (approx. 40 minutes since originally purchasing the subscription), launch the app again. It should now revert to the unsubscribed state and allow the user to resubscribe.

**Test restoring purchases after expiration:**

1. Subscribe to a monthly subscription.
2. Close the app and wait 35-40 minutes.
3. Launch the app (it should revert to the un-subscribed state).
4. Tap the “Restore Purchases” button.
5. No active subscription should be found, and the user should be shown a message to that effect.

**Test restoring purchases during active subscription:**

One big caveat in the sandbox environment is that there is no receipt file on the device until a purchase is made. This differs from the production sandbox and production environments, where a receipt file is generated at the time of installation. To fully test restores in the sandbox, you need to add a button, gesture, or other means to revert the app to the unsubscribed state.

1. Subscribe to a monthly subscription.
2. Use a button/gesture to revert the app to the unsubscribed state. 
3. Tap the “Restore Purchases” button.
4. If done before the 35-minute subscription cycle, an active subscription should be found, and the app should change to the subscribed state.

**Test restoring purchases across devices:**

1. Subscribe to a monthly subscription on device A.
2. Install the app on a device B before the subscription expires.
3. On device B, log into the same sandbox account that was used on device A.
4. Launch the app on device B.
5. Tap the “Restore Purchases” button.

**Test upgrades, downgrades, and crossgrades:**

Because the sandbox environment doesn’t have a subscription management UI like the production App Store, you’ll need to expose buttons or other means within the app to test purchases that trigger upgrades, downgrades, and cross grades.

## Important Takeaways
- Subscriptions renew at an accelerated rate in sandbox
- Subscriptions are automatically canceled and cannot be managed by the user
- There's no receipt available in sandbox until a purchase is made
- Upgrades/crossgrades don't work in sandbox

## References

[Apple: Test In-App Purchases](https://help.apple.com/app-store-connect/#/dev7e89e149d)

[Apple: Testing In-App Purchase Transactions](https://developer.apple.com/documentation/storekit/in-app_purchase/testing_in-app_purchase_transactions)


___________________________________________________________________
_If you see anything that needs to be fixed or have anything to add, please submit a pull request!_
