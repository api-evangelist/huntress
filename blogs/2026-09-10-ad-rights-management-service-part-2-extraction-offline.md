---
title: "AD Rights Management Service (Part 2): Extraction, Offline Decryption, and the Unrotatable Key"
url: "https://www.huntress.com/blog/ad-rms-slc-encryption-key"
date: "2026-09-10"
feed_url: "https://www.huntress.com/blog/rss.xml"
---
An AD RMS Service Group account exports the AD RMS Server Licensor Certificate private key. That 1172-byte key decrypts every document the deployment ever protected, offline, and keeps doing so after the deployment is rebuilt.
