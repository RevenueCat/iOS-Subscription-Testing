## Communicating with TestFlight Beta Testers

Because of the limitations of testing subscriptions via TestFlight (especially the short duration of subscriptions in the production sandbox), many developers choose to automatically unlock all features for beta testers.

One thing you definitely don’t want to do is rely on beta testers in TestFlight to test price or willingness to pay, A/B test paywalls, or anything else of the sort. Apple doesn’t allow developers to actually charge TestFlight users, and many beta testers know that, so results would be skewed. And even if Apple did allow developers to charge TestFlight users, they are typically some of your most loyal users, not at all a representative sample of people coming to the app for the first time.

All that said, it can be helpful to have a few beta testers at least view the paywall and/or walk through the steps from triggering the paywall all the way to making a sandbox purchase. The tricky part is explaining this process to testers and doing it in a way that will result in helpful feedback.

Most people don’t read, at best they skim. So, locking everyone out of the premium features and mentioning the limitations in the beta release notes isn’t a great option. You end up with confused beta testers who don’t get to test all the premium features.

One option is to unlock all features for beta testers, then mention paywall testing instructions in the release notes. That way, the people who actually read the notes can help with paywall testing and everyone else can help test the premium features.


As mentioned in the [Production Sandbox Testing section](basics/testflight.md), it can be helpful for testing to add a button or secret gesture to the TestFlight build that will revert the app to the free state and allow beta testers in the know to turn this on and encounter the paywall as normal users would once the app is live on the App Store. 

___________________________________________________________________
_If you see anything that needs to be fixed or have anything to add, please submit a pull request!_
