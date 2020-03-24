# TestFlight Testing

An app distributed via TestFlight will automatically use the production sandbox environment for purchases. Users can not be charged in a TestFlight build, but they can view the paywall and step through the purchase process without actually spending money.

Unfortunately, the production sandbox purchase process does not mimic the App Store purchase flow, which makes it even more confusing for beta testers. (Apple [briefly enabled](https://twitter.com/revenuecat/status/1220024020654907392?s=21) an App Store-like payment flow, but quickly reverted it. Here’s hoping it comes back some day)

## Subscription duration in the production sandbox

As with the developer sandbox, subscription length has been significantly shortened for testing purposes in the production sandbox. This allows you to quickly test multiple renewals and expirations.

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

### Testing Tips

To make testing easier, it can be helpful to add a button or secret gesture to the TestFlight build of your app that switches the app between various purchase states (make sure to set a build flag that removes this in the App Store build!). Make sure to [mention this in the TestFlight release notes](additional/testflight.md) to recruit a few beta testers in helping to test the paywall.

## Testing procedures

The testing procedure in TestFlight should be [the same as in sandbox](basics/sandbox.md#testing-procedures).