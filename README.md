<p align="center">
  <img src="App Logo/echo.png" alt="Echo Music Logo" width="120" height="120" style="border-radius: 24px;" />
</p>

<h1 align="center">Echo Music Canvas</h1>

Implementing a new way to get beautiful custom canvas background videos for the **Echo Music** app.

This repository acts as the central hub for mapping custom `.m3u8` or `.mp4` background visualizers to specific songs or albums within the Echo Music client.

---

## How to Add a New Canvas

If you find a custom vertical visualizer or music video clip and want it to display as a dynamic canvas background in Echo Music whenever a specific song plays, follow these steps:

### 1. Upload your Video File
Add your video file into either the `Song/` or `Album/` directories within this repository.
* **Format:** `.m3u8` or `.mp4`
* **Example:** `Song/dracula_visualizer.mp4`

### 2. Update `canvas.json`
Open the `canvas.json` file located in the root of the repository. Add a new item block mapping the exact song name and artist to your new video URL pointing to your deployed domain.

**Example entry:**
```json
{
  "items": [
    {
      "song": "Song Title",
      "artist": "Artist Name",
      "url": "https://echo-music-canvas.pages.dev/Song/your_video.mp4"
    }
  ]
}
```

### 3. Commit and Push
Once you have uploaded your video and updated `canvas.json`, commit your changes, push them to your repository fork, and submit a Pull Request.

> [!IMPORTANT]
> When opening a **Pull Request**, please include the **original song/album link** (YouTube Music, Spotify, or similar) in the description. This helps verify metadata and ensure the canvas matches the correct track.

```bash
git add .
git commit -m "feat: added canvas for Song Title"
git push origin main
```

Once your PR is accepted and merged, it will deploy automatically to Cloudflare Pages.

---

## Technical Requirements and Guidelines

To ensure the integrity of `canvas.json` and prevent layout or loading issues, make sure your visualizer files meet the following guidelines:

* **Aspect Ratio:** `9:16` (Vertical Canvas is required for mobile playback).
* **Format:** `.mp4` or `.m3u8` files.
* **File Size:** Max **5MB** for faster buffering and low data usage.
* **Looping:** 5–20 seconds duration with a clean loop transition.

---

## Continuous Integration (CI) and Automated Merging

We run an automated validation and auto-merge workflow on every Pull Request. If a Pull Request meets all the required checks and security conditions, the repository will automatically approve and merge the PR into the `main` branch.

### Automated Merge Conditions

For a Pull Request to be merged automatically, it must pass the following checks:

1. **Security Filters (File Constraints):**
   * The Pull Request must **only** modify `canvas.json` and files within the `Song/` or `Album/` directories.
   * Any modifications to scripts, GitHub Action workflows, web pages, or stylesheets will disable auto-merge and require manual developer review.

2. **Strict Sequential Naming (Series-Wise):**
   * Newly added canvas files must follow the numerical series format (e.g. `32.mp4` or `32.m3u8`).
   * New filenames must be strictly consecutive, continuing from the highest existing committed number (no gaps, skips, or random naming schemes allowed).
   * Grandfathered legacy files (e.g. non-numerical names) are exempt, but no new ones can be added.

3. **Maximum File Size Limit:**
   * All newly added files in a Pull Request must be **equal to or less than 5 MB** to ensure fast loading and prevent build issues on Cloudflare Pages.

4. **Formatting and Integrity:**
   * **JSON Syntax:** The `canvas.json` database must be correctly formatted JSON.
   * **Schema Integrity:** The `song`, `artist`, and `url` fields must be present and match the local directory structure.
   * **No Duplicates:** No two entries in `canvas.json` can map to the exact same song and artist combination.

You can run this validation locally prior to committing:
```bash
node scripts/validate_canvas.js
```

---

## Community and Support

Need help or want to join the Echo Music community?

* **Discord Community:** [Join our Discord](https://discord.com/invite/EcfV3AxH5c)
* **Telegram Channel:** [Join our Telegram](https://t.me/EchoMusicApp)
* **Issues:** If you encounter any bugs, please [open a GitHub Issue](https://github.com/EchoMusicApp/Echo-Music-Canvas/issues).

---

## Credits and Fork Origin

* **Fork Origin:** This project is a fork of [vivimusicanvas](https://github.com/vivizzz007/vivimusicanvas) developed by [vivizzz007](https://github.com/vivizzz007).

---

## License

This project is licensed under the **GNU General Public License v3.0**. See the [LICENSE](LICENSE) file for details.
