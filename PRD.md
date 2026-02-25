# Self-Hosted Beginner PDF - Project Specification

**Status:** PLANNING

## Overview
Create a 50+ page PDF guide: "Self-Hosted 101: The Zero-Jargon Guide for Absolute Beginners"

## Target Audience
- Non-technical people who want to self-host
- r/selfhosted beginners asking "where do I start?"
- People intimidated by command line

## Phase 1: Research
- [x] Scrape r/selfhosted for top beginner questions
- [x] Research popular self-hosted tools in 2026
- [x] Identify the beginner journey/steps
- [x] Output: research-findings.md

## Phase 2: TOC Design
- [x] Create detailed table of contents
- [x] Define 10-12 chapters
- [x] Ensure learning flow (easy → hard)
- [x] Output: table-of-contents.md

## Phase 3: Content Writing
- [x] Write Chapter 1: What is Self-Hosting?
- [x] Write Chapter 2: Why Self-Host? Benefits
- [x] Write Chapter 3: What Do You Need? (Hardware)
- [x] Write Chapter 4: Choosing Your First Service
- [x] Write Chapter 5: Getting Started with a Pi/Homelab
- [x] Write Chapter 6: Networking Basics
- [x] Write Chapter 7: Security Fundamentals
- [x] Write Chapter 8: Backups (Critical!)
- [x] Write Chapter 9: Popular Services to Start With
- [x] Write Chapter 10: Troubleshooting Common Issues
- [x] Write Chapter 11: Going Further
- [ ] Write Appendix: Resources & Links (optional)

## Phase 4: Consolidate
- [x] Merge all chapters into single markdown
- [x] Add cover page
- [ ] Convert to PDF (needs pandoc or similar)
- [ ] Proofread and format

## Technical
- Format: PDF (Markdown source)
- Length: 50+ pages
- Style: Zero jargon, beginner-friendly

## Ralph Loop Setup
- PRD items: Each chapter is a task
- Progress tracked in: progress.json
- Loop until all content complete
