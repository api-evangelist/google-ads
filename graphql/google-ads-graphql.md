# Google Ads GraphQL Schema

## Overview

This is a conceptual GraphQL schema for the Google Ads API. It is derived from the [Google Ads API v19 REST and Proto/gRPC services](https://developers.google.com/google-ads/api/reference/rpc) and represents the full breadth of resources available through the platform, including account management, campaign hierarchy, ad creatives, assets, audience targeting, bidding strategies, conversion tracking, and reporting.

The Google Ads API natively exposes REST and gRPC (Protobuf) endpoints. This GraphQL schema is a semantic translation that maps the core resource types and operations into a strongly typed graph, suitable for building unified API layers, developer tooling, or internal platforms.

## Source

- **API Version:** Google Ads API v19
- **Reference:** https://developers.google.com/google-ads/api/reference/rpc
- **GitHub:** https://github.com/googleads
- **Base URL:** https://googleads.googleapis.com

## Authentication

The Google Ads API uses OAuth 2.0 for authentication. All requests require:

- A valid OAuth 2.0 access token in the `Authorization` header.
- A `developer-token` header containing your Google Ads developer token.
- Optionally a `login-customer-id` header when accessing manager account data.

## Schema File

[google-ads-schema.graphql](google-ads-schema.graphql)

## Type Summary

The schema defines the following named types across all layers of the Google Ads resource hierarchy:

### Account and Billing (8 types)
| Type | Description |
|---|---|
| `Customer` | Full Google Ads account with settings, optimization score, and configuration |
| `CustomerSummary` | Lightweight account representation for list views |
| `AccountBudget` | Approved budget for an account with spend limits and billing linkage |
| `AccountBudgetProposal` | Pending request to modify an account budget |
| `BillingSetup` | Links a payments account to a Google Ads customer |
| `PaymentsAccount` | Payment profile used to fund advertising |
| `Invoice` | Billing invoice with line items and account budget summaries |
| `AccountBudgetSummary` | Per-budget subtotals within an invoice |

### Campaign Layer (8 types)
| Type | Description |
|---|---|
| `Campaign` | Top-level advertising entity with channel type, bidding, network, and targeting settings |
| `CampaignBudget` | Daily or lifetime spend limit attached to one or more campaigns |
| `CampaignCriterion` | Targeting rule applied at the campaign level (location, device, schedule, etc.) |
| `CampaignConversionGoal` | Conversion goal configuration scoped to a campaign |
| `CampaignAsset` | Association between a campaign and a creative asset |
| `CampaignPerformanceMaxUpgradeSetting` | Tracks upgrade status to Performance Max |
| `NetworkSettings` | Search, display, and partner network targeting flags |
| `ShoppingSetting` | Merchant Center linkage and shopping campaign configuration |

### Ad Group Layer (6 types)
| Type | Description |
|---|---|
| `AdGroup` | Container for ads and keywords within a campaign |
| `AdGroupAd` | Association between an ad group and a specific ad |
| `AdGroupAdAssetCombination` | Tracks which asset combinations were served for responsive ads |
| `AdGroupCriterion` | Keyword, audience, or placement targeting at the ad group level |
| `AdGroupBidModifier` | Adjusts bids by device, hotel, or other dimension at the ad group level |
| `AdGroupAsset` | Association between an ad group and a creative asset |

### Ad Formats (20+ types)
| Type | Description |
|---|---|
| `Ad` | Root ad object that contains format-specific sub-objects |
| `ExpandedTextAd` | Legacy three-headline text ad format |
| `ResponsiveSearchAd` | Machine-learning optimized ad with up to 15 headlines and 4 descriptions |
| `CallAd` | Ad that shows a phone number with call tracking |
| `ResponsiveDisplayAd` | Automatically assembled display ad from provided assets |
| `VideoAd` | YouTube video ad with in-stream, bumper, out-stream, or in-feed formats |
| `AppAd` | Universal app campaign ad for installs or engagement |
| `ShoppingProductAd` | Product listing ad sourced from Merchant Center |
| `SmartCampaignAd` | Simplified ad for Google Smart Campaigns |
| `DynamicSearchAd` | Automatically generated headline based on website content |
| `DiscoveryMultiAssetAd` | Multi-asset ad for Demand Gen campaigns |
| `DiscoveryCarouselAd` | Carousel format for Demand Gen campaigns |
| `VideoResponsiveAd` | Responsive video ad with multiple creative combinations |
| `GmailAd` | Expandable ad that appears in Gmail |
| `ImageAd` | Static image display ad |
| `LocalAd` | Ad format for local campaigns |
| `AppEngagementAd` | Re-engagement ad for existing app users |
| `DisplayUploadAd` | Custom HTML5 or media bundle display ad |
| `AppPreRegistrationAd` | Pre-registration ad for upcoming Android apps |

### Assets (12 types)
| Type | Description |
|---|---|
| `Asset` | Base asset entity shared across campaigns, ad groups, and ads |
| `TextAsset` | Plain text asset for headlines, descriptions, and callouts |
| `ImageAsset` | Image asset with dimension and MIME type metadata |
| `VideoAsset` | YouTube video asset with ISRC and advertising ID |
| `CallAsset` | Phone number asset with conversion tracking |
| `SitelinkAsset` | Sitelink with link text, two description lines, and scheduling |
| `CalloutAsset` | Short callout text with optional date scheduling |
| `StructuredSnippetAsset` | Header plus list of values for structured information |
| `PromotionAsset` | Promotional offer with discount details and occasion targeting |
| `LeadFormAsset` | Lead form with custom fields and webhook delivery |
| `PriceAsset` | Itemized price list with descriptions and landing page URLs |
| `PageFeedAsset` | Page URL with labels for dynamic search ad targeting |

### Keywords and Search Terms (5 types)
| Type | Description |
|---|---|
| `Keyword` | Individual keyword with text, match type, and bid |
| `NegativeKeyword` | Excluded keyword at campaign or ad group level |
| `KeywordPlanCampaign` | Campaign within a keyword plan for research and forecasting |
| `SearchTermView` | Actual search query that triggered an ad |
| `SmartCampaignSearchTermView` | Search terms surfaced in Smart Campaign reporting |

### Audiences and Targeting (8 types)
| Type | Description |
|---|---|
| `AudienceInsightsAttribute` | Attribute used to describe an audience segment for insights |
| `UserList` | Remarketing or customer match list |
| `Audience` | Structured audience with inclusion and exclusion dimensions |
| `CombinedAudience` | Audience built from combinations of existing segments |
| `GeoTargetConstant` | Geographic targeting entity (country, city, region, etc.) |
| `LanguageConstant` | Language targeting constant |
| `AdGroupCriterion` | Targeting applied at the ad group level (also in Ad Group layer) |
| `CampaignCriterion` | Targeting applied at the campaign level (also in Campaign layer) |

### Bidding Strategies (10 types)
| Type | Description |
|---|---|
| `BiddingStrategy` | Portfolio bidding strategy shared across campaigns |
| `AutomatedBid` | Marker type for automated bidding |
| `ManualCPC` | Manual cost-per-click bidding with optional Enhanced CPC |
| `MaximizeClicks` | Automated strategy to maximize clicks within a budget |
| `MaximizeConversions` | Automated strategy to maximize conversion volume |
| `MaximizeConversionValue` | Automated strategy to maximize conversion value |
| `TargetCPA` | Target cost-per-acquisition bidding |
| `TargetRoas` | Target return-on-ad-spend bidding |
| `TargetImpressionShare` | Target a specific impression share position |
| `TargetSpend` | Legacy target-spend strategy |

### Conversions (5 types)
| Type | Description |
|---|---|
| `ConversionAction` | Defines a conversion event with attribution and counting rules |
| `ConversionGoal` | High-level conversion category goal |
| `ConversionProductGoal` | Product-level conversion goal configuration |
| `ConversionActionValueSettings` | Default value and currency for a conversion action |
| `AttributionModelSettings` | Attribution model applied to conversion measurement |

### Reporting (4 types)
| Type | Description |
|---|---|
| `Report` | Response from a Google Ads Query Language (GAQL) report query |
| `ReportRow` | Individual result row from a report query |
| `Metrics` | Performance metrics (clicks, impressions, cost, conversions, etc.) |
| `Segments` | Segmentation dimensions for breaking down report data (date, device, network, etc.) |

### Authentication (2 types)
| Type | Description |
|---|---|
| `APIKey` | Developer token metadata |
| `Token` | OAuth 2.0 token response |

## Query Operations

The schema exposes the following root query operations:

- `customer(customerId)` — retrieve a full account
- `customers` — list all accessible accounts
- `accountBudgets(customerId)` — list account budgets
- `invoices(customerId, billingSetup, issueYear, issueMonth)` — retrieve invoices
- `campaigns(customerId, status)` — list campaigns
- `campaignBudgets(customerId)` — list campaign budgets
- `adGroups(customerId, campaignId, status)` — list ad groups
- `adGroupAds(customerId, adGroupId, status)` — list ads in ad groups
- `adGroupCriteria(customerId, adGroupId, type)` — list ad group targeting criteria
- `assets(customerId, type)` — list assets
- `userLists(customerId)` — list remarketing and customer match lists
- `audiences(customerId)` — list audiences
- `geoTargetConstants(query, countryCode)` — search geographic targets
- `languageConstants` — list all language targeting constants
- `biddingStrategies(customerId)` — list portfolio bidding strategies
- `conversionActions(customerId)` — list conversion actions
- `report(customerId, query, pageToken, pageSize)` — execute a GAQL query

## Mutation Operations

The schema exposes the following root mutation operations, each accepting a standard operation envelope with `create`, `update`, `remove`, and `updateMask` fields:

- `mutateCampaign` — create, update, or remove a campaign
- `mutateCampaignBudget` — create, update, or remove a campaign budget
- `mutateAdGroup` — create, update, or remove an ad group
- `mutateAdGroupAd` — create, update, or remove an ad
- `mutateAdGroupCriterion` — create, update, or remove a targeting criterion
- `mutateAsset` — create or update a shared asset
- `mutateUserList` — create or update a user list
- `mutateConversionAction` — create or update a conversion action
- `mutateBiddingStrategy` — create or update a portfolio bidding strategy

## Notes

- Money values throughout the schema use the `Micros` scalar (micro-units, one millionth of the base currency unit), consistent with how the Google Ads API represents monetary amounts.
- The `report` query accepts a [Google Ads Query Language (GAQL)](https://developers.google.com/google-ads/api/docs/query/overview) string, enabling flexible reporting across any combination of resources, metrics, and segments.
- Resource names follow the pattern `customers/{customer_id}/campaigns/{campaign_id}` and serve as the primary keys for most resource types.
- This schema covers API v19 types. Some legacy ad formats (Expanded Text Ads, Standard Shopping Ads) are included for completeness but may be sunset in future API versions.
