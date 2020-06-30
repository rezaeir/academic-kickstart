---
title: Bypassing Zotero Storage Limit
subtitle: a workaround to bypass Zotero storage limit using Google Drive
date: 2020-06-30T08:34:01.777Z
summary: a workaround to bypass Zotero storage limit using Google Drive
draft: false
featured: false
tags:
  - zotero
  - storage_limit
  - tutorial
  - google_drive
image:
  filename: featured.jpg
  focal_point: Smart
  preview_only: false
  caption: Photo by [Alfons
    Morales](https://unsplash.com/@alfonsmc10?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText)
    on [Unsplash](https://unsplash.com/)
  alt_text: an out of capacity library
---
## The Problem
I'm a graduate student, and [Zotero](https://www.zotero.org/) is one of the tools that I use regularly. However, I recently passed the 300 MB storage limit, and it was frustrating for me to lose this ability to sync the article's attachments, mostly PDF files, and access to them from my other devices. After searching for a way to fix this problem and not finding a good workaround, I got disappointed and just disabled attachment syncing in Zotero desktop. Whenever I wanted to save a paper in my local directory, I had to keep it separately across different devices or send that paper's Zotero folder to my other device! Soon, I understood that this isn't a viable solution and suddenly got an idea!

## Workaround
I always use Google Drive. I guess it is the best cloud storage system on the Internet. Because firstly, its free plan has much more available space than other cloud storage tools, and secondly, it connects to my Google account, which I use almost for everything. So, I thought, what if I could mount one of my Google Drive folders in both my windows devices and use that folder as my local Zotero storage. Guess what! This is a reasonably practical solution. So, without farther ado, here is the step by step tutorial.

## Tutorial

### Make a Folder for Zotero in your Google Drive
Just go to your google drive, make a new folder, and name it Zotero.

### Mount your Google Drive to access it from your File Explorer
Follow the link, download, and install the [Backup and Sync](https://www.google.com/drive/download/) tool for google drive. The installation procedure is very straight forward. It asks you to check the folders that it should backup in google drive, which you can uncheck all folders if you don't want to backup anything. In the next step, it asks you what folders in your google drive you'd like to share in your file explorer. Naturally, you should select the Zotero folder!

### Configure Zotero
Open your Zotero desktop and go to `edit --> preferences --> Advanced --> File and Folders --> Data Directory Location --> Custom`. You should give it the address to the Zotero folder on your google drive, which is by windows default in `C:\Users\<yourUserName>\Google Drive\Zotero`. After setting the location, Zotero asks you to restart the app. After re-opening, it warns you that:

> Storing the data directory in a cloud storage folder is very likely to corrupt your database.
`C:\Users\<yourUserName>\Google Drive\Zotero`
Are you sure you want to use this location?

which you should choose `Yes` and then it restarts again! If it warned you again, check the box that says, "don't ask again," The warning will go away.

### Import your old data
The setup is almost done, but you can't see any of your papers and their data in your Zotero Library. To fix this issue, you should copy the content of your old Zotero folder, which is in `C:\Users\<yourUserName>\Zotero` and paste it in your google drive folder at the location as mentioned above.

### Let Google Drive sync your content
At this moment, you can probably find the Backup and Sync app in your taskbar, which is trying to sync all those files. Depending on the size of your content, all those PDF files! It takes some time to sync.

### Disable Zotero Sync
Now that we are syncing our data with Google Drive, there is no need for Zotero to sync our data to its servers. So open your Zotero desktop and go to `edit --> preferences --> Sync` and uncheck the boxes related to automatic sync and syncing full-text content.

### Repeat all of the steps in your other devices
You already have the folder. So go through the above steps. If the first device you set was your primary device, meaning that most of your full-text papers were there, you don't need to import data from your old Zotero folder because your google drive will download the data from your primary device.

### From now on
On the surface, nothing has changed! Just go on using Zotero as always, and the data will be synced between your devices.

<h2 align="center">Ask me</h2>
<p align="center">If there is any question, feel free to ask me. I'll appreciate any feedback or comment. Enjoy reading your papers<span style='font-size:20px;'>&#128521;</span></p>
