---
title: "grubhook"
description: "A Go backend that fetches emails and serves takeaway order data to my nom-nom-watch device."
tags: ["Go", "Backend", "IoT"]
project_tags: ["Go", "Backend", "IoT"]
---

`Go`

[View on GitHub](https://github.com/ArunGautham-Soundarrajan/grubhook)

`grubhook` is the backend client for my `nom-nom-watch` project — a TinyGo ESP32 device I built to keep myself accountable on how often I order takeaway. It fetches the relevant emails, parses out the order data, and serves it to the device over an API.

It uses `sqlc` for type-safe SQL and a `justfile` for task automation, and is a good example of small, self-contained backend tooling built to support a piece of personal hardware rather than a general-purpose service.
