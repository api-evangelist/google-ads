---
title: "Merchant API is coming to Google Ads scripts starting April 22, 2026"
url: "http://ads-developers.googleblog.com/2026/04/merchant-api-is-coming-to-google-ads.html"
date: "2026-04-09T11:31:00.000-07:00"
author: "Google Ads Developer Advisor (noreply@blogger.com)"
feed_url: "http://ads-developers.googleblog.com/feeds/posts/default"
---
<p>
  The
  <a href="https://developers.google.com/shopping-content/guides/rel-notes?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-merchantapi-apr2026&amp;utm_content=readmore-contentapi">Content API for Shopping</a>
  will sunset on <strong>August 18, 2026</strong>, to be replaced by the
  <a href="https://developers.google.com/merchant/api?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-merchantapi-apr2026&amp;utm_content=readmore-merchantapi">Merchant API</a>. This migration provides a shift toward more robust, scalable, and
  feature-rich integrations. For Google Ads scripts users, the Google Ads
  scripts editor will begin rolling out Merchant API support on
  <strong>April 22, 2026</strong>. While the Content API for Shopping will
  remain available until its sunset, here’s what to expect from the Merchant
  API.
</p>
<h2>Understanding the Merchant API</h2>

<p>
  The Merchant API offers important changes and improvements over the Content
  API for Shopping:
</p>
<ul>
  <li>
    <strong>Modular Design:</strong> The Merchant API is broken down into
    sub-APIs. This allows for:
    <ul>
      <li>Faster access to new features and updates.</li>
      <li>Easier versioning and maintenance.</li>
      <li>
        Reduced disruption, as changes in one sub-API are less likely to impact
        others.
      </li>
    </ul>
  </li>

  <li>
    <strong>New Features & Capabilities:</strong>
    <ul>
      <li>
        <strong><a href="https://developers.google.com/merchant/api/guides/product-studio/overview?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-merchantapi-apr2026&amp;utm_content=readmore-productstudio_api">Google Product Studio API</a>:</strong>
        Leverage generative AI features.
      </li>
      <li>
        <strong><a href="https://developers.google.com/merchant/api/guides/reviews/products?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-merchantapi-apr2026&amp;utm_content=readmore-reviews_api">Reviews APIs</a>:</strong>
        Upload and manage product and store reviews.
      </li>
      <li>
        <strong><a href="https://developers.google.com/merchant/api/guides/accounts/notifications?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-merchantapi-apr2026&amp;utm_content=readmore-notifications_api">Notifications API</a>:</strong>
        Enable notifications for changes.
      </li>
      <li>
        <strong>Expanded Data Source Management:</strong> Create and manage
        various data source types, including:
        <ul>
          <li>
            <a href="https://developers.google.com/merchant/api/reference/rest/datasources_v1/accounts.dataSources?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-merchantapi-apr2026&amp;utm_content=readmore-supplemental_data#supplementalproductdatasource">Supplemental product data</a>
          </li>
          <li>
            <a href="https://developers.google.com/merchant/api/reference/rest/datasources_v1/accounts.dataSources?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-merchantapi-apr2026&amp;utm_content=readmore-local_inventory_data#localinventorydatasource">Local inventory data</a>
          </li>
          <li>
            <a href="https://developers.google.com/merchant/api/reference/rest/datasources_v1/accounts.dataSources?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-merchantapi-apr2026&amp;utm_content=readmore-regional_inventory_data#regionalinventorydatasource">Regional inventory data</a>
          </li>
          <li>
            <a href="https://developers.google.com/merchant/api/reference/rest/datasources_v1/accounts.dataSources?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-merchantapi-apr2026&amp;utm_content=readmore-promotion_data#promotiondatasource">Promotion data</a>
          </li>
        </ul>
      </li>
    </ul>
  </li>
  <li>
    <strong>Omnichannel Support:</strong> Designed with Omnichannel in mind,
    though it provides backward compatibility for legacy separate online/local
    offer structures using the <code>legacy_local</code> flag.
  </li>
</ul>
<p>
  Take a look at the
  <a href="https://developers.google.com/merchant/api/guides/compatibility/overview?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-merchantapi-apr2026&amp;utm_content=readmore-migration_guide">Merchant API migration guide</a>
  for more detail on the changes between APIs.
</p>

<h2>How to get started</h2>

<p>
  The Merchant API will be available as an Advanced API in the Google Ads
  scripts editor, just as the Content API is.
</p>
<p>
  If you have any questions or want to discuss this post, please reach out to us
  on our
  <a href="http://goo.gle/ads-and-measurement-discord">“Google Advertising and Measurement Community” Discord server</a>.
</p>

<p>
  <span class="byline-author"><img height="40" src="https://blogger.googleusercontent.com/img/a/AVvXsEhMd1fdKsHQ-Ld1S2S7p1QnHKGIsAxgkzDAnAZ4Ennu3TL968-LZlrDhnCAtVhhh-UUMIKK6ecAadUoYY2_S-nU6HNVWDZK4vE28WYzIilQUhe8Fh_FMOaFo5sahlfpyIV7j_sR8xS-HtM_KU_deoWN91Y3dk21HE65O2lzO4fd8aOAFTxqpd2-rVhO5XM" style="vertical-align: middle; border: none;" width="40" />&nbsp;-&nbsp;Dora Sun - Google Ads API Team</span>
</p>
