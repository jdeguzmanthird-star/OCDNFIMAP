# Western Visayas Prepositioned NFI Map

## Open and use

1. Save `index.html` to a folder on your computer. If using the ZIP, extract it first.
2. Your supplied official OCD logo is already embedded in the HTML. No separate logo file is needed.
3. Double-click `index.html` and open it in a current Chrome, Edge, Firefox, or Safari browser. No installation or server is required. Leaflet, PapaParse, inventory data, and the five province boundaries have embedded copies for offline use.
4. Hover over a circle to see its site, summed quantity, and item count. Click a marker or a site in the directory to open its complete inventory. Scroll inside the item table for long lists.
5. Use **Find a site** or **Which sites hold this item?** to filter the directory and markers. Regional totals and the marker legend continue to use the complete mapped dataset.
6. Open **Item totals** for quantities by exact item name. Selecting an item shows its sites. **Group similar items** is off by default. Turn it on to remove year / EP / EPA tags and a final plural s where appropriate. Original descriptions remain stored and are shown under a grouped name in site details.
7. Click **Upload CSV**, or drop one CSV onto the page. The new file replaces the current inventory immediately after validation. Missing-column errors leave the existing inventory intact. **Data review** lists skipped physical starting row numbers and reasons.
8. Open **Data tools** to download the sample CSV or current source CSV, export every mapped site's summary, or switch between the two built-in datasets. On mobile, use **Sites & totals** to open or close the directory.

Uploads stay in the current browser session. Reloading returns to the built-in updated inventory. Keep your current CSV and upload it again next time. Nothing is uploaded to a server.

## Your two source files

The updated workbook's **as of 2026** sheet supplies the default quantities. Its older **Aug 17 -SAO** sheet is not combined with current stock. The attached original CSV supplies every mapped coordinate and the original site labels. No locations were geocoded or estimated.

| Default inventory measure | Quantity |
| --- | ---: |
| Reported stock in updated workbook | 11,153 |
| Stock at sites with CSV coordinates | 10,443 |
| Stock awaiting usable coordinates | 710 |
| Known mapped sites | 8 |
| Mapped sites with listed stock | 7 |

The eighth mapped site, Camp Hernandez, has no item quantities listed in the updated workbook. Its known CSV position remains visible with **No quantities reported**. Blank workbook cells are not represented as confirmed zero stock. No artificial inventory row was created for that site.

The original CSV snapshot has 8 sites, 34 item rows, and a total quantity of 23,886. Its Iloilo Warehouse has 18 exact item descriptions. Select **Original coordinate CSV** in Data tools to inspect that snapshot. It does not represent the updated quantities.

All 18 updated workbook item-column totals were reconciled with its TOTAL row. Status of MOU and Remarks are not inventory items. Workbook spelling is retained, including `Mega-phone` and the line break in `Rain` / `boots`. These differ from the older CSV's `Megaphone` and `Rainboots`.

### Sites awaiting coordinates

| Workbook site | Stock | Treatment |
| --- | ---: | --- |
| LGU-PDRRMO Antique San Jose | 20 | Family Tent; coordinate fields left blank |
| LGU - Nueva Valencia | 160 | Family Packs 50; Family Hygiene Kits 50; Shelter Repair Kits 50; Sakoline 10 |
| LGU- Dao | 530 | Kitchen Kits; coordinate fields left blank |

These six inventory rows remain in `NFI_updated_inventory.csv`. The map skips them for marker placement and mapped totals, lists their quantities in Data review, and shows the reported inventory total separately. Supply confirmed latitude and longitude for those rows and upload the corrected CSV to include them on the map.

### Source-label matches

| Workbook label | Coordinate CSV label |
| --- | --- |
| OCD6 Warehouse- Ticud | OCD VI Iloilo Warehouse |
| Camp Jizmundo, Banga, Aklan | Camp Jizmundo, Banga, Aklan |
| Camp Hernandez, Dingle, Iloilo | Cp Hernandez, Dingle, Iloilo |
| Camp Peralta, Jamindan, Capiz | Cp Peralta, Jamindan, Capiz |
| LGU-Carles, Iloilo | Carles, Iloilo |
| LGU-Alternate EOC PDRRMO Antique, Culasi | PDRRMO Antique Alternate EOC |
| LGU - Culasi, Antique | Culasi, Antique |
| LGU - Jamindan | MDRRMO Jamindan, Capiz |

