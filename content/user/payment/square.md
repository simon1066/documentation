---
title: Square WebPay
description: How to collect payments with Square 
category: payment
weight: 10
---

This page discusses Square WebPay, the currently supported interface to Square.

There was an older Square module, based on the Square Payments Form library, which was built in to Zen Cart from 1.5.5 to 1.5.8.  However, Square has deprecated this library, so the older module no longer works.  The [Square Payments Form documentation](/user/payment/square_payments_form/) is maintained for historical purposes. 

## Square WebPay
- For PHP 7, the Square WebPay is an open source module available in the Plugins library as [Square Web Payments API plugin](https://www.zen-cart.com/downloads.php?do=file&id=2345).
- For PHP 8 and above, Square WebPay is a commercial extension which should be purchased from [the developer](/user/payment/square_commercial_module/). 

![Square Modules](/images/square_payment_modules.png)
- The top one ("Square") is the old deprecated Square module.
- The bottom ("Square WebPay") one is the new Square module.

## Requirements
1. You must be using SSL on your website
1. You will need a Square account, already validated and connected with your bank. You may [create a Square merchant account here](https://squareup.com/t/f_partnerships/d_partnerpage/p_zencart/c_general/o_free_processing/u_signup/l_us?route=signup%3Fsignup_token%3D6BB5B2E676).

Please note: do NOT remove the old Square files from your Zen Cart installation  if you are running Zen Cart 1.5.7 or 1.5.8.  (These have been removed from 2.0.0 and above.)

## Installing Square Web Payments - first time 
1. If you are a developer, ask your client to turn off 2FA on Square momentarily so you can login and do this work; they can turn it back on when you're done.
1. Install the Square Web Payments module files.  Then to go to Admin > Modules > Payments > Square WebPay, and click **Install**. 
1. Double check - did you just install the module "Square WebPay"?  If you're on the module "Square," it will look very similar but won't work. 
1. Login at [https://connect.squareup.com/apps](https://connect.squareup.com/apps) to view the apps you've connected to your account.
1. Click **+** to create a New Application for your Zen Cart store. Give it a name, such as "WebPay". **You cannot delete the app or change its name once it is created, so choose carefully.**  If it's for a test installation of your site with a different URL, call it WebPay-Test or something like that.
1. Ensure you have selected the correct API version.  See [Square API Version](/user/payment/square_api_version/).
    - Version 2.0.x of Square Web Payments requires API Version 2024-11-20.
    - Version 1.2.0 of Square Web Payments requires API Version 2024-02-22.
    - Version 1.0.1 of Square Web Payments requires API Version 2022-02-16.
1. Click on the application icon that was just created (named "WebPay" or whatever name you used).
1. The environment will be Sandbox by default.  Click "Production".
1. Copy and Paste the Production Application ID into your Square WebPay configuration *Application ID* field in Zen Cart admin. 
1. Click on the OAuth tab. In the "Redirect URL" field, enter `https://YOURSTORE.com/squareWebPay_handler.php` and click **Save** at the bottom. (Ensure the URL you enter points to the correct directory or subdirectory on your server.)
1. Now click **Show** on the Production Application secret field.  Copy and Paste the secret into your Square WebPay configuration *Application Secret (OAuth)* field in Zen Cart admin.
1. In your Zen Cart admin, do the following: 
    - Click **Update** to save the new Square WebPay config values. 
    - Click the green button in the Zen Cart admin sidebar that says "Click here to login and Authorize your account."  If everything is correct, the Sort Order LED for Square WebPay will go green. 
    - Click the **Edit** button one more time.  This will fill in the Location ID field.  Click **Update**. 
1. If this isn't working, check again to be sure you are editing the "Square WebPay" module not the old "Square" module - it's easy to get the two mixed up.
 
Once you have installed and successfully tested Square Webpay, you will want to [create a cron job to refresh the Square token](/user/payment/square_avoiding_token_expiry/). 
 
## Updating Square Web Payments 

1. Follow the guidance provided by [the Square WebPay developer](/user/payment/square_commercial_module/). 
2. You may need to update your Square app on https://connect.squareup.com/apps to change the API version.  See [Square API Version](/user/payment/square_api_version/).
3. If you are switching between a test and live website, you must remove and re-install the module in Zen Cart admin.  See the remarks in the next section.

## Installing Square Web Payments in a Test environment
If you import a live site database into a test environment, please be sure to delete and re-add the Square Web Payments app per the instructions above.  You cannot just replace the Application ID and Secret, you must reinstall the app. 

The error you will see if you try this without reinstalling will look something like this:

```
Your transaction failed due to an error: [INVALID_CARD_DATA] Card nonce not found in this application environment. Please ensure an application ID belonging to the same environment is used when generating the nonce.
```

## Handling Refunds, Captures, Voids

### Refunds
When viewing a transaction in your store Admin, if it was paid using Square within the last 120 days, you will be shown the option to Refund some or all of the payment. Simply enter the amount you wish to refund. Then check the box to confirm, and click **Submit**. You will see a status message confirming the refund has been issued.

NOTE: You SHOULD do all refunds via your store Admin. While you might be able to start a refund from your Square Dashboard, that will NOT automatically update your orders in Zen Cart to show the change in status. But if you do the refund from within your Zen Cart Admin, the refund will show in both places, as well as in the customer's order-status-history, which is a more friendly experience for them.

### Captures
If you've configured the module to "authorize only" instead of automatically capturing each "purchase", then you will also see an option to Capture the previously-authorized transaction. CAPTURES MUST BE DONE WITHIN 6 DAYS, or they will be voided automatically, releasing the hold on those funds for the customer.

NOTE: Captures can ONLY be done via your store Admin. You will not see uncaptured (authorize-only) transactions in your Square Dashboard.

### Voids
If you've configured the module to "authorize only", then you will see a Void option. This can be used to cancel an Authorization and release the "hold" on those funds back to the customer.

NOTE: Voids can ONLY be done via your store Admin. You will not see authorize-only transactions in your Square Dashboard.

## Reinstalling Square Web Payments

If your access token goes bad, you can get into a state where you have to delete and reinstall Square.  Here's what you need to do to configure the module once you have reinstalled it:

1. Login at [https://connect.squareup.com/apps](https://connect.squareup.com/apps) to view the apps you've connected to your account.
1. Click on the application icon that you created (probably named "WebPay" or whatever name you used).
1. Copy and Paste the Production Application ID into your Square WebPay configuration *Application ID* field in Zen Cart admin. 
1. Click on the OAuth tab. 
1. Now click **Show** on the Production Application secret field.  Copy and Paste the secret into your Square WebPay configuration *Application Secret (OAuth)* in Zen Cart admin.
1. In your Zen Cart admin, do the following: 
  - Click **Update** to save the new Square WebPay config values. 
  - Click the green button in the Zen Cart admin sidebar that says "Click here to login and Authorize your account."  If everything is correct, the Sort Order LED for Square WebPay will go green. 
  - Click the **Edit** button one more time.  This will fill in the Location ID field.  Click **Update**. 

## Upgrading to Square Web Payments from Square Payments Form 

1. Go to Admin > Modules > Payment > Square, click **Edit**, and set Enable Square Module to false, then click **Update**.
1. Login at [https://connect.squareup.com/apps](https://connect.squareup.com/apps).  Note that you will need to pick a new name from your existing Square app .  Unfortunately you cannot rename apps. 
1. Use the Installation instructions above. 
1. Once you are certain Square Web Payments is working, Go to Admin > Modules > Payment > Square and click **Remove**. 

## Square Errors 
If you get an error from Square (in particular, "The provided OAuth access token has expired"), see [Square Error Messages](/user/payment/square_errors/). 

