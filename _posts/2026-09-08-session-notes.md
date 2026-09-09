---
layout: post
title: "Session notes — September 8, 2026"
date: 2026-09-08
category: daily
tags: [epub, bookhaven, ai-evals, reading]
---

## What I worked on

| Session | Time | What | Status |
|---------|------|------|--------|
| Substack to EPUB | Evening | Hugo Bowne article on evals and harness engineering | Done |
| Lenny's Newsletter to EPUB | Evening | How we built Grok Bot in a month, plus Notion upload | Done |
| Paul Iuztin AI Evals series | Night | Eight Decoding AI articles turned into one EPUB | Done |
| BookHaven reader | Night | Heading divider and layout fixes | Done |
| MNC Job Monitor | Scheduled | Script missing, scraper failed | Needs fixing |

---

## Substack to EPUB

I converted Hugo Bowne's article "How Evals Are Central to Harness Engineering" into an EPUB. The article was written by Antaripa Saha, Hamel Husain, and Hugo Bowne-Anderson. It explains why testing (evals) should be at the center of building AI agent systems.

I used the youtube-content skill to pull the article from hugobowne.substack.com. Then I built a Python script that split the article into ten chapters based on the side headings, downloaded all six images, and made every link clickable.

The final EPUB is 621.7 KB and saved at F:/Articles/How Evals Are Central To Harness Engineering - Antaripa Saha.epub. The chapters cover: what a harness is, different types of harnesses, why evals give feedback, how to build eval-centric systems, and what evals are not.

---

## Lenny's Newsletter to EPUB and Notion

I converted Lenny's Newsletter article "How we built Grok Bot in a month" by Roman Ugarte into an EPUB. The article covers how a small team at SpaceXAI built Grok Bot in seven weeks, going from first line of code to public launch.

I wrote a Python script that creates the EPUB, uploads it to Notion, and attaches it to a page. The script used the three-step Notion file upload flow: create the upload, send the bytes, then reference the file in a block.

---

## Paul Iuztin AI Evals series

I compiled eight articles from Decoding AI Magazine by Paul Iusztin into a single EPUB. The articles walk through the full process of testing AI systems: building eval datasets, generating synthetic data, designing evaluators, evaluating the evaluators, and measuring RAG systems.

I built a Python script that reads the raw markdown files, strips out the Substack promotional content (subscribe buttons, course ads, avatar images), converts the markdown to clean HTML, and packages it all into an EPUB.

The final EPUB is 78 KB and saved at F:/Articles/YT/Paul_Iusztin_AI_Evals_and_Observability.epub. I checked all eight articles and confirmed none of them contain leftover promotional content. Article 2 has 38 links, 10 images, and 87 paragraphs.

---

## BookHaven reader

I compared the BookHaven reader prototype with reference screenshots and found the one thing it was missing: a thin horizontal line under the heading. That line is what makes a web page feel like a real book. It gives the eye a clear starting point.

I also fixed the ereader-minimalist.html layout. The table of contents and annotations buttons are now on the left of the navbar, the book title is centered, and the Aa button for font settings is on the right. I removed the search button, added a fullscreen icon instead of focus mode, and bumped the text size to 19px with tighter line spacing.

The dev server is running at http://localhost:1420/.

---

## MNC Job Monitor

The cron job failed because the script F:\job-agent\run_scraper.py no longer exists. The day before, it had found two high-scoring jobs: an AI/ML Computational Science Associate role at Accenture (score 75) and a Graduate Engineer Trainee role at Wipro (score 65).

---

## Resources

- Hugo Bowne's article: https://hugobowne.substack.com/p/how-evals-are-central-to-harness
- Lenny's Newsletter: https://www.lennysnewsletter.com/p/how-we-built-grok-bot-in-a-month
- Decoding AI Magazine: https://www.decodingai.com
- Hamel Husain's AI Evals Course: https://maven.com/parlance-labs/evals

---

## Tomorrow

- Fix the MNC job scraper script
- Continue MLT Week 2 (Kernel PCA) study
- Test the BookHaven reader with actual EPUB files
- Consider combining the EPUB conversion scripts into one tool
