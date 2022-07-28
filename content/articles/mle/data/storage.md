---
title: "Storage"
date: 2022-03-22T13:14:59+03:00
draft: false
---

# Data Storage

## Feature Store

**Feature store** is a central repository for storing documented, curated and access-controlled features.  
Features store enables the team to re-use shared features to avoid redundant work.

Key points:
- managing feature data from a single person to an enterprise
- Scalable and performant access to features for training and serving
- provide consistent and point-in-time correct access
- enable discovery, documentation and insights

Offline feature procesing:
- feature engineering, like feature crossing
- data quality control
- offline storage
- discoverability

Online feature usage:
- low-latency access
- access to pre-computed features (computing aggregations and joins online is very time-consuming)

## Data warehoues

Key features:
- subject-oriented
- integrated (multiple data sources)
- non-volatile (access to history)

## Data Lakes

- Aggregates raw data from multiple sources
- Structured and unsctructured
- Purpose of data may be not yet determined
- Doesn't involve any data processing