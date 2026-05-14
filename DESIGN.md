---
name: AetherForge Map Editor
colors:
  # --- Core Surfaces ---
  surface: '#161121'
  surface-dim: '#161121'
  surface-bright: '#3c3648'
  surface-container-lowest: '#100b1b'
  surface-container-low: '#1e1929'
  surface-container: '#221d2e'
  surface-container-high: '#2d2739'
  surface-container-highest: '#383244'
  on-surface: '#e9def6'
  on-surface-variant: '#bbcabf'
  inverse-surface: '#e9def6'
  inverse-on-surface: '#332e3f'
  outline: '#86948a'
  outline-variant: '#3c4a42'
  # --- Primary Accent: Emerald ---
  surface-tint: '#4edea3'
  primary: '#4edea3'
  on-primary: '#003824'
  primary-container: '#10b981'
  on-primary-container: '#00422b'
  inverse-primary: '#006c49'
  primary-fixed: '#6ffbbe'
  primary-fixed-dim: '#4edea3'
  on-primary-fixed: '#002113'
  on-primary-fixed-variant: '#005236'
  # --- Secondary Accent: Violet ---
  secondary: '#d0bcff'
  on-secondary: '#3c0091'
  secondary-container: '#571bc1'
  on-secondary-container: '#c4abff'
  secondary-fixed: '#e9ddff'
  secondary-fixed-dim: '#d0bcff'
  on-secondary-fixed: '#23005c'
  on-secondary-fixed-variant: '#5516be'
  # --- Tertiary ---
  tertiary: '#ccc2df'
  on-tertiary: '#332d43'
  tertiary-container: '#a89eba'
  on-tertiary-container: '#3c354c'
  tertiary-fixed: '#e9defc'
  tertiary-fixed-dim: '#ccc2df'
  on-tertiary-fixed: '#1e182d'
  on-tertiary-fixed-variant: '#4a435b'
  # --- Semantic ---
  error: '#ffb4ab'
  on-error: '#690005'
  error-container: '#93000a'
  on-error-container: '#ffdad6'
  success: '#4edea3'
  warning: '#facc15'
  danger: '#f87171'
  # --- Base ---
  background: '#161121'
  on-background: '#e9def6'
  surface-variant: '#383244'

typography:
  headline-lg:
    fontFamily: Inter
    fontSize: 32px
    fontWeight: '700'
    lineHeight: '1.2'
    letterSpacing: -0.02em
  headline-md:
    fontFamily: Inter
    fontSize: 24px
    fontWeight: '600'
    lineHeight: '1.3'
  body-md:
    fontFamily: Inter
    fontSize: 16px
    fontWeight: '400'
    lineHeight: '1.5'
  body-sm:
    fontFamily: Inter
    fontSize: 14px
    fontWeight: '400'
    lineHeight: '1.4'
  mono-label:
    fontFamily: JetBrains Mono
    fontSize: 13px
    fontWeight: '500'
    lineHeight: '1.2'
  mono-data:
    fontFamily: JetBrains Mono
    fontSize: 12px
    fontWeight: '400'
    lineHeight: '1.0'
  ui-label:
    fontFamily: Inter
    fontSize: 11px
    fontWeight: '600'
    lineHeight: '1.2'
    letterSpacing: 0.08em

rounded:
  sm: 0.125rem
  DEFAULT: 0.25rem
  md: 0.375rem
  lg: 0.5rem
  xl: 0.75rem
  full: 9999px

spacing:
  unit: 4px
  gutter: 12px
  panel-padding: 16px
  toolbar-height: 48px
  statusbar-height: 32px
  sidebar-width: 280px
  cell-size-sm: 16px
  cell-size-md: 32px
  cell-size-lg: 64px
---

# AetherForge Map Editor — Design System

## Brand & Vision

**AetherForge Map Editor**는 Unity 2D용 RPG 타일맵 초안을 제작하는 브라우저 기반 에디터입니다.
UI는 **Modern High-Contrast Dark** 미학을 따르며, 판타지 분위기를 유지하면서도 장시간 편집 작업에 적합한 눈 피로도 최소화를 목표로 합니다.

- **Primary Accent**: Emerald Green `#4edea3` — 활성 도구, 선택된 타일, 포커스 상태
- **Secondary Accent**: Violet `#d0bcff` — 선택 영역, 보조 인터랙션
- **Base**: Midnight Obsidian `#161121` — 패널, 툴바 배경

---

## Layout

