# ShiftTrack

A mobile-friendly web app for tracking time spent across work locations during a shift. Built as a single HTML file — no installation, no backend, no accounts required.

---

## What It Does

ShiftTrack lets you log which work locations you visit during a shift and how long you spend at each one. At the end of your day you get a full timeline and a breakdown of time per location.

It was built for a retail district manager visiting multiple store locations throughout the day, but works for anyone who moves between a fixed set of locations during a workday.

---

## Features

### Location Tracking
- **GPS auto-detection** — registers your coordinates at each location once, then detects you automatically when you arrive
- **Manual check-in** — tap to check in to any location if GPS is unavailable or slow
- **Detection radius** — adjustable from 30m to 300m depending on how your locations are spaced

### Home Screen
- List of all locations sorted by most recently visited
- Color-coded last visit timestamps (green = recent, amber = a few days, red = overdue)
- Shows which location you're currently at in real time

### Shift Management
- Start and end shifts manually
- **Auto-start** — automatically starts a shift at a set time on weekdays if none is active
- **Auto-end** — automatically ends and saves your shift at a scheduled time
- **Auto-save & resume** — active shift state is saved every 30 seconds; if your browser closes unexpectedly, the app detects the interrupted shift on next open and offers to resume, save, or discard it

### Timeline & Summary
- Full chronological timeline of every location visited during the shift
- Time spent per location with visual bar chart
- Total shift duration

### History
- All completed shifts saved and accessible
- Each shift shows date, start/end times, total duration, and locations visited
- Manual entries are clearly labeled

### Log Past Shifts
- Forgot to start your shift? Enter any past date and manually add location visits with arrival and departure times
- Full validation — catches missing fields, overlapping times, and reversed arrivals/departures

### Edit Any Shift
- Tap Edit on any history entry to adjust shift times or individual visit times
- Add or remove location visits after the fact

### Data & Backup
- **JSON backup** — exports everything (shifts, GPS pins, settings) to a `.json` file that can be re-imported to restore data on any device or browser
- **CSV export** — exports shift history as a spreadsheet, one row per location visit, ready for Excel or Google Sheets
- **Restore from backup** — upload a `.json` backup to merge data; duplicates are automatically skipped
- **Clear all data** — wipe everything with a confirmation prompt

---

## Setup

### First Time
1. Open the app in your browser
2. Go to the **Setup** tab
3. For each location, physically stand there and tap its card — the app saves your GPS coordinates
4. Set your **Auto-start** and **Auto-end** times if desired
5. Adjust the **Detection Radius** slider if needed (start at 100m)

### GPS Note
GPS auto-detection requires the app to be served over `https://` or `http://localhost`. The easiest way is to host it on **GitHub Pages** (free), which gives you a permanent `https://` URL where Chrome will save your location permission permanently.

Running from a local `file://` path will cause GPS errors in Chrome — this is a browser security restriction, not a bug in the app.

---

## Hosting on GitHub Pages

1. Create a new **public** repository on GitHub
2. Upload `shift_location_tracker_v6.html` to the repository
3. Go to **Settings → Pages**, set source to **main / root**, and click Save
4. After ~60 seconds your app will be live at:
   ```
   https://yourusername.github.io/your-repo-name/shift_location_tracker_v6.html
   ```
5. Bookmark this URL — GPS permission will persist across sessions

---

## How to Use

### Daily Workflow
1. Open the app (it will auto-start your shift at your scheduled time if configured)
2. The app detects your location automatically as you move between stores
3. Use **Manual Check-in** on the Shift tab if GPS is slow
4. End your shift manually or let it auto-end at your scheduled time
5. Review your day on the **Timeline** tab

### If You Forget to Start
Go to the **Log Past** tab, enter the date, set your shift start and end times, and add each location visit manually.

### Backing Up Your Data
Go to the **Data** tab and tap **Download Backup** regularly — especially before clearing your browser cache or switching devices. To restore, use the **Restore from Backup** upload zone on the same tab.

---

## Locations

Pre-loaded with the following locations:

| | | | |
|---|---|---|---|
| Store #102 | Store #103 | Store #104 | Store #201 |
| Store #203 | Store #205 | Store #206 | Store #207 |
| Store #208 | Store #211 | Store #222 | Store #364 |
| Store #381 | HQ | | |

To change the location list, open the HTML file in a text editor and update the `LOCATIONS` array near the top of the `<script>` section.

---

## Technical Notes

- **No server required** — runs entirely in the browser as a single HTML file
- **Data storage** — all data is saved in the browser's `localStorage`; clearing browser data will erase it (use the JSON backup to prevent data loss)
- **GPS** — uses the browser's `navigator.geolocation` API with the Haversine formula for distance calculations
- **Offline capable** — works without an internet connection once loaded (fonts may not load offline)
- **Auto-save interval** — active shift state is written to localStorage every 30 seconds and on every check-in
- **Auto-start/end check interval** — the app checks the current time every 15 seconds while the page is open

---

## Browser Compatibility

| Browser | GPS | Recommended |
|---------|-----|-------------|
| Chrome (desktop & mobile) | ✅ | ✅ Best experience |
| Safari (iOS) | ✅ | ✅ Works well |
| Firefox | ✅ | ✅ Works well |
| Edge | ✅ | ✅ Works well |

> **Important:** GPS requires the page to be served over `https://`. Local `file://` paths will not work for GPS in Chrome regardless of permission settings.

---

## File Structure

The entire app is a single self-contained file:

```
shift_location_tracker.html   — the complete app (HTML + CSS + JS)
README.md                        — this file
```

---

*Built with Claude — iterated from idea to working prototype in a single conversation.*
