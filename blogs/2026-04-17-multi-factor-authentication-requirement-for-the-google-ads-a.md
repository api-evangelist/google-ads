---
title: "Multi-factor authentication requirement for the Google Ads API"
url: "http://ads-developers.googleblog.com/2026/04/multi-factor-authentication-requirement.html"
date: "2026-04-17T06:41:00.000-07:00"
author: "Google Ads Developer Advisor (noreply@blogger.com)"
feed_url: "http://ads-developers.googleblog.com/feeds/posts/default"
---
<p>
As part of improving security for Google Ads accounts, the Google Ads API will start requiring Multi-factor authentication (MFA) for Google Ads API users. These important security updates will start rolling out from <strong>April 21, 2026</strong>, and will be enabled for all users over the next few weeks.
</p>
<p>
<strong>What is MFA?</strong>
</p>
<p>
MFA, also known as <a href="https://support.google.com/accounts/answer/185839" target="_blank">2-step verification</a> or 2SV, is an important security measure. In addition to your password, MFA requires another proof of identity, known as an authentication factor, to successfully sign in to an account. By requiring the second factor, you’re making it significantly harder for unauthorized users to breach your account, and a compromised password alone is not enough to gain access.
</p>
<p>
<strong>What is changing?</strong>
</p>
<p>
Once this change goes live, users following the <a href="https://developers.google.com/google-ads/api/docs/oauth/user-authentication?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-adsapi-2sv-apr2026&amp;utm_content=learnmore-apidocs-authentication" target="_blank">user authentication workflow</a> to generate new OAuth 2.0 refresh tokens for Google Ads API will always be challenged with a second factor for authentication in addition to a username and password.
</p>
<p>
If you don’t have 2-step verification enabled, you will be prompted to add a 2-step verification method.
</p>


<div class="separator" style="clear: both;"><a href="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjXtCbKx_eZoVXzq5RmUdzy6KmNKdtHPWg1iedRxqoufhqkdwOBcF-rVUPXHryFvjfPo8qy5qHZ8xTPUxGZDbwQebIQivXjbz79AcnrAON8c1lHJj_caXqgH1jWxPYMDayxZblWWTxk7QFvb8ZdjHcGzM5-ukDSzMcGqTaYwJLggZD-8XPcHIRIaYJSkyo/s1600/oauthimage.png" style="display: block; padding: 1em 0; text-align: center;"><img alt="" border="0" src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjXtCbKx_eZoVXzq5RmUdzy6KmNKdtHPWg1iedRxqoufhqkdwOBcF-rVUPXHryFvjfPo8qy5qHZ8xTPUxGZDbwQebIQivXjbz79AcnrAON8c1lHJj_caXqgH1jWxPYMDayxZblWWTxk7QFvb8ZdjHcGzM5-ukDSzMcGqTaYwJLggZD-8XPcHIRIaYJSkyo/s1600/oauthimage.png" /></a></div>


<p>
<strong>What action do I need to take?</strong>
</p>
<p>
You may be affected by this change, depending on the authentication workflow that your application uses.
</p><ul>

<li><strong><a href="https://developers.google.com/google-ads/api/docs/oauth/service-accounts?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-adsapi-2sv-apr2026&amp;utm_content=learnmore-apidocs-authentication" target="_blank">Service account workflow</a></strong>: Service account workflows are not affected by this change, so no action is required. We strongly recommend using service account workflow for applications that require automated or offline workflows.
<li><strong><a href="https://developers.google.com/google-ads/api/docs/oauth/user-authentication?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-adsapi-2sv-apr2026&amp;utm_content=learnmore-apidocs-authentication" target="_blank">User authentication workflow</a></strong>: If your app generates OAuth 2.0 refresh tokens for users, you will be affected as follows: <ul>

 <li>Existing OAuth refresh tokens are not affected by this change. They will continue to work as usual, and you won’t be prompted for reauthorization when obtaining OAuth access tokens.
 <li>New users will be challenged with a second factor for authentication in addition to a username and password. </li> </ul>
</li> </ul>

<p>
<strong>What other platforms are affected by this change?</strong>
</p>
<p>
If you use <a href="https://support.google.com/google-ads/editor/answer/2484521" target="_blank">Google Ads Editor</a>, <a href="https://developers.google.com/google-ads/scripts/docs/start?utm_source=googleblog-adsdevs&amp;utm_medium=blog&amp;utm_campaign=adr-adsapi-2sv-apr2026&amp;utm_content=learnmore-scripts" target="_blank">Google Ads Scripts</a>, <a href="https://docs.cloud.google.com/bigquery/docs/google-ads-transfer" target="_blank">BigQuery Data Transfer Service</a> or <a href="https://docs.cloud.google.com/data-studio/connect-to-google-ads" target="_blank">Data Studio</a> to manage Google Ads, you will start getting challenged with a second factor for authentication in addition to a username and password. If you don’t have 2-step verification enabled, you will be prompted to add a 2-step verification method.
</p>
<p>
<strong>How can users check and enable MFA?</strong>
</p>
<p>
Users can check whether MFA is enabled for their account by opening the <strong>Security</strong> tab of their <a href="https://myaccount.google.com/security" target="_blank">Google Account settings page</a>. The <strong>2-Step Verification</strong> setting is displayed in the <strong>How you sign in to Google</strong> section. If MFA isn’t enabled, follow the on-screen steps displayed in this section.
</p>
<p>
If you don't see the 2-Step Verification option for your account, your administrator might have disabled it. Contact <a href="https://support.google.com/a/answer/6208960" target="_blank">your administrator</a> for assistance.
</p>
<p>
<strong>Troubleshooting</strong>
</p>
<p>
<strong>Q:</strong> When I navigate to the <a href="https://myaccount.google.com/security" target="_blank">Google Account settings page</a>, I don’t see the 2-Step Verification option for my account.
</p>
<p>
<strong>A:</strong> If you don't see the 2-Step Verification option for your account, your administrator might have disabled it. Contact <a href="https://support.google.com/a/answer/6208960" target="_blank">your administrator</a> for assistance.
</p>
<p>
<strong>Q:</strong> I don’t have a 2-step verification option enabled for my account. When I attempt to sign in, I get an error that "Google couldn’t verify this account belongs to you." and I am prompted to <strong>Recover account </strong>instead of prompting me to <strong>add a 2-step verification</strong>.
</p>
<p>
<strong>A:</strong> In certain situations, Google needs additional verification before letting you add a second factor to your account. To fix the issue, navigate to the <strong>Security</strong> tab of your <a href="https://myaccount.google.com/security" target="_blank">Google Account settings page</a>. The <strong>2-Step Verification</strong> setting is displayed in the <strong>How you sign in to Google</strong> section. If 2-Step Verification isn’t enabled, follow the on-screen steps displayed in this section. Wait for a few minutes and attempt signing into the Google Ads API application again.
</p>
<p>
For any questions or further discussion regarding this update, please connect with us on the <a href="http://goo.gle/ads-and-measurement-discord" target="_blank">"Google Advertising and Measurement Community" Discord server</a>. 
</p>




<p><span class="byline-author"><a href="https://g.dev/anash" target="_blank"><img height="40" src="https://lh3.googleusercontent.com/a-/AD_cMMRmfdsXvZhyLvWsLuqqcScxtYI0ih7DPGCk8lTee140NzXH=s300" style="vertical-align: middle; border: none;" width="40" /></a>&nbsp;-&nbsp;<a href="https://g.dev/anash" rel="author" target="_blank">Anash P. Oommen</a>, Google Ads API Team</span></p>