**Location conflict to resolve:** the workbook places the Alternate EOC label in Culasi. The matching CSV's coordinates are 10.7442, 121.9412, farther south. The map retains exactly those supplied coordinates and displays a review notice. Confirm the identity and position of this site before relying on it operationally. The other sites' coordinates are likewise user-supplied and have not been surveyed or independently verified.

## CSV structure

Use these columns, with one item per site per row:

```csv
Name,Latitude,Longitude,Description,Quantity
"Camp Jizmundo, Banga, Aklan",11.6372,122.3325,Family Packs,95
"Camp Jizmundo, Banga, Aklan",11.6372,122.3325,Shelter Repair Kits,100
OCD VI Iloilo Warehouse,10.6923,122.576,N95 Mask,3000
```

The complete testing sample is `NFI_original_coordinate_data.csv`, copied from your original attachment. The updated inventory, including the rows awaiting coordinates, is `NFI_updated_inventory.csv`.

- Site identity is **Name + numeric Latitude + numeric Longitude**. The same name at different coordinates remains separate.
- Surround a comma-containing site name, item description, or quantity with CSV quotes. A quantity such as `"1,000"` is accepted as 1000.
- Leading and trailing spaces are trimmed. Exact item text, including punctuation, capitalization, and internal line breaks, is retained by default.
- Duplicate rows for the same site and exact item description are summed.
- Blank, invalid, negative, or non-finite quantities are skipped with an explanation. Explicit zero quantities are accepted.
- Latitude / longitude are required for markers. The broad Philippines range check is 4–22° N and 116–127° E. This is a sanity check, not a coastline or administrative-area test.
- Headers are case-insensitive. Aliases include Site Name, Location, Warehouse, Lat, Lng, Long, Lon, Item, Item Name, Qty, Count, and Stock. Ambiguous duplicate matching headers are rejected. Extra columns can be present but are ignored.
- Blank lines and multiline quoted cells are supported. Review row numbers are the physical starting lines of CSV records, with the header normally on line 1.
- Quantities across unlike items are added as requested. The grand total is a sum of reported inventory quantities, not a number of complete kits, beneficiaries, or pesos.

## Embedded official logo

The supplied `OCD Logo (DIGITAL)(2).png` is embedded without changing its image bytes. The HTML works as one file. To replace the logo later, open `index.html` in a text editor, find `const LOGO_PATH` at the start of the application script, and set another official PNG data URI:

```javascript
const LOGO_PATH = "data:image/png;base64,YOUR_PNG_BASE64_BYTES";
```

Use the base64 encoding of your actual official PNG. Do not include the placeholder text. You can encode it locally with PowerShell:

```powershell
$pngBytes = [IO.File]::ReadAllBytes((Resolve-Path '.\ocd-logo.png'))
[Convert]::ToBase64String($pngBytes) | Set-Clipboard
```

Paste that result after `data:image/png;base64,`. The current logo already uses this method. Its desktop height is 66 pixels and mobile height is 44 pixels, with its original proportions preserved. To use a separate image instead, change the same constant to `"ocd-logo.png"` and put that PNG beside the HTML.

## Real boundary source and maintenance

The embedded geometry is the **geoBoundaries PHL ADM2** simplified dataset, boundary ID `PHL-ADM2-2640588`, representing 2020. Metadata attributes the source to NAMRIA, PSA, and OCHA Philippines, with source license **CC BY 3.0 IGO**.

- Metadata and authoritative download links: https://www.geoboundaries.org/api/current/gbOpen/PHL/ADM2/
- Pinned simplified GeoJSON: https://github.com/wmgeolab/geoBoundaries/raw/41af8f1/releaseData/gbOpen/PHL/ADM2/geoBoundaries-PHL-ADM2_simplified.geojson
- Underlying source: https://data.humdata.org/dataset/philippines-administrative-levels-0-to-3
- Source license: https://creativecommons.org/licenses/by/3.0/igo/

Features were filtered by `properties.shapeName` to exactly Aklan, Antique, Capiz, Guimaras, and Iloilo. They were simplified with a 0.002-degree tolerance while preserving each geometry's topology and rounded to five decimal places for a compact reference map. Label positions were derived from the supplied province geometries. Negros Occidental and Bacolod City are excluded. Iloilo City is included in the municipal/city reference layer, while the province layer remains exactly five features.

The application never uses province boundaries to position, aggregate, or filter inventory. Province shapes and labels are non-interactive. If boundary geometry is absent or corrupt, markers and inventory continue to work. No street or satellite tiles are required.

