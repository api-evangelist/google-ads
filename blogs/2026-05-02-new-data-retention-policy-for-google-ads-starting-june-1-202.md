---
title: "New Data Retention Policy for Google Ads starting June 1, 2026"
url: "http://ads-developers.googleblog.com/2026/05/new-data-retention-policy-for-google.html"
date: "2026-05-01T17:40:17.036-07:00"
author: "Google Ads Developer Advisor (noreply@blogger.com)"
feed_url: "http://ads-developers.googleblog.com/feeds/posts/default"
---
<p>
Starting <strong>June 1, 2026</strong>, Google Ads and related measurement APIs will transition to a 37-month <a href="https://support.google.com/google-ads/answer/15188209?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-google-ads-data-retention-may2026&amp;utm_content=readmore-blog" target="_blank">data retention policy</a> for granular performance statistics (daily, hourly, and weekly). High-level data (monthly, quarterly, and yearly) will continue to be available for 11 years.
</p>

<table id="dataretensionmay2026">
  <tr style="background: #eee;">
   <td width="175"><strong>API</strong>
   </td>
   <td><strong>Impact</strong>
   </td>
   <td width="175"><strong>Next Steps</strong>
   </td>
  </tr>
  <tr>
   <td><a href="https://developers.google.com/google-ads/api/docs/start?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-google-ads-data-retention-may2026&amp;utm_content=readmore-blog" target="_blank">Google Ads API</a> and <a href="https://developers.google.com/google-ads/scripts/docs/start?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-google-ads-data-retention-may2026&amp;utm_content=readmore-blog" target="_blank">Google Ads scripts</a>
   </td>
   <td>Starting June 1, 2026, queries that request granular segments (such as segments.date, segments.week) for ranges older than 37 months from the current date will return a <code><a href="https://developers.google.com/google-ads/api/reference/rpc/latest/DateRangeErrorEnum.DateRangeError?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-google-ads-data-retention-may2026&amp;utm_content=readmore-invalid_date" target="_blank">DateRangeError.INVALID_DATE</a></code> error. Future API versions will return <code>DateRangeError.REQUESTED_DATE_GRANULARITY_NOT_SUPPORTED</code> error.
To retrieve data older than 37 months, you must update your queries to use <code>segments.month</code>, <code>segments.quarter</code>, or <code>segments.year</code>. Unsegmented queries for historical data must align perfectly with calendar month boundaries (1st to last day of month) to succeed.
   </td>
   <td>Please review your applications and make updates. If you require granular historical data beyond 37 months, we recommend exporting it prior to the June 1, 2026 deadline.
<p>
If you have any questions, you can contact us on our <a href="https://support.google.com/google-ads/contact/google_ads_api" target="_blank">Google Ads API support channel</a> or <a href="https://support.google.com/google-ads/contact/google_ads_scripts" target="_blank">Google Ads scripts support channel</a>.
   </td>
  </tr>
  <tr>
   <td><a href="https://developers.google.com/analytics/devguides/reporting/data/v1?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-google-ads-data-retention-may2026&amp;utm_content=readmore-blog" target="_blank">Google Analytics Data API</a>
   </td>
   <td>The Google Analytics Data API will truncate affected metrics to the latest 36-month window if the dimension "date" is also used in the report. Affected metrics include Advertiser Ad Cost, Clicks, and Impressions. Only reports with all of affected metrics, 37-months or older, and including the dimension "date" are impacted. Date-equivalent dimensions like "Day of week" and "day" are also impacted.
   </td>
   <td>Review your data stitching logic to account for this truncation.
   </td>
  </tr>
  <tr>
   <td><a href="https://developers.google.com/display-video/api/reference/rest?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-google-ads-data-retention-may2026&amp;utm_content=readmore-blog" target="_blank">DV360 API</a> and <a href="https://developers.google.com/doubleclick-advertisers/rest?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-google-ads-data-retention-may2026&amp;utm_content=readmore-blog" target="_blank">CM360 API</a>
   </td>
   <td>These APIs currently maintain a 24-month retention period, which remains unchanged.
   </td>
   <td>No impact.
   </td>
  </tr>
  <tr>
   <td><a href="https://docs.cloud.google.com/bigquery/docs/google-ads-transfer" target="_blank">BigQuery Data Transfer Service </a>
   </td>
   <td>Starting June 1, 2026, the <a href="https://docs.cloud.google.com/bigquery/docs/google-ads-transfer" target="_blank">BigQuery Data Transfer Service for Google Ads</a> and <a href="https://docs.cloud.google.com/bigquery/docs/search-ads-transfer" target="_blank">BigQuery Data Transfer Service for Search Ads 360</a> connectors will stop populating data for backfill runs with dates older than 37 months from the current date. Data transferred and stored in BigQuery will remain in the tables with no impact.
<p>
Starting June 1, 2026, <a href="https://docs.cloud.google.com/bigquery/docs/google-analytics-4-transfer" target="_blank">BigQuery Data Transfer Service for Google Analytics 4 connector</a> will stop populating data for backfill runs with dates older than 37 months from the current date. Data transferred and stored in BigQuery will remain in the tables, but if a transfer is manually triggered for a report date 37-months or older, the data of the date in BigQuery table will be overwritten by empty value.
   </td>
   <td>If you want to keep historical data beyond 37 months in BigQuery, we recommend starting backfilling runs early so that they can complete before June 1, 2026.
   </td>
  </tr>
</table>

<p>
If you have any questions or want to discuss this post, please reach out to us on our <a href="http://goo.gle/ads-and-measurement-discord" target="_blank">“Google Advertising and Measurement Community” Discord server</a>.  
</p>

<span class="byline-author"><img height="40" src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEirL384dk5kS3bbZT7SvdKdHtYvuL0HbdDhCIG92AVQY0Vv4aI-h4EnuzN4uNC-E-HQs7D2jKOUCe6U3GK1QY-ybACkyvNXnFoKqO-bqSF66spvNx_40LNrNs0GHYWi9UyhtEkdV9qpeuZcnPO1jqEXSW4Wi48y8UvWdYo070Dz6_tUh_3enwKSe2B58pA/s1600/ndsw.jpg" style="vertical-align: middle; border: none;" width="40" /> Nadine Wang, Advertising and Measurement APIs Team</span>
