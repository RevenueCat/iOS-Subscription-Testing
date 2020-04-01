# Random Tips

## Using Promo Codes for Subscriptions

You can generate promo codes for subscriptions in App Store Connect, but there are several caveats to be aware of before you decide to use them.

1. A subscription granted via promo code will not auto-renew. So if you give someone a promo code for a free month, they get that month free, then the subscription ends and they have to purchase the subscription using the normal in-app flow.

2. If you give a promo code for a free month to an existing subscriber, using it will cancel their existing subscription and give them a free month that won’t auto-renew.

3. If your app is a paid app, you’ll have to generate a separate promo code for downloading the app first.

[Apple: Promo Codes Overview](https://help.apple.com/app-store-connect/#/dev50869de4a)

## TestFlight Invites

You don’t need to collect a user’s App Store account email address in order to invite them to TestFlight. Invites can be sent to any email address. When a user taps the unique link they receive in a TestFlight email, it will associate the invite with whatever App Store account is currently logged in to that device. Future beta emails still go to the original email address, and Apple does not add the App Store account email address to your TestFlight tester list.

## Missing Receipts

When an app is downloaded from the App Store, there should always be a receipt in the app bundle. But there are times when that just doesn’t happen. One theory is that when a user backs up and restores their device using iTunes, the receipt is not transferred with the app (likely to prevent tampering with the receipt).

You’d think iOS would automatically download a fresh receipt in cases like this, but no. This is why it’s important to handle the edge case of an app bundle without a receipt and provide an easy-to-find “Restore Purchases” button to retrieve that receipt.

Trying to automatically download a fresh receipt in these cases seems like a good idea, but refreshing a receipt triggers a system-level request for a password, which many users will just cancel. So it’s best to find other ways to deal with this.

## Adding New Products

Once your app is live with subscriptions, you can add new products and get them approved from App Store Connect without an app update. It's important to remember that after new products are approved, they can take 24 hours to propagate throughout the App Store and become available. Because of this, you should set up your paywall such that you can enable new product offerings remotely. 

1. Your app is live on the App Store with `monthly_product_1`.
2. You create a new `monthly_product_2` in App Store Connect and submit it for approval.
3. Apple approves `monthly_product_2`.
4. Wait 24 hours.
5. Switch your app to display `monthly_product_2` through some remote configuration setting.

## Subscription Disclosures

Apple used to require apps to disclose all sorts of terms and conditions on any paywall screen. Those requirements have since been relaxed. You don’t even have to link to your Terms of Service and Privacy Policy on the paywall anymore (but they must be linked somewhere inside the app).

The only 3 things now required on a paywall are:

1. Title of auto-renewing subscription
2. Length of subscription
3. Price of subscription (and price per unit, if appropriate)

[Apple: Attracting Subscribers](https://developer.apple.com/app-store/subscriptions/#attracting-subscribers)

[Tweet: Jacob Eiting](https://twitter.com/jeiting/status/1137043638985216000?s=21)

## Paywall Rejections

Over the past several years Apple has gone through several rounds of tightening App Review restrictions on paywalls. As of March 2020, here are the 3 most important things to keep in mind for subscription apps:

1. Make sure the **price** is more prominent (larger font and/or more bold) than “Free Trial” or other similar language.
2. Any mention of “Free” or “Trial” must be accompanied by the actual price, even on pages/buttons that lead to your paywall.
3. The price displayed must be the actual price users are going to pay (e.g., you can’t say “$1 per month billed annually”—you must say “11.99 per year”).


___________________________________________________________________
_If you see anything that needs to be fixed or have anything to add, please submit a pull request!_
