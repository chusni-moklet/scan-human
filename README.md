# Scan Human Education — X-Ray Mirror (`scan-human`)

An interactive browser-based **X-Ray Mirror** that overlays real-time 3D head anatomy (skull, brain, facial muscles, eyes) and hand bones onto your live webcam feed using Three.js and MediaPipe.

- **Live Demo**: https://chusni-moklet.github.io/scan-human/
- **No-Camera Demo**: https://chusni-moklet.github.io/scan-human/#demo

## Features

- **Real-Time Face & Hand Tracking**: Tracks head pose, jaw movement, and up to two hands locally in the browser using MediaPipe `FaceLandmarker` and `HandLandmarker`.
- **Anatomy Layers & Presets**:
  - Toggle individual layers: **Skull** (cranium & articulated mandible), **Brain** (cerebrum & hindbrain), **Muscles**, **Eyes**, **Head outline**, and **Hand bones**.
  - Quick presets for **Skull**, **Brain**, **Muscles**, or **Everything**.
  - Toggleable **3D Anatomy Labels** for bones, brain lobes, muscles, eyes, and hand phalanges/metacarpals/carpals.
- **Visual Styles & Mixed Reality Controls**:
  - Switch between **X-ray** (additive glowing shader) and **Solid** (lit surface) look with adjustable **Brightness**.
  - Blend camera feed visibility (**Real me showing through**) and **Edge feather** softness.
  - **Reveal modes**: Whole head, Left half only, Right half only, Top of the head only, Lower face only, or **X-ray lens** (circular lens following your index fingertip or pointer).
- **Manual Head Fit & Diagnostics**:
  - Fine-tune overall size, width, height, depth, and X/Y/Z offsets (persisted in `localStorage`).
  - Optional live tracking data panel (face landmarks, estimated distance, head rotation, jaw openness, hand coordinates, and FPS).
- **No-Camera Demo Mode**: Append `#demo` to the URL to preview the 3D head and hand scene without a webcam.

## Running Locally

Because webcam access (`navigator.mediaDevices.getUserMedia`) requires a secure context (`localhost` or HTTPS), serve the directory over a local HTTP server rather than opening `index.html` via `file://`:

```bash
# Using Python
python3 -m http.server 8000

# Or using Node.js
npx serve .
```

Then open `http://localhost:8000` in Chrome or Edge (or `http://localhost:8000/#demo` to run without a camera).

## Tech Stack

- **Single-file app**: Self-contained HTML, CSS, ES module JavaScript, and quantized 3D mesh data in `index.html`.
- **3D Rendering**: [Three.js](https://threejs.org/) (`three@0.160.0` via jsDelivr) with custom GLSL vertex/fragment shaders.
- **Vision Tracking**: [MediaPipe Tasks Vision](https://developers.google.com/mediapipe) (`@mediapipe/tasks-vision@0.10.14` via jsDelivr) running locally on GPU with CPU fallback.

## Privacy & Disclaimer

- **Local Processing**: Video is processed entirely on your computer and is never uploaded.
- **Educational Use Only**: The anatomy is a 3D dataset of one adult, scaled and aligned to your tracked head pose. It illustrates where structures typically sit—not a scan of you—and is not a medical tool.

## Credits

- **Anatomy Models**: BodyParts3D, © The Database Center for Life Science, licensed under [CC Attribution-Share Alike 2.1 Japan](https://creativecommons.org/licenses/by-sa/2.1/jp/). Models were simplified and re-aligned.

