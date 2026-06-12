# devgreeny.github.io

Resume / portfolio site. Live at https://devgreeny.github.io

Single static page: `index.html` holds all content in one JSON block plus the rendering code. `media/` holds compressed web versions of project demos. No build step, no dependencies.

## Updating (weekly or whenever)

1. Edit the JSON inside `<script id="site-data">` at the top of `index.html`:
   - New project: copy an existing object in `projects`, edit it.
   - New stat, bullet, role, skill: edit the matching array.
   - Bump `profile.updated`.
2. New media: drop web-ready files in `media/` and reference them.
   Convert phone/screen recordings first (keeps the repo small):
   ```sh
   # landscape video
   ffmpeg -i in.mov -vf "scale=1600:-2" -c:v libx264 -crf 26 -pix_fmt yuv420p -an -movflags +faststart media/out.mp4
   # portrait (phone) video
   ffmpeg -i in.MP4 -vf "scale=-2:1400" -c:v libx264 -crf 27 -pix_fmt yuv420p -an -movflags +faststart media/out.mp4
   # screenshot
   ffmpeg -i in.png -vf "scale=1400:-2" -q:v 4 media/out.jpg
   ```
3. New resume: replace `noah-guarini-resume.pdf` (keep the filename).
4. Ship:
   ```sh
   git add -A && git commit -m "update" && git push
   ```
   Live about a minute later.

Or open Claude Code in this folder and describe the change.

## Preview locally

Open `index.html` directly, or `python3 -m http.server 8000` and visit http://localhost:8000.
