## Developer Sandbox Testing

To test in the developer sandbox, the app has to be built as a developer build in Xcode. This will most often be used by the developer to quickly test on-device during the development process, but you can provision up to 100 devices per account and distribute developer builds to QA and other internal testers without having to go through TestFlight and their beta app review.

Testing in the developer sandbox requires a sandbox account. Apple’s documentation on this is good and will hopefully stay up to date: [Apple: Create a sandbox tester account](Chttps://help.apple.com/app-store-connect/#/dev8b997bee1)

To sign in with this new sandbox account, go to the Settings app, tap iTunes & App Store, then scroll to the bottom and you should see the Sandbox Account section. Here you can log in and out of different sandbox accounts for testing. If you accidentally use a sandbox account on the production App Store, that account will no longer work in the sandbox. When in doubt, create a fresh sandbox account and re-test.

(The Sandbox Account section in the Settings app was introduced in iOS 12, when testing on iOS 11 or before, you’ll need to sign out of your production App Store account, then sign in with a test account when prompted within the app.)

### Sandbox reliability

The developer sandbox is notoriously unreliable. It’s unclear whether Apple intentionally degrades performance of the developer sandbox to mimic issues that might arise in production, or if Apple uses the developer sandbox as their own sandbox and accidentally breaks it frequently. Either way, keep in mind that even if your code is working as expected, things will sometimes go awry with the developer sandbox. When this happens it’s a great opportunity to look for ways to handle unexpected errors.

### Subscription duration in the developer sandbox

Subscription length has been significantly shortened for testing purposes. This allows users to quickly test multiple renewals and expirations.

Actual subscription duration -> Test duration

1 week -> 3 minutes
1 month -> 5 minutes
2 months -> 10 minutes
3 months -> 15 minutes
6 months -> 30 minutes
1 year -> 1 hour

The subscription will automatically renew 6 times per account per 8 hour window, then the subscription will automatically expire at the end of the final subscription period. These renewals happen automatically whether the app is open or not, just like renewals on the App Store. Unlike the App Store, there’s no option to cancel, so there’s no way to directly test cancelation. There’s also no way to test subscription management.

Each automatic renewal is added to the payment queue. The transaction, or transactions (depending on how much time has passed), is processed the next time the app is opened. If you’re refreshing the receipts server-side, these additional transactions should be see in the receipt.

### Testing procedures

**Testing renewals and expiration:**

1. Subscribe to a monthly subscription
2. Close the app and set a 5 minute timer
3. Launch the app
4. If prompt is displayed, enter password

At this point the app should continue to operate in the subscribed state. Repeat steps 2-4 several more times (or just close the app and wait) until 35 minutes has passed (6 renewals at 5 minutes each plus the original 5 minute subscription). The app should now revert to the un-subscribed state and allow the user to re-subscribe.

**Test restoring purchases after expiration:**

1. Subscribe to a monthly subscription
2. Close the app and wait 35 minutes
3. Launch the app
4. If prompt is displayed, enter password
[app should revert to the un-subscribed state]
5. Tap “Restore Purchases” button

No active subscription should be found and the user should be shown a message to that effect.

**Test restoring purchases during active subscription:**

Ideally, your app will automatically determine the subscription state and unlock or lock the app. But even if that’s working as expected, receipts do sometimes need to be refreshed.

1. Subscribe to a monthly subscription
2. Use the button/gesture created to revert the app to the unsubscribed state (or delete and reinstall the app)
3. If required, tap “Restore Purchases” button

If done before the 35 minute subscription cycle, an active subscription should be found (either automatically or after tapping the Restore Purchases button) and the app should change to the subscribed state.

Active subscription should be found and the app should change to the subscribed state.

**Test restoring purchases across devices:**

1. Subscribe to a monthly subscription
2. Install the app on a different device before the subscription expires
3. Launch the app
4. If required, tap “Restore Purchases” button

Active subscription should be found and the app should change to the subscribed state.