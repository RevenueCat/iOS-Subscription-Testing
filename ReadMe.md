# The Ultimate Guide to Subscription Testing on iOS
Testing App Store subscriptions is incredibly important, but also very hard to do well. Apple’s subscription related documentation is... um... _lacking_ and Apple has never been great about providing testing resources. This guide will evolve over time as Apple makes changes to subscriptions and we figure out better ways to test. **Please submit pull requests** for anything we got wrong or to provide details or tips we missed.

## The Basics

There are 3 distinct testing environments: Production (App Store), Production Sandbox (TestFlight), and Developer Sandbox. Each behaves slightly differently and needs to be tested independently.

### [1. Developer Sandbox Testing](https://github.com/RevenueCat/iOS-Subscription-Testing/blob/master/basics/developer-sandbox.md)
The developer sandbox is the first line of defense. Make sure you understand the quirks and limitations during development to save time as you move on to production testing.

### [2. Production Sandbox (TestFlight) Testing](https://github.com/RevenueCat/iOS-Subscription-Testing/blob/master/basics/production-sandbox.md)
While not especially helpful with beta testers, you should definitely spend some time testing the production sandbox before shipping.

### [3. Production Testing](https://github.com/RevenueCat/iOS-Subscription-Testing/blob/master/basics/production.md)
There are a few tricks to testing in production even before a release hits the App Store, but you’ll also want to keep testing live on the App Store as the app is updated.

## Additional Testing Strategies

### [Communicating with TestFlight Beta Testers](https://github.com/RevenueCat/iOS-Subscription-Testing/blob/master/additional/testflight.md)
The limitations of production sandbox subscription testing makes it tough for beta testers to adequately test subscriptions for you.

### [Testing Introductory Offers](https://github.com/RevenueCat/iOS-Subscription-Testing/blob/master/additional/introductory.md)
You can offer a discounted price or a free trial to new subscribers of an auto-renewable subscription so they can experience the value of your subscription before paying full price.

### [Testing Promotional Offers](https://github.com/RevenueCat/iOS-Subscription-Testing/blob/master/additional/promotional.md)
Apps with auto-renewable subscriptions can offer a discounted price for a specific duration for existing or previously subscribed customers.

### [QA Checklist](https://github.com/RevenueCat/iOS-Subscription-Testing/blob/master/additional/qa-checklist.md)
Here’s a handy checklist to make sure you’ve covered your bases while testing subscriptions.

### [Random Tips](https://github.com/RevenueCat/iOS-Subscription-Testing/blob/master/additional/random.md)
There are too many random, poorly documented behaviors to create a page for each. This is a collection of random things that might be helpful to know.
