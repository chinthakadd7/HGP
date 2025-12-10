# Hand Gesture Controlled Virtual Mouse

Control any Windows desktop with hand gestures captured from a webcam. The launcher app lets you pick between gesture, normal, presentation, and gaming profiles, each with tuned sensitivity and shortcuts.

---

## Features and Modes

| Mode | What it does | Typical demo |
| --- | --- | --- |
| Gesture | Full gesture-driven cursor, clicks, drag, scroll, window shortcuts | General desktop control, creative drawing apps |
| Normal | Traditional cursor with gesture-based clicks | Show fallback to classic mouse behaviour |
| Presentation | Slide-next/previous gestures with big visual prompts | PowerPoint, Google Slides, PDF decks |
| Gaming | High-sensitivity cursor with tap-to-click and drag for holding | Casual browser titles such as Bowling Champion |

The launcher (`frontend/launcher.py`) includes in-app instruction popups for each mode.

---

## Key Gestures

| Gesture | Effect |
| --- | --- |
| Index finger raised | Cursor movement |
| Index and middle fingers raised and held apart | Scroll up/down based on finger height |
| Index finger and middle finger pinched together | Left click |
| All fingers curled | Click-and-hold (drag) |
| All fingers extended | Release drag |
| Thumb pointing down | Exit the active mode |

Presentation mode maps index plus middle finger to next slide, and index only to previous slide. Additional shortcuts (minimize window, close tab) are available in gesture mode.

---

## Requirements

- Windows 10/11
- Python 3.10 or 3.11 (3.12 is not yet supported by `autopy`)
- A webcam with clear lighting

Install system dependencies such as the Microsoft Visual C++ Redistributable if `pip` reports build errors.

---

## Setup

```powershell
git clone <repository-url>
cd HGP
py -3.10 -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

If PowerShell blocks script execution, run `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned`, restart the shell, and activate the environment again.

---

## Launching the App

```powershell
python frontend\launcher.py
```

- Pick a mode in the launcher window; a separate instruction dialog appears before the mode starts.
- Use the Stop button before switching modes to ensure camera resources are released.
- The app can fall back to running the standalone scripts in `core/` when threading is unavailable.

To package for distribution, use the existing PyInstaller spec (`mouse.spec`) which copies the core scripts and assets and applies the `runtime_hook.py` path fix.

---

## Demo Ideas

- Presentations: combine Presentation Mode with PowerPoint or Google Slides and show the gesture prompts on screen.
- Games: try pointer-driven browser games such as `https://poki.com/en/g/bowling-champion`, `https://poki.com/en/g/stupid-zombies`, or management sims like Mini Metro to showcase responsiveness.
- Creative tools: sketch in Paint or whiteboard apps to highlight fine cursor control.
- Live stream: use OBS Studio to create a split view (Display Capture + Video Capture Device). Start the Virtual Camera to feed the composite into Zoom, Teams, or Meet so the audience can see both hand movement and the desktop.

---

## Troubleshooting

- `ModuleNotFoundError: No module named 'cv2'`: ensure the virtual environment is active and rerun `python -m pip install -r requirements.txt`.
- Camera unavailable: edit the camera index in the mode scripts or unplug other webcam applications before launching.
- Gestures feel laggy: improve room lighting, reduce background clutter, and avoid the drag gesture (all fingers down) unless needed.

---

## License

This project is released under the MIT License. Contributions via pull requests are welcome.
