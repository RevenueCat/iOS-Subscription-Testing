# Sandbox Testing

To test in the developer sandbox, the app has to be built as a developer build in Xcode. This will most often be used by the developer to quickly test on-device during the development process, but you can provision up to 100 devices per account and distribute developer builds to QA and other internal testers without having to go through TestFlight and their beta app review.

Testing in the developer sandbox requires a sandbox account. Apple’s documentation on this is good and will hopefully stay up to date: [Apple: Create a sandbox tester account](https://help.apple.com/app-store-connect/#/dev8b997bee1)

To sign in with this new sandbox account, go to the Settings app, tap iTunes & App Store, then scroll to the bottom and you should see the Sandbox Account section. Here you can log in and out of different sandbox accounts for testing. If you accidentally use a sandbox account on the production App Store, that account will no longer work in the sandbox. When in doubt, create a fresh sandbox account and re-test.

(The Sandbox Account section in the Settings app was introduced in iOS 12, when testing on iOS 11 or before, you’ll need to sign out of your production App Store account, then sign in with a test account when prompted within the app.)

## Sandbox reliability

The developer sandbox is notoriously unreliable. It’s unclear whether Apple intentionally degrades performance of the developer sandbox to mimic issues that might arise in production, or if Apple uses the developer sandbox as their own sandbox and accidentally breaks it frequently. Either way, keep in mind that even if your code is working as expected, things will sometimes go awry with the developer sandbox. When this happens it’s a great opportunity to look for ways to handle unexpected errors.

That said, **never assume an issue will magically fix itself when you launch in production**. There are certain known sandbox quirks that are documented in this guide, but you should still be able to fully test purchases end-to-end in sandbox before shipping your app.

## Subscription duration in the developer sandbox

Subscription length has been significantly shortened for testing purposes. This allows users to quickly test multiple renewals and expirations.

| Actual subscription duration  | Sandbox duration |
| --- | --- |
3 days | 2 minutes
1 week | 3 minutes
1 month | 5 minutes
2 months | 10 minutes
3 months | 15 minutes
6 months | 30 minutes
1 year | 1 hour

[Apple reference](https://help.apple.com/app-store-connect/#/dev7e89e149d)
(The 3 day duration isn’t documented anywhere, but can be found by looking at sandbox transactions)

The subscription will automatically renew ~6 times per account. After ~6 renewals the subscription will automatically stop renewing. These renewals happen automatically whether the app is open or not, just like renewals on the App Store. Unlike the App Store, there’s no option to unsubscribe or get a refund, so there’s no way to directly test those scenarios. There’s also no way to test subscription management.

Each automatic renewal is added to the payment queue. The transaction, or transactions (depending on how much time has passed), is processed the next time the app is opened. Make sure you close the app and re-open it to see the updated receipt. If you’re refreshing the receipts server-side, these additional transactions should be seen in the receipt.

## Testing procedures

**Testing renewals and expiration:**

- [ ] Subscribe to a monthly subscription
- [ ] Close the app and set a 20 minute timer
- [ ] After 20 minutes, launch the app again to make sure your app is still in the subscribed state
- [ ] Close the app and set another 20 minute timer
- [ ] After 20 more minutes (approx. 40 minutes since originally purchasing the subscription), launch the app again and it should now revert to the un-subscribed state and allow the user to re-subscribe.

**Test restoring purchases after expiration:**

- [ ] Subscribe to a monthly subscription
- [ ] Close the app and wait 35-40 minutes
- [ ] Launch the app (should revert to the un-subscribed state)
- [ ] Tap “Restore Purchases” button
- [ ] No active subscription should be found and the user should be shown a message to that effect.

**Test restoring purchases during active subscription:**

A big caveat in the sandbox environment is that there is no receipt file on the device until a purchase is made. This differs from production where a receipt file is generated at the time of install. This means that to fully test restores in sandbox, you may need to modify your app slightly in development builds.

- [ ] Subscribe to a monthly subscription
- [ ] Use a button/gesture or somehow revert app to the unsubscribed state 
- [ ] Tap “Restore Purchases” button
- [ ] If done before the 35 minute subscription cycle, an active subscription should be found and the app should change to the subscribed state.


**Test upgrades / downgrades / crossgrades:**
Changing subscription products **is not** supported in sandbox. This is a limitation of the sandbox environment and is related to the accelerated renewal rates and the in-ability to manage subscriptions.

### Important Takeaways
- Subscriptions will renew at an accelerated rate in sandbox
- Subscriptions will be automatically canceled and cannot be managed by the user
- There's no receipt available in sandbox until a purchase is made
- Upgrades / crossgrades don't work in sandbox