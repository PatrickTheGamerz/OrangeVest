<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>NovaInvest – Beginner Portfolio Simulator</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <style>
    /* 
    ==========================================
    GLOBAL STYLES
    ==========================================
    */

    :root {
      --bg-main: #060814;
      --bg-panel: #101322;
      --bg-panel-soft: #14182a;
      --bg-chip: #1e2236;
      --accent: #4f8cff;
      --accent-soft: rgba(79, 140, 255, 0.08);
      --accent-strong: #6ca0ff;
      --accent-green: #36d98b;
      --accent-red: #ff4d67;
      --text-main: #f7f8ff;
      --text-soft: #afb7d9;
      --text-muted: #6b7394;
      --border-subtle: #262c43;
      --shadow-soft: 0 18px 45px rgba(0, 0, 0, 0.55);
      --radius-xl: 18px;
      --radius-lg: 14px;
      --radius-md: 10px;
      --radius-pill: 999px;
      --font-sans: system-ui, -apple-system, BlinkMacSystemFont, "SF Pro Text",
        "Segoe UI", Roboto, sans-serif;
      --transition-fast: 0.18s ease-out;
      --transition-normal: 0.25s ease-out;
    }

    * {
      box-sizing: border-box;
    }

    html,
    body {
      margin: 0;
      padding: 0;
      background: radial-gradient(circle at top, #10142a 0, #050611 42%, #020308 100%);
      color: var(--text-main);
      font-family: var(--font-sans);
      -webkit-font-smoothing: antialiased;
      height: 100%;
    }

    body {
      display: flex;
      flex-direction: column;
      min-height: 100vh;
    }

    a {
      color: inherit;
      text-decoration: none;
    }

    button {
      font-family: inherit;
    }

    input,
    select {
      font-family: inherit;
    }

    /* 
    ==========================================
    LAYOUT
    ==========================================
    */

    .app-shell {
      display: flex;
      flex-direction: column;
      min-height: 100vh;
      padding: 18px clamp(14px, 2vw, 24px);
      gap: 16px;
    }

    .app-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 12px;
      padding: 14px 18px;
      border-radius: var(--radius-lg);
      background: linear-gradient(
          135deg,
          rgba(79, 140, 255, 0.19),
          rgba(19, 23, 50, 0.84) 22%,
          rgba(7, 9, 22, 0.96) 100%
        );
      border: 1px solid rgba(126, 153, 255, 0.25);
      box-shadow: 0 16px 40px rgba(0, 0, 0, 0.55);
      position: sticky;
      top: 10px;
      z-index: 10;
      backdrop-filter: blur(14px);
    }

    .app-brand {
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .brand-logo {
      width: 38px;
      height: 38px;
      border-radius: 14px;
      background: conic-gradient(
        from 210deg,
        #4f8cff,
        #36d98b,
        #ffc857,
        #4f8cff
      );
      position: relative;
      box-shadow: 0 0 0 1px rgba(11, 13, 31, 1),
        0 10px 25px rgba(7, 10, 30, 0.7);
      overflow: hidden;
    }

    .brand-logo-inner {
      position: absolute;
      inset: 2px;
      border-radius: 12px;
      background: radial-gradient(circle at 10% 0, #17233f, #03040c);
      display: flex;
      align-items: center;
      justify-content: center;
      color: #f7f8ff;
      font-weight: 700;
      font-size: 16px;
      letter-spacing: 0.06em;
    }

    .brand-text-primary {
      font-weight: 650;
      letter-spacing: 0.08em;
      text-transform: uppercase;
      font-size: 13px;
    }

    .brand-text-primary span {
      color: var(--accent);
    }

    .brand-text-secondary {
      font-size: 11px;
      color: var(--text-soft);
      letter-spacing: 0.08em;
      text-transform: uppercase;
    }

    .app-header-right {
      display: flex;
      align-items: center;
      gap: 12px;
      flex-wrap: wrap;
      justify-content: flex-end;
    }

    .pill-chip {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      padding: 6px 12px;
      border-radius: var(--radius-pill);
      background: rgba(4, 7, 20, 0.7);
      border: 1px solid rgba(84, 93, 150, 0.6);
      font-size: 11px;
      text-transform: uppercase;
      letter-spacing: 0.12em;
      color: var(--text-soft);
    }

    .pill-dot {
      width: 8px;
      height: 8px;
      border-radius: 999px;
      background: radial-gradient(circle, #6cf19a, #13a95a);
      box-shadow: 0 0 0 1px rgba(12, 32, 18, 1),
        0 0 12px rgba(108, 241, 154, 0.7);
    }

    .pill-badge {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      padding: 6px 11px;
      border-radius: var(--radius-pill);
      background: rgba(13, 18, 40, 0.8);
      border: 1px solid rgba(126, 153, 255, 0.6);
      font-size: 11px;
      letter-spacing: 0.08em;
      text-transform: uppercase;
      color: var(--accent-strong);
      position: relative;
      overflow: hidden;
    }

    .pill-badge::before {
      content: "";
      position: absolute;
      inset: 0;
      background: radial-gradient(
        circle at 0 0,
        rgba(255, 255, 255, 0.2),
        transparent 52%
      );
      opacity: 0.3;
      pointer-events: none;
    }

    .pill-badge-icon {
      width: 14px;
      height: 14px;
      border-radius: 999px;
      background: radial-gradient(circle at 30% 30%, #ffffff, #6ca0ff);
      display: inline-flex;
      align-items: center;
      justify-content: center;
      font-size: 10px;
      color: #050711;
    }

    .pill-badge-label {
      position: relative;
      z-index: 1;
    }

    .app-body {
      display: grid;
      grid-template-columns: minmax(0, 2.1fr) minmax(0, 1.4fr);
      gap: 16px;
      margin-top: 4px;
      flex: 1;
    }

    @media (max-width: 980px) {
      .app-body {
        grid-template-columns: minmax(0, 1fr);
      }
    }

    /* 
    ==========================================
    LEFT COLUMN – PORTFOLIO OVERVIEW
    ==========================================
    */

    .panel {
      background: linear-gradient(
        145deg,
        rgba(13, 16, 32, 0.98),
        rgba(6, 8, 20, 0.98)
      );
      border-radius: var(--radius-xl);
      border: 1px solid rgba(42, 49, 90, 0.95);
      box-shadow: var(--shadow-soft);
      padding: 16px 16px 18px;
      display: flex;
      flex-direction: column;
      gap: 14px;
      position: relative;
      overflow: hidden;
    }

    .panel::before {
      content: "";
      position: absolute;
      inset: 0;
      background: radial-gradient(
        circle at top left,
        rgba(79, 140, 255, 0.13),
        transparent 55%
      );
      opacity: 0.9;
      pointer-events: none;
    }

    .panel-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 8px;
      position: relative;
      z-index: 1;
    }

    .panel-title-block {
      display: flex;
      flex-direction: column;
      gap: 2px;
    }

    .panel-title {
      font-size: 14px;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      color: var(--text-soft);
    }

    .panel-subtitle {
      font-size: 11px;
      color: var(--text-muted);
    }

    .panel-actions {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      flex-wrap: wrap;
      justify-content: flex-end;
    }

    .btn-ghost {
      border-radius: var(--radius-pill);
      border: 1px solid rgba(74, 81, 133, 0.9);
      background: rgba(8, 11, 24, 0.92);
      color: var(--text-soft);
      padding: 7px 12px;
      font-size: 11px;
      letter-spacing: 0.10em;
      text-transform: uppercase;
      display: inline-flex;
      align-items: center;
      gap: 6px;
      cursor: pointer;
      transition: transform var(--transition-fast), box-shadow var(--transition-fast),
        border-color var(--transition-fast), background var(--transition-fast);
    }

    .btn-ghost:hover {
      transform: translateY(-1px);
      box-shadow: 0 8px 18px rgba(0, 0, 0, 0.5);
      border-color: rgba(113, 129, 214, 1);
      background: rgba(12, 16, 30, 1);
    }

    .btn-ghost-icon {
      width: 14px;
      height: 14px;
      border-radius: 999px;
      border: 1px solid rgba(92, 101, 163, 0.9);
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 10px;
    }

    /* 
    PORTFOLIO SUMMARY
    */

    .portfolio-summary {
      display: grid;
      grid-template-columns: minmax(0, 1.8fr) minmax(0, 1.2fr);
      gap: 16px;
      align-items: stretch;
      position: relative;
      z-index: 1;
      margin-top: 4px;
    }

    @media (max-width: 820px) {
      .portfolio-summary {
        grid-template-columns: minmax(0, 1fr);
      }
    }

    .portfolio-main-card {
      border-radius: var(--radius-lg);
      background: radial-gradient(
          circle at top left,
          rgba(79, 140, 255, 0.16),
          transparent 55%
        ),
        linear-gradient(145deg, #080a1b, #050612);
      border: 1px solid rgba(62, 77, 141, 0.95);
      padding: 14px 14px 12px;
      position: relative;
      overflow: hidden;
    }

    .portfolio-main-card::before {
      content: "";
      position: absolute;
      inset: 0;
      background: radial-gradient(
        circle at 110% 0,
        rgba(54, 217, 139, 0.12),
        transparent 50%
      );
      opacity: 1;
      pointer-events: none;
    }

    .portfolio-main-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 8px;
      margin-bottom: 10px;
      position: relative;
      z-index: 1;
    }

    .portfolio-main-label {
      font-size: 11px;
      letter-spacing: 0.15em;
      text-transform: uppercase;
      color: var(--text-soft);
    }

    .portfolio-main-meta {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      font-size: 11px;
      color: var(--text-muted);
    }

    .portfolio-main-badge {
      padding: 3px 8px;
      border-radius: var(--radius-pill);
      background: rgba(7, 11, 26, 0.9);
      border: 1px solid rgba(64, 81, 166, 0.9);
      color: var(--accent-strong);
      text-transform: uppercase;
      letter-spacing: 0.09em;
      font-size: 9px;
    }

    .portfolio-main-body {
      display: flex;
      flex-direction: column;
      gap: 10px;
      position: relative;
      z-index: 1;
    }

    .portfolio-total {
      font-size: 28px;
      font-weight: 650;
      letter-spacing: 0.03em;
    }

    .portfolio-total span {
      font-size: 12px;
      text-transform: uppercase;
      letter-spacing: 0.24em;
      color: var(--text-muted);
      margin-right: 10px;
    }

    .portfolio-change-row {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 10px;
      flex-wrap: wrap;
    }

    .portfolio-change {
      display: inline-flex;
      align-items: baseline;
      gap: 6px;
      font-size: 12px;
    }

    .portfolio-change-positive {
      color: var(--accent-green);
    }

    .portfolio-change-negative {
      color: var(--accent-red);
    }

    .portfolio-change-label {
      font-size: 10px;
      text-transform: uppercase;
      letter-spacing: 0.15em;
      color: var(--text-muted);
    }

    .portfolio-allocation {
      display: flex;
      align-items: center;
      gap: 6px;
      font-size: 11px;
      color: var(--text-soft);
    }

    .allocation-bar {
      flex: 1;
      height: 7px;
      border-radius: 999px;
      background: rgba(19, 23, 45, 1);
      overflow: hidden;
      position: relative;
    }

    .allocation-bar-fill {
      position: absolute;
      inset: 0;
      transform-origin: left;
      transform: scaleX(0.3);
      background: linear-gradient(90deg, #4f8cff, #36d98b, #ffc857);
      transition: transform 0.25s ease-out;
    }

    .allocation-legend {
      display: inline-flex;
      gap: 8px;
      flex-wrap: wrap;
      font-size: 10px;
      text-transform: uppercase;
      letter-spacing: 0.16em;
      color: var(--text-muted);
    }

    .allocation-legend span {
      display: inline-flex;
      align-items: center;
      gap: 4px;
    }

    .legend-dot {
      width: 8px;
      height: 8px;
      border-radius: 999px;
      background: #4f8cff;
    }

    .legend-dot.cash {
      background: #36d98b;
    }

    .legend-dot.other {
      background: #ffc857;
    }

    .portfolio-side-card {
      border-radius: var(--radius-lg);
      background: radial-gradient(
          circle at top right,
          rgba(255, 200, 87, 0.16),
          transparent 60%
        ),
        linear-gradient(145deg, #111329, #070819);
      border: 1px solid rgba(82, 61, 136, 0.9);
      padding: 12px 12px 10px;
      display: flex;
      flex-direction: column;
      gap: 6px;
    }

    .portfolio-side-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 6px;
    }

    .portfolio-side-label {
      font-size: 11px;
      text-transform: uppercase;
      letter-spacing: 0.16em;
      color: var(--text-soft);
    }

    .portfolio-side-chip {
      padding: 4px 8px;
      border-radius: var(--radius-pill);
      font-size: 10px;
      text-transform: uppercase;
      letter-spacing: 0.15em;
      background: rgba(21, 11, 41, 0.8);
      border: 1px solid rgba(160, 132, 254, 0.9);
      color: #c2b2ff;
    }

    .portfolio-side-body {
      display: flex;
      flex-direction: column;
      gap: 5px;
      margin-top: 2px;
    }

    .portfolio-side-row {
      display: flex;
      justify-content: space-between;
      align-items: baseline;
      font-size: 12px;
      color: var(--text-soft);
    }

    .portfolio-side-row strong {
      font-weight: 600;
      color: var(--text-main);
    }

    .portfolio-side-row-sub {
      font-size: 10px;
      color: var(--text-muted);
      text-transform: uppercase;
      letter-spacing: 0.16em;
    }

    .portfolio-side-highlight {
      color: var(--accent-green);
      font-weight: 600;
    }

    /* 
    PORTFOLIO CHART
    */

    .chart-section {
      border-radius: var(--radius-lg);
      background: radial-gradient(
          circle at 60% 0,
          rgba(79, 140, 255, 0.18),
          transparent 58%
        ),
        linear-gradient(160deg, #050612, #050612 18%, #070b1b);
      border: 1px solid rgba(49, 61, 116, 0.96);
      padding: 12px 12px 10px;
      display: flex;
      flex-direction: column;
      gap: 8px;
      position: relative;
      overflow: hidden;
    }

    .chart-section::before {
      content: "";
      position: absolute;
      inset: 0;
      background-image: linear-gradient(
          rgba(255, 255, 255, 0.03) 1px,
          transparent 1px
        ),
        linear-gradient(
          90deg,
          rgba(255, 255, 255, 0.03) 1px,
          transparent 1px
        );
      background-size: 40px 26px;
      opacity: 0.9;
      pointer-events: none;
    }

    .chart-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 6px;
      position: relative;
      z-index: 1;
    }

    .chart-title {
      font-size: 11px;
      text-transform: uppercase;
      letter-spacing: 0.15em;
      color: var(--text-soft);
    }

    .chart-legend {
      display: inline-flex;
      gap: 10px;
      font-size: 10px;
      text-transform: uppercase;
      letter-spacing: 0.12em;
      color: var(--text-muted);
      align-items: center;
    }

    .chart-legend span {
      display: inline-flex;
      align-items: center;
      gap: 4px;
    }

    .chart-legend-dot {
      width: 7px;
      height: 7px;
      border-radius: 999px;
      background: #4f8cff;
      border: 1px solid rgba(193, 204, 255, 0.9);
    }

    .chart-legend-dot.benchmark {
      background: rgba(255, 255, 255, 0.02);
      border-color: rgba(161, 168, 214, 0.9);
    }

    .chart-body {
      position: relative;
      z-index: 1;
      margin-top: 4px;
    }

    .chart-canvas-wrapper {
      position: relative;
      width: 100%;
      height: 140px;
      border-radius: 12px;
      overflow: hidden;
      background: linear-gradient(
        145deg,
        rgba(15, 20, 45, 0.9),
        rgba(7, 10, 25, 0.9)
      );
      border: 1px solid rgba(51, 59, 109, 1);
      box-shadow: 0 12px 26px rgba(0, 0, 0, 0.7);
    }

    canvas#portfolioChart {
      width: 100%;
      height: 100%;
      display: block;
    }

    .chart-footer {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-top: 8px;
      gap: 6px;
      font-size: 10px;
      color: var(--text-muted);
      position: relative;
      z-index: 1;
    }

    .chart-range-selector {
      display: inline-flex;
      padding: 2px;
      border-radius: var(--radius-pill);
      background: rgba(4, 7, 20, 0.95);
      border: 1px solid rgba(50, 61, 111, 0.96);
      gap: 2px;
    }

    .chart-range-btn {
      border: none;
      outline: none;
      cursor: pointer;
      border-radius: var(--radius-pill);
      padding: 4px 7px;
      background: transparent;
      color: var(--text-muted);
      font-size: 9px;
      text-transform: uppercase;
      letter-spacing: 0.14em;
      transition: background var(--transition-fast),
        color var(--transition-fast), box-shadow var(--transition-fast);
    }

    .chart-range-btn.active {
      background: linear-gradient(135deg, #4f8cff, #36d98b);
      color: #050612;
      box-shadow: 0 0 0 1px rgba(8, 16, 33, 0.9),
        0 8px 18px rgba(0, 0, 0, 0.7);
    }

    /* 
    ASSET TABLE
    */

    .portfolio-assets-section {
      position: relative;
      z-index: 1;
      margin-top: 4px;
      display: flex;
      flex-direction: column;
      gap: 10px;
    }

    .assets-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 8px;
      flex-wrap: wrap;
    }

    .assets-title {
      font-size: 11px;
      text-transform: uppercase;
      letter-spacing: 0.16em;
      color: var(--text-soft);
    }

    .assets-search-wrapper {
      display: flex;
      gap: 8px;
      align-items: center;
      flex-wrap: wrap;
    }

    .search-input {
      border-radius: var(--radius-pill);
      border: 1px solid rgba(45, 56, 112, 0.9);
      background: rgba(9, 11, 28, 0.96);
      padding: 6px 9px;
      font-size: 11px;
      color: var(--text-soft);
      min-width: 160px;
      display: inline-flex;
      align-items: center;
      gap: 6px;
    }

    .search-input input {
      border: none;
      outline: none;
      background: transparent;
      color: inherit;
      font-size: inherit;
      flex: 1;
      min-width: 0;
    }

    .search-input-icon {
      font-size: 11px;
      opacity: 0.7;
    }

    .assets-quick-filter {
      display: inline-flex;
      gap: 6px;
      flex-wrap: wrap;
      font-size: 10px;
    }

    .assets-quick-filter button {
      border-radius: var(--radius-pill);
      border: none;
      background: rgba(7, 10, 25, 0.95);
      color: var(--text-muted);
      padding: 4px 7px;
      cursor: pointer;
      text-transform: uppercase;
      letter-spacing: 0.16em;
      transition: background var(--transition-fast),
        color var(--transition-fast), transform var(--transition-fast);
    }

    .assets-quick-filter button.active {
      background: rgba(79, 140, 255, 0.16);
      color: var(--accent-strong);
      transform: translateY(-1px);
    }

    .assets-table-wrapper {
      border-radius: var(--radius-lg);
      background: radial-gradient(
          circle at 0 0,
          rgba(79, 140, 255, 0.08),
          transparent 50%
        ),
        linear-gradient(145deg, rgba(7, 10, 24, 0.98), rgba(4, 5, 16, 0.98));
      border: 1px solid rgba(42, 50, 95, 0.95);
      overflow: hidden;
      position: relative;
    }

    .assets-table {
      width: 100%;
      border-collapse: collapse;
      font-size: 12px;
    }

    .assets-table thead {
      background: linear-gradient(
        180deg,
        rgba(7, 9, 22, 0.98),
        rgba(3, 4, 12, 0.98)
      );
    }

    .assets-table th,
    .assets-table td {
      padding: 8px 10px;
      border-bottom: 1px solid rgba(24, 29, 65, 0.96);
      text-align: right;
      white-space: nowrap;
    }

    .assets-table th {
      font-size: 10px;
      text-transform: uppercase;
      letter-spacing: 0.16em;
      color: var(--text-muted);
      font-weight: 500;
      position: sticky;
      top: 0;
      z-index: 2;
      background: linear-gradient(
        180deg,
        rgba(7, 9, 22, 0.97),
        rgba(3, 4, 12, 0.99)
      );
      backdrop-filter: blur(12px);
    }

    .assets-table th:first-child,
    .assets-table td:first-child {
      text-align: left;
    }

    .assets-table tbody tr:last-child td {
      border-bottom: none;
    }

    .assets-table tbody tr {
      background: transparent;
      transition: background var(--transition-fast);
    }

    .assets-table tbody tr:hover {
      background: rgba(255, 255, 255, 0.02);
    }

    .asset-name-cell {
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .asset-avatar {
      width: 22px;
      height: 22px;
      border-radius: 999px;
      background: radial-gradient(circle at 20% 20%, #ffffff, #4f8cff);
      font-size: 11px;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      color: #050612;
      font-weight: 600;
      box-shadow: 0 0 0 1px rgba(5, 7, 20, 0.98);
    }

    .asset-name-labels {
      display: flex;
      flex-direction: column;
      gap: 2px;
    }

    .asset-symbol {
      font-size: 11px;
      font-weight: 600;
    }

    .asset-name {
      font-size: 10px;
      color: var(--text-muted);
    }

    .asset-pill {
      border-radius: var(--radius-pill);
      padding: 3px 6px;
      font-size: 10px;
      background: rgba(9, 14, 33, 0.96);
      border: 1px solid rgba(53, 64, 122, 0.96);
      color: var(--text-soft);
      display: inline-flex;
      align-items: center;
      gap: 5px;
    }

    .asset-pill-dot {
      width: 8px;
      height: 8px;
      border-radius: 999px;
      background: #4f8cff;
    }

    .asset-pill-dot.gain {
      background: #36d98b;
    }

    .asset-pill-dot.loss {
      background: #ff4d67;
    }

    .asset-change-pos {
      color: var(--accent-green);
    }

    .asset-change-neg {
      color: var(--accent-red);
    }

    .asset-actions-cell {
      display: flex;
      justify-content: flex-end;
      gap: 6px;
    }

    .btn-mini {
      border-radius: var(--radius-pill);
      border: 1px solid rgba(52, 61, 117, 1);
      background: rgba(4, 6, 16, 0.98);
      color: var(--text-soft);
      font-size: 10px;
      text-transform: uppercase;
      letter-spacing: 0.12em;
      padding: 4px 7px;
      cursor: pointer;
      transition: transform var(--transition-fast),
        box-shadow var(--transition-fast), border-color var(--transition-fast);
    }

    .btn-mini.primary {
      background: linear-gradient(140deg, #4f8cff, #36d98b);
      color: #050612;
      border-color: rgba(62, 223, 162, 0.9);
      box-shadow: 0 0 0 1px rgba(3, 8, 20, 0.96),
        0 9px 20px rgba(0, 0, 0, 0.9);
    }

    .btn-mini:hover {
      transform: translateY(-1px);
      box-shadow: 0 8px 16px rgba(0, 0, 0, 0.75);
      border-color: rgba(91, 109, 192, 1);
    }

    .btn-mini.primary:hover {
      border-color: rgba(255, 255, 255, 0.7);
    }

    .empty-state {
      padding: 14px 10px 16px;
      text-align: center;
      font-size: 12px;
      color: var(--text-muted);
      background: rgba(5, 7, 18, 0.96);
    }

    /* 
    ==========================================
    RIGHT COLUMN – INVEST CONTROLS
    ==========================================
    */

    .right-column {
      display: flex;
      flex-direction: column;
      gap: 14px;
    }

    .balance-card {
      border-radius: var(--radius-xl);
      background: radial-gradient(
          circle at 110% 0,
          rgba(54, 217, 139, 0.18),
          transparent 65%
        ),
        linear-gradient(160deg, #0b101f, #050611);
      border: 1px solid rgba(63, 85, 148, 0.96);
      padding: 14px 14px 12px;
      position: relative;
      overflow: hidden;
      box-shadow: var(--shadow-soft);
    }

    .balance-card::before {
      content: "";
      position: absolute;
      inset: 0;
      background-image: radial-gradient(
          circle at 20% -10%,
          rgba(79, 140, 255, 0.26),
          transparent 55%
        ),
        radial-gradient(
          circle at 130% 10%,
          rgba(255, 200, 87, 0.28),
          transparent 58%
        );
      opacity: 0.9;
      pointer-events: none;
    }

    .balance-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 10px;
      position: relative;
      z-index: 1;
    }

    .balance-labels {
      display: flex;
      flex-direction: column;
      gap: 3px;
    }

    .balance-label {
      font-size: 11px;
      text-transform: uppercase;
      letter-spacing: 0.16em;
      color: var(--text-soft);
    }

    .balance-amount {
      font-size: 24px;
      font-weight: 650;
      letter-spacing: 0.04em;
    }

    .balance-status {
      font-size: 10px;
      text-transform: uppercase;
      letter-spacing: 0.13em;
      color: var(--text-muted);
    }

    .balance-status span {
      color: var(--accent-green);
      font-weight: 600;
    }

    .balance-tag {
      padding: 4px 9px;
      border-radius: var(--radius-pill);
      font-size: 10px;
      text-transform: uppercase;
      letter-spacing: 0.14em;
      background: rgba(3, 5, 16, 0.92);
      border: 1px solid rgba(83, 111, 202, 0.95);
      color: #d5ddff;
      display: inline-flex;
      gap: 6px;
      align-items: center;
    }

    .balance-tag-badge {
      width: 12px;
      height: 12px;
      border-radius: 999px;
      background: radial-gradient(circle at 15% 15%, #ffffff, #4f8cff);
      display: inline-flex;
      align-items: center;
      justify-content: center;
      font-size: 9px;
      color: #050612;
      font-weight: 700;
    }

    .balance-body {
      margin-top: 10px;
      position: relative;
      z-index: 1;
      display: flex;
      flex-direction: column;
      gap: 10px;
    }

    .balance-bars {
      display: flex;
      flex-direction: column;
      gap: 4px;
    }

    .balance-bar-row {
      display: flex;
      align-items: center;
      gap: 8px;
      font-size: 11px;
      color: var(--text-soft);
    }

    .balance-bar-row span:first-child {
      flex: 0 0 70px;
      text-transform: uppercase;
      letter-spacing: 0.15em;
      font-size: 9px;
      color: var(--text-muted);
    }

    .balance-bar-track {
      flex: 1;
      height: 7px;
      background: rgba(3, 5, 16, 0.95);
      border-radius: 999px;
      overflow: hidden;
      position: relative;
      border: 1px solid rgba(36, 44, 90, 0.96);
    }

    .balance-bar-fill {
      position: absolute;
      inset: 0;
      transform-origin: left;
      transform: scaleX(0.35);
      transition: transform 0.25s ease-out;
      background: linear-gradient(90deg, #4f8cff, #36d98b);
    }

    .balance-bar-fill.cash {
      background: linear-gradient(90deg, #36d98b, #ffc857);
    }

    .balance-details-row {
      display: flex;
      justify-content: space-between;
      gap: 8px;
      font-size: 11px;
      color: var(--text-soft);
      flex-wrap: wrap;
    }

    .balance-mini-stat {
      display: inline-flex;
      flex-direction: column;
      gap: 3px;
    }

    .balance-mini-label {
      font-size: 9px;
      text-transform: uppercase;
      letter-spacing: 0.15em;
      color: var(--text-muted);
    }

    .balance-mini-value {
      font-size: 12px;
      font-weight: 500;
    }

    .balance-mini-value.positive {
      color: var(--accent-green);
    }

    .balance-mini-value.negative {
      color: var(--accent-red);
    }

    .balance-footer {
      margin-top: 6px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-size: 10px;
      color: var(--text-muted);
      gap: 8px;
      flex-wrap: wrap;
    }

    .balance-footer span {
      display: inline-flex;
      align-items: center;
      gap: 6px;
    }

    .risk-chip {
      padding: 3px 8px;
      border-radius: var(--radius-pill);
      border: 1px solid rgba(133, 92, 255, 0.9);
      background: rgba(16, 8, 34, 0.9);
      color: #d6c8ff;
      text-transform: uppercase;
      letter-spacing: 0.14em;
      font-size: 9px;
    }

    /* 
    INVEST FORM
    */

    .invest-panel {
      border-radius: var(--radius-xl);
      background: radial-gradient(
          circle at 50% -10%,
          rgba(79, 140, 255, 0.16),
          transparent 55%
        ),
        linear-gradient(150deg, #090c22, #03040d);
      border: 1px solid rgba(45, 56, 112, 0.98);
      padding: 12px 14px 14px;
      box-shadow: var(--shadow-soft);
      position: relative;
      overflow: hidden;
    }

    .invest-panel::before {
      content: "";
      position: absolute;
      inset: 0;
      background-size: 80px 80px;
      background-image: radial-gradient(
        circle at 0 0,
        rgba(255, 255, 255, 0.05) 1px,
        transparent 1px
      );
      opacity: 0.5;
      pointer-events: none;
    }

    .invest-header {
      position: relative;
      z-index: 1;
      display: flex;
      flex-direction: column;
      gap: 4px;
      margin-bottom: 8px;
    }

    .invest-title-row {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 8px;
      flex-wrap: wrap;
    }

    .invest-title {
      font-size: 13px;
      letter-spacing: 0.14em;
      text-transform: uppercase;
      color: var(--text-soft);
    }

    .invest-title span {
      color: var(--accent-strong);
    }

    .invest-subtitle {
      font-size: 11px;
      color: var(--text-muted);
    }

    .invest-mode-toggle {
      display: inline-flex;
      border-radius: var(--radius-pill);
      background: rgba(3, 5, 14, 0.96);
      border: 1px solid rgba(41, 53, 112, 0.96);
      padding: 2px;
      gap: 2px;
    }

    .invest-mode-btn {
      border-radius: var(--radius-pill);
      border: none;
      background: transparent;
      color: var(--text-muted);
      font-size: 9px;
      letter-spacing: 0.14em;
      text-transform: uppercase;
      padding: 4px 7px;
      cursor: pointer;
      transition: background var(--transition-fast),
        color var(--transition-fast), transform var(--transition-fast),
        box-shadow var(--transition-fast);
    }

    .invest-mode-btn.active {
      background: linear-gradient(135deg, #4f8cff, #36d98b);
      color: #050612;
      box-shadow: 0 0 0 1px rgba(5, 9, 24, 0.9),
        0 7px 18px rgba(0, 0, 0, 0.7);
      transform: translateY(-0.5px);
    }

    .invest-body {
      position: relative;
      z-index: 1;
      margin-top: 6px;
      display: flex;
      flex-direction: column;
      gap: 10px;
    }

    .invest-form-row {
      display: flex;
      flex-direction: column;
      gap: 6px;
    }

    .input-label-row {
      display: flex;
      justify-content: space-between;
      align-items: baseline;
      font-size: 11px;
      color: var(--text-soft);
      flex-wrap: wrap;
      gap: 4px;
    }

    .input-label-row label {
      font-size: 11px;
      text-transform: uppercase;
      letter-spacing: 0.15em;
      color: var(--text-muted);
    }

    .input-label-helper {
      font-size: 10px;
      color: var(--text-soft);
    }

    .input-label-helper span {
      color: var(--accent-green);
      font-weight: 600;
    }

    .nova-input {
      border-radius: var(--radius-md);
      border: 1px solid rgba(40, 51, 104, 0.96);
      background: rgba(5, 7, 20, 0.98);
      padding: 7px 9px;
      display: flex;
      align-items: center;
      gap: 7px;
      font-size: 12px;
      color: var(--text-main);
    }

    .nova-input input,
    .nova-input select {
      border: none;
      outline: none;
      background: transparent;
      color: inherit;
      font-size: inherit;
      flex: 1;
      min-width: 0;
    }

    .nova-input-prefix,
    .nova-input-suffix {
      font-size: 11px;
      color: var(--text-muted);
      text-transform: uppercase;
      letter-spacing: 0.14em;
    }

    .nova-input-tag {
      font-size: 10px;
      color: var(--accent-strong);
      text-transform: uppercase;
      letter-spacing: 0.13em;
      padding: 3px 6px;
      border-radius: var(--radius-pill);
      background: rgba(22, 28, 66, 0.96);
      border: 1px solid rgba(75, 97, 185, 0.96);
    }

    .nova-input select {
      appearance: none;
      -webkit-appearance: none;
      -moz-appearance: none;
      padding-right: 12px;
    }

    .nova-input.select::after {
      content: "▾";
      font-size: 10px;
      color: var(--text-muted);
    }

    .input-hint {
      font-size: 10px;
      color: var(--text-muted);
      margin-top: 2px;
    }

    .quick-amount-row {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 6px;
      flex-wrap: wrap;
      font-size: 10px;
      color: var(--text-muted);
    }

    .quick-amount-buttons {
      display: inline-flex;
      gap: 4px;
      flex-wrap: wrap;
    }

    .quick-amount-buttons button {
      border-radius: var(--radius-pill);
      border: 1px solid rgba(36, 45, 97, 0.96);
      background: rgba(5, 8, 22, 0.98);
      color: var(--text-soft);
      font-size: 9px;
      text-transform: uppercase;
      letter-spacing: 0.16em;
      padding: 3px 7px;
      cursor: pointer;
      transition: background var(--transition-fast),
        color var(--transition-fast), transform var(--transition-fast);
    }

    .quick-amount-buttons button:hover {
      background: rgba(79, 140, 255, 0.14);
      color: var(--accent-strong);
      transform: translateY(-1px);
    }

    .invest-cta-row {
      display: flex;
      flex-direction: column;
      gap: 6px;
      margin-top: 6px;
    }

    .btn-primary-wide {
      border-radius: 12px;
      border: none;
      background: linear-gradient(135deg, #4f8cff, #36d98b);
      color: #050612;
      font-size: 12px;
      font-weight: 600;
      letter-spacing: 0.16em;
      text-transform: uppercase;
      padding: 9px 10px;
      cursor: pointer;
      box-shadow: 0 0 0 1px rgba(3, 7, 18, 0.96),
        0 12px 26px rgba(0, 0, 0, 0.95);
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 8px;
      transition: transform var(--transition-normal),
        box-shadow var(--transition-normal), filter var(--transition-normal);
    }

    .btn-primary-wide:hover {
      transform: translateY(-1px);
      box-shadow: 0 14px 30px rgba(0, 0, 0, 0.98);
      filter: brightness(1.04);
    }

    .btn-primary-wide:active {
      transform: translateY(0);
      box-shadow: 0 8px 16px rgba(0, 0, 0, 0.95);
      filter: brightness(0.98);
    }

    .btn-primary-icon {
      width: 18px;
      height: 18px;
      border-radius: 999px;
      background: rgba(7, 8, 16, 0.98);
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 11px;
      color: var(--accent-strong);
    }

    .invest-note {
      font-size: 10px;
      color: var(--text-muted);
      display: flex;
      align-items: flex-start;
      gap: 6px;
    }

    .invest-note-dot {
      width: 6px;
      height: 6px;
      border-radius: 999px;
      background: rgba(255, 255, 255, 0.18);
      margin-top: 3px;
    }

    /* 
    ACTIVITY LOG
    */

    .activity-panel {
      border-radius: var(--radius-xl);
      background: radial-gradient(
          circle at 0 0,
          rgba(79, 140, 255, 0.18),
          transparent 60%
        ),
        linear-gradient(145deg, #070918, #020309);
      border: 1px solid rgba(39, 48, 98, 0.96);
      padding: 12px 14px 10px;
      box-shadow: var(--shadow-soft);
      position: relative;
      overflow: hidden;
    }

    .activity-panel::before {
      content: "";
      position: absolute;
      inset: 0;
      background-image: linear-gradient(
        rgba(255, 255, 255, 0.02) 1px,
        transparent 1px
      );
      background-size: auto 32px;
      opacity: 0.9;
      pointer-events: none;
    }

    .activity-header {
      position: relative;
      z-index: 1;
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 10px;
    }

    .activity-title {
      font-size: 11px;
      text-transform: uppercase;
      letter-spacing: 0.16em;
      color: var(--text-soft);
    }

    .activity-title span {
      color: var(--accent-strong);
    }

    .activity-filter {
      border-radius: var(--radius-pill);
      padding: 4px 8px;
      border: 1px solid rgba(43, 53, 101, 0.96);
      background: rgba(5, 8, 20, 0.96);
      font-size: 9px;
      text-transform: uppercase;
      letter-spacing: 0.16em;
      color: var(--text-muted);
      display: inline-flex;
      align-items: center;
      gap: 6px;
      cursor: default;
    }

    .activity-body {
      position: relative;
      z-index: 1;
      margin-top: 8px;
      max-height: 190px;
      overflow-y: auto;
      padding-right: 4px;
    }

    .activity-list {
      list-style: none;
      margin: 0;
      padding: 0;
      display: flex;
      flex-direction: column;
      gap: 6px;
      font-size: 11px;
    }

    .activity-item {
      border-radius: 10px;
      background: rgba(5, 7, 18, 0.96);
      border: 1px solid rgba(29, 36, 80, 0.96);
      padding: 7px 8px;
      display: flex;
      flex-direction: column;
      gap: 3px;
    }

    .activity-item-header {
      display: flex;
      justify-content: space-between;
      gap: 8px;
      flex-wrap: wrap;
      align-items: baseline;
    }

    .activity-item-title {
      font-size: 11px;
    }

    .activity-item-title span {
      font-weight: 600;
    }

    .activity-item-meta {
      font-size: 10px;
      color: var(--text-muted);
      text-transform: uppercase;
      letter-spacing: 0.13em;
      display: inline-flex;
      gap: 4px;
      align-items: center;
    }

    .activity-tag-buy {
      color: var(--accent-green);
    }

    .activity-tag-sell {
      color: var(--accent-red);
    }

    .activity-item-footer {
      display: flex;
      justify-content: space-between;
      align-items: baseline;
      gap: 8px;
      flex-wrap: wrap;
      font-size: 10px;
      color: var(--text-soft);
    }

    .activity-item-footer span {
      white-space: nowrap;
    }

    .activity-empty {
      font-size: 11px;
      color: var(--text-muted);
      padding: 10px 4px 6px;
      text-align: center;
    }

    /* 
    SCROLLBARS
    */

    .activity-body::-webkit-scrollbar,
    .assets-table-wrapper::-webkit-scrollbar {
      width: 7px;
      height: 7px;
    }

    .activity-body::-webkit-scrollbar-track,
    .assets-table-wrapper::-webkit-scrollbar-track {
      background: rgba(3, 5, 15, 0.5);
    }

    .activity-body::-webkit-scrollbar-thumb,
    .assets-table-wrapper::-webkit-scrollbar-thumb {
      background: rgba(53, 64, 122, 0.96);
      border-radius: 999px;
    }

    .activity-body::-webkit-scrollbar-thumb:hover,
    .assets-table-wrapper::-webkit-scrollbar-thumb:hover {
      background: rgba(86, 102, 176, 0.96);
    }

    /* 
    FOOTER
    */

    .app-footer {
      margin-top: 10px;
      padding: 8px 3px 2px;
      font-size: 10px;
      color: var(--text-muted);
      text-align: center;
      letter-spacing: 0.15em;
      text-transform: uppercase;
    }

    .app-footer span {
      color: var(--accent-strong);
    }

    /* Utility states */

    .text-muted-soft {
      color: var(--text-muted);
    }

    .highlight {
      color: var(--accent-strong);
    }

    .hidden {
      display: none !important;
    }
  </style>
</head>
<body>
  <div class="app-shell">

    <!-- ==========================================
         HEADER
    =============================================== -->
    <header class="app-header">
      <div class="app-brand">
        <div class="brand-logo">
          <div class="brand-logo-inner">NI</div>
        </div>
        <div>
          <div class="brand-text-primary">
            NOVA<span>INVEST</span>
          </div>
          <div class="brand-text-secondary">
            Start with 100 • Learn by doing
          </div>
        </div>
      </div>
      <div class="app-header-right">
        <div class="pill-chip">
          <span class="pill-dot"></span>
          LIVE PAPER MODE
        </div>
        <div class="pill-badge">
          <span class="pill-badge-icon">★</span>
          <span class="pill-badge-label">Beginner‑friendly investing sandbox</span>
        </div>
      </div>
    </header>

    <!-- ==========================================
         BODY
    =============================================== -->
    <div class="app-body">

      <!-- LEFT COLUMN -->
      <section class="panel">
        <div class="panel-header">
          <div class="panel-title-block">
            <div class="panel-title">Portfolio overview</div>
            <div class="panel-subtitle">Track how your simulated $100 evolves over time.</div>
          </div>
          <div class="panel-actions">
            <button class="btn-ghost" id="resetPortfolioBtn" title="Reset everything back to 100 dollars">
              <span class="btn-ghost-icon">↺</span>
              RESET TO $100
            </button>
          </div>
        </div>

        <!-- PORTFOLIO SUMMARY -->
        <div class="portfolio-summary">
          <div class="portfolio-main-card">
            <div class="portfolio-main-header">
              <div>
                <div class="portfolio-main-label">Total portfolio value</div>
              </div>
              <div class="portfolio-main-meta">
                <div class="portfolio-main-badge">Paper account</div>
              </div>
            </div>
            <div class="portfolio-main-body">
              <div class="portfolio-total">
                <span>USD</span><span id="portfolioTotal">$100.00</span>
              </div>
              <div class="portfolio-change-row">
                <div class="portfolio-change portfolio-change-positive" id="portfolioChange">
                  <span id="portfolioChangeAmount">+$0.00</span>
                  <span id="portfolioChangePercent">(0.00%)</span>
                </div>
                <div class="portfolio-allocation">
                  Allocation
                </div>
              </div>
              <div class="allocation-bar">
                <div class="allocation-bar-fill" id="allocationBarFill"></div>
              </div>
              <div class="allocation-legend">
                <span><span class="legend-dot"></span>Invested</span>
                <span><span class="legend-dot cash"></span>Cash</span>
                <span><span class="legend-dot other"></span>Other</span>
              </div>
            </div>
          </div>

          <div class="portfolio-side-card">
            <div class="portfolio-side-header">
              <div class="portfolio-side-label">Quick stats</div>
              <div class="portfolio-side-chip">Today snapshot</div>
            </div>
            <div class="portfolio-side-body">
              <div class="portfolio-side-row">
                <span class="portfolio-side-row-sub">Invested capital</span>
                <span><strong id="investedCapital">$0.00</strong></span>
              </div>
              <div class="portfolio-side-row">
                <span class="portfolio-side-row-sub">Unrealized P/L</span>
                <span class="portfolio-side-highlight" id="unrealizedPnL">+$0.00</span>
              </div>
              <div class="portfolio-side-row">
                <span class="portfolio-side-row-sub">Number of assets</span>
                <span><strong id="assetCount">0</strong></span>
              </div>
            </div>
          </div>
        </div>

        <!-- CHART -->
        <div class="chart-section">
          <div class="chart-header">
            <div class="chart-title">Portfolio journey</div>
            <div class="chart-legend">
              <span><span class="chart-legend-dot"></span>Value</span>
              <span><span class="chart-legend-dot benchmark"></span>Initial $100</span>
            </div>
          </div>
          <div class="chart-body">
            <div class="chart-canvas-wrapper">
              <canvas id="portfolioChart"></canvas>
            </div>
            <div class="chart-footer">
              <div>Each step represents one action you take.</div>
              <div class="chart-range-selector">
                <button class="chart-range-btn active" data-range="short">SHORT</button>
                <button class="chart-range-btn" data-range="full">FULL</button>
              </div>
            </div>
          </div>
        </div>

        <!-- ASSETS TABLE -->
        <div class="portfolio-assets-section">
          <div class="assets-header">
            <div class="assets-title">Your holdings</div>
            <div class="assets-search-wrapper">
              <div class="search-input">
                <span class="search-input-icon">🔍</span>
                <input
                  type="text"
                  id="assetsSearchInput"
                  placeholder="Filter by symbol or name..."
                />
              </div>
              <div class="assets-quick-filter">
                <button data-filter="all" class="active">ALL</button>
                <button data-filter="gainers">GAINERS</button>
                <button data-filter="losers">LOSERS</button>
                <button data-filter="cash">CASH HEAVY</button>
              </div>
            </div>
          </div>
          <div class="assets-table-wrapper">
            <table class="assets-table">
              <thead>
                <tr>
                  <th>Asset</th>
                  <th>Price</th>
                  <th>Qty</th>
                  <th>Value</th>
                  <th>P/L</th>
                  <th>Actions</th>
                </tr>
              </thead>
              <tbody id="assetsTableBody">
                <!-- Asset rows dynamically injected here -->
              </tbody>
            </table>
            <div class="empty-state" id="assetsEmptyState">
              You own no assets yet. Use the form on the right to buy your first position.
            </div>
          </div>
        </div>
      </section>

      <!-- RIGHT COLUMN -->
      <section class="right-column">

        <!-- BALANCE CARD -->
        <div class="balance-card">
          <div class="balance-header">
            <div class="balance-labels">
              <div class="balance-label">Available cash</div>
              <div class="balance-amount" id="availableCash">$100.00</div>
              <div class="balance-status">
                Starting balance <span>$100.00</span>
              </div>
            </div>
            <div class="balance-tag">
              <span class="balance-tag-badge">$</span>
              <span>Safe practice only</span>
            </div>
          </div>
          <div class="balance-body">
            <div class="balance-bars">
              <div class="balance-bar-row">
                <span>Cash</span>
                <div class="balance-bar-track">
                  <div class="balance-bar-fill cash" id="cashBarFill"></div>
                </div>
              </div>
              <div class="balance-bar-row">
                <span>Invested</span>
                <div class="balance-bar-track">
                  <div class="balance-bar-fill" id="investedBarFill"></div>
                </div>
              </div>
            </div>
            <div class="balance-details-row">
              <div class="balance-mini-stat">
                <div class="balance-mini-label">Total portfolio</div>
                <div class="balance-mini-value" id="miniTotalPortfolio">$100.00</div>
              </div>
              <div class="balance-mini-stat">
                <div class="balance-mini-label">Total P/L</div>
                <div class="balance-mini-value" id="miniTotalPnL">+$0.00</div>
              </div>
              <div class="balance-mini-stat">
                <div class="balance-mini-label">Cash ratio</div>
                <div class="balance-mini-value" id="cashRatio">100%</div>
              </div>
            </div>
            <div class="balance-footer">
              <span>100% virtual • Learn, experiment, iterate</span>
              <span class="risk-chip">Risk: Tutorial only</span>
            </div>
          </div>
        </div>

        <!-- INVEST FORM -->
        <div class="invest-panel">
          <div class="invest-header">
            <div class="invest-title-row">
              <div class="invest-title">
                Place a <span>virtual order</span>
              </div>
              <div class="invest-mode-toggle">
                <button
                  class="invest-mode-btn active"
                  data-mode="buy"
                  id="modeBuyBtn"
                >
                  BUY
                </button>
                <button
                  class="invest-mode-btn"
                  data-mode="sell"
                  id="modeSellBtn"
                >
                  SELL
                </button>
              </div>
            </div>
            <div class="invest-subtitle">
              Define your own assets (like AAPL, BTC, “MyIdea”) and practice with a realistic order flow.
            </div>
          </div>
          <div class="invest-body">

            <!-- Asset symbol -->
            <div class="invest-form-row">
              <div class="input-label-row">
                <label for="assetSymbolInput">Symbol</label>
                <div class="input-label-helper">
                  Example: <span>AAPL</span>, <span>BTC</span>, <span>FUND</span>
                </div>
              </div>
              <div class="nova-input">
                <span class="nova-input-prefix">SYM</span>
                <input
                  type="text"
                  id="assetSymbolInput"
                  placeholder="Type a ticker-like symbol"
                  maxlength="8"
                />
                <span class="nova-input-tag" id="assetTypeTag">New asset</span>
              </div>
              <div class="input-hint">
                If symbol doesn’t exist yet, a new asset will be created with the given price and description.
              </div>
            </div>

            <!-- Asset name -->
            <div class="invest-form-row">
              <div class="input-label-row">
                <label for="assetNameInput">Asset name</label>
                <div class="input-label-helper">
                  Keep it short & clear
                </div>
              </div>
              <div class="nova-input">
                <input
                  type="text"
                  id="assetNameInput"
                  placeholder="E.g. Apple Inc., Bitcoin, Idea Fund"
                  maxlength="32"
                />
              </div>
            </div>

            <!-- Price -->
            <div class="invest-form-row">
              <div class="input-label-row">
                <label for="assetPriceInput">Price</label>
                <div class="input-label-helper">
                  Current simulated price for each unit
                </div>
              </div>
              <div class="nova-input">
                <span class="nova-input-prefix">$</span>
                <input
                  type="number"
                  id="assetPriceInput"
                  placeholder="10"
                  min="0.01"
                  step="0.01"
                />
                <span class="nova-input-suffix">PER UNIT</span>
              </div>
              <div class="input-hint">
                You control the price. Try changing it later to simulate gain or loss on a position you already own.
              </div>
            </div>

            <!-- Quantity -->
            <div class="invest-form-row">
              <div class="input-label-row">
                <label for="assetQuantityInput">Quantity</label>
                <div class="input-label-helper">
                  Max you can buy right now: <span id="maxBuyHint">10.00</span> units
                </div>
              </div>
              <div class="nova-input">
                <input
                  type="number"
                  id="assetQuantityInput"
                  placeholder="1"
                  min="0.01"
                  step="0.01"
                />
                <span class="nova-input-suffix">UNITS</span>
              </div>
              <div class="quick-amount-row">
                <div>Quick amount</div>
                <div class="quick-amount-buttons">
                  <button data-quick="0.25">25%</button>
                  <button data-quick="0.5">50%</button>
                  <button data-quick="1">MAX</button>
                </div>
              </div>
              <div class="input-hint">
                Percentage buttons use available cash (for buy) or your holding (for sell) to calculate a sensible quantity.
              </div>
            </div>

            <!-- Order summary -->
            <div class="invest-form-row">
              <div class="input-label-row">
                <label>Order summary</label>
                <div class="input-label-helper">
                  Est. impact on cash and portfolio
                </div>
              </div>
              <div class="nova-input">
                <span class="nova-input-prefix" id="orderTypeLabel">BUY</span>
                <span id="orderSummaryMain">Ready when you are.</span>
              </div>
              <div class="input-hint" id="orderSummaryHint">
                Start by choosing a symbol and quantity.
              </div>
            </div>

            <!-- CTA -->
            <div class="invest-cta-row">
              <button class="btn-primary-wide" id="submitOrderBtn">
                <span class="btn-primary-icon">✓</span>
                <span id="submitOrderLabel">PLACE BUY ORDER</span>
              </button>
              <div class="invest-note">
                <span class="invest-note-dot"></span>
                <span>
                  This is a practice environment only. No real money or real markets are used here.
                  The goal is to help you experiment, reflect, and learn in a safe space.
                </span>
              </div>
            </div>
          </div>
        </div>

        <!-- ACTIVITY LOG -->
        <div class="activity-panel">
          <div class="activity-header">
            <div class="activity-title">
              Activity <span>timeline</span>
            </div>
            <div class="activity-filter">
              <span>Newest first</span> • <span>Simulated orders</span>
            </div>
          </div>
          <div class="activity-body">
            <ul class="activity-list" id="activityList">
              <!-- Activity items will be injected here -->
            </ul>
            <div class="activity-empty" id="activityEmptyState">
              Every buy or sell operation will show up here with details.
            </div>
          </div>
        </div>
      </section>
    </div>

    <!-- ==========================================
         FOOTER
    =============================================== -->
    <footer class="app-footer">
      NOVA<span>INVEST</span> • Practice portfolio, starting with $100 virtual cash
    </footer>
  </div>

  <!-- ==========================================
       SCRIPT
  =============================================== -->
  <script>
    // Core app state
    const INITIAL_CASH = 100;

    const state = {
      cash: INITIAL_CASH,
      assets: [], // { id, symbol, name, price, quantity, invested, averagePrice }
      history: [], // portfolio value after each action for chart
      activity: [], // logs
      mode: "buy", // or "sell"
    };

    // DOM references
    const portfolioTotalEl = document.getElementById("portfolioTotal");
    const portfolioChangeAmountEl = document.getElementById("portfolioChangeAmount");
    const portfolioChangePercentEl = document.getElementById("portfolioChangePercent");
    const allocationBarFillEl = document.getElementById("allocationBarFill");
    const investedCapitalEl = document.getElementById("investedCapital");
    const unrealizedPnLEl = document.getElementById("unrealizedPnL");
    const assetCountEl = document.getElementById("assetCount");

    const availableCashEl = document.getElementById("availableCash");
    const miniTotalPortfolioEl = document.getElementById("miniTotalPortfolio");
    const miniTotalPnLEl = document.getElementById("miniTotalPnL");
    const cashRatioEl = document.getElementById("cashRatio");
    const cashBarFillEl = document.getElementById("cashBarFill");
    const investedBarFillEl = document.getElementById("investedBarFill");

    const assetsTableBodyEl = document.getElementById("assetsTableBody");
    const assetsEmptyStateEl = document.getElementById("assetsEmptyState");
    const assetsSearchInputEl = document.getElementById("assetsSearchInput");
    const assetsFilterButtons = document.querySelectorAll(
      ".assets-quick-filter button"
    );

    const modeBuyBtn = document.getElementById("modeBuyBtn");
    const modeSellBtn = document.getElementById("modeSellBtn");
    const submitOrderBtn = document.getElementById("submitOrderBtn");
    const submitOrderLabelEl = document.getElementById("submitOrderLabel");

    const assetSymbolInputEl = document.getElementById("assetSymbolInput");
    const assetNameInputEl = document.getElementById("assetNameInput");
    const assetPriceInputEl = document.getElementById("assetPriceInput");
    const assetQuantityInputEl = document.getElementById("assetQuantityInput");
    const maxBuyHintEl = document.getElementById("maxBuyHint");
    const assetTypeTagEl = document.getElementById("assetTypeTag");
    const orderTypeLabelEl = document.getElementById("orderTypeLabel");
    const orderSummaryMainEl = document.getElementById("orderSummaryMain");
    const orderSummaryHintEl = document.getElementById("orderSummaryHint");

    const quickAmountButtons = document.querySelectorAll(
      ".quick-amount-buttons button"
    );

    const activityListEl = document.getElementById("activityList");
    const activityEmptyStateEl = document.getElementById("activityEmptyState");

    const resetPortfolioBtn = document.getElementById("resetPortfolioBtn");

    const chartCanvas = document.getElementById("portfolioChart");
    const chartRangeButtons = document.querySelectorAll(".chart-range-btn");

    let chartCtx = null;

    // Utility functions
    function formatMoney(value) {
      return "$" + value.toFixed(2);
    }

    function formatPercent(value) {
      const sign = value > 0 ? "+" : value < 0 ? "-" : "";
      return sign + Math.abs(value).toFixed(2) + "%";
    }

    function clamp(num, min, max) {
      return Math.min(Math.max(num, min), max);
    }

    function generateId() {
      return (
        Date.now().toString(36) + Math.random().toString(36).substring(2, 8)
      );
    }

    function getAssetBySymbol(symbol) {
      const normalized = symbol.trim().toUpperCase();
      return state.assets.find((a) => a.symbol === normalized) || null;
    }

    // Portfolio math
    function computePortfolio() {
      let investedCapital = 0;
      let currentValue = 0;
      let totalInvestedForPnL = 0;

      state.assets.forEach((asset) => {
        const value = asset.price * asset.quantity;
        const invested = asset.averagePrice * asset.quantity;
        investedCapital += invested;
        currentValue += value;
        totalInvestedForPnL += invested;
      });

      const totalPortfolioValue = state.cash + currentValue;
      const pnl = totalPortfolioValue - INITIAL_CASH;
      const pnlPercent =
        INITIAL_CASH === 0 ? 0 : (pnl / INITIAL_CASH) * 100;

      const unrealizedPnL = currentValue - totalInvestedForPnL;

      return {
        investedCapital,
        currentValue,
        totalPortfolioValue,
        pnl,
        pnlPercent,
        unrealizedPnL,
      };
    }

    function recordHistoryPoint() {
      const { totalPortfolioValue } = computePortfolio();
      state.history.push({
        value: totalPortfolioValue,
        timestamp: Date.now(),
      });
    }

    // Rendering functions
    function renderPortfolio() {
      const {
        investedCapital,
        totalPortfolioValue,
        pnl,
        pnlPercent,
        unrealizedPnL,
      } = computePortfolio();

      portfolioTotalEl.textContent = formatMoney(totalPortfolioValue);

      const changeClass =
        pnl >= 0 ? "portfolio-change-positive" : "portfolio-change-negative";
      document
        .getElementById("portfolioChange")
        .classList.remove("portfolio-change-positive", "portfolio-change-negative");
      document.getElementById("portfolioChange").classList.add(changeClass);

      portfolioChangeAmountEl.textContent = (pnl >= 0 ? "+" : "") + formatMoney(Math.abs(pnl));
      portfolioChangePercentEl.textContent = `(${formatPercent(pnlPercent)})`;

      investedCapitalEl.textContent = formatMoney(investedCapital);
      unrealizedPnLEl.textContent =
        (unrealizedPnL >= 0 ? "+" : "-") +
        formatMoney(Math.abs(unrealizedPnL));
      unrealizedPnLEl.style.color =
        unrealizedPnL >= 0 ? "var(--accent-green)" : "var(--accent-red)";
      assetCountEl.textContent = state.assets.length.toString();

      availableCashEl.textContent = formatMoney(state.cash);
      miniTotalPortfolioEl.textContent = formatMoney(totalPortfolioValue);
      miniTotalPnLEl.textContent =
        (pnl >= 0 ? "+" : "-") + formatMoney(Math.abs(pnl));
      miniTotalPnLEl.classList.toggle("positive", pnl >= 0);
      miniTotalPnLEl.classList.toggle("negative", pnl < 0);

      const cashRatio =
        totalPortfolioValue === 0
          ? 0
          : (state.cash / totalPortfolioValue) * 100;

      cashRatioEl.textContent = `${cashRatio.toFixed(0)}%`;

      const investedRatio =
        totalPortfolioValue === 0
          ? 0
          : investedCapital / totalPortfolioValue;

      const cashScale = clamp(state.cash / INITIAL_CASH, 0, 1);
      cashBarFillEl.style.transform = `scaleX(${cashScale})`;
      investedBarFillEl.style.transform = `scaleX(${clamp(investedRatio, 0, 1)})`;
      allocationBarFillEl.style.transform = `scaleX(${clamp(
        investedRatio,
        0,
        1
      )})`;

      const newState =
        pnl >= 0
          ? `Up ${formatPercent(pnlPercent)} from start`
          : `Down ${formatPercent(Math.abs(pnlPercent))} from start`;
      document.querySelector(".balance-status span").textContent = newState;

      renderAssetsTable();
      renderChart();
    }

    function renderAssetsTable() {
      const searchTerm = assetsSearchInputEl.value.trim().toLowerCase();
      const activeFilter = document.querySelector(
        ".assets-quick-filter button.active"
      ).dataset.filter;

      const { totalPortfolioValue } = computePortfolio();
      const cashHeavyThreshold = 0.7;

      let filteredAssets = state.assets.slice();

      if (searchTerm) {
        filteredAssets = filteredAssets.filter(
          (asset) =>
            asset.symbol.toLowerCase().includes(searchTerm) ||
            (asset.name || "").toLowerCase().includes(searchTerm)
        );
      }

      if (activeFilter === "gainers") {
        filteredAssets = filteredAssets.filter((asset) => {
          const diff = asset.price - asset.averagePrice;
          return diff > 0;
        });
      } else if (activeFilter === "losers") {
        filteredAssets = filteredAssets.filter((asset) => {
          const diff = asset.price - asset.averagePrice;
          return diff < 0;
        });
      } else if (activeFilter === "cash") {
        const cashShare =
          totalPortfolioValue === 0
            ? 1
            : state.cash / totalPortfolioValue;
        if (cashShare <= cashHeavyThreshold) {
          filteredAssets = [];
        }
      }

      assetsTableBodyEl.innerHTML = "";

      if (filteredAssets.length === 0) {
        assetsEmptyStateEl.classList.remove("hidden");
        return;
      } else {
        assetsEmptyStateEl.classList.add("hidden");
      }

      filteredAssets.forEach((asset) => {
        const tr = document.createElement("tr");

        const value = asset.price * asset.quantity;
        const invested = asset.averagePrice * asset.quantity;
        const diff = value - invested;
        const diffPercent = invested === 0 ? 0 : (diff / invested) * 100;

        const isGain = diff >= 0;

        const avatarText = asset.symbol.slice(0, 3).toUpperCase();

        tr.innerHTML = `
          <td>
            <div class="asset-name-cell">
              <div class="asset-avatar">${avatarText}</div>
              <div class="asset-name-labels">
                <div class="asset-symbol">${asset.symbol}</div>
                <div class="asset-name">${asset.name || "Custom asset"}</div>
              </div>
            </div>
          </td>
          <td>
            <div>${formatMoney(asset.price)}</div>
            <div class="asset-pill">
              <span class="asset-pill-dot ${
                isGain
                  ? diff === 0
                    ? ""
                    : "gain"
                  : "loss"
              }"></span>
              <span>${
                diff === 0 ? "Flat" : formatPercent(diffPercent)
              }</span>
            </div>
          </td>
          <td>${asset.quantity.toFixed(2)}</td>
          <td>${formatMoney(value)}</td>
          <td class="${
            diff === 0
              ? ""
              : isGain
              ? "asset-change-pos"
              : "asset-change-neg"
          }">
            ${(isGain ? "+" : "-") + formatMoney(Math.abs(diff))}
          </td>
          <td>
            <div class="asset-actions-cell">
              <button class="btn-mini" data-action="update-price" data-id="${
                asset.id
              }">Price</button>
              <button class="btn-mini primary" data-action="quick-trade" data-id="${
                asset.id
              }">Trade</button>
            </div>
          </td>
        `;

        assetsTableBodyEl.appendChild(tr);
      });
    }

    function renderActivity() {
      activityListEl.innerHTML = "";

      if (state.activity.length === 0) {
        activityEmptyStateEl.classList.remove("hidden");
        return;
      } else {
        activityEmptyStateEl.classList.add("hidden");
      }

      state.activity
        .slice()
        .reverse()
        .forEach((entry) => {
          const li = document.createElement("li");
          li.className = "activity-item";

          const typeLabel = entry.type.toUpperCase();
          const tagClass =
            entry.type === "buy" ? "activity-tag-buy" : "activity-tag-sell";

          li.innerHTML = `
            <div class="activity-item-header">
              <div class="activity-item-title">
                <span>${typeLabel}</span> ${entry.quantity.toFixed(
            2
          )} ${entry.symbol} at ${formatMoney(entry.price)}
              </div>
              <div class="activity-item-meta">
                <span class="${tagClass}">${typeLabel}</span>
                <span>•</span>
                <span>${new Date(entry.timestamp).toLocaleTimeString([], {
                  hour: "2-digit",
                  minute: "2-digit",
                })}</span>
              </div>
            </div>
            <div class="activity-item-footer">
              <span>Total: ${formatMoney(entry.total)}</span>
              <span>Cash after: ${formatMoney(entry.cashAfter)}</span>
            </div>
          `;

          activityListEl.appendChild(li);
        });
    }

    // Chart rendering
    function initChart() {
      if (!chartCanvas) return;
      chartCtx = chartCanvas.getContext("2d");
      resizeCanvas();
      renderChart();
      window.addEventListener("resize", () => {
        resizeCanvas();
        renderChart();
      });
    }

    function resizeCanvas() {
      const rect = chartCanvas.getBoundingClientRect();
      const dpr = window.devicePixelRatio || 1;
      chartCanvas.width = rect.width * dpr;
      chartCanvas.height = rect.height * dpr;
      chartCtx.scale(dpr, dpr);
    }

    function renderChart() {
      if (!chartCtx) return;

      const rect = chartCanvas.getBoundingClientRect();
      const width = rect.width;
      const height = rect.height;

      chartCtx.clearRect(0, 0, width, height);

      const points = state.history.length
        ? state.history
        : [{ value: INITIAL_CASH, timestamp: Date.now() }];

      const selectedRangeBtn = document.querySelector(
        ".chart-range-btn.active"
      );
      const rangeMode = selectedRangeBtn.dataset.range;

      let slice = points;
      if (rangeMode === "short" && points.length > 15) {
        slice = points.slice(points.length - 15);
      }

      const minValue = Math.min(...slice.map((p) => p.value), INITIAL_CASH * 0.6);
      const maxValue = Math.max(...slice.map((p) => p.value), INITIAL_CASH * 1.4);

      const paddingLeft = 10;
      const paddingRight = 10;
      const paddingTop = 10;
      const paddingBottom = 12;

      const innerWidth = width - paddingLeft - paddingRight;
      const innerHeight = height - paddingTop - paddingBottom;

      function mapX(index) {
        if (slice.length === 1) return paddingLeft + innerWidth / 2;
        return (
          paddingLeft +
          (index / (slice.length - 1)) * innerWidth
        );
      }

      function mapY(value) {
        const ratio =
          (value - minValue) / (maxValue - minValue || 1);
        return paddingTop + (1 - ratio) * innerHeight;
      }

      // Baseline for initial cash
      chartCtx.save();
      chartCtx.setLineDash([4, 4]);
      chartCtx.strokeStyle = "rgba(200, 206, 255, 0.3)";
      chartCtx.lineWidth = 1;
      chartCtx.beginPath();
      const baselineY = mapY(INITIAL_CASH);
      chartCtx.moveTo(paddingLeft, baselineY);
      chartCtx.lineTo(width - paddingRight, baselineY);
      chartCtx.stroke();
      chartCtx.restore();

      // Portfolio area & line
      chartCtx.beginPath();
      slice.forEach((point, index) => {
        const x = mapX(index);
        const y = mapY(point.value);
        if (index === 0) {
          chartCtx.moveTo(x, y);
        } else {
          chartCtx.lineTo(x, y);
        }
      });

      chartCtx.strokeStyle = "rgba(108, 160, 255, 1)";
      chartCtx.lineWidth = 1.6;
      chartCtx.stroke();

      // Area fill
      const gradient = chartCtx.createLinearGradient(
        0,
        paddingTop,
        0,
        height - paddingBottom
      );
      gradient.addColorStop(0, "rgba(79, 140, 255, 0.38)");
      gradient.addColorStop(1, "rgba(79, 140, 255, 0)");
      chartCtx.lineTo(
        paddingLeft + innerWidth,
        height - paddingBottom
      );
      chartCtx.lineTo(paddingLeft, height - paddingBottom);
      chartCtx.closePath();
      chartCtx.fillStyle = gradient;
      chartCtx.fill();

      // Last point marker
      const last = slice[slice.length - 1];
      const lastX = mapX(slice.length - 1);
      const lastY = mapY(last.value);

      chartCtx.beginPath();
      chartCtx.arc(lastX, lastY, 4, 0, Math.PI * 2);
      chartCtx.fillStyle = "#4f8cff";
      chartCtx.fill();

      chartCtx.beginPath();
      chartCtx.arc(lastX, lastY, 7, 0, Math.PI * 2);
      chartCtx.strokeStyle = "rgba(79, 140, 255, 0.4)";
      chartCtx.lineWidth = 1;
      chartCtx.stroke();

      // Small label for last value
      chartCtx.font = "10px system-ui";
      chartCtx.fillStyle = "rgba(214, 220, 255, 0.9)";
      chartCtx.textBaseline = "bottom";
      const labelText = formatMoney(last.value);
      chartCtx.fillText(labelText, lastX + 6, lastY - 4);
    }

    // Order logic
    function updateOrderSummary() {
      const symbolRaw = assetSymbolInputEl.value.trim();
      const symbol = symbolRaw.toUpperCase();
      const name = assetNameInputEl.value.trim();
      const price = parseFloat(assetPriceInputEl.value);
      const quantity = parseFloat(assetQuantityInputEl.value);

      const asset = symbol ? getAssetBySymbol(symbol) : null;
      const isExisting = !!asset;

      assetTypeTagEl.textContent = isExisting ? "Existing asset" : "New asset";

      const isBuy = state.mode === "buy";
      orderTypeLabelEl.textContent = isBuy ? "BUY" : "SELL";

      if (!symbol || !price || !quantity || quantity <= 0 || price <= 0) {
        orderSummaryMainEl.textContent = "Ready when you are.";
        orderSummaryHintEl.textContent =
          "Fill symbol, price, and quantity to see estimated impact.";
        return;
      }

      const total = price * quantity;
      const {
        totalPortfolioValue: beforeValue,
      } = computePortfolio();

      let afterCash = state.cash;
      let afterPortfolio = beforeValue;

      if (isBuy) {
        afterCash = state.cash - total;
        afterPortfolio = afterCash + beforeValue - state.cash;
      } else {
        afterCash = state.cash + total;
        afterPortfolio = afterCash + (beforeValue - state.cash);
      }

      const impactCash = afterCash - state.cash;
      const impactPortfolio = afterPortfolio - beforeValue;

      const cashDirection = impactCash >= 0 ? "increase" : "decrease";
      const portfolioDirection =
        impactPortfolio >= 0 ? "gain" : "drop";

      orderSummaryMainEl.textContent = `${isBuy ? "Spend" : "Receive"} ${formatMoney(
        total
      )} • Cash ${
        cashDirection
      }s to ${formatMoney(afterCash)} • Estimated ${portfolioDirection} ${
        isBuy ? "not guaranteed" : "depends on position"
      }`;

      if (isBuy) {
        if (total > state.cash) {
          orderSummaryHintEl.textContent =
            "You don't have enough virtual cash for this order.";
        } else {
          orderSummaryHintEl.textContent =
            "If markets were live, this is how much cash you would use for this buy.";
        }
      } else {
        if (!asset || asset.quantity < quantity) {
          orderSummaryHintEl.textContent =
            "You don't hold enough units to sell this quantity.";
        } else {
          orderSummaryHintEl.textContent =
            "This is a simulated exit from part of your position.";
        }
      }
    }

    function updateMaxHints() {
      const price = parseFloat(assetPriceInputEl.value);
      if (!price || price <= 0) {
        maxBuyHintEl.textContent = "0.00";
        return;
      }

      const maxBuyUnits = state.cash / price;
      maxBuyHintEl.textContent = maxBuyUnits.toFixed(2);
    }

    function applyQuickAmount(multiplier) {
      const isBuy = state.mode === "buy";
      const price = parseFloat(assetPriceInputEl.value);

      if (!price || price <= 0) return;

      if (isBuy) {
        const affordableUnits = state.cash / price;
        const targetUnits = affordableUnits * multiplier;
        assetQuantityInputEl.value = targetUnits.toFixed(2);
      } else {
        const symbol = assetSymbolInputEl.value.trim().toUpperCase();
        const asset = getAssetBySymbol(symbol);
        if (!asset) return;
        const targetUnits = asset.quantity * multiplier;
        assetQuantityInputEl.value = targetUnits.toFixed(2);
      }

      updateOrderSummary();
    }

    function submitOrder() {
      const symbolRaw = assetSymbolInputEl.value.trim();
      const symbol = symbolRaw.toUpperCase();
      const name = assetNameInputEl.value.trim();
      const price = parseFloat(assetPriceInputEl.value);
      const quantity = parseFloat(assetQuantityInputEl.value);
      const isBuy = state.mode === "buy";

      if (!symbol || !price || !quantity || quantity <= 0 || price <= 0) {
        alert("Please provide a valid symbol, price, and quantity.");
        return;
      }

      let asset = getAssetBySymbol(symbol);
      const isExisting = !!asset;

      if (!isExisting && !name) {
        alert(
          "You're creating a new asset. Please give it a short, descriptive name."
        );
        return;
      }

      if (!isBuy && (!asset || asset.quantity < quantity)) {
        alert("You don't hold enough units to sell this amount.");
        return;
      }

      const total = price * quantity;

      if (isBuy && total > state.cash) {
        alert("Not enough virtual cash for this buy order.");
        return;
      }

      if (!asset) {
        asset = {
          id: generateId(),
          symbol,
          name: name || symbol,
          price,
          quantity: 0,
          invested: 0,
          averagePrice: 0,
        };
        state.assets.push(asset);
      } else {
        if (name) {
          asset.name = name;
        }
      }

      if (isBuy) {
        const previousInvested = asset.invested;
        const additionalInvested = total;
        const newInvested = previousInvested + additionalInvested;
        const newQuantity = asset.quantity + quantity;
        const newAverage =
          newQuantity === 0 ? 0 : newInvested / newQuantity;

        asset.invested = newInvested;
        asset.quantity = newQuantity;
        asset.averagePrice = newAverage;
        asset.price = price;

        state.cash -= total;
      } else {
        const fractionSold =
          asset.quantity === 0 ? 0 : quantity / asset.quantity;
        const investedReduction = asset.invested * fractionSold;

        asset.quantity -= quantity;
        asset.invested -= investedReduction;
        asset.price = price;

        state.cash += total;

        if (asset.quantity <= 0.0001) {
          state.assets = state.assets.filter((a) => a.id !== asset.id);
        }
      }

      state.activity.push({
        id: generateId(),
        type: isBuy ? "buy" : "sell",
        symbol,
        name: asset.name,
        price,
        quantity,
        total,
        cashAfter: state.cash,
        timestamp: Date.now(),
      });

      recordHistoryPoint();
      renderPortfolio();
      renderActivity();
      updateMaxHints();
      updateOrderSummary();

      assetQuantityInputEl.value = "";
      if (!isExisting) {
        assetNameInputEl.value = "";
      }
    }

    function resetPortfolio() {
      if (
        !confirm(
          "Reset everything back to $100 and clear all assets and history?"
        )
      ) {
        return;
      }

      state.cash = INITIAL_CASH;
      state.assets = [];
      state.history = [];
      state.activity = [];
      recordHistoryPoint();
      renderPortfolio();
      renderActivity();
      updateMaxHints();
      updateOrderSummary();
    }

    // Event listeners
    assetsSearchInputEl.addEventListener("input", () => {
      renderAssetsTable();
    });

    assetsFilterButtons.forEach((btn) => {
      btn.addEventListener("click", () => {
        assetsFilterButtons.forEach((b) => b.classList.remove("active"));
        btn.classList.add("active");
        renderAssetsTable();
      });
    });

    modeBuyBtn.addEventListener("click", () => {
      state.mode = "buy";
      modeBuyBtn.classList.add("active");
      modeSellBtn.classList.remove("active");
      submitOrderLabelEl.textContent = "PLACE BUY ORDER";
      updateMaxHints();
      updateOrderSummary();
    });

    modeSellBtn.addEventListener("click", () => {
      state.mode = "sell";
      modeSellBtn.classList.add("active");
      modeBuyBtn.classList.remove("active");
      submitOrderLabelEl.textContent = "PLACE SELL ORDER";
      updateMaxHints();
      updateOrderSummary();
    });

    [
      assetSymbolInputEl,
      assetNameInputEl,
      assetPriceInputEl,
      assetQuantityInputEl,
    ].forEach((el) => {
      el.addEventListener("input", () => {
        updateMaxHints();
        updateOrderSummary();
      });
    });

    quickAmountButtons.forEach((btn) => {
      btn.addEventListener("click", () => {
        const multiplier = parseFloat(btn.dataset.quick);
        applyQuickAmount(multiplier);
      });
    });

    submitOrderBtn.addEventListener("click", () => {
      submitOrder();
    });

    assetsTableBodyEl.addEventListener("click", (event) => {
      const target = event.target;
      if (!(target instanceof HTMLElement)) return;

      const action = target.dataset.action;
      const id = target.dataset.id;
      if (!action || !id) return;

      const asset = state.assets.find((a) => a.id === id);
      if (!asset) return;

      if (action === "update-price") {
        const newPriceStr = prompt(
          `Update price for ${asset.symbol} (current ${formatMoney(
            asset.price
          )}):`,
          asset.price.toFixed(2)
        );
        if (!newPriceStr) return;
        const newPrice = parseFloat(newPriceStr);
        if (!newPrice || newPrice <= 0) {
          alert("Please enter a valid positive price.");
          return;
        }
        asset.price = newPrice;
        recordHistoryPoint();
        renderPortfolio();
        updateOrderSummary();
      } else if (action === "quick-trade") {
        assetSymbolInputEl.value = asset.symbol;
        assetNameInputEl.value = asset.name;
        assetPriceInputEl.value = asset.price.toFixed(2);
        assetQuantityInputEl.value = "";
        state.mode = "buy";
        modeBuyBtn.classList.add("active");
        modeSellBtn.classList.remove("active");
        submitOrderLabelEl.textContent = "PLACE BUY ORDER";
        updateMaxHints();
        updateOrderSummary();
      }
    });

    resetPortfolioBtn.addEventListener("click", resetPortfolio);

    chartRangeButtons.forEach((btn) => {
      btn.addEventListener("click", () => {
        chartRangeButtons.forEach((b) => b.classList.remove("active"));
        btn.classList.add("active");
        renderChart();
      });
    });

    // Initial setup
    (function init() {
      recordHistoryPoint();
      renderPortfolio();
      renderActivity();
      updateMaxHints();
      updateOrderSummary();
      initChart();
    })();
  </script>
</body>
</html>
