# OAM to COCO Y0 Automation

This app provides 5 pages:

1. `Input Data`
2. `Ranked Data`
3. `COCO Y0 Estimation`
4. `Result`
5. `Correlation Matrix`

## Flow

1. Upload OAM CSV from the sidebar.
2. Review parsed objects/attributes/input sheet in `Input Data`.
3. Rank data in `Ranked Data` and run COCO Y0.
4. Review COCO Y0 tables/metrics in `COCO Y0 Estimation`.
5. Generate final object ranking in `Result`.
6. Inspect attribute relationships in `Correlation Matrix`.

## Correlation Matrix

The `Correlation Matrix` page computes Pearson correlation across attribute columns (`X` data).

- Uses attribute display labels with units when available (for example: `Internet Usage 2010% [%]`).
- Shows only the lower triangle (upper triangle is muted gray/blank for readability).
- Color scale:
  - Diagonal (`1.0`): green
  - Positive correlation (`0` to `1`): yellow -> green
  - Negative correlation (`0` to `-1`): light red -> red
- Number formatting follows app rules:
  - 2 significant digits overall
  - No trailing zeros (example: `0.60` -> `0.6`)

## CSV Requirements

Required row labels in column 0:
- `Direction ID`
- `Attribute ID`
- `Attribute`

Rules:
- `Direction ID = 0`: higher value is better.
- `Direction ID = 1`: lower value is better.
- `Attribute Unit` row is optional but recommended (used in table headers).

## Tech Stack

- Python
- Streamlit
- Pandas / NumPy
- Requests + BeautifulSoup4
- OpenPyXL
- Matplotlib (optional, PNG export)

## Project Structure

```text
COCO_OAM_Automation_Lite/
  app.py
  README.md
  requirements.txt
  src/
    coco_client.py
    coco_parse.py
    oam_io.py
    ranking.py
    ui_display.py
```

## Run

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
streamlit run app.py
```

## COCO Dependency

This app submits to:
- `https://miau.my-x.hu/myx-free/coco/beker_y0.php`

Internet access is required for COCO runs.
