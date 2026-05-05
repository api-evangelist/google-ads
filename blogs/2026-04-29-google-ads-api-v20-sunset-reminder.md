---
title: "Google Ads API v20 sunset reminder"
url: "http://ads-developers.googleblog.com/2026/04/google-ads-api-v20-sunset-reminder.html"
date: "2026-04-29T10:47:00.000-07:00"
author: "Google Ads Developer Advisor (noreply@blogger.com)"
feed_url: "http://ads-developers.googleblog.com/feeds/posts/default"
---
<p>
Google Ads API v20 will <a href="https://developers.google.com/google-ads/api/docs/sunset-dates?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-v20-sunset&amp;utm_content=readmore-deprecationandsunset" target="_blank">sunset</a> on June 10, 2026. Starting on this date, all v20 API requests will begin to fail. Migrate to a <a href="https://developers.google.com/google-ads/api/docs/release-notes?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-v20-sunset&amp;utm_content=readmore-releasenotes" target="_blank">newer version</a> prior to June 10, 2026 to ensure your API access is unaffected.
</p>
<p>
Here are some resources to help you with the migration:
</p><ul>

<li><a href="https://developers.google.com/google-ads/api/docs/version-migration?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-v20-sunset&amp;utm_content=upgrade" target="_blank">Upgrade to the newest version</a>
<li><a href="https://developers.google.com/google-ads/api/docs/release-notes?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-v20-sunset&amp;utm_content=readmore-releasenotes-2" target="_blank">Release notes</a></li></ul>

<p>
You can view a list of methods and services your project has recently called using the <a href="https://console.cloud.google.com?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-v20-sunset&amp;utm_content=tryitout-cloudconsole" target="_blank">Google Cloud Console</a>:
</p><ol>

<li>Open <strong>APIs & Services</strong> in the Google Cloud Console.
<li>Click <strong>Google Ads API</strong> in the table.
<li>On the <strong>Metrics</strong> subtab, you should see your recent requests plotted on each graph. You can see which methods you've sent requests to in the <strong>Methods</strong> table. The method name includes a Google Ads API version, a service, and a method name, such as 

    

<pre class="prettyprint">google.ads.googleads.v20.services.GoogleAdsService.Mutate.
</pre>

<ol>

<li>(Optional) Choose the timeframe you want to view for your requests.</li></ol>
</li></ol>

<p>
If you have any questions or want to discuss this post, please reach out to <a href="https://developers.google.com/google-ads/api/support?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-v20-sunset&amp;utm_content=support-gaapi" target="_blank">Google Ads API support</a> or start a discussion on our <a href="http://goo.gle/ads-and-measurement-discord" target="_blank">“Google Advertising and Measurement Community” Discord server</a>.
</p>

<span class="byline-author"><img height="40" src="https://lh3.googleusercontent.com/a-/AOh14GhFLgYJAFpYHUS1kBcLzMIT2gKkUyYcjWCuOWM3=s600-p" style="border: none; vertical-align: middle;" width="40" /> - Ben Karl, on behalf of the Google Ads API Team</span>
