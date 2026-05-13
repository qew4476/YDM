# Agents Guide

## Project Summary

YDM is a legacy Windows desktop application for downloading videos from YouTube playlists through Internet Download Manager (IDM). The repository contains multiple UI experiments, but the core user-facing flows are centered on playlist parsing and handing resolved media URLs to IDM.

## Primary Entry Points

- `yListerFull.py`: older Tkinter-based playlist downloader flow
- `tabbed_Extended.py`: PyQt4-based GUI wrapper around `ydmAPI.py`
- `ydmAPI.py`: helper functions for folder picking and per-video stream discovery
- `ylister.py`: older command-line playlist parsing script
- `Makefile`: simple helper for regenerating `tabbedUI.py` from `tabbedUI.ui`

## Repository Layout

- `pafy/`: vendored dependency used for YouTube metadata and stream extraction
- `tabbedUI.ui`, `first.ui`, `videoOptionWidget.ui`: Qt Designer UI files
- `tabbedUI.py`: generated Qt UI code
- `README.md`: original project description and legacy setup notes
- `temp.html`: scratch output used by older parsing flow

## Environment Expectations

- OS target is Windows
- Python target in the original project is Python 3.4+, but the code is old and not guaranteed to run on modern Python unchanged
- PyQt4 is referenced directly and may not be available in current environments
- IDM is expected at:
  - `C:\Program Files (x86)\Internet Download Manager\IDMan.exe`

## Important Constraints

- Treat this as a legacy codebase
- Preserve existing behavior unless the task explicitly calls for modernization
- Be careful with Python 3.12+ compatibility changes
- Do not assume the vendored `pafy` implementation is interchangeable with current upstream packages
- The repo may contain generated UI code; prefer editing `.ui` sources or the thin wrapper files unless regeneration is part of the task

## Practical Working Notes

- Check both Tkinter and PyQt paths before changing shared logic
- If a task touches download execution, verify path quoting carefully because IDM is launched through a command string
- If a task touches playlist parsing, expect brittle YouTube HTML assumptions in the legacy logic
- Prefer targeted fixes over broad refactors unless explicitly requested

## Suggested Validation

- Static read-through of the affected entry point
- Run the smallest relevant script for the change
- If UI changes are made, verify the startup path used by that UI stack
- If dependency or runtime issues block execution, document the blocker clearly
