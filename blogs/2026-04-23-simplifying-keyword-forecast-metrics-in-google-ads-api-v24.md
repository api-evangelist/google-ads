---
title: "Simplifying Keyword Forecast Metrics in Google Ads API v24"
url: "http://ads-developers.googleblog.com/2026/04/simplifying-keyword-forecast-metrics-in.html"
date: "2026-04-23T09:40:00.000-07:00"
author: "Google Ads Developer Advisor (noreply@blogger.com)"
feed_url: "http://ads-developers.googleblog.com/feeds/posts/default"
---
<p>
To provide a more streamlined and reliable experience, we have unified our forecasting infrastructure. Google Ads API v24 introduces an updated <code><a href="https://developers.google.com/google-ads/api/reference/rpc/v24/KeywordPlanIdeaService/GenerateKeywordForecastMetrics?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-keyword-simplification-apr2026&amp;utm_content=keywordplanning-refdocs" target="_blank">GenerateKeywordForecastMetrics</a></code> method that simplifies the planning process by focusing on the metrics that most directly impact your performance.

<h2>What's changing?</h2>


<p>
To streamline our systems and focus on the primary data that drives successful Search planning, Google Ads API v24 introduces the following refinements:
</p>
<h3>1. Alignment with Bidding Strategies</h3>


<p>
To provide a more consistent experience across Google Ads tools, forecasts now focus exclusively on the primary metrics that your chosen bidding strategy directly impacts. This alignment ensures that the data you use for planning is synchronized with the high-impact performance indicators for your actual campaigns:
</p><ul>

<li><strong>Manual CPC and Maximize Clicks</strong>: Forecasts provide clicks, average CPC, and cost.
<li><strong>Maximize Conversions</strong>: Forecasts provide conversions, average CPA, and cost.
<li><strong>Metric Focus</strong>: To maintain consistency across the platform, forecasts no longer include cross-metric data (such as conversion estimates for click-oriented strategies) or secondary metrics like impressions and conversion value.</li></ul>

<h3>2. Streamlined Request Parameters</h3>


<p>
We have made the following updates to simplify forecasting requests, improve system reliability, and remove inputs which have a minimal effect on overall forecast accuracy:
</p><ul>

<li><code><a href="https://developers.google.com/google-ads/api/reference/rpc/v23/CampaignToForecast#geo_modifiers[]?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-keyword-simplification-apr2026&amp;utm_content=keywordplanning-refdocs" target="_blank">CampaignToForecast.geo_modifiers[]</a></code> is replaced by <code><a href="https://developers.google.com/google-ads/api/reference/rpc/v24/CampaignToForecast#geo_target_constants[]?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-keyword-simplification-apr2026&amp;utm_content=keywordplanning-refdocs" target="_blank">CampaignToForecast.geo_target_constants[]</a></code>
<li><code><a href="https://developers.google.com/google-ads/api/reference/rpc/v23/ForecastAdGroup#biddable_keywords[]?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-keyword-simplification-apr2026&amp;utm_content=keywordplanning-refdocs" target="_blank">ForecastAdGroup.biddable_keywords[]</a></code> is replaced by <code><a href="https://developers.google.com/google-ads/api/reference/rpc/v24/ForecastAdGroup#keywords?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-keyword-simplification-apr2026&amp;utm_content=keywordplanning-refdocs" target="_blank">ForecastAdGroup.keywords[]</a></code>.
<li>The following fields are removed: <ul>

 <li><code>CampaignToForecast.keyword_plan_network</code>
 <li><code>CampaignToForecast.negative_keywords</code>
 <li><code>ForecastAdGroup.max_cpc_bid_micros</code>
 <li><code>ForecastAdGroup.negative_keywords</code>
 <li><code>CriterionBidModifier</code></li> </ul>
</li> </ul>

<h2>Timeline</h2>


<p>
The transition follows our standard release and sunset cycle:
</p><ul>

<li><strong>April 2026</strong>: Google Ads API v24 is available with the updated <code>GenerateKeywordForecastMetrics</code> functionality.
<li><strong>February 2027</strong>: Google Ads API v23 is <a href="https://developers.google.com/google-ads/api/docs/sunset-dates?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-keyword-simplification-apr2026&amp;utm_content=keywordplanning-sunsetdates" target="_blank">scheduled for sunset</a>. At this time, all versions of the Google Ads API will utilize this unified forecasting infrastructure.</li></ul>

<h2>Next Steps</h2>


<p>
Developers that use <code>GenerateKeywordForecastMetrics</code> should review their integrations to ensure compatibility with the updated parameter set in v24. Review the Generate Forecast Metrics guide and the <code><a href="https://developers.google.com/google-ads/api/reference/rpc/v24/KeywordPlanIdeaService/GenerateKeywordForecastMetrics?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-keyword-simplification-apr2026&amp;utm_content=keywordplanning-refdocs" target="_blank">GenerateKeywordForecastMetrics</a></code> v24 reference for the latest usage details.

<p>
If you have any questions about this announcement or want to discuss it with our team and the community, please reach out to us on our <a href="https://goo.gle/ads-and-measurement-discord" target="_blank">Ads and Measurement Community Discord server</a>.
</p>

<span class="byline-author"><img height="40" src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg1QyLBN_MNIUNy20yCmmeYUsmqBl083GUng1w8D2sZvZrGVShmgPa6XkCPlYaMn1MmENzAk8sfjNbHIv2E8jAvZ5hnEUT6Z0WcIpMzUNbrsLNk0B0etRPWMv6YlP-4Is6YQZzva1TDeJeix5PD3zOKSLsZEUEYmyNVy-dIVsU6EF2o4hvI5HrEiuxGVGg/s1600/laura_linkedin.jpeg" style="vertical-align: middle; border: none;" width="40" />&nbsp;-&nbsp;Laura Chevalier, Google Ads API Team</span>
