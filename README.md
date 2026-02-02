# MediaPipe Proctoring Starter (Face + Missing + Attention Proxy + EAR)

A minimal, webcam-based proctoring starter that demonstrates how you can detect and visualize:
- **Face presence** (face detected vs missing)
- **Face missing duration** (tracks how long the face disappears)
- **Looking-away proxy** (simple dx/dy heuristic using face landmarks)
- **Eye Aspect Ratio (EAR)** for **eye closure / wink / prolonged closure**

This is a *starter* for building cheating-detection signals — not a complete proctoring system.

---

## What this does

### Signals implemented
1. **Face detection + landmarks**
   - Uses MediaPipe Tasks **FaceLandmarker**
   - Draws a subset of landmarks for speed

2. **Face missing timer**
   - Starts a timer when no face is detected
   - Flags when missing time crosses a threshold (default: 2s)

3. **Looking-away (proxy)**
   - Computes `dx` and `dy` based on the nose position vs the midpoint of both eyes
   - Flags if:
     - `abs(dx)` is too large (left/right deviation)
     - `dy` is too large (head down / looking away)

4. **Eye closure / wink detection**
   - Calculates **EAR** for left and right eyes
   - Uses persistence logic to ignore normal blinks
   - Flags:
     - Both eyes closed
     - Left wink
     - Right wink

---

## Imports & dependencies (explicit)

The main script relies on the following Python standard libraries and third-party packages.

### Standard library imports
These come with Python by default.

```python
import time
import urllib.request
from pathlib import Path
## Repository structure