```
┌──────────────────────────────────────────────────────────────┐
│                    Top Toolbar (48px)                        │
│  [Logo] [File][Edit][View]  [Tools]  [New][Open][Save][Undo] │
├─────────────────┬────────────────────────┬───────────────────┤
│  Tile Palette   │     Map Canvas         │  Layers + Props   │
│   (280px)       │   (flex: 1)            │   (280px)         │
│                 │                        │                   │
│  [Terrain]      │   <canvas>             │  LAYERS           │
│  [Objects]      │   grid lines           │  ─ Ground_01 ●    │
│  [Events]       │   tile cells           │  ─ Objects        │
│                 │                        │  ─ Collision      │
│                 │   [+] [-] [⊙] zoom     │  ─ Events         │
│                 │                        │                   │
│  Active Tool    │                        │  PROPERTIES       │
│  [brush icon]   │                        │  Name / X / Y     │
├─────────────────┴────────────────────────┴───────────────────┤
│  Status Bar (32px)  X:12 Y:08 | Tool: Brush | Zoom: 100%    │
└──────────────────────────────────────────────────────────────┘
```

### Region Rules
- **Top Toolbar**: 48px 고정. 앱 이름, 메뉴 바, 도구 그룹, 파일 액션 그룹 포함.
- **Left Sidebar**: 280px 고정. 타일 팔레트 + 활성 도구 표시.
- **Center Canvas**: 나머지 너비를 채움. `<canvas>` 단일 요소만 포함 — DOM 자식 없음.
- **Right Sidebar**: 280px 고정. 레이어 패널(상단, 스크롤) + 속성 패널(하단, 260px 고정).
- **Status Bar**: 32px 고정, 하단 고정. 모노스페이스 폰트만 사용.

---

## Color Usage Rules

| Token | Hex | 용도 |
|---|---|---|
| `background` | #161121 | 앱 전체 배경 |
| `surface` | #161121 | 툴바, 패널 배경 |
| `surface-container-low` | #1e1929 | 사이드바 내부 |
| `surface-container` | #221d2e | 패널 섹션, 레이어 행 |
| `surface-container-high` | #2d2739 | 호버 상태 |
| `surface-container-lowest` | #100b1b | 캔버스 배경, 인풋 배경 |
| `primary` | #4edea3 | 활성 도구, 선택 타일 테두리 글로우, 포커스 인풋 |
| `primary-container` | #10b981 | 주요 액션 버튼 (Export, Save) |
| `secondary` | #d0bcff | 보조 버튼, 선택 사각형 stroke |
| `outline-variant` | #3c4a42 | 패널 테두리, 구분선 |
| `on-surface` | #e9def6 | 기본 텍스트 |
| `on-surface-variant` | #bbcabf | 보조 텍스트, 비활성 아이콘 |
| `success` | #4edea3 | Toast 성공 |
| `warning` | #facc15 | Toast 경고 |
| `danger` | #f87171 | Toast 에러 |

---

## Components

### Toolbar — Top Bar

**App Name** (좌측)
- Font: `headline-md`, color: `primary`
- Text: `"AetherForge Map Editor"`

**Menu Bar** (앱 이름 우측)
- 버튼: File / Edit / View
- Style: `body-sm`, color `on-surface-variant`, hover `bg-surface-variant`
- **File 드롭다운 항목**:
  - New Map (`note_add`)
  - Open… (`folder_open`) — .json 파일
  - Import Map Image (`image_search`) — 이미지→타일맵 변환
  - ─ 구분선 ─
  - Save (`save`) — .json, 단축키 Ctrl+S
  - Export TMX (`download`)
  - Export PNG (`image`)

**Tool Group** (중앙)
- 아이콘: `brush` / `eraser` / `format_color_fill` / `crop_square`
- 크기: 32×32px, `rounded-md`
- Default: 배경 없음, 아이콘 `on-surface-variant`
- **Active**: `bg-secondary-container/30`, 좌측 border 2px `primary`, 아이콘 `primary`, glow `0 0 8px #4edea3`
- Hover: `bg-surface-container-high`

**File Action Group** (tool group 우측, 구분선으로 분리)
- 아이콘 버튼: `note_add`(New) / `folder_open`(Open) / `save`(Save) / `undo`(Undo) / `redo`(Redo) / `image_search`(Import Image)
- 크기·스타일: Tool Group과 동일
- 단축키: Save = Ctrl+S, Undo = Ctrl+Z, Redo = Ctrl+Y

**Export Button** (우측 끝)
- Background: `primary-container`, text: `on-primary-container`
- Font: `mono-label`, bold
- Hover glow: `0 0 8px #10b981`

