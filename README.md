# Video Downloader: TikTok No Watermark, Instagram, YouTube, X

Paste links from **any** social network, get videos that **play everywhere**, in the resolution you choose, with or without sound. One Actor for TikTok (no watermark), Instagram Reels and posts, YouTube videos and Shorts, X/Twitter, Facebook videos and Reels, **Threads**, **Reddit** (no login), **Kwai** and **Kuaishou** (no watermark), **Douyin** (no watermark, no cookies), **Vimeo**, **Snapchat Spotlight**, **Bilibili**, Pinterest, LinkedIn, Bluesky, Twitch, Weibo, Dailymotion, VK, Telegram posts, Streamable, SoundCloud and 1,000+ other sites. Mix platforms in the same run.

**[Run it on Apify](https://apify.com/pomlabs/video-downloader?utm_source=github&utm_medium=readme&utm_campaign=video-downloader)**: no install, no login, free credit on a new Apify account.

## What you get

- **MP4 that always plays.** TikTok and Facebook often serve their best quality as HEVC/H.265 or VP9, which many phones, browsers, Windows players and editors can't open, and some downloaders return video without sound. With `compatibleMp4` (on by default) you get **H.264 video + AAC audio in one .mp4**; when the platform has no H.264 version at all (many Facebook Reels), we convert it for you. Every item says the real `videoCodec`, `audioCodec`, `width`, `height` and `fileDurationSeconds` we measured on the saved file.
- **Links that don't die tomorrow.** Instagram and Facebook download links expire (in our test: Instagram after about 1.5 days, Facebook after about 4.5) and TikTok/YouTube links only open from the IP that asked for them. In `file` mode we save the video in your run's storage and give you a stable `fileUrl`. In `link` mode we tell you **when the link expires** (`linkExpiresAt`).
- **Two prices for two jobs.** Need the file? `file` mode. Only need the URL for your own pipeline? `link` mode costs 70% less.
- **Pick the resolution**: `best`, 4K, 1440p, 1080p, 720p, 480p, 360p, 240p, 144p or `smallest`. We take the best one up to your choice, and every item lists what the site offers (`availableQualities`) and what you got (`quality`, `width`, `height`). 1080 means 1080p also for vertical videos (1080x1920), not a shrunken 608x1080.
- **With sound, without sound, or sound only**: `audio: "none"` gives a muted MP4 (no audio bytes downloaded when the site has separate tracks); `audio: "only"` gives m4a (original AAC, no re-encoding), mp3 (64 to 320 kbps) or wav for podcasts, music and transcription pipelines.
- **List before you download**: `mode: "info"` returns title, author, counters and **every resolution and format** the site has (codec, size, bitrate, direct link when the site allows) for the price of a link.
- **Sites other downloaders skip**: Reddit without an account, Douyin without cookies, Kwai/Kuaishou and Vimeo from server IPs, Snapchat Spotlight, Bilibili up to 720p, Threads.
- **Clip by time**: set `clipStart`/`clipEnd` (seconds or mm:ss) to get only the part you need.
- **SHA-256 checksum** and exact byte size for every file, for archiving and deduplication.
- **Clear status per link**: `ok`, `private_or_login`, `unavailable`, `not_video`, `unsupported`, `too_large`, `invalid_url`, `blocked`, `live`, `drm_protected`.

## Pricing

**You pay only for videos delivered: $0.005 per saved video ($5 per 1,000; YouTube $0.015), or $0.0015 per direct link ($1.50 per 1,000).** Private, deleted, login-only or invalid links are listed with the reason and **never charged**.

That is the free-plan price; Apify paid plans (Bronze, Silver, Gold) pay less per item.

## Call it by API

```bash
curl -X POST "https://api.apify.com/v2/acts/pomlabs~video-downloader/run-sync-get-dataset-items?token=YOUR_APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"urls": ["https://x.com/historyinmemes/status/1790637656616943991", "https://www.instagram.com/reel/DZk8a2Us7bf/"]}'
```

Python:

```python
from apify_client import ApifyClient

client = ApifyClient("YOUR_APIFY_TOKEN")
run = client.actor("pomlabs/video-downloader").call(run_input={"urls": ["https://x.com/historyinmemes/status/1790637656616943991", "https://www.instagram.com/reel/DZk8a2Us7bf/"]})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

## Use it from Claude, Cursor or any MCP client

```bash
claude mcp add video-downloader "https://mcp.apify.com?tools=pomlabs/video-downloader" -t http
```

## Ready-made examples

- [Download TikTok without watermark in HD (MP4)](https://apify.com/pomlabs/video-downloader/examples/download-tiktok-without-watermark-hd)
- [Download an Instagram Reel as MP4](https://apify.com/pomlabs/video-downloader/examples/download-instagram-reel-mp4)
- [Download a video from X (Twitter)](https://apify.com/pomlabs/video-downloader/examples/download-x-twitter-video)

## More Actors by Pom Labs

- [YouTube Transcript Scraper: Translate, No Login · $3/1K](https://apify.com/pomlabs/youtube-transcript-scraper?utm_source=github&utm_medium=readme&utm_campaign=video-downloader)
- [Instagram Transcript Scraper: Reels, TikTok, Facebook, Hook](https://apify.com/pomlabs/social-video-transcript?utm_source=github&utm_medium=readme&utm_campaign=video-downloader)
- [Reddit Scraper: Deleted & Removed, Mods, Hidden Profiles](https://apify.com/pomlabs/reddit-posts-comments-scraper?utm_source=github&utm_medium=readme&utm_campaign=video-downloader)
- [LinkedIn Company Scraper (No Cookies): Posts, Similar Companies](https://apify.com/pomlabs/linkedin-company-scraper?utm_source=github&utm_medium=readme&utm_campaign=video-downloader)
- [YouTube Comments Scraper + Replies, Shorts · No API Key · $1/1K](https://apify.com/pomlabs/youtube-comments-scraper?utm_source=github&utm_medium=readme&utm_campaign=video-downloader)
- [Instagram Profile Scraper: Exact Followers, Reels Views](https://apify.com/pomlabs/instagram-profile-data?utm_source=github&utm_medium=readme&utm_campaign=video-downloader)
- [LinkedIn Profile Scraper (No Cookies) + Similar Profiles](https://apify.com/pomlabs/linkedin-profile-scraper?utm_source=github&utm_medium=readme&utm_campaign=video-downloader)
- [Threads Scraper: Keyword Search, Posts & Profiles · No Login](https://apify.com/pomlabs/threads-scraper?utm_source=github&utm_medium=readme&utm_campaign=video-downloader)
- [AliExpress Scraper: Exact Units Sold, Prices, Search · $1/1K](https://apify.com/pomlabs/aliexpress-scraper?utm_source=github&utm_medium=readme&utm_campaign=video-downloader)
- [AI Brand Visibility Tracker - ChatGPT, Claude & Perplexity](https://apify.com/pomlabs/ai-brand-visibility?utm_source=github&utm_medium=readme&utm_campaign=video-downloader)
- [Mercado Livre & Amazon BR Coupon Code Checker](https://apify.com/pomlabs/mercadolivre-coupon-checker?utm_source=github&utm_medium=readme&utm_campaign=video-downloader)
- [Page Time Machine · Wayback Diff + AI · No Login · $2.5/1K](https://apify.com/pomlabs/page-time-machine?utm_source=github&utm_medium=readme&utm_campaign=video-downloader)
- [NSFW Image Detector & Image Tagger - Moderation + Categories](https://apify.com/pomlabs/image-moderation-tagger?utm_source=github&utm_medium=readme&utm_campaign=video-downloader)
- [Google Trends Scraper: Related Queries, No 429 · $2/1K](https://apify.com/pomlabs/google-trends-scraper?utm_source=github&utm_medium=readme&utm_campaign=video-downloader)

Full documentation, input fields and output format: [Video Downloader: TikTok No Watermark, Instagram, YouTube, X on Apify](https://apify.com/pomlabs/video-downloader?utm_source=github&utm_medium=readme&utm_campaign=video-downloader).
