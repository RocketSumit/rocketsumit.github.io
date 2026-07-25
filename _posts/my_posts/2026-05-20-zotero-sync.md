---
layout: post
title: Unlimited Zotero PDF Sync with Google Drive or OneDrive Using ZotMoov
date: 2026-05-20 21:00:00
description: Store unlimited Zotero PDFs on your own cloud storage while keeping citations synced for free.
tags: [zotero, research, productivity, google-drive, onedrive]
categories: tech
---

If you're doing academic research, **Zotero** is one of the best reference managers available. It's free, open-source, cross-platform, and has an excellent ecosystem of plugins.

One limitation you'll quickly encounter, however, is Zotero's **300 MB free cloud storage limit**. While bibliographic metadata (citations, notes, tags, collections) syncs for free, PDF attachments count against your storage quota.

Fortunately, there's a simple solution.

By using the **ZotMoov** plugin together with **Google Drive**, **OneDrive**, Dropbox, or any other cloud storage provider, you can store your PDFs on your own cloud drive while continuing to use Zotero's free sync service.

In this guide, we'll set everything up in just a few minutes.

- [Why Not Use Zotero Storage?](#why-not-use-zotero-storage)
- [How It Works](#how-it-works)
- [Prerequisites](#prerequisites)
- [Step 1: Install ZotMoov](#step-1-install-zotmoov)
- [Step 2: Configure Your Cloud Folder](#step-2-configure-your-cloud-folder)
- [Step 3: Save Your First Paper](#step-3-save-your-first-paper)
  - [Option 1: Using the Zotero Connector (Recommended)](#option-1-using-the-zotero-connector-recommended)
  - [Option 2: Drag and Drop an Existing PDF](#option-2-drag-and-drop-an-existing-pdf)
- [Step 4: Verify Everything Works](#step-4-verify-everything-works)
- [Advantages](#advantages)
- [Things to Keep in Mind](#things-to-keep-in-mind)
- [Conclusion](#conclusion)

---

## Why Not Use Zotero Storage?

Zotero synchronizes two different things:

- **Metadata** (citations, notes, collections, tags)
- **Attachments** (PDFs, images, supplementary files)

Metadata is tiny and syncs for free.

Attachments are what consume storage.

The free plan includes only **300 MB**, which is enough for roughly a few dozen papers before running out of space.

Upgrading to Zotero Storage is certainly an option, but many researchers already have access to large cloud storage through:

- Google Drive
- Microsoft OneDrive
- Dropbox
- Box
- Institutional cloud storage

Rather than paying for another storage subscription, we can simply reuse the storage we already have.

---

## How It Works

Instead of storing PDFs inside Zotero's cloud storage:

1. Zotero downloads the paper normally.
2. ZotMoov automatically moves the PDF into your cloud storage folder.
3. Zotero replaces the attachment with a **linked attachment** pointing to that file.
4. Your cloud provider synchronizes the PDF across all of your devices.

The result is:

- Zotero syncs citations and notes.
- Google Drive (or OneDrive) syncs PDFs.
- Everything appears seamlessly inside Zotero.

---

## Prerequisites

Before starting, make sure you have:

- Zotero Desktop installed
- A cloud storage desktop client installed (Google Drive for Desktop, OneDrive, Dropbox, etc.)
- A cloud folder that is synchronized locally on your computer

This method does **not** work using the Zotero web interface alone since ZotMoov is a desktop plugin.

---

## Step 1: Install ZotMoov

Download the latest `.xpi` release of ZotMoov from its GitHub Releases page.

<div class="row justify-content-md-center">
  <div class="col-sm-10 text-center">
    {% include figure.liquid path="./assets/blogs/zotero/download_xpi_file.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption"> Download .xpi file from the ZotMoov github repository </div>
  </div>
</div>

Then:

1. Open **Zotero**.
2. Navigate to **Tools → Add-ons**.
3. Click the **⚙️** icon.
4. Choose **Install Add-on From File...**
5. Select the downloaded `.xpi` file.
6. Restart Zotero.

Once restarted, a new **ZotMoov** settings page will appear in Zotero's preferences.

<div class="row justify-content-md-center">
  <div class="col-sm-10 text-center">
    {% include figure.liquid path="./assets/blogs/zotero/add_zotmoov_plugin.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption"> Install ZotMoov plugin </div>
  </div>
</div>

---

## Step 2: Configure Your Cloud Folder

Open

**Preferences → ZotMoov**

Locate **Linked Attachment Base Directory**.

Choose a folder inside your synchronized cloud storage.

For example:

```text
Google Drive/
└── My Drive/
    └── Zotero_PDFs/
```

or

```text
OneDrive/
└── Documents/
    └── Zotero_PDFs/
```

This is where every downloaded PDF will be stored.

<div class="row justify-content-md-center">
  <div class="col-sm-10 text-center">
    {% include figure.liquid path="./assets/blogs/zotero/zotmoov_preferences.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption"> Update ZotMoov preferences </div>
  </div>
</div>

---

## Step 3: Save Your First Paper

There are two ways to add PDFs to your library.

### Option 1: Using the Zotero Connector (Recommended)

Open a journal article in your browser and click the **Zotero Connector** extension.

Zotero will automatically:

- save the citation
- download the PDF
- move the PDF into your configured cloud folder using ZotMoov

### Option 2: Drag and Drop an Existing PDF

If you already have a PDF downloaded on your computer, simply drag and drop it into your Zotero library.

Zotero will automatically:

- create a new library item (or attach it to an existing item if you choose)
- import the PDF
- move it into your configured cloud folder using ZotMoov

After either method, you'll notice that the PDF attachment in Zotero has a small **link** icon instead of a regular attachment icon. This indicates that the PDF is stored in your cloud drive rather than Zotero's cloud storage.

<div class="row justify-content-md-center">
  <div class="col-sm-12 text-center">
    {% include figure.liquid path="./assets/blogs/zotero/linked_attachment_example.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption"> Example paper attachment icon with link indicator </div>
  </div>
</div>

---

## Step 4: Verify Everything Works

Double-click the linked PDF.

It should open normally inside Zotero's built-in PDF reader.

Annotations, highlighting, and note-taking all continue to work exactly as before.

If your cloud storage is synchronized across multiple computers, the linked PDFs will also be available there, provided the linked attachment base directory is configured consistently.

---

## Advantages

Using ZotMoov offers several benefits:

- Unlimited PDF storage (limited only by your cloud provider)
- Continue using Zotero's excellent citation management
- Save money if you already have cloud storage
- Keep using Zotero's built-in PDF reader and annotations
- Works with Google Drive, OneDrive, Dropbox, Box, and other synchronized folders across different machines

---

## Things to Keep in Mind

There are a few caveats worth mentioning:

- Every device should use the same relative cloud folder structure.
- PDFs are synchronized by your cloud provider, not by Zotero.
- If a PDF hasn't finished syncing yet, it won't be available on another device immediately.
- Moving or renaming files outside Zotero can break linked attachments.

For most users, these are minor trade-offs compared to eliminating storage limits.

---

## Conclusion

Zotero is an outstanding research tool, but its free cloud storage fills up surprisingly quickly once you begin collecting papers.

By combining **ZotMoov** with your preferred cloud storage provider, you can keep using Zotero's free synchronization while storing an effectively unlimited number of PDFs in Google Drive, OneDrive, Dropbox, or any other synchronized folder.

It's a simple one-time setup that can save both storage costs and frustration over the lifetime of your research library.