To replace the boundaries, download the metadata's simplified GeoJSON, filter to the same five names, and put the resulting FeatureCollection inside the HTML's `province-data` JSON script block. Set each feature's `properties.name` from `shapeName`. Optional `properties.labelPoint` is a `[latitude, longitude]` label location derived from geometry. No separate boundary file or fetch is required.

## Technical notes and later extensions

Leaflet 1.9.4 and PapaParse 5.5.3 are pinned. The page tries their CDN copies for up to 900 ms, then uses embedded source copies without depending on a prior browser cache. Leaflet CSS is embedded. Uploads are read and parsed locally with PapaParse. CSV text is escaped before HTML rendering, and summary CSV exports use formula escaping.

Circle radius and blue shade use a square-root scale relative to the largest site total. Markers that collide are displaced in screen pixels and connected to their exact supplied coordinates by a dashed line. Displacement is recalculated on zoom and filter changes. The coordinates displayed and exported always remain the original values. For a much larger network of sites, replace screen offsets with a clustering/spiderfying library.

Code comments identify the colors, dataset blocks, logo path, column aliases, and boundaries. The full source is also supplied as one HTML code block in `NFI_Map_Complete_Code.md`.

Possible extensions:

- Add Type, Province, and Date columns; store them during parsing and use them for filters or freshness labels. The current version ignores extra columns.
- Add a verified coordinate register so new warehouses can be matched without manual copying.
- Add unit-of-measure columns if packs, pieces, sets, and water containers need separate summaries.
- Add a database and access controls if several offices must update one shared inventory. The current version is a local file.

## Navy appearance update — October 29, 2026

The map now uses OCD navy blue, keyed to the navy in your actual supplied logo (`#02055a`). Province fills use navy tones. Stock circles use light blue through navy with white outlines, preserving the existing size and quantity scale. Thin city and municipal boundary lines, a subtle land stipple/hatch, and a light water grid add detail. These textures are decorative and do not represent terrain, elevation, hazards, or operational data.

The embedded municipal/city reference contains **101 features**: Aklan 17, Antique 18, Capiz 17, Guimaras 5, and Iloilo including Iloilo City 44. Labels appear at zoom 10 and above. Lines and labels do not intercept marker clicks or assign inventory to municipalities.

Source: geoBoundaries PHL ADM3, boundary ID `PHL-ADM3-30758251`, representing 2020, with NAMRIA / PSA / OCHA attribution and CC BY 3.0 IGO source license. Metadata: https://www.geoboundaries.org/api/current/gbOpen/PHL/ADM3/

Pinned source: https://github.com/wmgeolab/geoBoundaries/raw/9469f09/releaseData/gbOpen/PHL/ADM3/geoBoundaries-PHL-ADM3_simplified.geojson

Municipal features were selected spatially against the real five-province boundary data. Iloilo City was included explicitly. Coordinates were rounded to five decimal places; no invented boundary geometry was used. Everything is embedded for offline use.

This is an appearance update. The existing built-in inventory snapshots are preserved. Upload your latest `NFIS_Map_Ready.csv` as before to show your latest warehouse coordinates and quantities. That current CSV is included in the ZIP for convenience and was verified in the revised map: **10 sites, 32 item rows, total quantity 11,153**.

Regression checks confirmed 26 technical functions and the four existing embedded data blocks are unchanged. The original 13 data tests passed. Browser checks confirmed the supplied logo, 101 municipal boundary paths, zoom-dependent labels, warehouse inventory scrolling, site search, latest CSV upload, offline initialization, and mobile scrolling.

## Verification

Thirteen automated data checks passed: workbook reconciliation, both dataset totals, coordinate grouping, exact item names, optional grouping, duplicate summation, flexible headers, quoted commas, missing/ambiguous headers, physical CSV row numbering, invalid coordinates and quantities, HTML escaping, and the five province features.

Browser checks passed for updated and original dataset selection, the complete scrollable warehouse table, CSV upload, three coincident/near-coincident sites remaining separate and clickable, original coordinate display after visual offset, literal display of HTML-like site text, site search, item filtering, grouping without changing grand totals, per-site CSV export, offline initialization with external connections blocked, a 390-pixel mobile layout and mobile item scrolling, and operation with no boundary features.

The summary download was inspected and reconciled. Drag-and-drop is implemented but was not separately exercised through browser automation. The test browser blocks `file://` navigation, so direct double-click opening could not be exercised there. The file uses embedded resources and local file-reading APIs; no server-dependent data requests are required.
