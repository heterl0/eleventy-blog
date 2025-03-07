---
title: "Building MonkeyType Logger: A Typing Tracker Error Extension"
description: How I built MonkeyType Logger, a browser extension that records and analyzes typing errors to improve speed and accuracy.
date: 2025-02-28
tags:
  - experience
  - development
  - open-source
  - touch-typing
  - productivity
pageType: blog
og_image: monkeytype-extension.png
---


## Table of Contents
1. [My Journey to Faster and More Accurate Typing](#my-journey-to-faster-and-more-accurate-typing)
2. [Automating the Error Tracking Process](#automating-the-error-tracking-process)
3. [Extension for Tracking Typing Errors](#extension-for-tracking-typing-errors)
   - [Content.js (Capturing Typing Results)](#contentjs-capturing-typing-results)
   - [background.js (Handling Events)](#backgroundjs-handling-events)
   - [popup.html & popup.js (User Interface)](#popuphtml--popupjs-user-interface)
4. [Analyzing Typing Errors](#analyzing-typing-errors)
   - [Jupyter Notebook (AI-Based Analysis)](#jupyter-notebook-ai-based-analysis)
   - [Website for Data Visualization](#website-for-data-visualization)
5. [Conclusion](#conclusion)
6. [Check Out My Work](#check-out-my-work)

## My Journey to Faster and More Accurate Typing

### The Beginning

Around **four months ago**, I started practicing **Monkeytype daily** to improve my **typing speed and coding efficiency**. Initially, I made good progress, but after about **one month**, I got stuck at a speed of **80-90 WPM** and couldn’t improve further.

To break through this plateau, I decided to **track my typing mistakes** systematically. I began **writing down all the words I mistyped** and used **AI to analyze them**, identifying patterns and areas for improvement. Additionally, I started practicing specific coding-related typing techniques to enhance accuracy.

Check out my extension here! [Monkeytype History Logger - Microsoft Edge Addons](https://microsoftedge.microsoft.com/addons/detail/monkeytype-history-logger/ophgnpohledibffckhpabdcciniinnjo)
## Automating the Error Tracking Process

I then thought: *Why not automate this tracking process?* This led me to develop a **browser extension** that **automatically records error words** from my typing history.

## **Extension for Tracking Typing Errors**

### **Content.js** (Capturing Typing Results)

This file detects the **appearance of result history elements** on the screen and sends an event to `background.js` for processing.

```json
{
    "id": 1740714390907,
    "time": "2025-02-28T03:46:30.907Z",
    "words": [
      { "reason": "corrected", "word": "be" },
      { "reason": "corrected", "word": "part" },
      { "reason": "corrected", "word": "not" },
      { "reason": "error", "word": "then" },
      { "reason": "error", "word": "some" }
    ]
}
```

Each record consists of:
- **id**: A unique identifier for the session.
- **time**: The timestamp of the recorded session.
- **words**: A list of words where mistakes occurred.
  - **reason**: Explanation for the mistake:
    - `corrected`: A word that was mistyped but corrected.
    - `error`: A word that was mistyped and skipped.
  - **word**: The actual word that caused the issue.

### **background.js** (Handling Events)

This script listens for events and processes them. It currently supports three key actions:
- **Saving Records**: The `SaveRecords` event stores error logs in `chrome.storage.local`. With the `unlimitedStorage` permission, we can store up to **10,000 records** (each 100 records take about **50KB**).
- **Deleting Last Record**: The `DeleteLastRecords` event removes the most recent entry for data management.
- **Downloading Records**: This event enables users to **download their records as a JSON file** for offline analysis.

### **popup.html & popup.js** (User Interface)

The extension’s popup displays:
- Extension name
- Last recorded session
- Total stored records
- Buttons for **download, delete, and import** functionalities

**Current Issue**: Sometimes, `chrome.storage.local` loses the records, resetting them to zero. As a workaround, I manually **download and re-import** the data. Fixing this bug is a priority for the next update.

## **Analyzing Typing Errors**

### **Jupyter Notebook (AI-Based Analysis)**

If you're familiar with **Python** and **Jupyter Notebook**, you can analyze your typing data using AI techniques. Simply:
1. Place `monkeytype_data.json` in the same directory as your Jupyter Notebook file.
2. Run the notebook to see **detailed insights** into your typing mistakes and improvements.

[📊 View My Jupyter Notebook Analysis](https://github.com/heterl0/monkeytype-logger/blob/main/monkeytype-analysis/typing-error-analysis-notebook.ipynb)

### **Website for Data Visualization**

I also built a **Next.js web app** (deployed on **Vercel Hobby Tier**) that lets users:
- Upload their JSON file.
- Visualize typing mistakes and progress trends.
- Gain personalized insights for improvement.

[🌐 Visit My Analysis Website](https://monkeytype-analysis.heterl0.live/)

This analysis helps me **refine my typing habits** and develop an **AI-based assistant** for further improvements.

## **Conclusion**

If you want to improve your typing skills like I did, try this **free and open-source extension**. Follow the instructions and start tracking your mistakes.

💡 **Benefits:**
- Real-time tracking of errors and corrections
- AI-powered analysis for targeted improvements
- Web-based visualization of your progress

🚀 **How to Get Started:**
1. Install the extension on your preferred browser.
2. Practice typing and let the extension track mistakes automatically.
3. Regularly review your errors and adjust your practice accordingly.

Remember, **consistent practice is key** to increasing your typing speed and accuracy. Happy typing! 🎯

## **Check Out My Work**

🔗 [My Extension on GitHub](https://github.com/heterl0/monkeytype-logger)
🔗 [My Extension on Store](https://microsoftedge.microsoft.com/addons/detail/monkeytype-history-logger/ophgnpohledibffckhpabdcciniinnjo)
🔗 [My Jupyter Notebook Analysis](https://github.com/heterl0/monkeytype-logger/blob/main/monkeytype-analysis/typing-error-analysis-notebook.ipynb)
🔗 [My Website for Analysis](https://monkeytype-analysis.heterl0.live/)
🔗 [Follow My Blog Feed](https://heterl0.live/feed/feed.xml)