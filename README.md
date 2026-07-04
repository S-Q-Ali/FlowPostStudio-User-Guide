# FlowPost Studio — User Guide

> Upload once, publish everywhere. A complete guide to managing your video and image distribution across YouTube Shorts, Instagram Reels, Facebook Pages, and TikTok.

---

## Table of Contents

1. [Getting Started](#getting-started)
2. [Dashboard](#dashboard)
3. [Uploading & Distributing Content](#uploading--distributing-content)
4. [Managing Your Queue](#managing-your-queue)
5. [Content Calendar](#content-calendar)
6. [Google Sheets Workflows](#google-sheets-workflows)
7. [Connected Accounts](#connected-accounts)
8. [Troubleshooting](#troubleshooting)

---

## Getting Started

### Authentication

FlowPost Studio uses a dual authentication system.

**Email & Password (Admin users)**

Enter your email and the app password configured by the administrator. If you are an admin user, you will be prompted to answer your security questions to complete the sign-in.

**Google OAuth (Regular users)**

Click **Sign in with Google** to authenticate using your Google account. A session is created linking your Google account for publishing to YouTube.

> **Note:** New signups are currently disabled. Only users with an existing account in the system can authenticate.

### Security Questions (Admin 2FA)

Admin users must answer two security questions after email sign-in:

- **Favourite Teacher** — Your childhood teacher's name
- **Best Night Date** — A memorable date

These are set once by the administrator and can be used to recover access if the password changes.

After successful authentication, you will be redirected to the Dashboard.

---

## Dashboard

The Dashboard provides an at-a-glance overview of your content publishing activity.

![Dashboard overview]

### Stats Cards

| Metric | Description |
|---|---|
| **Videos Uploaded** | Total number of videos/images you have uploaded |
| **Scheduled** | Number of posts waiting to be published |
| **Published** | Number of successfully published posts |
| **Connected Accounts** | Number of social accounts linked to FlowPost |

### Recent Activity

The lower section shows your five most recent posts with their current status and platform icons. Click any post to navigate to the Queue for more details.

---

## Uploading & Distributing Content

### Step-by-Step Guide

#### 1. Upload a File

Navigate to **Upload** in the sidebar.

- Drag and drop a video or image onto the upload area, or click to browse
- For **videos**: Accepted formats are **MP4** and **MOV**, recommended aspect ratio **9:16** (vertical / portrait)
- For **images**: Accepted formats are **JPEG** and **PNG**
- File size limit: **500 MB**

![Upload area]

#### 2. Select Platforms

Choose which platforms to publish to:

- **YouTube Shorts**
- **Instagram Reels**
- **Facebook Page**
- **TikTok** ![Beta badge]

After selecting a platform, choose which connected account to use. You can select multiple accounts per platform (e.g., multiple YouTube channels).

Platform availability depends on whether you have selected a video or image. TikTok and YouTube only accept videos; images can be published to Facebook and Instagram.

#### 3. Customize Content Per Platform

Each platform has its own fields:

| Platform | Field | Purpose |
|---|---|---|
| **YouTube** | Title (required) | Video title that appears in search results |
| **YouTube** | Description | Longer description for the video page |
| **Instagram** | Caption | Post caption displayed with the Reel |
| **Facebook** | Caption | Post caption displayed with the video |
| **TikTok** | Caption | Post caption (max 2,200 characters) |

#### 4. Content Settings

**Altered Content Disclosure**
YouTube requires you to disclose if your video contains altered or synthetic content. Select **Yes** or **No**.

**Auto-Captions**
Toggle burn-in subtitles to embed auto-generated captions directly into the video.

**YouTube Quota Warning**
If your daily YouTube quota usage reaches **50%**, a yellow badge appears. At **80%** the badge turns red and shows the estimated number of remaining uploads. This helps you avoid hitting the 10,000 unit daily limit (each upload consumes approximately 1,600 units).

#### 5. Publish or Schedule

Choose when to publish:

**Publish Now**
The file is uploaded and publishing begins immediately. You will be redirected to the Queue to monitor progress.

**Schedule**
Pick a future date and time. The video will be published automatically at the scheduled time.

![Publish options]

#### 6. Monitor Progress

During upload, a progress bar shows the current status:

- **Uploading** — File is being transferred to cloud storage (percentage shown)
- **Processing** — Publishing has been triggered on the platform
- Check the **Queue** page for detailed per-platform status

---

## Managing Your Queue

The Queue page shows all your posts — both scheduled and in-progress.

### Post Statuses

| Status | Meaning |
|---|---|
| **Scheduled** | Awaiting its scheduled publish time |
| **Processing** | Currently being published (file uploading to platform) |
| **Publishing** | Platform is still processing the file |
| **Published** | Successfully published |
| **Failed** | Publishing encountered an error |

### Actions

| Action | How |
|---|---|
| **Edit** | Click the pencil icon to change captions, hashtags, or scheduled time |
| **Reschedule** | Open the post and pick a new date/time |
| **Delete** | Click the trash icon to cancel a scheduled or failed post |
| **Retry** | Click the retry icon on a failed post to re-schedule it for re-publishing in 1 minute (only available within 24 hours of upload) |
| **Bulk select** | Use checkboxes to select multiple posts for bulk operations |

### Bulk Operations

Buttons at the top let you:

- **Select All** — Select all visible posts
- **Select 20** — Select the first 20 posts
- **Clear** — Clear the current selection
- **Delete N** — Delete all selected posts (appears when items are selected)

### Filters

Use the filter buttons to show posts by status: **All**, **Scheduled**, **Processing**, **Published**, or **Failed**.

---

## Content Calendar

The Calendar page provides a monthly view of all your scheduled and published content.

### Views

| View | Description |
|---|---|
| **Month** | See all posts arranged by date on a calendar grid |
| **List** | Chronological list of all posts for the selected month |

### Navigation

- Use the left/right arrows to switch between months
- Click any date to see posts scheduled for that day
- Click on a post card to view details in a popup dialog

---

## Google Sheets Workflows

Workflows automate content publishing by pulling videos or images directly from a Google Sheet and posting them on a recurring schedule.

### How It Works

1. You maintain a Google Sheet with rows of media links (videos or images)
2. FlowPost checks the sheet on a configurable schedule
3. Rows marked **"ready to post"** are automatically processed
4. Media is uploaded to the platforms you specify

### Setting Up a Workflow

#### Step 1 — Prepare Your Sheet

Create a Google Sheet with these columns (header row is required):

| Column Name | Required | Description |
|---|---|---|
| `video_url` | For video workflows | Google Drive sharing URL of the video |
| `image_url` | For image workflows | Direct image URL |
| `fb_ig_caption` | No | Caption used for Facebook and Instagram video posts |
| `image_fb_ig_caption` | No | Caption used for Facebook and Instagram image posts |
| `tiktok_caption` | No | Caption for TikTok (max 2,200 characters) |
| `status` | Yes | Set to **`ready to post`** to trigger publishing |

Each platform reads its own caption column. There are no fallback chains — if a column is empty, an empty string is used.

#### Step 2 — Choose Media Type

When creating a workflow, select the **Media Type**:

| Type | Supported Platforms | Sheet Columns Used |
|---|---|---|
| **Video** | YouTube, Instagram, Facebook, TikTok | `video_url`, `fb_ig_caption`, `tiktok_caption` |
| **Image** | Facebook, Instagram | `image_url`, `image_fb_ig_caption` |

Image workflows automatically exclude YouTube and TikTok.

#### Step 3 — Create a Workflow

1. Go to **Workflows** in the sidebar
2. Click **Create Workflow**
3. Fill in:

| Field | Description |
|---|---|
| **Name** | A label for this workflow |
| **Media Type** | Video or Image |
| **Google Sheet URL** | The URL of your Google Sheet |
| **Platforms** | Which platforms to publish to |
| **Accounts** | Specific platform accounts to use |
| **Max Posts Per Run** | How many posts to process each time (default: 1) |
| **Post as Story** | Also publish as an Instagram/Facebook story after the main post |

#### Step 4 — Choose a Scheduling Mode

FlowPost offers three independent scheduling modes. Choose the one that fits your publishing cadence:

| Mode | Description |
|---|---|
| **Once Daily** | Runs once per day within a set hour window (e.g., between 9 AM and 5 PM UTC). A random minute within the window is selected to avoid congestion. |
| **Interval** | Runs repeatedly every N hours (e.g., every 4 hours) on selected days of the week |
| **Custom Ranges** | Define precise per-day time ranges (e.g., Monday 9-11 AM and 2-4 PM, Tuesday 10 AM-12 PM) |

**Per-Day Time Overrides**
You can optionally set different time windows for specific days of the week, overriding the global trigger window.

#### Step 5 — Activate

Toggle the workflow to **Active**. The system will begin checking the sheet on its schedule.

### Processing Behavior

- Only rows with `status = "ready to post"` are processed
- After processing, the sheet status is updated to **"posted"** or **"failed"**
- Multiple workflows can run independently
- Manual runs can be triggered from the Workflows page for immediate processing

### Best Practices

- Keep video files under 500 MB
- Use Google Drive share links that are accessible by the service account
- Only mark rows as "ready to post" when the file is finalized
- For image workflows, ensure `image_url` columns contain direct image URLs

---

## Connected Accounts

The Accounts page manages all your social media connections.

### Supported Platforms

| Platform | What You Can Do |
|---|---|
| **YouTube** | Publish Shorts to your channel(s) |
| **Facebook** | Publish videos and images to your Page(s) |
| **Instagram** | Publish Reels, Photo posts, and Stories to your Business account(s) |
| **TikTok** | Publish videos to your TikTok account (Beta) |

> TikTok is currently in **Beta**. Videos are published with `SELF_ONLY` privacy while app review is in progress.

### Connecting an Account

1. Go to **Accounts** in the sidebar
2. Click **Connect** next to the platform you want to link
3. You will be redirected to the platform's authorization page
4. Grant the requested permissions
5. You will be returned to FlowPost with the account connected

**Important notes per platform:**

| Platform | Notes |
|---|---|
| **YouTube** | Requires a Google account. Multiple channels supported. |
| **Facebook** | Requires a Facebook Page. You can connect multiple Pages. |
| **Instagram** | Connected automatically when you connect a Facebook Page that has a linked Instagram Business account. You cannot connect Instagram directly. |
| **TikTok** | Requires a TikTok account with developer access. Currently shows a Beta badge. |

### Managing Connections

| Action | How |
|---|---|
| **View status** | Each account shows its connection status (Connected / Not Connected) |
| **Disconnect** | Click Disconnect to remove an account from FlowPost |
| **YouTube quota** | A yellow/red badge next to YouTube accounts shows your daily upload usage |

### Token Expiry

OAuth tokens expire periodically. FlowPost automatically attempts to refresh tokens when possible. If a token cannot be refreshed, you will see a notification prompting you to reconnect the account.

---

## Troubleshooting

### Upload Fails

| Symptom | Likely Cause | Solution |
|---|---|---|
| "Failed to obtain upload URL" | System configuration issue | Contact the administrator |
| File rejected | Unsupported format | Use MP4/MOV (video) or JPEG/PNG (image) |
| Upload stalls at 0% | System configuration issue | Contact the administrator |
| "File too large" | Exceeds 500 MB limit | Compress the file or split into shorter clips |

### Post Stuck on "Processing" or "Publishing"

Posts can remain in these states if an error occurs during publishing.

Common causes:
- **OAuth token expired** — Reconnect the account in Accounts page
- **File URL inaccessible** — Verify the file is still accessible
- **API quota exceeded** — Check your platform's API usage limits
- **Instagram still processing** — Instagram Reels require processing before publishing. FlowPost waits up to 4 minutes, checking periodically, before reporting a failure.

### Retrying Failed Posts

If a post fails, you can retry it from the Queue page:

1. Navigate to **Queue** and filter by **Failed**
2. Click the **retry icon** (circular arrow) next to the failed post
3. The post is re-scheduled for retry shortly after
4. **24-hour limit** — Retry is only available within 24 hours of the original upload. After that, the file is removed from storage.

### OAuth Errors

| Error | Solution |
|---|---|
| "Google hasn't verified this app" | The Google OAuth consent screen is in testing mode. Add your email as a test user in Google Cloud Console. |
| "Access token not found" | Reconnect the account |
| "Token refresh failed" | The refresh token may have expired. Reconnect the account |

### Google Sheets Workflow Not Triggering

| Symptom | Solution |
|---|---|
| Workflow is active but nothing happens | Check that the trigger window includes the current hour and the correct scheduling mode is selected |
| "Failed to read sheet" error | Ensure the Google Sheet is shared with the FlowPost system |
| Rows not being processed | Ensure row status is exactly **`ready to post`** (lowercase) |
| File not found | Verify the URL is correct and the file is accessible |
| Wrong caption used | Ensure you are using the correct column: `fb_ig_caption` for videos, `image_fb_ig_caption` for images |

### TikTok-Specific Issues

| Symptom | Solution |
|---|---|
| "Privacy level not allowed" | TikTok Beta mode publishes with `SELF_ONLY` visibility. Only the account owner can see the video. |
| "Creator not authorized" | The TikTok account may need to be reconnected. Go to Accounts and reconnect. |
| TikTok fails to publish | TikTok captions are limited to 2,200 characters. Ensure your caption fits within this limit. |

### Getting Help

If you encounter issues not covered here, contact the administrator with the post ID and any error message shown in the app.
