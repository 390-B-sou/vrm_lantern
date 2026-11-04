# VRM Lantern Viewer

**A single-HTML 3D model viewer with head-tracked stereoscopic display (the "peephole window" effect)**

[日本語](README.md) | English

## Overview

I built this model viewer as a simulator for a lantern-shaped display device that uses head-tracked 3D (the peephole window effect). Because it is a single HTML file, you can try it with several PCs, phones and tablets in the browser alone and get a feel for how the device would behave.

It detects your face with the front camera and aims to make the model look as if it were really there from your point of view. The front camera's field of view is narrow, so the effect is modest, but I hope you enjoy it. Feel free to modify it.

No installation required. It runs on any OS with a supported browser: Windows, macOS, Linux, iPhone, Android. An internet connection is needed to fetch external libraries and the face-tracking model.

Note: if opening an HTML file directly is difficult (on iPhone, for example), use the online version (GitHub Pages) described in "Quick start" below.

## Features

- **Single HTML, no installation**: just open it in a browser
- **Head-tracked stereoscopic display**: face tracking (MediaPipe) and tilt sensors drive an off-axis projection
- **1 to 8 panel layouts**: switch from a single screen to a polyhedron display and a 3D preview
- **Multi-device linking (WebRTC)**: currently two panels (host + one client). Connect automatically via ntfy.sh or manually with a code. Up to 8 panels is planned
- **Environment and effects**
  - Shader-rendered day/night cycle, sky, clouds and stars
  - Particle effects (fireflies, snow, petals, rain)
  - Glowing fairies (auto-flying, they act as light sources)
  - Depth of field (blur) and backlit light pooling
  - Perspective-corrected floor photo (4-point homography) with ambient-light reflection
  - Transparent mode (AR-style display with the rear-camera feed as the background)
- **Models and motion**: load VRM / MMD, apply motions across VRM and MMD, foot-ground correction, leg-crossing prevention
- **Data storage**: saved in the browser via IndexedDB / localStorage

## Quick start

The latest version is always available on GitHub Pages:

https://390-b-sou.github.io/vrm_lantern/

Bookmark it, or put it on your desktop or home screen for easy access.

1. Open `index.html` in your browser
2. **Menu (メニュー) → File (ファイル関係) → Add model (モデルを追加)** to load a `.vrm` / `.zip` / `.pmx`
3. Press **Start camera (カメラ開始)** and allow camera access (on iPhone you will also be asked for motion-sensor permission)
4. Move your face and the view follows your viewpoint
5. To animate, add a **motion (モーション, .vrma / .vmd)** and press **Play (再生)**
6. Choose backgrounds, floors, particles and fairies in **Background settings (背景設定)**

## Supported formats

| Type | Formats |
|---|---|
| Models | `.vrm` `.zip` `.pmx` `.pmd` (MMD set) `.glb` (props) |
| Motions | `.vrma` `.vmd` |
| Background / floor | Any image, rear-camera feed |
| Audio | Any audio file the browser can play |

## Requirements and notes

- External libraries and the face-tracking model are fetched from CDNs (jsDelivr / Google Storage).
- Viewpoint tracking and two-device linking need camera permission and an internet connection.
- The app uses standard browser features such as WebGL, WebRTC and DeviceOrientation. Support and performance vary by browser and device.

## Libraries used

| Library | License | Purpose |
|---|---|---|
| Three.js 0.160.0 | MIT | 3D rendering, off-axis projection, animation. Bundled GLTFLoader / MMDLoader / MMDAnimationHelper are also used |
| @pixiv/three-vrm 3.0.0 | MIT | VRM loading, expressions, secondary motion (SpringBone) |
| @pixiv/three-vrm-animation 3.0.0 | MIT | VRMA loading and applying motion to VRM/MMD |
| fflate 0.8.2 | MIT | Unzipping MMD archives |
| MediaPipe Face Landmarker 0.10.14 | Apache-2.0 | Viewpoint estimation from face landmarks |
| Ammo.js | zlib | MMD physics (loaded only when needed) |

The viewpoint projection math, automatic baking of the background billboard figures, floor-photo distortion correction, approximate foot IK, foot-ground correction and knee-crossing prevention are all implemented within the HTML itself.

## Rights

- Rights to external libraries belong to their respective authors.
- Follow the rights holders' terms for any models, motions, images and audio you load.
- This app, including its bundled files, may be modified and redistributed freely.
- Attribution is not required, but it would be appreciated.
