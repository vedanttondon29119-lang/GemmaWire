# 🪄 GemmaWire: Local Whiteboard-to-UI Compiler
> **Hacktoberfest Hack Day | Qualifier Round Submission**
> *Track 2: Best Use of Gemma 4 / Gemma 4 Open-Source*

**GemmaWire turns a phone photo of a hand-drawn whiteboard wireframe into working HTML + Tailwind CSS, using an open-weight Gemma 4 model that runs entirely on your own machine. Your designs never leave your device.**

---

## Team Details

| Name | Role | GitHub |
|------|------|--------|
| Vedant Jayant Tondon | Team Lead, AI and Backend Developer: Gemma 4 setup, model connection and server logic, output cleanup, error handling, testing, documentation, final demo |_vedanttondon29119-lang_|
| Vedang Gupta | Backend Developer: image upload and API | _ved062_ |
| Devanshu Bawane | Frontend Developer: web interface and live preview | _noice-hello_ |

**Challenge Selected:** Track 2: Best Use of Gemma 4 / Gemma 4 Open-Source
## 1. Project Name
**GemmaWire**

## 2. Problem Statement
Turning a whiteboard sketch from a design meeting into a first UI scaffold is slow, manual work. Developers re-interpret boxes, arrows and handwritten labels into HTML/CSS by hand. The obvious shortcut, uploading the sketch to a cloud AI design tool, is a problem for many teams, because unreleased product designs are confidential and often cannot be sent to third-party servers.

### Existing Solutions & Why GemmaWire Is Different
Sketch/screenshot-to-code tools already exist, and GemmaWire does not claim to be the first. It targets the gap they leave open: **private, offline, open-model, whiteboard-first.**

**Cloud design-to-code tools** (e.g. v0, Uizard, Locofy)
- Run on the vendor's servers, so your design is uploaded.
- Closed models, paid by subscription or credits, need internet.
- Built mainly for mockups, screenshots and text prompts.

**Open-source screenshot-to-code projects**
- Often default to cloud APIs; local use depends on how you set them up.
- Focused on polished screenshots rather than hand-drawn sketches.

**GemmaWire**
- Runs **entirely on your own machine**. The design never leaves your device.
- Uses the **open-weight Gemma 4** model, with no ongoing cost after setup.
- Works **offline**, because all assets are served locally.
- Built for **hand-drawn whiteboard photos** as the primary input.

**Why this matters:** teams in enterprise, finance, healthcare and government often cannot upload unreleased designs to outside servers. GemmaWire lets them use multimodal AI for scaffolding without that trade-off.

## 3. Project Overview
GemmaWire is a local-first multimodal web app. A user uploads a photo of a hand-drawn wireframe; a locally hosted, quantized Gemma 4 vision-language model reads the layout and handwriting and produces semantic HTML with Tailwind CSS utility classes. The result is shown in a live preview next to the raw code, ready to copy.

## 4. Proposed Solution
A lightweight, build-step-free web application with a local AI pipeline:
1. The user uploads an image in a vanilla HTML5 interface.
2. A Python FastAPI backend validates and Base64-encodes the image and sends it to a local Gemma 4 model served by Ollama.
3. The backend sanitizes the model output (strips markdown fences and conversational filler) and returns clean HTML.
4. The frontend renders it in a sandboxed iframe and shows the code in an inspector pane.

## 5. Objectives
*   **Meaningful multimodal use:** Use Gemma 4's vision capability to read spatial layout and handwriting directly, with no separate OCR step.
*   **Hardware feasibility:** Show that useful UI generation can run fully locally on consumer-grade hardware using a quantized model.
*   **Developer speed:** Turn a photographed sketch into a working scaffold in one step instead of hours of manual markup.
*   **Privacy by design:** No network calls to external AI services at any point.

## 6. Target Users / Use Case
*   **Primary users:** UI/UX designers, product managers, and frontend engineers, especially on privacy-sensitive teams.
*   **Use case:** After a sprint planning session, a developer photographs the whiteboard, uploads it to GemmaWire, and gets a responsive Tailwind scaffold to start a new feature branch.

## 7. Open-Source AI Technology Selected
*   **Model:** Gemma 4 (vision-capable variant)
*   **Configuration:** 4-bit quantized GGUF for edge deployment
*   **Inference engine:** Ollama / llama.cpp, running locally

## 8. Why This Technology Was Selected
Gemma 4 processes text and images in one model, so it can relate boxes, nesting and handwritten labels without a fragile separate OCR pipeline. Being open-weight, it can run fully on the user's own machine, which is what makes the privacy guarantee possible. Its small, quantizable variants make consumer-hardware deployment realistic.

## 9. AI's Role in the System
The model is the core **sketch-to-UI compiler**. It:
1. Identifies containers, rows, columns, buttons, inputs and other components from the sketch.
2. Transcribes handwritten text into UI copy.
3. Emits Tailwind utility classes (`flex`, `grid`, `p-4`, `rounded-lg`) that reproduce the sketched structure.

## 10. System Architecture

```
[ User / Developer ]
       │ (Uploads JPEG/PNG)
       ▼
[ Vanilla JS Frontend ] ───(Multipart Form POST)───┐
       ▲                                           │
       │ (Live render via sandboxed iframe)        ▼
       │                                 [ FastAPI Gateway ]
       │                                           │ (Validate + Base64 encode)
       │                                           ▼
[ Output Sanitizer ] ◄───(Raw model output)─── [ Local Gemma 4 via Ollama ]
```

## 11. Component-Level Architecture
*   **Frontend:** Vanilla HTML/JS/CSS, no Node or bundler. Tailwind's browser build is **bundled locally** and served by the backend, so preview works offline.
*   **Backend (FastAPI, Python 3.11):** Multipart upload handling, file type and size validation, Base64 conversion, timeouts and error responses.
*   **Inference layer:** Python `requests` calls to the local Ollama HTTP API.

## 12. Data / Information Flow
1. **Ingestion:** User uploads an image in the browser.
2. **Transport:** Frontend posts the file via `FormData` to `/api/generate`.
3. **Validation & encoding:** Backend checks type/size and Base64-encodes the bytes.
4. **Prompting:** A payload with a strict system prompt (low temperature, e.g. `0.1`) and the image goes to the local Gemma 4 server.
5. **Sanitization:** Backend extracts the content from `<!DOCTYPE html>` to `</html>`. If the closing tag is missing (truncated output), it falls back to extracting the first complete HTML block, and if that also fails it returns a clear error with a retry option._(Thank you! for reading till now >:D . Theres not much left)_
6. **Delivery:** Clean HTML is returned and rendered in the preview iframe.

## 13. Agentic Workflow
The MVP uses a single-turn, deterministic pipeline to keep latency low and behavior predictable. Reflection loops are intentionally left out of the MVP and listed under future scope.

## 14. Technology Stack
*   **Frontend:** HTML5, CSS3, ES6 JavaScript
*   **Backend:** Python 3.11, FastAPI, Uvicorn, Pydantic, python-multipart
*   **AI infrastructure:** Gemma 4, Ollama / llama.cpp
*   **Output styling:** Tailwind CSS (bundled locally)


