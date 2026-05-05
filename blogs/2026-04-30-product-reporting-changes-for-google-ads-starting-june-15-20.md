---
title: "Product reporting changes for Google Ads starting June 15, 2026"
url: "http://ads-developers.googleblog.com/2026/04/product-reporting-changes-for-google.html"
date: "2026-04-30T07:47:00.000-07:00"
author: "Google Ads Developer Advisor (noreply@blogger.com)"
feed_url: "http://ads-developers.googleblog.com/feeds/posts/default"
---
<p>
Starting June 15, 2026, the <a href="https://developers.google.com/google-ads/api?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-productperformancereportingchangesapr2026&amp;utm_content=readmore-api" target="_blank">Google Ads API</a> will begin transitioning <a href="https://developers.google.com/google-ads/api/docs/shopping-ads/reporting?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-productperformancereportingchangesapr2026&amp;utm_content=readmore-reporting" target="_blank">product reporting</a> to include data from all Performance Max networks. This update also provides comprehensive performance metrics across all campaign types and channels, including Performance Max, Shopping, Video, App, and Demand Gen.
</p>
<h3><strong>What is changing?</strong></h3>


<p>
Previously, reporting for products in Video, Demand Gen, and App campaigns was limited to high-level metrics like impressions and clicks. Also for Performance Max campaigns, only some networks were reported. This update introduces:
</p><ul>

<li><strong>Expanded metrics for <code><a href="https://developers.google.com/google-ads/api/fields/latest/shopping_product?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-productperformancereportingchangesapr2026&amp;utm_content=readmore-shopping_product" target="_blank">shopping_product</a></code>: </strong><a href="https://developers.google.com/google-ads/api/fields/latest/shopping_product?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-productperformancereportingchangesapr2026&amp;utm_content=readmore-cost#metrics.cost_micros" target="_blank">Cost</a> and <a href="https://developers.google.com/google-ads/api/fields/latest/shopping_product?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-productperformancereportingchangesapr2026&amp;utm_content=readmore-conversion#metrics.conversions" target="_blank">Conversion</a> metrics will start returning data for Video, Demand Gen, and App campaigns, not just Shopping and Performance Max.
<li><strong>Consistent campaign reporting with <code>shopping_performance_view</code>:</strong> All campaign types that use <a href="https://support.google.com/merchants/answer/12159157?hl=en" target="_blank">Google Merchant Center (GMC)</a> will have results returned with <code><a href="https://developers.google.com/google-ads/api/fields/latest/shopping_performance_view?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-productperformancereportingchangesapr2026&amp;utm_content=readmore-shopping_performance_view" target="_blank">shopping_performance_view</a></code>.
<li><strong>Network transparency for Performance Max:</strong> All <a href="https://developers.google.com/google-ads/api/fields/latest/shopping_performance_view?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-productperformancereportingchangesapr2026&amp;utm_content=readmore-networks#segments.ad_network_type" target="_blank">networks</a> will start being returned for Performance Max campaigns when querying for <code>shopping_performance_view</code>, so you may notice a one-time increase in all product reporting metrics for these campaigns. Note that data for these new metrics and expanded campaign coverage will only be available starting from <strong>June 15 2026</strong>. Historical API requests for dates prior to the launch will not contain this expanded data.</li></ul>

<p>
If you have any questions or want to discuss this post, please reach out to us on our <a href="http://goo.gle/ads-and-measurement-discord" target="_blank">“Google Advertising and Measurement Community” Discord server</a>. 
</p>

<p><span class="byline-author"><img height="40" src="https://blogger.googleusercontent.com/img/a/AVvXsEhMd1fdKsHQ-Ld1S2S7p1QnHKGIsAxgkzDAnAZ4Ennu3TL968-LZlrDhnCAtVhhh-UUMIKK6ecAadUoYY2_S-nU6HNVWDZK4vE28WYzIilQUhe8Fh_FMOaFo5sahlfpyIV7j_sR8xS-HtM_KU_deoWN91Y3dk21HE65O2lzO4fd8aOAFTxqpd2-rVhO5XM" style="vertical-align: middle; border: none;" width="40" />&nbsp;-&nbsp;Dora Sun - Google Ads API Team</span></p>
