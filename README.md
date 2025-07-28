# Understand Your Document - Hackathon Submission

## Overview

This project extracts a structured outline from PDFs (title, H1/H2/H3 headings with page numbers) for the hackathon challenge.

## Approach

- PDF parsing with PyMuPDF (fitz) for fast, reliable extraction.
- Headings detected by combining font size, font style (bold), keywords, and multi-language patterns (English/Japanese).
- Title guessed by picking large prominent text on the first page.
- Outputs JSON files with the outline structure per input PDF.

## Requirements

- Python 3.10+
- PyMuPDF

## How to Build & Run

**Build Docker image:**

