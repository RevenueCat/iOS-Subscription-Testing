# The Ultimate Guide to Subscription Testing on iOS
Testing App Store subscriptions is incredibly important, but also very hard to do well. Apple’s subscription-related documentation is... um... _lacking_, and Apple has never been great about providing testing resources. This guide will evolve over time as Apple makes changes to subscriptions and we figure out better ways to test. If you see anything that needs to be fixed or have anything to add, **please submit a pull request!**

## The Basics

There are 3 distinct testing environments: Production (App Store), TestFlight (Production Sandbox), and Sandbox (Developer Builds). Each behaves slightly differently and needs to be tested independently.

### [1. Sandbox Testing](basics/sandbox.md)
The developer sandbox is the first line of defense. Make sure you understand the quirks and limitations during development to save time when you move on to production testing.

### [2. TestFlight Testing](basics/testflight.md)
While not especially helpful with beta testers, you should definitely spend some time testing in the production sandbox before shipping. TestFlight behaves like the sandbox but uses production App Store accounts.

### [3. Production Testing](basics/production.md)

There are a few tricks to testing in production even before a release hits the App Store, but you’ll also want to keep testing live on the App Store as the app is updated.

## Additional Testing Strategies

### [Communicating with TestFlight Beta Testers](additional/testflight.md)
The limitations of production sandbox subscription testing makes it tough for beta testers to adequately test subscriptions for you.

### [Testing Free Trials and Other Introductory Offers](additional/introductory.md)
You can offer a discounted price or free trial of an auto-renewable subscription so new customers can experience the value of your subscription before paying full price.

### [Testing Subscription Offers](additional/offers.md)
Apps with auto-renewable subscriptions can offer a discounted price for a specific duration for existing or previously subscribed customers.

### [QA Checklist](additional/qa-checklist.md)
This handy checklist will help you make sure you’ve covered your bases while testing subscriptions.

### [Random Tips](additional/random.md)

There are too many random, poorly documented behaviors to create a page for each. This is a collection of random things that might be helpful to know.
