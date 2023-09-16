---
title: "VM time and date (NTP) incorrect"
weight: 1
---

## Scenario

Post start, you find your VM's time and date is not up to date. Sometimes off by weeks or months.

## Common Causes

1. This happens when the `sudo sntp -sS time.apple.com` fails inside of the VM post-start. We've disabled automatic NTP syncing to support suspended VM states (it causes problems), so our addons will execute the `sntp` command post-start.
   - Addons log to `/var/log/anka.log` inside of the VM and may indicate/log what went wrong.

## Solution

1. You can manually run `sudo sntp -sS time.apple.com` in your jobs to ensure macOS is synced properly.

## Still experiencing problems?

Talk to us! we are available via [slack](https://slack.veertu.com/) or [email](mailto:support@veertu.com)