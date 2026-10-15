---
title: "Automated Extraction of Governing-Law and Payment-Calendar Data from Fixed Income Filings"
excerpt: "Undergraduate capstone sponsored by Bloomberg (Drexel University, 2025–2026). Developed a pipeline for automated extraction and normalization of governing-law and payment-calendar information from Fixed Income filings."
collection: portfolio
---

**Bloomberg-sponsored Undergraduate Capstone (Senior Design), Drexel University** · September 2025 – June 2026

## Overview

Developed a pipeline for automated extraction and normalization of governing-law and payment-calendar information from Fixed Income filings for Bloomberg.

## Payment Calendar Project

This project aimed to capture and normalize payment-calendar information for Fixed Income securities whose documents define the "Business Day" conventions that drive actual payment dates. This helped client cash-management workflows for a market of ~300,000 active securities. The workstream will extract core security descriptors, locate and parse payment-calendar text, and map the extracted calendars to Bloomberg's calendar codes, routing unmapped or undefined cases for manual review.

## Governing Law Project

This project sought to extract, categorize, and standardize governing-law provisions across corporate, loan, and mortgage instruments. This captured all governing-law attributes for distinct legal regimes that potentially govern the note's terms and conditions, collateral, subordination, and disposition. The workflow included extracting security descriptors, locating the "Governing Law" section, identifying all applicable jurisdictions with categories, and mapping each to Bloomberg's enumerations.

## My contributions

- Utilized Python, NLP, and data engineering workflows to develop and evaluate experimental methods for identifying and structuring complex textual data.
- Engineered structured prompts with explicit JSON schemas and category classification across 4 governing law types.