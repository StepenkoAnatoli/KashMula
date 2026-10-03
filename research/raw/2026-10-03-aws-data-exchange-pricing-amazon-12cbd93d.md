---
url: https://aws.amazon.com/data-exchange/pricing/
retrieved: 2026-10-03
command: firecrawl scrape https://aws.amazon.com/data-exchange/pricing/ --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
title: AWS Data Exchange Pricing
---
## Select your cookie preferences

We use essential cookies and similar tools that are necessary to provide our site and services. We use performance cookies to collect anonymous statistics, so we can understand how customers use our site and make improvements. Essential cookies cannot be deactivated, but you can choose “Customize” or “Decline” to decline performance cookies.

If you agree, AWS and approved third parties will also use cookies to provide useful site features, remember your preferences, and display relevant content, including relevant advertising. To accept or decline all non-essential cookies, choose “Accept” or “Decline.” To make more detailed choices, choose “Customize.”

AcceptDeclineCustomize

## Customize cookie preferences

We use cookies and similar tools (collectively, "cookies") for the following purposes.

### Essential

Essential cookies are necessary to provide our site and services and cannot be deactivated. They are usually set in response to your actions on the site, such as setting your privacy preferences, signing in, or filling in forms.

Allowed

### Performance

Performance cookies provide anonymous statistics about how customers navigate our site so we can improve site experience and performance. Approved third parties may perform analytics on our behalf, but they cannot use the data for their own purposes.

Allowed

### Functional

Functional cookies help us provide useful site features, remember your preferences, and display relevant content. Approved third parties may set these cookies to provide certain site features. If you do not allow these cookies, then some or all of these services may not function properly.

Allowed

### Advertising

Advertising cookies may be set through our site by us or our advertising partners and help us deliver relevant marketing content. If you do not allow these cookies, you will experience less relevant advertising.

Allowed

