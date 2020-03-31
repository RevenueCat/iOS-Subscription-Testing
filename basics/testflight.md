# TestFlight Testing

An app distributed via TestFlight will automatically use the production sandbox environment for purchases. Users cannot be charged in a TestFlight build, but they can view the paywall and step through the purchase process without actually spending money.

Unfortunately, the production sandbox purchase process does not mimic the App Store purchase flow, which makes it confusing for beta testers. (Apple [briefly enabled](https://twitter.com/revenuecat/status/1220024020654907392?s=21) an App Store-like payment flow but quickly reverted it. Here’s hoping it comes back someday!)

## Subscription Duration in the Production Sandbox

Subscription length has been significantly shortened for testing purposes. This allows developers to quickly test multiple renewals and expirations. Check the [Sandbox Testing](https://github.com/RevenueCat/iOS-Subscription-Testing/blob/master/basics/sandbox.md#subscription-duration-in-the-developer-sandbox) section for details and caveats.

## Testing Tips

To make testing easier, it can be helpful to add a button or secret gesture to the TestFlight build of your app that switches the app between various purchase states (make sure to set a build flag that removes this in the App Store build!). And don’t forget to [mention this in the TestFlight release notes](https://github.com/RevenueCat/iOS-Subscription-Testing/blob/master/additional/testflight.md) when recruiting beta testers to help test the paywall.

Keep in mind that while TestFlight uses the production sandbox environment, the build that is submitted to TestFlight should be the same one that gets published to the App Store. If you have a backend with a staging and a production environment, this means that TestFlight runs on your production backend, but the purchases go to the production sandbox environment. A typical setup is: 

| App Version | App Store | Your Backend |
| :-------------: | :-------------: | :-----: |
| Sandbox | Sandbox | Staging |
| TestFlight | Production Sandbox | Production |
| App Store | Production | Production |

## Testing Procedures

The testing procedure in TestFlight should be [the same as in sandbox](https://github.com/RevenueCat/iOS-Subscription-Testing/blob/master/basics/sandbox.md#testing-procedures).

## References

[Apple: Testing Apps with TestFlight](https://testflight.apple.com)

[Apple: Test In-App Purchases](https://help.apple.com/app-store-connect/#/dev7e89e149d)

[Apple: Beta Testing Made Simple with TestFlight](https://developer.apple.com/testflight/)


___________________________________________________________________
_If you see anything that needs to be fixed or have anything to add, please submit a pull request!_
