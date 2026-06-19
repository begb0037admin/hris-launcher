# CLAUDE.md — hris-launcher
> AI bootstrap entry point. Read this first.
> Keep this file under 200 lines.

## Identity
- **Project:** HRIS Launcher
- **Purpose:** Central launch pad for University of Oxford HRIS Support Centre — single-click access to all production and non-production HRIS environments, support tools, and service catalogues.
- **Owner:** Kevin Lelitte, Manager/Director HR Systems, University of Oxford
- **Status:** Active — static, minimal maintenance required
- **Repo:** https://github.com/begb0037admin/hris-launcher
- **Live site:** https://begb0037admin.github.io/hris-launcher/
- **Last updated:** 2026-06-18

## Bootstrap Order
1. This file (orientation)
2. `index.html` — the entire dashboard, single file

## Architecture
| Component | Description |
|---|---|
| `index.html` | Single-file static dashboard. Oxford navy sidebar, all HRIS environment tiles. No framework, no build step, no server. |

## What's in the Dashboard
- **Production UOXP:** Back Office, Staff Portal, e-Recruitment, HR Reporting, Tableau Server, Discoverer Plus/Viewer, Customer Success Portal
- **Non-Production PeopleXD:** UOXZ (Sandpit & Training), UOXC (Config), UOXU (UAT)
- **Non-Production HR Reporting:** DEV, TEST, QA
- **Sidebar:** HRIS Support, Support Tools, Service Catalogue, Other Teams, Data Protection

## Day-to-Day
Nothing to do — open the live URL. It is always up.
Share `https://begb0037admin.github.io/hris-launcher/` with the team.

## How to Update
1. Edit `index.html` — update tile URLs, nav links, or clone dates
2. Push directly to main — GitHub Pages rebuilds in ~60 seconds
3. Update clone dates when a non-prod environment is refreshed: search for the env code (UOXZ, UOXC, UOXU) and update the `env-date` div

## Hard Rules
- Single `index.html` — no framework, no build step
- No credentials in any file
- Always push directly to main

## Branch and Merge Protocol
Always push directly to main. If a branch must be used, merge it to main immediately upon completion — never leave files on a branch.
