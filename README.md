# MTM Program Dashboard

Single-page dashboard for Rethink Food's MTM program. Reads aggregated weekly metrics from a published Google Sheet CSV. No backend — deploys to GitHub Pages as a static file.

---

## Setup checklist

### 1. Publish the CSV URL

1. Open the export Google Sheet (`1P_l_FMfoaHfr59mwkbWXteee2oRyVaxz5ixRVIrArE8`)
2. **File → Share → Publish to web**
3. Choose **Sheet1** and format **CSV**, then click **Publish**
4. Copy the URL provided
5. In `index.html`, replace `YOUR_PUBLISHED_CSV_URL_HERE` with that URL

### 2. Deploy to GitHub Pages

1. Push this repo to GitHub
2. Go to **Settings → Pages → Source → Deploy from branch → main / root**
3. Copy the resulting URL (e.g. `https://rethink-food.github.io/MTM-Dashboard/`)

### 3. Configure email reports

1. Open the export Google Sheet
2. Go to **Extensions → Apps Script**
3. Paste the contents of `Code.gs` into the editor (or append the three `send*` functions if `snapshotCurrentWeek` is already there)
4. At the top of the file, fill in:
   - `RECIPIENTS` — array of email addresses
   - `DASHBOARD_URL` — the GitHub Pages URL from step 2
5. Add time-based triggers (**Triggers → + Add Trigger**):
   | Function | Day | Time |
   |---|---|---|
   | `snapshotCurrentWeek` | Every Friday | 6–7 pm |
   | `sendMondayReport` | Every Monday | 8–9 am |
   | `sendFridayReport` | Every Friday | 4–5 pm |
   | `sendTuesdayReport` | Every Tuesday | 9–10 am |

---

## Data privacy note

The dashboard only reads the **export sheet** (`Sheet1`), which contains aggregated numbers only — no PII. The source Members, Schedule, and Grocery Schedule tabs are never accessed.

---

## Local development

Open `index.html` directly in a browser. The fetch will fail until a CSV URL is configured (CORS-safe once published via Google's publish-to-web).
