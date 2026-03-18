# Quiltix

> Convert any photo into a pixel-style quilt pattern with fabric yardage calculations.

See [VISION.md](./VISION.md) for the product north star, goals, and non-goals. Start there before contributing.

---

## Stack

| Layer | Technology |
|---|---|
| Frontend | React |
| Backend | Python, FastAPI |
| Image Processing | Pillow, scikit-learn |
| PDF Export | ReportLab |
| Testing (logic) | pytest |
| Testing (UI) | Playwright |

---

## How It Works

1. User uploads a photo and provides inputs (quilt size, block size, fabric count, seam allowance)
2. The image is resized to match the quilt grid dimensions
3. K-means color quantization reduces the image to N colors
4. Each pixel is mapped to its nearest quantized color
5. Yardage per color is calculated (cut size = finished size + 2× seam allowance)
6. A visual grid preview and fabric requirements list are returned to the user
7. User exports a printable pattern

---

## Project Structure

```
quiltix/
├── VISION.md               # Product north star — read first
├── README.md               # This file
├── docs/
│   └── stories/            # User stories by feature area
│       ├── US-001-photo-upload.md
│       ├── US-002-quilt-inputs.md
│       ├── US-003-color-quantization.md
│       ├── US-004-grid-preview.md
│       ├── US-005-yardage-calculation.md
│       └── US-006-pattern-export.md
├── frontend/               # React application
├── backend/                # FastAPI + image processing
└── tests/
    ├── unit/               # Logic and math assertions
    └── e2e/                # Playwright UI tests
```

---

## Getting Started

> Setup instructions will live here once the initial implementation is underway.

---

## User Stories

User stories are stored in `docs/stories/`. Each file covers one feature area and includes acceptance criteria that map directly to automated tests. This is intentional — the stories are the specification, and the tests are the verification.

This project is also Case Study 1 for the [story-first-ai](https://github.com/[your-handle]/story-first-ai) methodology experiment.

---

## Development Notes

- Seam allowance defaults to **1/4"**. Cut size = finished size + 1/2".
- All measurements flow through a unit-aware data model. Imperial ships first; metric is a future toggle.
- Color quantization quality is an accepted risk. Tuning happens with stakeholder feedback post-MVP.
