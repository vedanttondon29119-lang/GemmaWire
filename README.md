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

