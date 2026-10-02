---
url: https://docs.stripe.com/payouts
retrieved: 2026-10-02
command: firecrawl scrape https://docs.stripe.com/payouts --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
title: Receive payouts | Stripe Documentation
---
hCaptcha

hCaptcha

Please try again. ⚠️

Verify

Afrikaans

Albanian

Amharic

Arabic

Armenian

Azerbaijani

Basque

Belarusian

Bengali

Bulgarian

Bosnian

Burmese

Catalan

Cebuano

Chinese

Chinese Simplified

Chinese Traditional

Corsican

Croatian

Czech

Danish

Dutch

English

Esperanto

Estonian

Finnish

French

Frisian

Gaelic

Galacian

Georgian

German

Greek

Gujurati

Haitian

Hausa

Hawaiian

Hebrew

Hindi

Hmong

Hungarian

Icelandic

Igbo

Indonesian

Irish

Italian

Japanese

Javanese

Kannada

Kazakh

Khmer

Kinyarwanda

Kirghiz

Korean

Kurdish

Lao

Latin

Latvian

Lithuanian

Luxembourgish

Macedonian

Malagasy

Malay

Malayalam

Maltese

Maori

Marathi

Mongolian

Nepali

Norwegian

Nyanja

Oriya

Persian

Polish

Portuguese (Brazil)

Portuguese (Portugal)

Pashto

Punjabi

Romanian

Russian

Samoan

Shona

Sindhi

Sinhalese

Serbian

Slovak

Slovenian

Somali

Southern Sotho

Spanish

Sundanese

Swahili

Swedish

Tagalog

Tajik

Tamil

Tatar

Teluga

Thai

Turkish

Turkmen

Uyghur

Ukrainian

Urdu

Uzbek

Vietnamese

Welsh

Xhosa

Yiddish

Yoruba

Zulu

EN

