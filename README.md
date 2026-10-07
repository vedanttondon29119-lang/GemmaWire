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