Blocking some types of cookies may impact your experience of our sites. You may review and change your choices at any time by selecting Cookie preferences in the footer of this site. We and selected third-parties use cookies or similar technologies as specified in the [AWS Cookie Notice](https://aws.amazon.com/legal/cookies/).

CancelSave preferences

## Your privacy choices

We and our advertising partners (“we”) may use information we collect from or about you to show you ads on other websites and online services. Under certain laws, this activity is referred to as “cross-context behavioral advertising” or “targeted advertising.”

To opt out of our use of cookies or similar technologies to engage in these activities, select “Opt out of cross-context behavioral ads” and “Save preferences” below. If you clear your browser cookies or visit this site from a different device or browser, you will need to make your selection again. For more information about cookies and how we use them, read our [Cookie Notice](https://aws.amazon.com/legal/cookies/).

Allow cross-context behavioral adsOpt out of cross-context behavioral ads

To opt out of the use of other identifiers, such as contact information, for these activities, fill out the form [here](https://pulse.aws/application/ZRPLWLL6?p=0).

For more information about how AWS handles your information, read the [AWS Privacy Notice](https://aws.amazon.com/privacy/).

CancelSave preferences

## Unable to save cookie preferences

We will only store essential cookies at this time, because we were unable to save your cookie preferences.

If you want to change your cookie preferences, try again later using the link in the AWS console footer, or contact support if the problem persists.

Dismiss

 [Skip to main content](https://aws.amazon.com/data-exchange/pricing/#aws-page-content-main)

AWS Data Exchange

- More


# AWS Data Exchange Pricing

[Get started for free](https://portal.aws.amazon.com/gp/aws/developer/registration/index.html?pg=dataexprice&cta=herobtn)

[Request a pricing quote](https://aws.amazon.com/contact-us/sales-support/?pg=dataexprice&cta=herobtn)

**[DATA RECEIVERS](https://aws.amazon.com/data-exchange/pricing/#subscribers)     \|     [DATA SENDERS](https://aws.amazon.com/data-exchange/pricing/#providers)     \| [RESOURCES](https://aws.amazon.com/data-exchange/pricing/#resources)**

## Data receivers

### Fees associated with purchasing products in AWS Marketplace (based on pricing model)

**Subscription-based products:** For products that support subscription pricing, you can see a list of prices varying by subscription durations that are set by the data provider on the product’s detail page. Subscriptions can be configured to bill upfront or are billed based on a schedule, along with applicable sales taxes.

**Pay-as-you-go based products:** For products that support pay-as-you-go pricing, you can see the pricing information on the product’s detail page. You will be billed for usage during the calendar month, along with applicable sales taxes.

### Data transfer fees

Standard Amazon Simple Storage Service (S3) rates apply when importing or exporting file-based assets across AWS Regions. If you use signed URLs to export file-based assets, standard transfer rates to the internet apply. For information about data transfer costs, see [Amazon S3 pricing](https://aws.amazon.com/s3/pricing/).

### AWS service costs

You will incur charges for any AWS services you choose to store, process, or analyze the data products. Charges for each service are billed to your AWS account according to your pricing plan. See [AWS pricing](https://aws.amazon.com/pricing/) for more details.

## Data sender

### Data grants

AWS Data Exchange charges data senders for each hour a data grant is active. A data grant is active when a data receiver has accepted a data grant. The number of hours your data grants are active is added up at the end of the month to generate your monthly charges.

* * *

Region:

##### Pricing example 1

Let’s say you send a data grant for an Amazon Redshift datashare data set that will be accessible for 6 months (180 days or 4,320 hours). Once the data receiver accepts the data grant, you will be charged $.04167 per hour until your data grant expires. In total this will equal $.04167 X 4,382 active data grant hours or $180.01.

##### Pricing example 1

Let’s say that you send a data grant for an AWS Data Exchange Files data set that will be accessible for one month (31 days or 744 hours). The data set is in US East (N. Virginia) and contains 100 GB for all 31 days of the month. For the month your bill will be $33.30 , a total that includes $2.30 for storage and $31.00 for the active data grant.

### Tiered fulfillment fees

AWS Marketplace charges tiered fulfillment fees for revenue collections made by AWS for all new subscriptions to your data products. If you already have subscribers, you can [Create Bring Your Own Subscription (BYOS) offers](https://docs.aws.amazon.com/data-exchange/latest/userguide/create-byos-offers.html) to migrate and fulfill pre-existing subscriptions with AWS customers at no additional cost.

### Fees associated with your data sets

#### i) Storage fees for products containing Files

AWS Data Exchange charges customers to store data you load to the service. Your storage usage is measured in Byte-Hours that are added up at the end of the month to generate your monthly charges. You are charged less where AWS Data Exchange costs are less; prices are based on the size of data and on the Region, as shown below.

* * *

Region:

##### Pricing example

As an example, if you had a data set in US East (N. Virginia) containing 100 GB for all 31 days of a given month, and published another 100 TB to that data set with 16 days remaining in the month, you would have accumulated 42.3 quadrillion Byte-Hours of usage (\[100 GB x 31 days x (24 hours/day)\] + \[100TB x 16 days x (24 hours/day)\], which equals $1,217.89 in monthly storage charges (at $0.023/GB/month).

##### Data transfer fees

Standard S3 rates apply when importing or exporting file-based assets across AWS Regions. If you use signed URLs to export file-based assets, standard transfer rates to the internet apply. For information about data transfer costs, see [Amazon S3 pricing](https://aws.amazon.com/s3/pricing/).

#### ii) Amazon Redshift fees for products containing Amazon Redshift datashares

You may incur additional charges from Amazon Redshift to set up and use AWS Data Exchange for Amazon Redshift products. For information about Amazon Redshift data transfer charges, see [Amazon Redshift pricing](https://aws.amazon.com/redshift/pricing/).

#### iii) Amazon API Gateway fees for products containing API data sets

You may incur additional charges from API Gateway when using AWS Data Exchange for APIs. For information about additional charges, see [Amazon API Gateway pricing](https://aws.amazon.com/api-gateway/pricing/).

#### iv) Amazon S3 fees for products containing direct access to your S3 objects

You do not need to load your data to AWS Data Exchange and pay associated S3 storage fees. However, standard S3 rates apply to store your data in Amazon S3 and move objects into any storage class. For information about storage costs, see [Amazon S3 pricing](https://aws.amazon.com/s3/pricing/). When configuring direct access to your S3 objects, it is recommended to enable Requester Pays such that requesters pay for data requests and downloads from your shared Amazon S3 buckets. If you choose to disable Requester Pays, you may incur additional charges from Amazon S3 for subscribers to request and download data from your shared Amazon S3 buckets. For information about Request Pays, see [Requester Pays documentation](https://docs.aws.amazon.com/AmazonS3/latest/userguide/RequesterPaysBuckets.html).

## Additional pricing resources

[AWS Pricing Calculator](https://calculator.aws/)

Easily calculate your monthly costs with AWS.

[Get pricing assistance](https://aws.amazon.com/contact-us/sales-support-pricing/)

Contact AWS specialists to get a personalized quote.

## Connect with AWS Data Exchange

### Find data sets

Discover and subscribe to over 3,500 third-party data sets.


### Get started with AWS Data Exchange

Speak with a data expert to find solutions that enhance your business.


### Register for a workshop

Get hands-on guidance on how to use AWS Data Exchange.


Hi, I can connect you with an AWS representative or answer questions you have on AWS.

Need more info? Highlight any text to get an explanation generated with AWS generative AI.

2
