# Understand Your Document - Hackathon Submission

## Overview

This project extracts a structured outline from PDFs (≤50 pages) in JSON format, capturing:

- Document **title**
- Headings categorized as **H1**, **H2**, and **H3**
- Page numbers for each heading

The solution is designed to work fully **offline**, on **CPU-only** environments, with a runtime under 10 seconds per 50-page PDF. It supports **multiple languages**, including **Japanese**.

## Approach

- **PDF Parsing:** Uses [PyMuPDF (fitz)](https://pymupdf.readthedocs.io/en/latest/) for fast and reliable text extraction, including Unicode and CJK (Chinese/Japanese/Korean) support.

- **Heading Detection:**  
  Combines multiple heuristics, including:
  - Font size and style (boldness, capitalization)
  - Presence of common heading keywords and patterns (e.g., "Chapter", "Section", "第1章" in Japanese)
  - Text position and visual cues  
  This avoids relying solely on font size, making it robust against different PDF styles.

- **Title Extraction:**  
  Selects the largest and most prominent text on the first page as the document title.

- **Multilingual Support:**  
  Detects English and Japanese heading cues to support a variety of documents.

- **Output Structure:**  
  Produces one JSON file per input PDF containing the document title and an array of headings with their levels and page numbers.

## Dependencies

- Python 3.10+
- [PyMuPDF](https://pymupdf.readthedocs.io/en/latest/) (installed via `requirements.txt`)

## How to Build & Run

### Prerequisites

- Docker installed on a Linux/amd64-compatible machine  
- No internet connection is required after image build

### Steps

1. **Build the Docker image:**

docker build --platform linux/amd64 -t mysolutionname:somerandomidentifier .


2. **Prepare folders:**

- Create an `input/` folder and place your PDF files there.
- Create an empty `output/` folder where JSON results will be saved.

3. **Run the container:**

docker run --rm
-v $(pwd)/input:/app/input
-v $(pwd)/output:/app/output
--network none
mysolutionname:somerandomidentifier


4. **Check results:**

- For each PDF in `input/`, a corresponding `.json` outline will be available in `output/`.

## Output JSON Example

{
"title": "Understanding AI",
"outline": [
{ "level": "H1", "text": "Introduction", "page": 1 },
{ "level": "H2", "text": "What is AI?", "page": 2 },
{ "level": "H3", "text": "History of AI", "page": 3 }
]
}


## Key Strengths

- **Modular, readable code:** Separation of PDF parsing (`main.py`) and heading extraction logic (`utils/heading_extractor.py`).
- **No models or external services:** Fully offline with no ML model dependency.
- **Language-agnostic heuristics:** Support for English, Japanese, and similar languages with Unicode-compatible methods.
- **Efficient:** Processes 50-page PDFs in under 10 seconds on CPU-only environments.
- **Robust heading detection:** Combines font size, font style, regex patterns, and spatial cues to improve accuracy.

## Notes

- The solution assumes that input PDFs are reasonably formatted with clear heading styles.
- Does not rely on document-specific hardcoded logic — fully generic.
- Designed to run consistently inside a Docker container for easy portability.

If you have any questions or require additional details, feel free to reach out!


