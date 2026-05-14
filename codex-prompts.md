# RPG Map Editor — Codex Prompt Guide
> VSCode + ChatGPT Codex 작업용 프롬프트 모음  
> 작업 순서대로 하나씩 사용하세요. 각 단계가 완료된 후 다음 단계로 진행합니다.

---

## 작업 전 준비사항

- `code.html` 파일을 VSCode에서 열어둔 상태로 시작
- Codex에 파일 전체를 컨텍스트로 제공 (파일 첨부 또는 전체 복사)
- 각 프롬프트는 **하나씩 순서대로** 실행 (한꺼번에 요청 금지)

---

## STEP 1 — Canvas 요소 삽입 및 기본 그리드 렌더링

```
The attached file is a static HTML UI prototype for a 2D RPG Map Editor.
It uses Tailwind CSS and Material Symbols icons.

TASK: Replace the center canvas section with a working <canvas> element and implement a basic grid renderer.

Requirements:
1. Replace the existing center <section> mock content (the div with class "canvas-grid" and its children) with a single <canvas id="map-canvas"> element that fills the available space.
2. Add a <script> block at the bottom of <body> with the following logic:
   - Define constants: CELL_SIZE = 32, MAP_COLS = 40, MAP_ROWS = 30
   - Initialize a 2D array: mapData[row][col] = 0 (empty)
   - On window load, size the canvas to fill its parent container
   - Draw function: clear canvas, then draw grid lines using ctx.strokeStyle = 'rgba(16, 185, 129, 0.08)' (matches the emerald theme)
   - Call draw() on load and on window resize
3. Do NOT change any existing HTML structure outside the center section.
4. Do NOT remove the toolbar, sidebars, or footer.
5. Keep all existing Tailwind classes intact.

Output: the complete modified HTML file.
```

---

## STEP 2 — 마우스 클릭/드래그로 셀 칠하기

```
The attached file is an RPG Map Editor HTML file with a working <canvas> grid.

TASK: Implement mouse interaction so the user can paint cells on the canvas.

Requirements:
1. On mousedown on the canvas, calculate which cell was clicked:
   col = Math.floor(mouseX / CELL_SIZE)
   row = Math.floor(mouseY / CELL_SIZE)
2. Set mapData[row][col] = 1 (painted)
3. On mousemove while mousedown is held, continue painting cells (drag painting)
4. On mouseup, stop painting
5. In the draw() function, for each cell where mapData[row][col] !== 0, fill it with color:
   ctx.fillStyle = 'rgba(78, 222, 163, 0.35)' (primary color at 35% opacity)
6. After filling, redraw grid lines on top so grid is always visible
7. The currently hovered cell should show a highlight:
   ctx.fillStyle = 'rgba(78, 222, 163, 0.15)' (lighter hover preview)
8. Track mouse position for the status bar footer:
   Update the footer text "X: 12, Y: 08" to reflect the real cursor cell position in real time.

Do NOT modify HTML structure, sidebar, toolbar, or footer layout.
Output: the complete modified HTML file.
```

---

## STEP 3 — 타일 ID 시스템 및 색상 팔레트 연결

```
The attached file is an RPG Map Editor HTML with working grid painting.

TASK: Replace the single paint color with a tile ID system connected to the left palette panel.

Requirements:
1. Define a TILE_COLORS map (JS object) with at least 6 tile types:
   {
     0: null,                          // empty
     1: 'rgba(34, 85, 34, 0.85)',      // grass (dark green)
     2: 'rgba(194, 154, 82, 0.85)',    // dirt/sand (tan)
     3: 'rgba(30, 80, 160, 0.85)',     // water (deep blue)
     4: 'rgba(120, 120, 130, 0.85)',   // mountain (grey)
     5: 'rgba(60, 100, 50, 0.85)',     // forest (deep green)
     6: 'rgba(200, 170, 90, 0.85)'    // desert (sandy yellow)
   }

2. Add a variable: let selectedTileId = 1

3. In the left sidebar, find the asset grid (the placeholder image divs).
   Replace those placeholder divs with colored tile swatches using inline styles matching TILE_COLORS.
   Each swatch: 
   - Displays the color as background
   - Shows a short label below (Grass, Dirt, Water, Mountain, Forest, Desert)
   - On click: sets selectedTileId to that tile's ID
   - Active swatch: add a 2px border in #4edea3 (primary color) and a subtle glow

4. mapData[row][col] now stores the selectedTileId instead of always 1.

5. draw() uses TILE_COLORS[tileId] to fill each cell.

Do NOT change layout structure.
Output: the complete modified HTML file.
```

---

## STEP 4 — 지우개 도구 및 툴바 연결

