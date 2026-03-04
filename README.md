# SimpleLapse

SimpleLapse is a **browser-based timelapse image capture tool** (HTML + JavaScript) that lets you preview a camera feed and save JPEG frames to a folder at a fixed interval—no Python installs, no OpenCV, no CLI.

![SimpleLapse Screenshot](1.jpg)

## What you can do with SimpleLapse

- Pick from available cameras (dropdown)
- Choose a target resolution (or custom)
- Set capture interval (seconds)
- Set a capture duration (hours / minutes / seconds) — **0 = infinite**
- Pick an output folder and a **project name** (used as the save subfolder)
- Get clear on-screen status showing whether it’s capturing, plus counters for saved frames and failures

---

## Usage

1. **Open SimpleLapse in your browser** (see Installation below).
2. Click **Choose folder…** and select where you want frames saved.
3. (Optional) Enter a **Project name**:
   - If you leave it blank, SimpleLapse creates a folder like: `run_YYYYMMDD_HHMMSS`
   - If the project folder already exists, SimpleLapse shows a warning and requires confirmation before continuing.
4. Select your **Camera** from the dropdown.
5. Choose a **Resolution** (or select **Custom…** and enter width/height).
6. Set your **Interval (seconds)** and (optional) **Duration**.
7. Click **Start Preview** to verify the camera view.
8. Click **Start Capture** to begin saving images.
9. Click **Stop** (or press **Q**) to stop capturing.

Saved images are written as JPEGs named like:

- `frame_000001_YYYYMMDD_HHMMSS_mmm.jpg`

---

## Settings

### Output directory
- **Choose folder…**: Selects the parent folder where SimpleLapse will create the project subfolder.
- Your browser will ask for permission to read/write in the selected folder.

### Project name
- Used as the **subfolder name** inside the chosen output directory.
- If the folder already exists:
  - A warning appears
  - You must check the confirmation box to proceed
- If empty, SimpleLapse uses the timestamp style:
  - `run_YYYYMMDD_HHMMSS`

### Camera
- Dropdown lists detected camera devices.
- If names are blank or the list seems incomplete:
  - Click **Start Preview** once to grant camera permission
  - Then click **Reload Cameras**

### Resolution
- Select a common preset (e.g., 1920×1080) or choose **Custom…**
- Note: browsers/cameras may not honor every requested resolution. The **actual** resolution is shown in the preview panel.

### Interval (seconds)
- How often SimpleLapse saves a frame.
- Example: `2.0` saves one image every 2 seconds.

### JPEG quality (0–1)
- Output quality for saved JPEGs.
- Example: `0.95` is high quality.

### Duration (hours / minutes / seconds)
- Total capture time.
- Set all to `0` for infinite capture (runs until you stop it).

### Capture status & counters
- Preview overlay and header pill indicate **Capturing** vs **Idle**
- Counters show:
  - **Saved**: number of frames written
  - **Failures**: frames that failed to capture/write (permission, device hiccups, etc.)
  - **Next capture**: next scheduled capture time

---

## Installation / Running

SimpleLapse is a static site (just HTML/JS). You don’t “install” it—just serve it locally so the browser can access camera + folder APIs.

### Option A: VS Code + Live Server (recommended)
1. Install **Visual Studio Code**
2. Install the extension **Live Server** (by Ritwick Dey)
3. Open this repo folder in VS Code
4. Right-click `index.html` → **Open with Live Server**
5. Your browser opens SimpleLapse at a local address (usually `http://127.0.0.1:5500/`)

### Option B: Any simple local web server
You can use any local server that serves the repo over `http://localhost`:

- **Node.js**: `npx serve`
- **Python** (if you happen to have it): `python -m http.server`
- **Other**: any local dev server of your choice

> Tip: For best compatibility, use **Chrome** or **Edge**.  
> The folder-saving feature relies on the **File System Access API**, which is best supported in Chromium-based browsers.

---

## Notes / Limitations

- You can’t type an arbitrary filesystem path (that’s a browser security restriction). You must **pick a folder**.
- Camera permissions and device labels may require granting permission first.
- Not all cameras support all resolutions; SimpleLapse shows the **actual** resolution being delivered by the camera.
