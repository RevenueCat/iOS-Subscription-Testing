# Production Testing

For an app that has yet to be released on the App Store, getting an early version of the app approved is a great way to test subscriptions.

### Pre-launch Testing

1. Submit a beta version of the app to App Review. Make sure to set “Version Release” to “Manually release this version” so that the app is not released on the App Store.
2. Generate promo codes for the app. This can be done for free apps that are approved but not yet live on the App Store.
3. Download the app from the App Store using a promo code.
4. Subscribe.

Since this app has gone through approval, subscriptions will perform exactly as they will when the app is live on the App Store—including charging testers who subscribe and allowing testers to manage their subscription on the App Store app. You can give testers promo codes to let them test the app for free. Subscriptions paid for via promo code work exactly like paid subscriptions except that they don’t auto-renew.

One other thing to note here is that apps downloaded via promo codes before the app is live on the App Store don’t seem to have a proper receipt file in the download bundle. The receipt should be refreshed with a purchase, but this issue could be used to test the rare scenario where real users of the app somehow end up in a state where an accurate receipt is not contained in the app bundle.

## New Product Propagation Times

One thing to watch out for is that the app and in-app purchases (products) might not propagate to the App Store at the same time. This seems to only impact new products, not products that have previously been released with the app. **It can take more than 24 hours for a new app, app update, or new product to be available on the App Store, and the app/update might show up hours before the products can be purchased**. This means that you’ll be able to download the production version of the app, but the app won’t be able to buy any products. Be patient and try again 24+ hours after the app and products are approved.

See tips on [adding new products](https://github.com/RevenueCat/iOS-Subscription-Testing/blob/master/additional/random.md#adding-new-products) for more info.


## Testing Renewals and Expirations

Testing renewals and expirations is difficult in production since the subscriptions aren’t shortened. To test a monthly renewal in production, you have to wait a month. To test the expiration of an annual subscription, you have to wait a year. This is impractical, which is why Apple shortens subscription durations in the sandbox testing environments. If renewals and expirations are working correctly in those environments, they *should* work just fine on the App Store.

## Testing Cancelations and Refunds

Since it’s impossible to test cancellations in the sandbox environments, it’s important to test them in production.

**Testing cancelations:**

1. Subscribe to a monthly subscription.
2. Make sure the app enters the subscribed state with features unlocked.
3. Go to the App Store app and cancel the subscription.
4. Wait a minute or two to give Apple time to add the cancelation to the payment queue.
5. Reopen the app.

At this point, auto-renew should be disabled on the receipt. The app should remain in the subscribed state, then revert to the unsubscribed state after the current billing period ends.


**Testing refunds:**

1. Subscribe to a monthly subscription.
2. Make sure the app enters the subscribed state with features unlocked.
3. Contact Apple and [request a refund](https://support.apple.com/HT204084).
4. Wait a day to give Apple time to process the refund and add it to the payment queue.
5. Reopen the app.

At this point, the refund event should be read from the payment queue and the app should revert to the unsubscribed state.

**Testing the “Restore Purchase” button:**

Ideally, your app will automatically determine the subscription state and unlock or lock the app. But even if that’s working as expected, receipts sometimes need to be refreshed.

1. Subscribe to the app.
2. Delete the app, restart the device, and reinstall the app.
3. Launch the app.
4. If necessary, tap the “Restore Purchases” button.

An active subscription should be found and the app should change to the subscribed state.


___________________________________________________________________
_If you see anything that needs to be fixed or have anything to add, please submit a pull request!_