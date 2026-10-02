---
url: https://medium.com/@yogendramanawat/accept-payments-in-your-saas-using-lemonsqueezy-68075b7e01b1
retrieved: 2026-10-02
command: firecrawl scrape https://medium.com/@yogendramanawat/accept-payments-in-your-saas-using-lemonsqueezy-68075b7e01b1 --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
title: Accept payments in your SaaS using LemonSqueezy. | by Yogendra Manawat | Medium
---
[Sitemap](https://medium.com/sitemap/sitemap.xml)

[Open in app](https://play.google.com/store/apps/details?id=com.medium.reader&referrer=utm_source%3DmobileNavBar&source=---top_nav_layout_nav-------------------------------------------)

Sign up

[Sign in](https://medium.com/m/signin?operation=login&redirect=https%3A%2F%2Fmedium.com%2F%40yogendramanawat%2Faccept-payments-in-your-saas-using-lemonsqueezy-68075b7e01b1&source=post_page---top_nav_layout_nav-----------------------global_nav--------------------)

[Medium Logo](https://medium.com/?source=---top_nav_layout_nav-------------------------------------------)

Get app

[Write](https://medium.com/m/signin?operation=register&redirect=https%3A%2F%2Fmedium.com%2Fnew-story&source=---top_nav_layout_nav-----------------------new_post_topnav--------------------)

[Search](https://medium.com/search?source=---top_nav_layout_nav-------------------------------------------)

Sign up

[Sign in](https://medium.com/m/signin?operation=login&redirect=https%3A%2F%2Fmedium.com%2F%40yogendramanawat%2Faccept-payments-in-your-saas-using-lemonsqueezy-68075b7e01b1&source=post_page---top_nav_layout_nav-----------------------global_nav--------------------)

![Unknown user](https://miro.medium.com/v2/resize:fill:32:32/1*dmbNkD5D-u45r44go_cf0g.png)

[SaaS](https://medium.com/tag/saas?source=post_page---header_tags--68075b7e01b1-----------------------------------------)

[Lemon Squeezy](https://medium.com/tag/lemon-squeezy?source=post_page---header_tags--68075b7e01b1-----------------------------------------)

[Payments](https://medium.com/tag/payments?source=post_page---header_tags--68075b7e01b1-----------------------------------------)

[Payment Integration](https://medium.com/tag/payment-integration?source=post_page---header_tags--68075b7e01b1-----------------------------------------)

# Accept payments in your SaaS using LemonSqueezy.

[![Yogendra Manawat](https://miro.medium.com/v2/da:true/resize:fill:32:32/0*HfhIQ_OLCbe0ARhr)](https://medium.com/@yogendramanawat?source=post_page---byline--68075b7e01b1-----------------------------------------)

[Yogendra Manawat](https://medium.com/@yogendramanawat?source=post_page---byline--68075b7e01b1-----------------------------------------)

Follow

8 min read

·

Feb 25, 2024

106

1

[Listen](https://medium.com/m/signin?actionUrl=https%3A%2F%2Fmedium.com%2Fplans%3Fdimension%3Dpost_audio_button%26postId%3D68075b7e01b1&operation=register&redirect=https%3A%2F%2Fmedium.com%2F%40yogendramanawat%2Faccept-payments-in-your-saas-using-lemonsqueezy-68075b7e01b1&source=---header_actions--68075b7e01b1---------------------post_audio_button--------------------)

Share

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*zhdDwiM9b6FBR2YB-74afg.png)

lemon squeezy landing page

### What is Lemon Squeezy?

It’s the ultimate tool for SaaS businesses, handling payments, taxes, subscriptions, and fraud prevention, making your life easier. With LemonSqueezy, you can focus on growing your business while it takes care of the complicated stuff. Whether it’s processing payments worldwide, preventing fraud, or managing subscriptions seamlessly, LemonSqueezy has you covered. In this blog, I’ll guide you on how you can easily integrate LemonSqueezy into your SaaS business.

The tasks we will be doing:

1. **Setup Lemon Squeezy**: Sign up at Lemon Squeezy and set up your store and products to start taking payments.
2. **Create custom checkouts**: Creating custom checkouts according to the customer will help you identify who paid the payment, and you can count that in your code.
3. **Setup webhooks**: Webhooks are a way to send data from one system to another when an event occurs, such as payment success or failure. Lemon Squeezy sends a POST request with the data.
4. **Count usage (usage-based billing/ credit-based billing)**: We will look at how we can count usage and deduct it from the user’s plan.
5. **Customer Portal (additional)**: Whenever a user buys a plan at your store, a customer portal gets created for the user, where they can see their purchased plans and modify them as well.
6. **Activate your store**: Activate your store to start getting some real payments.

## Setup Lemon Squeezy

Sign up for Lemon Squeezy and create an account. After that, create a store. Make sure you have test mode ON. On publishing the store, it will turn OFF; check on the bottom left side.

![](https://miro.medium.com/v2/resize:fit:272/1*92VvOMiP3f9nHhR8LhTqOA.png)

Now, set up the products. If you have multiple plans, you can either create individual products or variants of one product only. If you create variants, all the variants will be visible on checkout where the user can choose from.

Go to [https://app.lemonsqueezy.com/products](https://app.lemonsqueezy.com/products) to add some products. There are multiple pricing options for creating products: Single Payment, Subscription, and Pay-What-You-Want.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/0*SXlMl9gJ4Sv2FJZk)

In this, we have multiple pricing model options: standard pricing, package pricing, graduating pricing, and volume pricing. All these are different from each other; you can read more at [https://docs.lemonsqueezy.com/help/products/pricing-models](https://docs.lemonsqueezy.com/help/products/pricing-models).

In simple words for a subscription, **Standard pricing** is just a single payment in an interval like $49 per month. **Package pricing** has a minimum and maximum unit count and price according, like $49 for 0–100 units and $100 for 100–250 units. But it’s again a single amount according to the unit count. **Graduating pricing** is more flexible; it’s like a flat fee + $2/unit till 100 units and $1/unit more than that.

You can also add usage-based billing with these, but then the person will not be charged at first. Read more at [https://docs.lemonsqueezy.com/help/products/usage-based-billing](https://docs.lemonsqueezy.com/help/products/usage-based-billing).

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/0*3_TO6cuKj1KcECiU)

After setting up the product properly according to your needs, we have to create custom checkouts using code so that we can know who is making the payment and count that in our database. But before that, we will require some data to fill like **store ID** and **variant ID**. Go to settings for that, here, we have store ID #49595.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*0UhZqwBovE0d9bUZzc3bSg.png)

sores in settings

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*nW8Q3k_bQdCCtC9BA06sig.png)

copy variant ID from product details from the product page

If you choose to create multiple variants in a single product then copy the ID of variants from

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*Dxqr2EjNvmPOEY_9menBow.png)

### Get an API Key

Now let’s get an API key from settings. Create one key choose any name, copy the key, and save it in your .env.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*gWJONW8ceMl49IrbcD0uhw.png)

## Create custom checkout

To create a custom checkout with LemonSqueezy, we need to go beyond the default checkout process, which only collects email for identification. Instead, we’ll create a checkout that sends custom data along with the purchase, allowing us to receive specific information through webhooks provided by LemonSqueezy.

## Get Yogendra Manawat’s stories in your inbox

Join Medium for free to get updates from this writer.

Subscribe

Subscribe

Remember me for faster sign in

Below is an example of the request and payload you need to send to LemonSqueezy to create a custom checkout:

```
curl -X "POST" "https://api.lemonsqueezy.com/v1/checkouts" \
     -H 'Accept: application/vnd.api+json' \
     -H 'Content-Type: application/vnd.api+json' \
     -H 'Authorization: Bearer {api_key}' \
     -d $'{
  "data": {
    "type": "checkouts",
    "attributes": {
      "product_options": {
        //add the variant ids to show at the checkout,
        "enabled_variants": [57839]
      },
      "checkout_options": {
        //you can set the color of button according your theme
        "button_color": "#2DD272"
      },
      // this checkout data will get filled automatically in the checkout
      "checkout_data": {
        "email": "yogendramanawat@gmail.com",
        "name": "Yogendra Manawat",
        // this is the custom data we will get back in webhooks
        "custom": {
          "planName": "BASIC_PLAN",
          "userId": "123"
        },
        // here we can set the quantities of each variant we have like credits in each of the plans
        "variant_quantities": []
      },
      "expires_at": "",
      "preview": false
    },
    "relationships": {
      "store": {
        "data": {
          "type": "stores",
          // put the id of store here
          "id": 5373
        }
      },
      "variant": {
        "data": {
          "type": "variants",
          // put variant id here
          "id": 1346
        }
      }
    }
  }
}'
```

By following the URL provided in the response (`response.data.attributes.url`), users will be directed to the checkout page where they can make payments. for more read here: [https://docs.lemonsqueezy.com/api/checkouts#create-a-checkout](https://docs.lemonsqueezy.com/api/checkouts#create-a-checkout)

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*_0FZqxTCl0gTAAe9JPMFjA.png)

Here the user will make the payment, and LemonSqueezy will then send webhook events for successful or failed payments. Now, let’s set up the webhooks.

## Setup webhook

Well as you know Webhooks are a way to send data from one system to another when an event occurs.

Lemon Squeezy will notify us for the success or failure of our payment by sending a POST API request, so therefore first we need to create an endpoint in our backend server to process this webhook API call.

Setting up webhooks involves providing LemonSqueezy with a URL where they can send data when events like payment success or failure occur. You can set up your URL like `www.yourdomain.com/lemonSqueezy_webhook`. For testing locally, you can use NGROK and put that link in LemonSqueezy settings. Go to the settings and choose webhooks. set your URL as the callback URL.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*iSzddIbOo9slF3aUM2PPiA.png)

Choose all the events you want feedback on.

![](https://miro.medium.com/v2/resize:fit:533/1*Dj90HsEXqTxUPU-4qwZaBQ.png)

to know about the events Lemon Squeezy has read here [https://docs.lemonsqueezy.com/help/webhooks#event-types](https://docs.lemonsqueezy.com/help/webhooks#event-types)

### Payload structure of Webhooks

```
{
  "data": {
    "id": "646575",
    "type": "subscription-invoices",
    "links": {
      "self": "https://api.lemonsqueezy.com/v1/subscription-invoices/646575"
    },
    "attributes": {
      "tax": 882,
      "urls": {
        "invoice_url": "https://app.lemonsqueezy.com/my-orders/c61e5ec9-d3f6-4da0-a21c-79b785006ca9/subscription-invoice/646575?signature=3456789"
      },
      "total": 5782,
      "status": "paid",
      "tax_usd": 882,
      "currency": "USD",
      "refunded": false,
      "store_id": 49595,
      "subtotal": 4900,
      "test_mode": true,
      "total_usd": 5782,
      "user_name": "Yogendra Manawat",
      "card_brand": "visa",
      "created_at": "2024-02-14T06:57:08.000000Z",
      "updated_at": "2024-02-14T07:57:31.000000Z",
      "user_email": "yogendramanawat@gmail.com",
      "customer_id": 1836511,
      "refunded_at": null,
      "subtotal_usd": 4900,
      "currency_rate": "1.00000000",
      "tax_formatted": "$8.82",
      "tax_inclusive": false,
      "billing_reason": "renewal",
      "card_last_four": "4242",
      "discount_total": 0,
      "subscription_id": 207468,
      "total_formatted": "$57.82",
      "status_formatted": "Paid",
      "discount_total_usd": 0,
      "subtotal_formatted": "$49.00",
      "discount_total_formatted": "$0.00"
    },
    "relationships": {
      "store": {
        "links": {
          "self": "https://api.lemonsqueezy.com/v1/subscription-invoices/646575/relationships/store",
          "related": "https://api.lemonsqueezy.com/v1/subscription-invoices/646575/store"
        }
      },
      "customer": {
        "links": {
          "self": "https://api.lemonsqueezy.com/v1/subscription-invoices/646575/relationships/customer",
          "related": "https://api.lemonsqueezy.com/v1/subscription-invoices/646575/customer"
        }
      },
      "subscription": {
        "links": {
          "self": "https://api.lemonsqueezy.com/v1/subscription-invoices/646575/relationships/subscription",
          "related": "https://api.lemonsqueezy.com/v1/subscription-invoices/646575/subscription"
        }
      }
    }
  },
  "meta": {
    "test_mode": true,
    "event_name": "subscription_payment_success",
    "webhook_id": "6f7eb0ad-45b1-43c6-ba88-a50f8da4f3bd",
    "custom_data": {
      "planName" : "BASIC_PLAN",
      "userId": "123",
    }
  }
}
```

The payload structure of webhooks includes various data, but for our purposes, we are primarily interested in the `meta` object:

```
{
  "data": {...},

  "meta": {
    "test_mode": true,
    "event_name": "subscription_payment_success",
    "webhook_id": "6f7eb0ad-45b1-43c6-ba88-a50f8da4f3bd",
    "custom_data": {
      "planName" : "BASIC_PLAN",
      "userId": "123",
    }
  }

}
```

This `meta` object contains custom data we sent with the checkout, such as the plan name and user ID. With this information, you can update your database accordingly, marking which plan the user has chosen and any other relevant details like credits or whatever you want.

## **Customer Portal**

If you want to allow your users to see the track of their past payments, you can send a user to the customer portal using the `customer_id` you will get in the webhook payload (`body.data.attributes.customer_id`).

Now request Lemon Squeezy to get the customer portal of that user, these customer portal links normally last 24 hours only.

`GET /v1/customers/:id`

```
curl "https://api.lemonsqueezy.com/v1/customers/customer_id_here"
     -H 'Accept: application/vnd.api+json'
     -H 'Content-Type: application/vnd.api+json'
     -H 'Authorization: Bearer {api_key}'
```

You will get a whole customer object in response.

```
{
  "jsonapi": {
    "version": "1.0"
  },
  "links": {
    "self": "https://api.lemonsqueezy.com/v1/customers/1"
  },
  "data": {
    "type": "customers",
    "id": "1",
    "attributes": {
      "store_id": 1,
      "name": "Luke Skywalker",
      "email": "lukeskywalker@example.com",
      "status": "subscribed",
      "city": null,
      "region": null,
      "country": "US",
      "total_revenue_currency": 84332,
      "mrr": 1999,
      "status_formatted": "Subscribed",
      "country_formatted": "United States",
      "total_revenue_currency_formatted": "$843.32",
      "mrr_formatted": "$19.99",
      "urls": {
        "customer_portal": "https://my-store.lemonsqueezy.com/billing?expires=1666869343&signature=23456787654"
      },
      "created_at": "2022-12-01T13:01:07.000000Z",
      "updated_at": "2022-12-09T09:05:21.000000Z",
      "test_mode": false
    },
    "relationships": {...}
  }
}
```

You will get the customer portal URL at (`response.data.data.attributes.urls.customer_portal`)

### Activate Your Store

To activate your store, navigate to the left side and click on “Activate Store.” Complete the setup by providing your real business name, business website URL, and any other necessary details. If you’ve already completed this step, simply turn off the test mode. Don’t forget to add payout methods for withdrawing payments. And that’s it! Your store is now ready to start accepting payments.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*NHQq5FJK6AHHukE4g0C6Wg.png)

That’s it.

In conclusion, integrating LemonSqueezy into your SaaS business is straightforward. Simply set up your store and products on LemonSqueezy, configure your payout methods, and optionally customize your checkout process. With LemonSqueezy handling payments, taxes, and subscriptions, you can focus on growing your business hassle-free.

Will discuss usage-based in another blog. Thanks for reading, and happy selling with LemonSqueezy!

[SaaS](https://medium.com/tag/saas?source=post_page---footer_tags--68075b7e01b1-----------------------------------------)

[Lemon Squeezy](https://medium.com/tag/lemon-squeezy?source=post_page---footer_tags--68075b7e01b1-----------------------------------------)

[Payments](https://medium.com/tag/payments?source=post_page---footer_tags--68075b7e01b1-----------------------------------------)

[Payment Integration](https://medium.com/tag/payment-integration?source=post_page---footer_tags--68075b7e01b1-----------------------------------------)

[![Yogendra Manawat](https://miro.medium.com/v2/resize:fill:48:48/0*HfhIQ_OLCbe0ARhr)](https://medium.com/@yogendramanawat?source=post_page---post_author_info--68075b7e01b1-----------------------------------------)

[![Yogendra Manawat](https://miro.medium.com/v2/resize:fill:64:64/0*HfhIQ_OLCbe0ARhr)](https://medium.com/@yogendramanawat?source=post_page---post_author_info--68075b7e01b1-----------------------------------------)

Follow

[**Written by Yogendra Manawat**](https://medium.com/@yogendramanawat?source=post_page---post_author_info--68075b7e01b1-----------------------------------------)

[49 followers](https://medium.com/@yogendramanawat/followers?source=post_page---post_author_info--68075b7e01b1-----------------------------------------)

· [4 following](https://medium.com/@yogendramanawat/following?source=post_page---post_author_info--68075b7e01b1-----------------------------------------)

AI Researcher

Follow

[Help](https://help.medium.com/hc/en-us?source=post_page-----68075b7e01b1-----------------------------------------)

[Status](https://status.medium.com/?source=post_page-----68075b7e01b1-----------------------------------------)

[About](https://medium.com/about?autoplay=1&source=post_page-----68075b7e01b1-----------------------------------------)

[Careers](https://medium.com/jobs-at-medium/work-at-medium-959d1a85284e?source=post_page-----68075b7e01b1-----------------------------------------)

[Press](mailto:pressinquiries@medium.com)

[Blog](https://blog.medium.com/?source=post_page-----68075b7e01b1-----------------------------------------)

[Store](https://medium.com/store)

[Privacy](https://policy.medium.com/medium-privacy-policy-f03bf92035c9?source=post_page-----68075b7e01b1-----------------------------------------)

[Rules](https://policy.medium.com/medium-rules-30e5502c4eb4?source=post_page-----68075b7e01b1-----------------------------------------)

[Terms](https://policy.medium.com/medium-terms-of-service-9db0094a1e0f?source=post_page-----68075b7e01b1-----------------------------------------)

[Text to speech](https://speechify.com/medium?source=post_page-----68075b7e01b1-----------------------------------------)