[hCaptcha logo, opens new window with more information](https://www.hcaptcha.com/what-is-hcaptcha-about?ref=b.stripecdn.com&utm_campaign=5034f7f0-a742-48aa-89e2-062ece60f0d6&utm_medium=challenge&hl=en "hCaptcha logo, opens new window with more information")

[Skip to content](https://docs.stripe.com/payouts#main-content)

Receive payouts

[Create account](https://dashboard.stripe.com/register) or [Sign in](https://dashboard.stripe.com/login?redirect=https%3A%2F%2Fdocs.stripe.com%2Fpayouts)

[The Stripe Docs logo](https://docs.stripe.com/)

Search

`/`Ask AI

[Create account](https://dashboard.stripe.com/register) [Sign in](https://dashboard.stripe.com/login?redirect=https%3A%2F%2Fdocs.stripe.com%2Fpayouts)

APIs & SDKsHelp

[Overview](https://docs.stripe.com/payments) [Accept a payment](https://docs.stripe.com/payments/accept-a-payment)

Online payments

[Overview](https://docs.stripe.com/payments/online-payments) [Find your use case](https://docs.stripe.com/payments/use-cases/get-started)

Use Payment Links

Build a payments page

Build a custom integration with Elements

Build an in-app integration

Use Managed Payments

[Recurring payments](https://docs.stripe.com/recurring-payments) [Migrate legacy integrations](https://docs.stripe.com/payments/migrations)

In-person payments

Terminal overview

[Availability](https://docs.stripe.com/terminal/payments/collect-card-payment/supported-card-brands)

Readers

Ready-made apps

Custom integration

Payment methods

Add payment methods

Manage payment methods

Faster checkout with Link

Payment operations

Analytics

[Balances and settlement time](https://docs.stripe.com/payments/balances)

Compliance and security

Currencies

Declines

Disputes

Payouts

Receive payouts

[Payout reconciliation](https://docs.stripe.com/payouts/reconciliation)

[Payout trace IDs](https://docs.stripe.com/payouts/trace-id)

[Payout statement descriptors](https://docs.stripe.com/payouts/statement-descriptors)

[Multi-currency settlement](https://docs.stripe.com/payouts/multi-currency-settlement)

[Next-day settlement](https://docs.stripe.com/payouts/next-day-settlement)

[Instant Payouts](https://docs.stripe.com/payouts/instant-payouts)

[Customized start of day](https://docs.stripe.com/payouts/customized-start-of-day)

[Minimum balances for automatic payouts](https://docs.stripe.com/payouts/minimum-balances-for-automatic-payouts)

[Receipts](https://docs.stripe.com/receipts) [Refunds and cancellations](https://docs.stripe.com/refunds)

Advanced integrations

Custom payment flows

Flexible acquiring

Off-Session Payments

Multiprocessor orchestration

Beyond payments

Incorporate your company

Agentic commerce

Financial Connections

Climate

United States

English (United States)

# Receivepayouts

## Set up your bank account to receive payouts.

Ask about this page

Copy for LLM

View as Markdown

Install tools

Stripe sends funds from your available balance to your bank account as payouts:

- **First payout:** After you successfully receive your first live payment, Stripe typically schedules your initial payout to complete within 7–14 days, depending on your industry, country of operation, and risk level.
- **Subsequent payouts:** Payouts follow your account’s [payout schedule](https://docs.stripe.com/payouts#payout-schedule). The time when funds become available depends on your [settlement timing](https://docs.stripe.com/payouts#payout-speed), and your bank might take additional time to make the funds available after receiving them.
- **Track a payout:** View your payouts and their expected deposit dates in the [Dashboard](https://dashboard.stripe.com/test/payouts).

If you’re a [Connect](https://docs.stripe.com/connect) platform, see [Connect payouts](https://docs.stripe.com/connect/payouts-connected-accounts).

## Add or update your bank account

You can add a bank account or update existing account details in [Payout settings](https://dashboard.stripe.com/settings/money-management) in the Dashboard. To update an account, click **Edit** next to the bank account.

The account details required depend on your bank’s location. The bank account currency must match the currency in your [Payout settings](https://dashboard.stripe.com/settings/money-management). Use the following table to find the required bank details for each country:

Albania (AL)Algeria (DZ)Angola (AO)Antigua and Barbuda (AG)Argentina (AR)Armenia (AM)Australia (AU)Austria (AT)Azerbaijan (AZ)Bahamas (BS)Bahrain (BH)Bangladesh (BD)Belgium (BE)Benin (BJ)Bhutan (BT)Bolivia (BO)Bosnia and Herzegovina (BA)Botswana (BW)Brazil (BR)Brunei (BN)Bulgaria (BG)Cambodia (KH)Canada (CA)Chile (CL)Colombia (CO)Costa Rica (CR)Côte d'Ivoire (CI)Croatia (HR)Cyprus (CY)Czech Republic (CZ)Denmark (DK)Dominican Republic (DO)Ecuador (EC)Egypt (EG)El Salvador (SV)Estonia (EE)Ethiopia (ET)Finland (FI)France (FR)Gabon (GA)Gambia (GM)Germany (DE)Ghana (GH)Gibraltar (GI)Greece (GR)Guatemala (GT)Guyana (GY)Hong Kong (HK)Hungary (HU)Iceland (IS)India (IN)Indonesia (ID)Ireland (IE)Israel (IL)Italy (IT)Jamaica (JM)Japan (JP)Jordan (JO)Kazakhstan (KZ)Kenya (KE)Kuwait (KW)Laos (LA)Latvia (LV)Liechtenstein (LI)Lithuania (LT)Luxembourg (LU)Macau (MO)Madagascar (MG)Malaysia (MY)Malta (MT)Mauritius (MU)Mexico (MX)Moldova (MD)Monaco (MC)Mongolia (MN)Morocco (MA)Mozambique (MZ)Namibia (NA)Netherlands (NL)New Zealand (NZ)Niger (NE)Nigeria (NG)North Macedonia (MK)Norway (NO)Oman (OM)Pakistan (PK)Panama (PA)Paraguay (PY)Peru (PE)Philippines (PH)Poland (PL)Portugal (PT)Qatar (QA)Romania (RO)Rwanda (RW)Saint Lucia (LC)Saudi Arabia (SA)San Marino (SM)Senegal (SN)Serbia (RS)Singapore (SG)Slovakia (SK)Slovenia (SI)South Africa (ZA)South Korea (KR)Spain (ES)Sri Lanka (LK)Sweden (SE)Switzerland (CH)Taiwan (TW)Tanzania (TZ)Thailand (TH)Trinidad & Tobago (TT)Tunisia (TN)Türkiye (TR)United Kingdom (GB)United States (US)United Arab Emirates (AE)Uruguay (UY)Uzbekistan (UZ)Vietnam (VN)

| Bank account information | Example data |
| --- | --- |
| Routing Number | 111000000 (9 characters) |
| Account number | Format varies by bank |

### Supported bank account types

You can use various types of bank accounts for your Stripe payouts, including traditional accounts offered by established financial institutions (such as checking and savings accounts), virtual bank accounts (such as N26, Revolut, and Wise), and debit cards for [instant payouts](https://docs.stripe.com/payouts#instant-payouts) (if eligible).

#### Note

Although Stripe supports non-standard bank accounts, you might see higher payout failures for these accounts.

### Financial accounts

For eligible businesses in the US, payment proceeds settle in your [financial account](https://docs.stripe.com/treasury). You only need to add your bank account information for external payouts.

### Supported accounts and settlement currencies

Bank accounts generally must be located in a country where the settlement currency is an official currency. For example, SEK bank accounts must be based in Sweden. Stripe also allows you to settle and pay out to banks in select additional currencies, or pay out to non-domestic bank accounts in the local currency. Some additional settlement currencies incur a fee when funds settle. Learn more about [presenting and settling in multiple currencies](https://docs.stripe.com/payouts/multi-currency-settlement).

Stripe supports certain non-primary currencies without a settlement fee. The following table lists the supported free currencies by country:

Viewing supported settlement currencies for Stripe accounts in:

Australia (AU)Austria (AT)Belgium (BE)Brazil (BR)Bulgaria (BG)Canada (CA)Croatia (HR)Cyprus (CY)Czech Republic (CZ)Denmark (DK)Estonia (EE)Finland (FI)France (FR)Germany (DE)Gibraltar (GI)Greece (GR)Hong Kong (HK)Hungary (HU)India (IN)Ireland (IE)Italy (IT)Japan (JP)Latvia (LV)Liechtenstein (LI)Lithuania (LT)Luxembourg (LU)Malaysia (MY)Malta (MT)Mexico (MX)Netherlands (NL)New Zealand (NZ)Norway (NO)Poland (PL)Portugal (PT)Romania (RO)Singapore (SG)Slovakia (SK)Slovenia (SI)Spain (ES)Sweden (SE)Switzerland (CH)Thailand (TH)United Arab Emirates (AE)United Kingdom (GB)United States (US)

| Settlement currency | Can be paid out to banks in these countries |
| --- | --- |
| USD | United States |

Acquiring fees, where applicable, are based on the settlement currency. You can find these acquiring fees listed by currency on your country’s pricing page.

### Multiple bank accounts for different settlement currencies

In supported countries, you can enable settlements and payouts in additional currencies by adding one bank account per supported settlement currency. If you use multiple bank accounts, you must select a default settlement currency, which you can change at any time.

Charges that are [presented](https://docs.stripe.com/currencies#presentment-currencies) in any enabled settlement currency settle without [currency conversion](https://docs.stripe.com/currencies). Payments presented in a currency that you haven’t configured an additional bank account for automatically convert to your default currency.

For example, you’re based in the United Kingdom and added both GBP and USD bank accounts, with GBP selected as the default settlement currency. USD payments (where USD is the presentment currency) are automatically paid out to the USD bank account without conversion, while payments in all other currencies are converted into GBP.

You can manage your bank accounts and default settlement currency from the [Bank accounts and currencies](https://dashboard.stripe.com/settings/money-management) settings in the Dashboard.

## Receive Capital payouts

If your Stripe Capital application is approved, you can choose to receive your financing proceeds directly into your [financial account](https://docs.stripe.com/treasury) instead of your external bank account. This gives you access to funds within minutes and enables you to spend those financing proceeds to convert currencies, send money, and manage expenses.

During the Capital application process, select your financial account as the payout destination. You can also choose your default external bank account if you prefer.

New Stripe users aren’t immediately eligible for Capital. To learn more about Capital financing and payout options, see [How Stripe Capital works](https://docs.stripe.com/capital/how-stripe-capital-works).

## Payout schedule

Your payout schedule determines when Stripe sends money to your bank account. You can select your preferred payout schedule during onboarding or update it any time in the Stripe Dashboard.

#### Time zone difference

All payments and payouts are processed according to [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time) time, [except for Asia-Pacific (APAC) markets](https://support.stripe.com/questions/default-start-of-day-for-asia-pacific-%28apac%29-payouts). As a result, the processed date might not be the same as your local time zone.

| Payout schedule | Description |
| --- | --- |
| Manual payouts | You choose when to send payouts and how much to transfer. |
| Daily payouts | Stripe automatically transfers your available funds every business day. |
| Weekly or monthly payouts | You can specify particular days of the week or days of the month for payouts. For example, payouts on Mondays and Thursdays, or on the 1st and 15th of each month. |
| Monthly adjustments | If your selected payout day doesn’t exist in a given month (for example, the 31st in a 30-day month), Stripe moves the payout to the last day of that month. |
| Non-business days | Payouts scheduled on weekends or holidays arrive on the next business day. |

### How payout timing works

Choosing a payout schedule doesn’t change how long it takes for your pending balance to become available. It only controls when payouts are sent.

For example, if your account is set to daily payouts with a 3-business-day [settlement timing](https://docs.stripe.com/payouts#payout-speed), Stripe pays out funds daily from transactions that were captured 3 business days earlier.

### Country-specific payout restrictions

Some countries have preset payout schedules because of local regulations:

- Brazil and India: Payouts are always automatic and daily.
- Japan: Daily payouts aren’t available. The default schedule is manual. You can also choose weekly and monthly payout schedules.
- Thailand: The default schedule is daily automatic payouts.

These restrictions might differ if you use [cross-border payouts](https://docs.stripe.com/connect/cross-border-payouts).

### Manual payouts

If you turn off automatic payouts, you must manually send funds to your bank account through the [Dashboard](https://dashboard.stripe.com/settings/payouts) or by using the API to [create payouts](https://docs.stripe.com/api/payouts/create).

Manual payouts are available in all regions except Brazil and India, where payouts are always automatic and daily. Manual payouts typically take 1–4 business days to arrive in your bank account after you initiate them. Same-day manual payouts are available in the US, UK, and Eurozone under the conditions outlined in the following table:

| Region | Eligible currency | Eligible businesses | Payout limit |
| --- | --- | --- | --- |
| United States | USD | Standard [T+2 settlement timing](https://docs.stripe.com/payouts#payout-speed) or slower | Manual payouts initiated before 5 pm US/Eastern are eligible for same-day manual payouts. The limit is 10 same-day manual payouts per day with a maximum of 1 million USD each. All other manual payouts typically arrive within 1 business day. |
| United Kingdom | GBP | Standard [T+3 settlement timing](https://docs.stripe.com/payouts#payout-speed) or slower | Manual payouts initiated before 5 pm Europe/London are eligible for same-day manual payouts. The limit is 10 same-day manual payouts per day with a maximum of 1 million GBP each. All other manual payouts typically arrive within 2 business days. |
| Switzerland, EU, United Kingdom, Malta, and Norway | EUR | Standard [T+3 settlement timing](https://docs.stripe.com/payouts#payout-speed) or slower. If your recipient bank has a high failure rate for same-day banking rails, funds arrive the next business day. | Manual payouts initiated before 4 pm Europe/Copenhagen are eligible for same-day manual payouts. The limit is 10 same-day manual payouts per day with a maximum of 1 million EUR each. All other manual payouts typically arrive within 1 business day. |

Command Line

Select a language

cURL

cURL

Stripe CLI

Ruby

Python

PHP

Java

Node.js

Go

.NET

```
curl https://api.stripe.com/v1/payouts \
  -u "sk_test_BQokikJOvBiI2HlWgH4olfQ2:" \
  -d amount=5000 \
  -d currency=usd
```

## Settlement timing

The payout schedule refers to the cadence at which your funds are paid out, for example, day of the week. The settlement timing refers to the amount of time it takes for your funds to become available. Settlement timing varies per country and is typically expressed as “T+X” days. Some payment processors might start “T” from their internal settlement time, meaning when the funds land in their bank accounts.

Stripe uses “T” to refer to the transaction time, which indicates the time of the original payment confirmation or capture, and the counting starts earlier. If your Stripe account is in a country with a T+3 standard settlement timing and you use a manual payout schedule, your Stripe balance is available for payout within 3 business days of capturing a payment. However, if you use a daily automatic payout schedule with a T+3 standard settlement timing, Stripe pays out funds daily from transactions captured 3 business days earlier.

Most banks deposit payouts into your bank account as soon as they receive them, though some might take a few extra days to make them available. The type of business and the country you’re in can also affect payout timing.

### Definition of days

There are two definitions of days that affect settlement and payout timing:

- **Calendar days**: Includes every day, including weekends and holidays.
- **Business days**: Only includes working days, typically Monday through Friday, and excludes public holidays.

For example, a charge created on a Saturday could have two different timings depending on which definition of day you use:

- If you use calendar days, Saturday is day 0.
- If you use business days, the next Monday is day 0.

### Delay behavior per account country

As the platform, you can set [delay\_days](https://docs.stripe.com/connect/manage-payout-schedule#delay_days) on your connected accounts. The delay applies as a **business day** or **calendar day** delay, based on the country of the connected account. The following table shows which countries apply the delay by business or calendar day.

| Country | Delay type |
| --- | --- |
| Australia, India, Japan, Malaysia, New Zealand, Thailand, United Arab Emirates, and United States | Business day (Monday - Friday) |
| Brazil1, Canada, Gibraltar, Hong Kong, Liechtenstein, Mexico, Norway, Singapore2, Switzerland, United Kingdom, and supported EU countries | Calendar day (Sunday - Saturday) |

1 Delays for Pix, Boleto, debit, and prepaid payouts in Brazil apply in business days.

2 Delays for PayNow in Singapore apply in business days.

### Settlement timing by country

Use the following collapsed table to determine your country’s settlement timing. The initial settlement timing applies to your first payout, and the default settlement timing applies to subsequent payouts.

#### Note

In some cases, risk criteria might prevent your account from changing to the default settlement timing.

### Country and settlement timing

### Settlement timing by payment method

Bank payment methods typically have longer settlement times than card payments because of the underlying banking systems. These payments have a higher risk of returns or reversals, which factors into their longer settlement periods.

| Payment method | Settlement timing |
| --- | --- |
| ACH Debit | 4 business days |
| SEPA Direct Debit | 6 business days |
| Bacs Direct Debit | 4 business days |
| AU BECS Direct Debit | 2 business days |
| NZ BECS Direct Debit | 2 business days |
| PAD Canada | 5 business days |
| [USD Bank Transfers](https://docs.stripe.com/payments/bank-transfers) | 5 business days |

To manage your cash flow and cover potential refunds, disputes, and fees that might lead to negative balances, you can set a [minimum balance](https://docs.stripe.com/payouts/minimum-balances-for-automatic-payouts) in your Stripe account.

## Accelerate settlement timing

Stripe offers products and payment methods that have reduced settlement time depending on your location and are subject to eligibility criteria.

### 2-day ACH settlement

For eligible US merchants, Stripe offers faster ACH settlement that reduces the settlement time from 4 business days to 2 business days from payment creation. For more details about eligibility and activation, see the [ACH support page](https://support.stripe.com/questions/two-day-settlement-for-ach-direct-debit).

### Instant Payouts

With [Instant Payouts](https://docs.stripe.com/payouts/instant-payouts), you can instantly send funds to a supported debit card or bank account. You can request Instant Payouts any time, including weekends and holidays, and funds usually appear in the associated bank account within 30 minutes. New Stripe users aren’t immediately eligible for Instant Payouts. You can check your [eligibility](https://docs.stripe.com/payouts/instant-payouts#eligibility-and-daily-volume-limits) in the [Dashboard](https://dashboard.stripe.com/payouts/instant_payouts_eligibility).

## Minimum payout amounts

The minimum payout amount depends on the lowest amount we can support with our banking partners. For example, if you’re located in the US and you have less than 1 cent (0.01 of 1 dollar) USD in your Stripe account, you must wait until you accept more payments and increase your balance before you can receive a payout. If your available account balance is less than the minimum payout amount, it remains in your Stripe account until your balance increases.

If you’re in a supported country, you can use [multi-currency settlement](https://docs.stripe.com/payouts/multi-currency-settlement) to send a payout to your local bank accounts in a foreign currency. For example, if you’re based in France, you can receive a USD payout in your French bank account, instead of paying for multiple currency exchanges.

Minimum payout amounts are typically one base unit of the local currency. See the following collapsed table for a list of countries and their minimum payout amounts:

### Minimum payout amounts per country

## Negative payouts

Each payout reflects your available account balance at the time it was created. In some cases, you might have a negative account balance. For example, if you receive 100 USD in payments but refund 200 USD of prior payments, your account balance would be -100 USD. If you don’t receive further payments to balance out the negative amount, Stripe creates a payout that _debits_ your bank account.

Your bank account must support both credit and debit transactions so that Stripe can perform any required payouts.

## Test payouts

Use the following test bank and debit card numbers to trigger certain events when testing [payouts](https://docs.stripe.com/connect/payouts-connected-accounts). You can only use these values while testing with test API keys.

Test payouts simulate a live payout but aren’t processed with the bank. Test accounts with Stripe Dashboard access always have payouts enabled, as long as valid external bank information and other relevant conditions are met, and never requires real identity verification.

#### Note

You can’t use test bank and debit card numbers in the Stripe Dashboard on a live mode connected account. If you’ve entered your bank account information on a live mode account, you can still use a sandbox, and test payouts will simulate a live payout without processing actual money.

### Bank numbers

Use these test bank account numbers to test payouts. You can only use them with test API keys.

AlbaniaAlgeriaAngolaAntigua & BarbudaArgentinaArmeniaAustraliaAustriaAzerbaijanBahamasBahrainBangladeshBelgiumBeninBhutanBoliviaBosnia & HerzegovinaBotswanaBrazilBruneiBulgariaCambodiaCanadaChileColombiaCosta RicaCôte d’IvoireCroatiaCyprusCzech RepublicDenmarkDominican RepublicEcuadorEgyptEl SalvadorEstoniaEthiopiaFinlandFranceGabonGambiaGermanyGhanaGibraltarGreeceGuatemalaGuyanaHong KongHungaryIcelandIndiaIndonesiaIrelandIsraelItalyJamaicaJapanJordanKazakhstanKenyaKuwaitLaosLatviaLiechtensteinLithuaniaLuxembourgMacao SAR ChinaMadagascarMalaysiaMaltaMauritiusMexicoMoldovaMonacoMongoliaMoroccoMozambiqueNamibiaNetherlandsNew ZealandNigerNigeriaNorth MacedoniaNorwayOmanPakistanPanamaParaguayPeruPhilippinesPolandPortugalQatarRomaniaRwandaSan MarinoSaudi ArabiaSenegalSerbiaSingaporeSlovakiaSloveniaSouth AfricaSouth KoreaSpainSri LankaSt. LuciaSwedenSwitzerlandTaiwanTanzaniaThailandTrinidad & TobagoTunisiaTurkeyUnited Arab EmiratesUnited Kingdom (IBAN)United Kingdom (Sort Code)United StatesUruguayUzbekistanVietnam

| Routing | Account | Type |
| --- | --- | --- |
| `110000000` | `000123456789` | Payout succeeds. |
| `110000000` | `000111111116` | Payout fails with a `no_account` code. |
| `110000000` | `000111111113` | Payout fails with a `account_closed` code. |
| `110000000` | `000222222227` | Payout fails with a `insufficient_funds` code. |
| `110000000` | `000333333335` | Payout fails with a `debit_not_authorized` code. |
| `110000000` | `000444444440` | Payout fails with a `invalid_currency` code. |
| `110000000` | `000888888883` | Payout fails if `method` is `instant`. Bank account is not eligible for Instant Payouts. |

### Debit card numbers

Use these test debit card numbers to test payouts to a debit card. You can only use them with test API keys.

United StatesCanadaSingaporeAustraliaUnited Arab EmiratesUnited KingdomAustriaBelgiumCroatiaCyprusEstoniaFinlandFranceGermanyGreeceIrelandItalyLatviaLithuaniaLuxembourgMaltaNetherlandsPortugalSlovakiaSloveniaSpainDenmarkMalaysiaNew ZealandNorwaySwedenCzechiaHungaryPolandRomania

| Number | Token | Type |
| --- | --- | --- |
| 4000056655665556 | `tok_visa_debit_us_transferSuccess` | Visa debit. Payout succeeds. |
| 4000056655665572 | `tok_visa_debit_us_transferFail` | Visa debit. Payout fails with a `could_not_process` code. |
| 4000056755665555 | `tok_visa_debit_us_instantPayoutUnsupported` | Visa debit. Card isn’t eligible for Instant Payouts. |
| 5200828282828210 | `tok_mastercard_debit_us_transferSuccess` | Mastercard debit. Payout succeeds. |
| 6011981111111113 | `tok_discover_debit_us_transferSuccess` | Discover debit. Payout succeeds. |

## Payout failures

If your bank account can’t receive a payout for any reason, your bank returns the funds to us. You’ll receive an error with the [reason for the failure](https://docs.stripe.com/api/payouts/object#payout_object-failure_code). It can take up to 5 additional business days for your bank to return the payout and inform us that it failed. If this happens, you’re notified by email and in the [Dashboard](https://dashboard.stripe.com/test/payouts). If a payout fails, make sure your bank account details are correct by re-entering them. Stripe then reattempts the payout at the next scheduled payout interval.

#### Caution

When a payout fails, the status might initially show as `paid`, but then change to `failed` within 5 business days.

Stripe sends the funds using the bank account information that you enter. If you provide incorrect information, such as a mistyped account number or an incorrect routing number, Stripe might send payouts to the wrong bank account and might not be able to recover the funds.

Any fees or losses that you incur because of incorrect information fall under your responsibility. If your banking details are correct and the payout failure is for other reasons, contact your bank. After you resolve any issues with your bank, you can reactivate the payouts by clicking **Resume Payouts**. If you don’t receive a payout from Stripe after clicking **Resume Payouts**, and you haven’t received a failure notification within a reasonable time frame, [contact us](https://support.stripe.com/contact).

## Payout fees

Stripe doesn’t charge you a fee to initiate normal payouts. When you use [multi-currency settlement](https://docs.stripe.com/payouts/multi-currency-settlement) in a non-primary currency, Stripe charges the applicable fee when the funds settle, rather than when you pay them out.

## See also

- [Payout reconciliation report](https://docs.stripe.com/reports/payout-reconciliation)
- [Financial reports](https://docs.stripe.com/reports/select-a-report)

On this page

[Add or update your bank account](https://docs.stripe.com/payouts#adding-bank-account-information "Add or update your bank account")

[Supported bank account types](https://docs.stripe.com/payouts#supported-bank-account-types "Supported bank account types")

[Financial accounts](https://docs.stripe.com/payouts#financial-accounts "Financial accounts")

[Supported accounts and settlement currencies](https://docs.stripe.com/payouts#supported-accounts-and-settlement-currencies "Supported accounts and settlement currencies")

[Multiple bank accounts for different settlement currencies](https://docs.stripe.com/payouts#multiple-bank-accounts "Multiple bank accounts for different settlement currencies")

[Receive Capital payouts](https://docs.stripe.com/payouts#receive-capital-payouts "Receive Capital payouts")

[Payout schedule](https://docs.stripe.com/payouts#payout-schedule "Payout schedule")

[How payout timing works](https://docs.stripe.com/payouts#how-payout-timing-works "How payout timing works")

[Country-specific payout restrictions](https://docs.stripe.com/payouts#country-specific-payout-restrictions "Country-specific payout restrictions")

[Manual payouts](https://docs.stripe.com/payouts#manual-payouts "Manual payouts")

[Settlement timing](https://docs.stripe.com/payouts#payout-speed "Settlement timing")

[Definition of days](https://docs.stripe.com/payouts#definition-of-days "Definition of days")

[Delay behavior per account country](https://docs.stripe.com/payouts#delay-behavior-per-account-country "Delay behavior per account country")

[Settlement timing by country](https://docs.stripe.com/payouts#standard-payout-timing "Settlement timing by country")

[Settlement timing by payment method](https://docs.stripe.com/payouts#settlement-timing-by-payment-method "Settlement timing by payment method")

[Accelerate settlement timing](https://docs.stripe.com/payouts#accelerate-settlement-timing "Accelerate settlement timing")

[2-day ACH settlement](https://docs.stripe.com/payouts#2-day-ach-settlement "2-day ACH settlement")

[Instant Payouts](https://docs.stripe.com/payouts#instant-payouts "Instant Payouts")

[Minimum payout amounts](https://docs.stripe.com/payouts#minimum-payout-amounts "Minimum payout amounts")

[Negative payouts](https://docs.stripe.com/payouts#negative-payouts "Negative payouts")

[Test payouts](https://docs.stripe.com/payouts#test-payouts "Test payouts")

[Bank numbers](https://docs.stripe.com/payouts#account-numbers "Bank numbers")

[Debit card numbers](https://docs.stripe.com/payouts#test-debit-card-numbers "Debit card numbers")

[Payout failures](https://docs.stripe.com/payouts#payout-failures "Payout failures")

[Payout fees](https://docs.stripe.com/payouts#payout-fees "Payout fees")

[See also](https://docs.stripe.com/payouts#see-also "See also")
