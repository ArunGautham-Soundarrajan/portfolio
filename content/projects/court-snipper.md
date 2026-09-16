---
title: "Court Snipper"
description: "An automated bot that books contested sports courts the moment slots open, using headless browser automation."
tags: ["Go", "Automation", "Browser Automation"]
project_tags: ["Go", "Automation", "Browser Automation"]
---

`Go`

_Private project — source not public._

`Court Snipper` is a bot that automates booking sports courts before they get taken. It signs in to the booking site, checks a configured set of time slots on a schedule, and books the first one available, using headless Chrome automation ([go-rod](https://github.com/go-rod/rod)) driven from a scheduled GitHub Actions workflow.

It deals with the messy realities of automating a real website rather than a clean API: distinguishing similarly-named selectors, retrying failed bookings with backoff, and running reliably headless in CI — virtual displays, sandboxing flags, the works — instead of only on a local machine.