---

### Tile Palette — Left Sidebar

**Category Tabs** (상단 전체 너비)
- **3개 탭만**: Terrain / Objects / Events
- ⚠️ Lights, NPCs 탭 금지 — 맵 에디터 범위 초과
- Active: `bg-secondary-container`, `on-secondary-container` 텍스트, 좌측 border 2px `primary`
- Inactive: `on-surface-variant`, hover `bg-surface-container-high`

**Tile Grid**
- 4열, `gap-2`
- 각 타일 스와치: `aspect-square`, `rounded-sm`, `border border-outline-variant`
- Default: 타일 색상 또는 스프라이트 이미지
- Hover: border 2px `primary`, transition 150ms
- **Selected**: border 2px `primary`, glow `0 0 8px #4edea3`, scale 1.05
- 레이블: 10px `mono-data`, 스와치 하단 중앙

**Terrain 탭 내 서브카테고리 필터 칩**
- Grass / Dirt / Water / Mountain / Forest / Desert
- 스타일: pill형, `bg-surface-container`, `on-surface-variant`
- Active: `bg-primary/20`, `primary` 텍스트, border `primary`

**Active Tool Indicator** (좌측 사이드바 하단)
- 현재 도구명 + 아이콘 표시
- Background: `bg-surface-container-high`, border `outline-variant`
- 아이콘: 32×32 `primary-container` 배경, `on-primary` 색상
- 텍스트: `mono-label` 도구명 + 10px `on-surface-variant` 힌트

---

### Canvas — Center

**Canvas Element**
- Background: `#100b1b` (`surface-container-lowest`)
- 단일 `<canvas id="map-canvas">` — DOM 자식 없음
- load 및 window resize 시 부모 크기에 맞게 조정

**Grid Lines**
- Color: `rgba(78, 222, 163, 0.06)` (에메랄드, 매우 미묘)
- 타일 채색 후 위에 그림 — 항상 최상위
- 기본 셀 크기: 32px

**Cell States**

| 상태 | 스타일 |
|---|---|
| Empty | 채색 없음 (캔버스 배경 노출) |
| Painted | 타일 색상, opacity 85% |
| Hovered | `rgba(78, 222, 163, 0.12)` 오버레이 |
| Selected (rect) | `rgba(208, 188, 255, 0.25)` fill + 1px `secondary` stroke |

**Cursor Indicator**
- 32×32px 오버레이 div, `border-2 border-primary`, `bg-primary/10`
- Glow: `box-shadow: 0 0 12px rgba(78,222,163,0.5)`
- 마우스 따라 이동, `pointer-events: none`

**Zoom Controls** (캔버스 우하단 플로팅)
- 버튼: `add` / `remove` / `center_focus_strong`
- 크기: 40×40px, `bg-surface-container`, `border border-outline-variant`, `rounded`
- Hover: `bg-surface-variant`
- 줌 범위: 25% – 400%, 25% 단위

---

### Layers Panel — Right Sidebar (상단)

**Panel Header**
- 타이틀 "LAYERS", font `ui-label`, color `on-surface-variant`
- 우측 아이콘: `add_box`, `delete` — 18px, hover시 `primary`

**Layer Row**
- 높이: 36px, padding: 0 16px
- 구성: visibility 아이콘 / 레이어명 / lock 아이콘
- Default: `on-surface-variant` 텍스트, 아이콘 muted
- **Active**: `bg-secondary-container/20`, 좌측 border 2px `primary`, 텍스트 `on-surface`
- Hover: `bg-surface-container-high`
- 숨김 레이어: 텍스트 opacity 50%, `visibility_off` 아이콘

**기본 레이어 순서**: Ground_01 (기본 활성) → Objects_Top → Collision_Map → Trigger_Events

---

### Properties Panel — Right Sidebar (하단 260px 고정)

**Panel Header**: "PROPERTIES", font `ui-label`, color `on-surface-variant`

**Fields**
- Name (text input), X Pos / Y Pos (나란히 배치), Opacity (range slider)
- Input: `bg-surface-container-lowest`, border `outline-variant`, `rounded`
- Focus: border → `primary`, ring 없음
- Font: `mono-label`

---

### Status Bar — Footer

- 높이: 32px, background `surface-container-lowest`
- Border top: 1px `outline-variant`
- Font: `mono-data`, color `on-surface-variant`
- **좌측**: `X: 00, Y: 00 | Tool: Brush | Zoom: 100% | Layer: Ground_01`
- **우측**: Documentation / Shortcuts / 버전 `v1.0.0`
- 구분자: `|`, 양쪽 6px 간격

