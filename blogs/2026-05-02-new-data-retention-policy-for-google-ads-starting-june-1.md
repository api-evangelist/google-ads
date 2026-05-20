---
title: "New Data Retention Policy for Google Ads starting June 1, 2026"
url: "http://ads-developers.googleblog.com/2026/05/new-data-retention-policy-for-google.html"
date: "2026-05-01T17:40:17.036-07:00"
author: "Google Ads Developer Advisor (noreply@blogger.com)"
feed_url: "https://ads-developers.googleblog.com/atom.xml"
---
Starting June 1, 2026 , Google Ads and related measurement APIs will transition to a 37-month data retention policy for granular performance statistics (daily, hourly, and weekly). High-level data (monthly, quarterly, and yearly) will continue to be available for 11 years. API Impact Next Steps Google Ads API and Google Ads scripts Starting June 1, 2026, queries that request granular segments (such as segments.date, segments.week) for ranges older than 37 months from the current date will return a DateRangeError.INVALID_DATE error.
