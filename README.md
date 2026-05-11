# TrackMountRoblox

> Curated Roblox mount route archive containing recorded movement tracks, WASD variants, coil/VIP routes, and order-route datasets for replay, testing, and route sharing.

<p align="left">
  <img alt="format" src="https://img.shields.io/badge/format-JSON-111111?logo=json&logoColor=white">
  <img alt="platform" src="https://img.shields.io/badge/platform-Roblox-000000?logo=roblox&logoColor=white">
  <img alt="data" src="https://img.shields.io/badge/data-Mount%20Tracks-0E9F6E">
  <img alt="routes" src="https://img.shields.io/badge/routes-50%2B-6D4CFF">
  <img alt="status" src="https://img.shields.io/badge/status-Curated-1177AA">
  <img alt="owner" src="https://img.shields.io/badge/by-FyyWannaFly-5865F2">
</p>

This repository stores cleaned and consistently named mount route recordings for Roblox mount movement workflows. Each file is a standalone JSON track with frame-by-frame movement data such as position, velocity, rotation, movement direction, timing, and character state values.

The repo is intentionally simple: no app framework, no build step, and no package manager. It is a route library that can be downloaded, inspected, and consumed by external tooling.

---

## Table of contents

1. [Project overview](#project-overview)
2. [Data model](#data-model)
3. [Repository layout](#repository-layout)
4. [Route naming system](#route-naming-system)
5. [Route categories](#route-categories)
6. [Using the files](#using-the-files)
7. [Maintenance rules](#maintenance-rules)
8. [Notes](#notes)

---

## Project overview

At a high level, this repository provides:

1. **Mount route recordings**
   - recorded movement paths for different mount maps/routes
   - JSON arrays of sampled player movement frames
   - route variants for different control styles and setups

2. **Clean human-readable filenames**
   - every mount file starts with `Mount`
   - every word is capitalized for easier browsing
   - route modifiers such as `WASD`, `VIP`, `R6`, and `V2` are kept readable

3. **Order route data**
   - selected files prefixed with `Order Mount`
   - useful for routes that represent an ordered playback or order-specific path

4. **A compact route archive**
   - no generated junk files
   - no temporary test uploads
   - no unrelated binary folders

---

## Data model

Most files contain a JSON array of recorded frames:

```json
[
  {
    "time": 0,
    "position": {
      "x": -40.03893280029297,
      "y": 9.005918502807617,
      "z": 2.5321121215820312
    },
    "velocity": {
      "x": -19.240800857543945,
      "y": 0.00007808336522430182,
      "z": 1.1801910400390625
    },
    "moveDirection": {
      "x": -0.9981241226196289,
      "y": 0,
      "z": 0.061222873628139496
    },
    "rotation": 1.6229817867279053,
    "hipHeight": 4.955921173095703
  }
]
```

Common fields:

- `time` - frame timestamp or playback offset
- `position` - recorded world position
- `velocity` - movement velocity at that frame
- `moveDirection` - input/movement direction vector
- `rotation` - character or mount facing direction
- `hipHeight` - Roblox humanoid height state captured with the frame

---

## Repository layout

```text
.
├─ Mount Axis.json
├─ Mount Axis WASD.json
├─ Mount H2C.json
├─ Mount Yahayuk R6.json
├─ Order Mount Axis.json
├─ Order Mount Freestyle WASD.json
└─ README.md
```

The actual repository contains many more route files, but the layout stays flat on purpose. Keeping every route in the root makes it easy to download individual JSON files from GitHub or browse them by name.

---

## Route naming system

The current naming convention is:

```text
Mount <Route Name> <Variant>.json
Order Mount <Route Name> <Variant>.json
```

Examples:

- `Mount Axis.json`
- `Mount Axis WASD.json`
- `Mount Aetheria Coil VIP.json`
- `Mount Yahayuk Jalur 1.json`
- `Mount Yahayuk R6.json`
- `Order Mount Freestyle WASD.json`

### Naming rules

- Start normal route files with `Mount`
- Start ordered route files with `Order Mount`
- Use spaces instead of underscores
- Capitalize each route word
- Keep short technical tags uppercase where useful:
  - `WASD`
  - `VIP`
  - `R6`
  - `V2`
  - `H2C`

---

## Route categories

### Standard mount routes

Files such as:

- `Mount Axis.json`
- `Mount Granite.json`
- `Mount Luna.json`
- `Mount Velora.json`
- `Mount Yume.json`

These are the base route recordings for a named mount route.

### WASD variants

Files such as:

- `Mount Axis WASD.json`
- `Mount Bjirlah WASD.json`
- `Mount Gemi Jalur WASD.json`
- `Mount H2C WASD.json`
- `Mount Yume WASD.json`

These are route variants intended for WASD-style movement playback or control-specific movement captures.

### Coil / VIP variants

Files such as:

- `Mount Aetheria Coil VIP.json`
- `Mount Astralyn Coil 2.json`
- `Mount Gemi Coil VIP.json`
- `Mount Yahayuk Coil VIP.json`

These routes are separated because movement behavior can change depending on coil/VIP setup.

### Jalur variants

Files such as:

- `Mount Serrat Jalur 1.json`
- `Mount Serrat Jalur 2.json`
- `Mount Yahayuk Jalur 1.json`
- `Mount Yahayuk Jalur 2.json`
- `Mount Yahayuk Jalur 3.json`

These represent numbered paths or alternate route lanes.

### Order routes

Files such as:

- `Order Mount Axis.json`
- `Order Mount Freestyle WASD.json`
- `Order Mount Granite.json`
- `Order Mount Yume.json`

These are kept separate from normal mount files so tooling can identify order-specific route data quickly.

---

## Using the files

### Download a single route

Open a JSON file on GitHub, click **Raw**, then save the file locally.

### Clone the full archive

```bash
git clone https://github.com/FyyWannaFly/TrackMountRoblox.git
```

### Pull updates

```bash
git pull origin main
```

### Read from code

Any JSON parser can load the route data as an array of frame objects.

```js
const fs = require("fs");

const route = JSON.parse(fs.readFileSync("Mount Axis.json", "utf8"));
console.log(`Loaded ${route.length} frames`);
```

---

## Maintenance rules

To keep the archive clean:

- do not add temporary test files such as `aaa`, `sda.json`, or random upload dumps
- do not commit unrelated folders or zip files
- keep route filenames readable and title-cased
- prefer one route per JSON file
- use `Order Mount` only for order-specific datasets
- keep large route files as raw JSON unless a future tool needs a different format

---

## Notes

This repository is a data archive, not the route recorder/player implementation itself. Any playback behavior, automation logic, or Roblox-side integration should live in the tool that consumes these JSON files.

