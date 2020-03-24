# Random Tips

## Using Promo Codes for Subscriptions

In App Store Connect you can generate promo codes for subscriptions, but there are several caveats to be aware of if you use them.

1. A subscription granted via promo code will not auto-renew. So if you give someone a promo code for a free month, they get that month free then the subscription ends and they have to purchase the subscription using the normal in-app flow.

2. If you give a subscription promo code for a single month to an existing subscriber, using it will cancel their existing subscription and give them a free month that won’t auto-renew.

3. If the app is a paid app, you’ll have to generate a separate promo code to download the app first.

## Missing receipts

When an app is downloaded from the App Store, there should always be a receipt in the app bundle. But there are times when that just doesn’t happen. One theory is that when a user backs up and restores their device via iTunes the receipt is not transferred with the app (likely to prevent tampering with the receipt).

You’d think iOS would automatically download a fresh receipt in cases like this, but no. This is why it’s important to handle the edge case of an app bundle without a receipt, and provide an easy to find Restore Purchases button to retrieve that receipt.

Trying to automatically download a fresh receipt in these cases seems like a good idea, but refreshing a receipt triggers a system level request for password, which many users will just cancel, so it’s best to find other ways to deal with this.

## Adding new products

Once your app is live with subscriptions, you can add new products and get them approved from App Store Connect without an app update. It's important to remember that after new products are approved, they can take 24 hours to propagate throughout the App Store and become available. Because of this, you should set up your paywall in such a way were you can enable new "offerings" of products remotely. 

1. App is live in the App Store with `monthly_product_1`.
2. You create a new `monthly_product_2` in App Store Connect and submit it for approval.
3. Apple approves `monthly_product_2`.
4. Wait 24 hours.
5. Switch your app to display `monthly_product_2` through some remote configuration setting.