```
The attached file is an RPG Map Editor with tile color painting.

TASK: Connect the toolbar tool buttons to actual tool switching logic.

Requirements:
1. Define: let activeTool = 'brush'  (options: 'brush', 'eraser')

2. In the top toolbar, find the existing tool icon buttons (brush, eraser icons).
   Add onclick handlers:
   - Brush button → activeTool = 'brush'
   - Eraser button → activeTool = 'eraser'
   Active tool button should have a visible active state:
   - Add class or inline style: background = 'rgba(78,222,163,0.2)', border = '1px solid #4edea3'
   - Inactive buttons: no background, no border

3. Mouse paint logic:
   - If activeTool === 'brush': mapData[row][col] = selectedTileId
   - If activeTool === 'eraser': mapData[row][col] = 0

4. Update the "Active Tool" display in the left sidebar bottom section:
   - Show "Paint Brush" when brush is active
   - Show "Eraser" when eraser is active
   - Change the icon accordingly

5. Status bar footer: add current tool name after cursor coords.
   Example: "X: 05, Y: 12 | Tool: Brush | Layer: Ground_01"

Output: the complete modified HTML file.
```

---

## STEP 5 — JSON 저장 및 불러오기

```
The attached file is an RPG Map Editor with brush/eraser tools working.

TASK: Implement Save and Load (Open) functionality using JSON files.

Requirements:
1. SAVE function (triggered by the existing "Save" or export button in toolbar):
   - Serialize the current state to JSON:
     {
       "version": "1.0",
       "mapCols": MAP_COLS,
       "mapRows": MAP_ROWS,
       "cellSize": CELL_SIZE,
       "layers": [
         { "name": "Ground_01", "data": mapData }
       ]
     }
   - Trigger browser file download: filename = "map_export.json"
   - Use Blob + URL.createObjectURL for the download (no server needed)

2. LOAD function (triggered by File menu "Open" or a new toolbar button):
   - Open a hidden <input type="file" accept=".json"> 
   - On file select, read with FileReader
   - Parse JSON and restore mapData and MAP_COLS, MAP_ROWS from file
   - Call draw() to re-render the restored map

3. Add a keyboard shortcut: Ctrl+S → triggers Save

4. After save, briefly show a toast notification at the bottom:
   "Map saved successfully" — styled with the primary emerald color
   Auto-dismiss after 2 seconds.

Do NOT change layout. Keep all existing HTML structure.
Output: the complete modified HTML file.
```

---

## STEP 6 — 이미지 → 타일맵 자동 변환 (Color Clustering Import)

```
The attached file is an RPG Map Editor with save/load working.

TASK: Add an "Import Map Image" feature that converts a fantasy map image into a tilemap draft using color clustering.

Requirements:
1. Add an "Import Image" button to the File menu in the top toolbar (or as a toolbar icon).
   Icon: "image" (Material Symbol)

2. On click: open a hidden <input type="file" accept="image/*">

3. On image select:
   a. Draw the image onto a hidden off-screen <canvas> (same size as map: MAP_COLS * CELL_SIZE x MAP_ROWS * CELL_SIZE)
      Use ctx.drawImage() scaled to fit.
   b. For each cell (row, col), sample the CENTER pixel of that cell:
      px = col * CELL_SIZE + CELL_SIZE/2
      py = row * CELL_SIZE + CELL_SIZE/2
      Get RGBA via ctx.getImageData(px, py, 1, 1).data
   c. Classify the pixel color to a tile ID using these HSL-based rules:
      - Hue 90-160 AND Saturation > 30% AND Lightness 20-60% → 5 (Forest, deep green)
      - Hue 60-90 AND Saturation > 20% AND Lightness > 50%  → 1 (Grass, light green)
      - Hue 30-60 AND Saturation > 20% AND Lightness < 55%  → 2 (Dirt/Sand)
      - Hue 200-260 AND Saturation > 30%                    → 3 (Water, blue)
      - Lightness < 30%                                      → 0 (Empty/Shadow)
      - Saturation < 15% AND Lightness > 50%                → 4 (Mountain, grey-white)
      - Hue 30-50 AND Lightness > 60%                       → 6 (Desert, sandy)
      - Fallback                                             → 1 (Grass)
   d. Helper function: rgbToHsl(r, g, b) → [h, s, l]
   e. Set mapData[row][col] = classified tile ID
   f. Call draw() to render the imported tilemap

4. Show a toast notification after import:
   "Map imported! Terrain draft generated — refine with brush tools."
   Styled with emerald primary color, auto-dismiss after 3 seconds.

5. The off-screen canvas must NOT be visible to the user.

Do NOT change existing layout.
Output: the complete modified HTML file.
```

---

## 작업 완료 기준 체크리스트

| Step | 기능 | 완료 |
|---|---|---|
| 1 | Canvas 그리드 렌더링 | ☐ |
| 2 | 마우스 클릭/드래그 페인팅 | ☐ |
| 3 | 타일 ID + 색상 팔레트 | ☐ |
| 4 | 브러시/지우개 도구 전환 | ☐ |
| 5 | JSON 저장/불러오기 | ☐ |
| 6 | 이미지 → 타일맵 자동 변환 | ☐ |

---

## Codex 사용 팁

- 각 Step 프롬프트 앞에 **"The attached file is..."** 로 시작하므로 반드시 해당 시점의 최신 HTML 파일을 첨부하세요.
- Codex가 레이아웃을 건드렸다면: *"Revert any HTML structure changes outside the `<script>` block and center canvas section"* 추가 요청
- 결과물이 길어 잘리면: *"Continue from where you left off"* 요청
- 한 Step이 완료되면 파일을 저장하고 브라우저에서 열어 동작 확인 후 다음 Step 진행