---

### Toast Notification

**위치**: fixed, 우하단, `bottom: 48px` (상태바 위), `right: 16px`
**크기**: min-width 260px, padding 12px 16px, `rounded-lg`

**Variants**:
| 종류 | 좌측 border | 아이콘 |
|---|---|---|
| Success | 3px `primary` (emerald) | `check_circle` |
| Warning | 3px `warning` | `warning` |
| Error | 3px `danger` | `error` |

**구성**: 아이콘(18px) + 메시지(`body-sm`) + 닫기 버튼(선택)
**애니메이션**: 우측에서 슬라이드 인 (translateX 100%→0, 200ms ease-out), 자동 페이드 아웃 (300ms, 2~3초 후)

**사용 케이스**:
- Save 완료 → `"Map saved successfully"` (success, 2초)
- Import 완료 → `"Terrain draft generated — refine with brush tools"` (success, 3초)
- 처리 중 → `"Analyzing map colors…"` (spinner 포함, 수동 해제)
- 로드 실패 → `"Failed to load file. Invalid format."` (error, 4초)

---

### Import Map Image — 진입점 및 플로우

**진입점**: File 메뉴 → "Import Map Image" (`image_search` 아이콘)
또는 툴바 File Action Group의 `image_search` 아이콘 버튼

**플로우**:
1. 클릭 → 숨겨진 `<input type="file" accept="image/*">` 트리거 (모달 불필요)
2. 파일 선택 후 처리 중: `"Analyzing map colors…"` Toast (로딩 스피너 포함)
3. 완료: 로딩 Toast 해제 → success Toast 표시
4. 오류: error Toast 표시

---

## Interaction States — 전역 규칙

모든 인터랙티브 요소에 일관되게 적용:

| 상태 | 스타일 |
|---|---|
| **Default** | 컴포넌트별 정의 참조 |
| **Hover** | `bg-surface-container-high` 또는 `bg-surface-variant` |
| **Active / Selected** | Emerald border 2px `#4edea3` + `bg-secondary-container/20` |
| **Focus** | border color → `primary`, outline ring 없음 |
| **Disabled** | opacity 40%, `cursor: not-allowed` |
| **Destructive hover** | border/icon → `error` color |

- Transition: **150ms ease** (color, border 모든 전환)
- 클릭 피드백: `active:scale-95`

---

## Elevation & Depth

| Level | 색상 | 용도 |
|---|---|---|
| 0 — Canvas | `#100b1b` | 맵 편집 캔버스 (가장 깊음) |
| 1 — Panels | `#161121` + border `#3c4a42` | 툴바, 사이드바 |
| 2 — Hover rows | `#2d2739` | 활성 행, 선택 항목 |
| 3 — Toast/Popover | `#221d2e` + shadow `0 4px 24px rgba(0,0,0,0.5)` | 플로팅 요소 |

Active glow: `0 0 8px rgba(78,222,163,0.5)` — 활성 도구, 선택 타일에만 사용

---

## Iconography

- **라이브러리**: Material Symbols Outlined (`'FILL' 0`)
- **크기**: 18px (패널), 24px (툴바), 14px (상태바)

| 카테고리 | 아이콘 |
|---|---|
| 도구 | `brush`, `eraser`, `format_color_fill`, `crop_square` |
| 파일 액션 | `note_add`, `folder_open`, `save`, `undo`, `redo`, `image_search` |
| 레이어 | `visibility`, `visibility_off`, `lock`, `lock_open`, `add_box`, `delete` |
| 줌 | `add`, `remove`, `center_focus_strong` |
| Toast | `check_circle`, `warning`, `error`, `close` |

---

## Spacing Scale

| Token | Value | 용도 |
|---|---|---|
| `unit` | 4px | 기본 단위, 아이콘 간격 |
| `gutter` | 12px | 상태바 패딩, 소형 간격 |
| `panel-padding` | 16px | 사이드바 내부 패딩 |
| `toolbar-height` | 48px | 상단 툴바 고정 높이 |
| `statusbar-height` | 32px | 하단 상태바 고정 높이 |
| `sidebar-width` | 280px | 좌우 패널 너비 |
| `cell-size-sm` | 16px | 소형 그리드 셀 |
| `cell-size-md` | 32px | 기본 그리드 셀 |
| `cell-size-lg` | 64px | 대형 그리드 셀 |
