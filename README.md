# Husseinverse

A Next.js campus explorer for **Universiti Tun Hussein Onn Malaysia, Parit Raja**. The first version combines an original walkable Three.js campus with links and embeds for UTHM's real 360° photography.

## Run locally

Requires Node.js 20.9 or newer.

```sh
npm ci
npm run dev
```

Open http://127.0.0.1:4173. For a production build:

```sh
npm run build
npm start
```

The Next.js App Router project uses `output: 'export'`. Its production output is `out/`; it can be served by a static host. The project is also compatible with a normal Next.js deployment on Vercel. No API keys or database are required.

## Included

- Six destinations: PTTA library, Dewan Sultan Ibrahim, Masjid Sultan Ibrahim, swimming centre, stadium, and an aerial campus view.
- Orbiting campus view, smooth camera transitions, zoom, daylight/evening lighting, and selectable landmark markers.
- Third-person walking using WASD, arrow keys or on-screen controls. Shift runs; V changes view. Drag turns the camera.
- Building collision boundaries and checked arrival points.
- Real 360° tour navigation using the exact panorama identifiers published by UTHM's International Office.
- Browser-local visit progress, responsive controls, keyboard focus, and modal help.
- Optional feature-detected WebMCP navigation tools that share the visible interface's actions.

## Accuracy and current limits

This is an **independent prototype, not an official UTHM service or a surveyed digital twin**. The 3D campus is an original simplified interpretation. Major landmark relationships were checked against the January 2023 official campus map. The library and mosque use visual cues from official photographs. Other building dimensions, roads, landscaping and the avatar are illustrative. The compass indicates camera rotation, not verified geographic north. Building interiors are not modeled.

The real panorama media remain hosted by Momento360 and are credited to UTHM's published tour. The top-level library panorama was visually verified. Embedded panoramas did not render inside the development app's in-app browser, so every tour stop includes **Open full view** as a direct alternative and a delayed-loading message. External media availability depends on that provider and the visitor's browser. This implementation does not download or rehost the panorama files.

The 3D scene, landmark selection, walking mode, visit state and production build were checked. All arrival positions are validated against collision bounds during initialization. Phone-specific styles are included, but the available browser's viewport override did not take effect, so phone rendering needs a real-device check.

## Project structure

- `app/`: Next.js App Router page, metadata and global styles.
- `components/CampusExplorer.jsx`: React interface and client-only scene lifecycle.
- `lib/campus.js`: Three.js scene, landmark data, controls, tour state and navigation tools.
- `public/icon.svg`: project icon.
- `scripts/serve.mjs`: local server for the built static export.
- `.openai/hosting.json`: optional private Sites deployment identity; no credentials.

Three.js is loaded from the pinned npm dependency, not a remote script. React and Next.js own the page and client lifecycle. The scene is imported after mounting and disposes its renderer and listeners on unmount.

## What the references use

[Messenger's developer interview](https://www.commarts.com/webpicks/messenger) identifies Blender and Houdini for modeling, Three.js for the frontend, and custom controls, shaders, camera and networking. [Jalan KL](https://kl.jalanmalaysia.com/) describes original Blender models and a single-player world; its public renderer bundle also identifies Three.js.

There is no verified evidence that either reference used Blender MCP. MCP can automate Blender asset creation; it is not the runtime that runs these games in a browser. No Blender MCP connection was available during this build. No source code or models were copied from either reference.

## Path to a faithful campus reconstruction

1. Obtain an up-to-date campus plan and authorized ground-level photographs for each elevation of the priority buildings. The 2023 map is a useful reference, not a current survey.
2. Build original Blender models of PTTA, the mosque, DSI and the main entrance from those references. Match footprints and proportions before adding facade detail.
3. Export optimized GLB assets, with lightweight collision meshes and distance-based detail. Replace the corresponding procedural landmark functions without changing the tour interface.
4. Check walkable routes against campus paths and validate scale and landmarks with UTHM students or staff.
5. For a seamless realistic tour, obtain permission and source files for UTHM's panoramas or produce original 360° captures. That allows a first-party panorama viewer without relying on an external iframe.

## Factual and visual sources

- [UTHM International Office — Iconic Buildings & Facilities and embedded 360° scenes](https://io.uthm.edu.my/more-info/uthm-virtual-tour?catid=17&id=112&view=article)
- [International Student Guide, January 2023 — campus map on PDF page 4](https://io.uthm.edu.my/images/Guideline%20Book/091122-a-guide-book-for-international-student-io.pdf#page=4)
- [PTTA library history](https://ptta.uthm.edu.my/about-us/corporate-info/history.html)
- [Dewan Sultan Ibrahim — convocation location](https://convocation.uthm.edu.my/ms/istiadat/lokasi)
- [Masjid Sultan Ibrahim profile](https://pi.uthm.edu.my/tentang-kami/sejarah-penubuhan-pusat-islam-dan-masjid-sultan-ibrahim/profail-masjid-sultan-ibrahim-uthm)
- [UTHM Sports Centre facilities](https://sukan.uthm.edu.my/index.php/facilities-and-services)
- [Official mosque photograph used as modeling reference](https://pi.uthm.edu.my/images/Masjid/Masjid%20view%20sebelah%20kanan.jpg)
- [Official library photograph used as modeling reference](https://io.uthm.edu.my/media/yootheme/cache/f1/ptta%20banner-f1ef9fc6.png)

Original code and original scene geometry are included in this repository. External panoramas, linked university materials, fonts and npm packages retain their respective owners' rights and licenses. Their availability online does not transfer ownership to this project.
