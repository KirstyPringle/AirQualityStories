# Air Quality Stories — GitHub Pages Starter


A minimal Jekyll site for collecting stories via a form and plotting approved entries on a map.


## Quick start


1. **Create repo** named `yourusername.github.io` (or any repo with GitHub Pages enabled).
2. **Upload** all files from this folder structure to the repo root.
3. **Enable Pages**: Settings → Pages → Deploy from a branch → `main` → `/ (root)`.
4. **Form email**:
- Sign up at https://formspree.io
- Create a form and get the endpoint like `https://formspree.io/f/abcde123`.
- Edit `submit.md` and replace `YOUR_FORM_ID` with your ID.
5. **Approve stories**: When you receive a submission by email, copy the details into `data/stories.geojson` as a new `Feature` with `[lon, lat]` coordinates and commit. The map updates automatically.


## Tips
- Ask submitters for lon/lat to avoid manual geocoding, or later wire in an API (Mapbox/OpenCage).
- To keep history tidy, you can store raw submissions elsewhere and only publish approved ones here.
- If the map shows nothing, open the browser console for errors and validate your GeoJSON at https://geojson.io.


## Privacy
Add any additional consent or privacy notes in `submit.md` and/or a dedicated `privacy.md` page.

Link is here:  https://kirstypringle.github.io/AirQualityStories/
