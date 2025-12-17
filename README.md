<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>NovaTrade – Online Trading Platform</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <style>
    :root {
      --bg-dark: #060b10;
      --bg-card: #0d151f;
      --bg-card-alt: #101927;
      --accent: #1ecc7c;
      --accent-soft: rgba(30, 204, 124, 0.15);
      --danger: #ff5c5c;
      --text-main: #f5f7fb;
      --text-muted: #8a94a7;
      --border-soft: #1a2535;
      --shadow-soft: 0 20px 50px rgba(0, 0, 0, 0.55);
      --radius-lg: 16px;
      --radius-md: 10px;
      --radius-pill: 999px;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
      background: radial-gradient(circle at top, #182a40 0, #060b10 50%, #020408 100%);
      color: var(--text-main);
      min-height: 100vh;
    }

    a {
      color: inherit;
      text-decoration: none;
    }

    img {
      max-width: 100%;
      display: block;
    }

    .page {
      max-width: 1200px;
      margin: 0 auto;
      padding: 20px 18px 60px;
    }

    header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 24px;
      gap: 16px;
    }

    .logo {
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .logo-icon {
      width: 32px;
      height: 32px;
      border-radius: 10px;
      background: conic-gradient(from 120deg, #1ecc7c, #27a3e4, #7a5cff, #1ecc7c);
      position: relative;
      box-shadow: 0 0 18px rgba(30, 204, 124, 0.6);
    }

    .logo-icon::after {
      content: "";
      position: absolute;
      inset: 4px;
      border-radius: inherit;
      background:
        radial-gradient(circle at 30% 20%, rgba(255, 255, 255, 0.2), transparent 60%),
        radial-gradient(circle at 80% 80%, rgba(0, 0, 0, 0.8), #050910);
    }

    .logo-text {
      display: flex;
      flex-direction: column;
      line-height: 1.1;
    }

    .logo-text span:first-child {
      font-weight: 700;
      letter-spacing: 0.05em;
      font-size: 18px;
    }

    .logo-text span:last-child {
      font-size: 11px;
      color: var(--text-muted);
      text-transform: uppercase;
    }

    nav {
      display: flex;
      align-items: center;
      gap: 18px;
      font-size: 14px;
    }

    .nav-links {
      display: flex;
      gap: 14px;
      color: var(--text-muted);
    }

    .nav-links a {
      padding: 6px 8px;
      border-radius: 999px;
      transition: color 0.2s ease, background 0.2s ease;
    }

    .nav-links a:hover {
      color: var(--text-main);
      background: rgba(255, 255, 255, 0.04);
    }

    .nav-links a.active {
      color: var(--accent);
      background: var(--accent-soft);
    }

    .nav-cta {
      display: flex;
      gap: 10px;
      align-items: center;
    }

    .btn {
      border-radius: var(--radius-pill);
      padding: 8px 16px;
      font-size: 13px;
      border: 1px solid transparent;
      cursor: pointer;
      background: transparent;
      color: var(--text-main);
      transition: background 0.2s ease, border 0.2s ease, transform 0.1s ease,
        box-shadow 0.1s ease;
      display: inline-flex;
      align-items: center;
      gap: 6px;
      text-decoration: none;
    }

    .btn-ghost {
      border-color: var(--border-soft);
      color: var(--text-muted);
    }

    .btn-ghost:hover {
      background: rgba(255, 255, 255, 0.03);
      color: var(--text-main);
    }

    .btn-primary {
      background: linear-gradient(135deg, #22d38a, #11b16b);
      border-color: transparent;
      box-shadow: 0 0 18px rgba(30, 204, 124, 0.65);
      font-weight: 600;
    }

    .btn-primary:hover {
      transform: translateY(-1px);
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.8);
    }

    .btn-small {
      padding: 6px 12px;
      font-size: 12px;
    }

    .btn-text {
      border: none;
      background: none;
      color: var(--text-muted);
      font-size: 12px;
      cursor: pointer;
    }

    .btn-text:hover {
      color: var(--text-main);
    }

    .main-grid {
      display: grid;
      grid-template-columns: 1.35fr 1fr;
      gap: 24px;
      align-items: flex-start;
    }

    .hero-card {
      background:
        radial-gradient(circle at top left, rgba(30, 204, 124, 0.1), transparent),
        linear-gradient(135deg, rgba(17, 25, 39, 0.98), rgba(7, 11, 18, 0.98));
      border-radius: var(--radius-lg);
      padding: 20px 20px 18px;
      box-shadow: var(--shadow-soft);
      border: 1px solid rgba(255, 255, 255, 0.03);
    }

    .hero-header {
      display: flex;
      justify-content: space-between;
      gap: 12px;
      margin-bottom: 18px;
    }

    .hero-title {
      max-width: 360px;
    }

    .hero-title-badge {
      font-size: 11px;
      letter-spacing: 0.08em;
      text-transform: uppercase;
      color: var(--accent);
      background: rgba(30, 204, 124, 0.12);
      border-radius: var(--radius-pill);
      padding: 4px 10px;
      display: inline-flex;
      align-items: center;
      gap: 6px;
      margin-bottom: 8px;
      border: 1px solid rgba(30, 204, 124, 0.25);
    }

    .hero-title-badge-dot {
      width: 6px;
      height: 6px;
      border-radius: 50%;
      background: var(--accent);
      box-shadow: 0 0 10px rgba(30, 204, 124, 0.9);
    }

    .hero-title h1 {
      font-size: 26px;
      margin-bottom: 6px;
    }

    .hero-title p {
      font-size: 13px;
      color: var(--text-muted);
    }

    .hero-kpis {
      display: grid;
      grid-auto-flow: column;
      gap: 10px;
      font-size: 12px;
    }

    .kpi {
      background: rgba(3, 8, 15, 0.8);
      border-radius: var(--radius-md);
      border: 1px solid rgba(255, 255, 255, 0.04);
      padding: 8px 10px;
      min-width: 120px;
    }

    .kpi-label {
      color: var(--text-muted);
      margin-bottom: 4px;
      font-size: 11px;
    }

    .kpi-value {
      font-size: 13px;
      font-weight: 600;
    }

    .kpi-trend {
      font-size: 11px;
      color: var(--accent);
    }

    .kpi-trend.negative {
      color: var(--danger);
    }

    .chart-card {
      margin-top: 10px;
      background: linear-gradient(180deg, #050912, #020307);
      border-radius: var(--radius-md);
      padding: 14px 14px 12px;
      border: 1px solid #171f2a;
      position: relative;
      overflow: hidden;
    }

    .chart-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 12px;
      font-size: 12px;
    }

    .asset-name {
      font-weight: 600;
    }

    .asset-symbol {
      color: var(--text-muted);
      font-size: 11px;
    }

    .asset-price {
      font-weight: 600;
      font-size: 14px;
    }

    .asset-price-change {
      font-size: 11px;
      color: var(--accent);
      background: rgba(30, 204, 124, 0.1);
      padding: 2px 8px;
      border-radius: var(--radius-pill);
      margin-left: 6px;
    }

    .asset-price-change.negative {
      color: var(--danger);
      background: rgba(255, 92, 92, 0.12);
    }

    .chart-timeframe {
      display: flex;
      gap: 6px;
      font-size: 11px;
    }

    .chart-timeframe button {
      border-radius: 999px;
      border: 1px solid transparent;
      background: transparent;
      color: var(--text-muted);
      padding: 4px 8px;
      cursor: pointer;
      font-size: inherit;
      transition: 0.15s ease background, 0.15s ease color, 0.15s ease border;
    }

    .chart-timeframe button.active {
      background: rgba(30, 204, 124, 0.14);
      color: var(--accent);
      border-color: rgba(30, 204, 124, 0.65);
    }

    .chart-timeframe button:hover {
      color: var(--text-main);
      background: rgba(255, 255, 255, 0.03);
    }

    .chart-body {
      position: relative;
      height: 190px;
    }

    .chart-grid {
      position: absolute;
      inset: 0;
      background-image:
        linear-gradient(to right, rgba(255, 255, 255, 0.04) 1px, transparent 1px),
        linear-gradient(to top, rgba(255, 255, 255, 0.04) 1px, transparent 1px);
      background-size: 42px 42px;
      opacity: 0.4;
    }

    .chart-line {
      position: absolute;
      inset: 18px 6px 16px;
      border-radius: 30px;
      border: 2px solid transparent;
      background:
        linear-gradient(120deg, rgba(30, 204, 124, 0.1), transparent 40% 70%, rgba(255, 92, 92, 0.08)) border-box,
        radial-gradient(circle at 15% 20%, rgba(255, 255, 255, 0.25), transparent 50%),
        radial-gradient(circle at 55% 70%, rgba(30, 204, 124, 0.55), transparent 50%),
        radial-gradient(circle at 90% 15%, rgba(255, 92, 92, 0.6), transparent 50%);
      opacity: 0.97;
    }

    .chart-glow {
      position: absolute;
      inset: 70px 0 0;
      background: radial-gradient(circle at 50% 0, rgba(30, 204, 124, 0.35), transparent 68%);
      opacity: 0.32;
      pointer-events: none;
    }

    .chart-footer {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding-top: 10px;
      border-top: 1px solid rgba(17, 24, 38, 0.8);
      margin-top: 8px;
      font-size: 11px;
      color: var(--text-muted);
    }

    .chart-legend {
      display: flex;
      gap: 12px;
    }

    .legend-item {
      display: flex;
      align-items: center;
      gap: 4px;
    }

    .dot-buy,
    .dot-sell {
      width: 8px;
      height: 8px;
      border-radius: 50%;
    }

    .dot-buy {
      background: var(--accent);
    }

    .dot-sell {
      background: var(--danger);
    }

    .side-column {
      display: flex;
      flex-direction: column;
      gap: 14px;
    }

    .side-card {
      background: linear-gradient(145deg, #050a11, #090f18);
      border-radius: var(--radius-lg);
      padding: 16px 14px 14px;
      border: 1px solid rgba(255, 255, 255, 0.03);
      box-shadow: 0 16px 40px rgba(0, 0, 0, 0.7);
      font-size: 13px;
    }

    .side-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 10px;
    }

    .side-header h2 {
      font-size: 15px;
    }

    .side-header span {
      font-size: 11px;
      color: var(--text-muted);
    }

    .markets-list {
      margin-top: 4px;
      border-radius: 12px;
      border: 1px solid rgba(255, 255, 255, 0.04);
      overflow: hidden;
    }

    .market-row {
      display: grid;
      grid-template-columns: 1.5fr 1fr 0.9fr 0.8fr;
      align-items: center;
      padding: 8px 10px;
      background: rgba(7, 11, 20, 0.9);
      border-bottom: 1px solid rgba(15, 23, 37, 0.9);
    }

    .market-row:nth-child(even) {
      background: rgba(4, 8, 15, 0.92);
    }

    .market-row:last-child {
      border-bottom: none;
    }

    .market-name {
      display: flex;
      flex-direction: column;
      gap: 2px;
    }

    .market-symbol {
      font-size: 11px;
      color: var(--text-muted);
    }

    .market-spread {
      font-size: 11px;
      color: var(--text-muted);
    }

    .market-change.positive {
      color: var(--accent);
    }

    .market-change.negative {
      color: var(--danger);
    }

    .market-actions {
      display: flex;
      gap: 6px;
      justify-content: flex-end;
    }

    .btn-buy,
    .btn-sell {
      font-size: 11px;
      padding: 4px 8px;
      border-radius: var(--radius-pill);
      border: none;
      cursor: pointer;
      color: #fff;
    }

    .btn-buy {
      background: linear-gradient(135deg, #25d586, #16b16b);
    }

    .btn-sell {
      background: linear-gradient(135deg, #ff6b6b, #ff3b3b);
      opacity: 0.4;
      cursor: not-allowed;
    }

    .balance-row {
      display: flex;
      justify-content: space-between;
      margin-bottom: 6px;
    }

    .balance-row span:first-child {
      color: var(--text-muted);
      font-size: 12px;
    }

    .balance-row span:last-child {
      font-weight: 500;
      font-size: 13px;
    }

    .progress-wrap {
      margin: 10px 0 6px;
    }

    .progress-label {
      display: flex;
      justify-content: space-between;
      font-size: 11px;
      color: var(--text-muted);
      margin-bottom: 4px;
    }

    .progress-bar {
      width: 100%;
      height: 7px;
      border-radius: 99px;
      background: #050910;
      overflow: hidden;
      border: 1px solid #151d2a;
    }

    .progress-fill {
      height: 100%;
      width: 0%;
      border-radius: inherit;
      background: linear-gradient(90deg, #1ecc7c, #27a3e4);
      box-shadow: 0 0 12px rgba(30, 204, 124, 0.75);
      transition: width 0.2s ease;
    }

    .small-pill {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      border-radius: 999px;
      padding: 3px 9px;
      font-size: 11px;
      background: rgba(9, 16, 26, 0.96);
      border: 1px solid rgba(255, 255, 255, 0.06);
      color: var(--text-muted);
      margin-top: 4px;
    }

    .small-pill strong {
      color: var(--accent);
      font-weight: 600;
      font-size: 11px;
    }

    .account-footer {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-top: 10px;
      border-top: 1px dashed rgba(255, 255, 255, 0.06);
      padding-top: 8px;
      font-size: 11px;
      color: var(--text-muted);
    }

    .risk-status {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      border-radius: 999px;
      padding: 3px 8px;
      background: rgba(4, 12, 24, 0.95);
      border: 1px solid rgba(255, 255, 255, 0.04);
    }

    .risk-dot {
      width: 7px;
      height: 7px;
      border-radius: 50%;
      background: #ffb020;
      box-shadow: 0 0 10px rgba(255, 176, 32, 0.7);
    }

    .ticker {
      margin-top: 18px;
      background: linear-gradient(90deg, #050910, #081120);
      border-radius: var(--radius-pill);
      border: 1px solid rgba(255, 255, 255, 0.05);
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.7);
      padding: 6px 12px;
      font-size: 12px;
      display: flex;
      align-items: center;
      gap: 14px;
      overflow: hidden;
      position: relative;
    }

    .ticker-label {
      text-transform: uppercase;
      letter-spacing: 0.1em;
      font-size: 10px;
      color: var(--text-muted);
      border-right: 1px solid rgba(255, 255, 255, 0.06);
      padding-right: 10px;
    }

    .ticker-track {
      display: flex;
      gap: 20px;
      animation: ticker-scroll 22s linear infinite;
      white-space: nowrap;
    }

    .ticker-item {
      display: inline-flex;
      gap: 6px;
      align-items: baseline;
    }

    .ticker-symbol {
      font-size: 11px;
      color: var(--text-muted);
    }

    .ticker-price {
      font-size: 12px;
      font-weight: 500;
    }

    .ticker-change {
      font-size: 11px;
    }

    .ticker-change.positive {
      color: var(--accent);
    }

    .ticker-change.negative {
      color: var(--danger);
    }

    @keyframes ticker-scroll {
      0% {
        transform: translateX(0);
      }
      100% {
        transform: translateX(-50%);
      }
    }

    footer {
      max-width: 1200px;
      margin: 24px auto 0;
      padding: 0 18px;
      font-size: 11px;
      color: var(--text-muted);
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      justify-content: space-between;
    }

    footer span {
      opacity: 0.85;
    }

    /* Auth modal */

    .backdrop {
      position: fixed;
      inset: 0;
      background: rgba(0, 0, 0, 0.65);
      display: none;
      align-items: center;
      justify-content: center;
      z-index: 20;
    }

    .backdrop.show {
      display: flex;
    }

    .modal {
      background: #050910;
      border-radius: 18px;
      padding: 18px 18px 16px;
      width: 92%;
      max-width: 360px;
      border: 1px solid rgba(255, 255, 255, 0.08);
      box-shadow: 0 18px 40px rgba(0, 0, 0, 0.8);
      position: relative;
    }

    .modal-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 10px;
    }

    .modal-header h2 {
      font-size: 18px;
    }

    .modal-toggle {
      display: flex;
      gap: 4px;
      background: #070d18;
      border-radius: 999px;
      padding: 2px;
      border: 1px solid rgba(255, 255, 255, 0.06);
      font-size: 11px;
    }

    .modal-toggle button {
      flex: 1;
      border-radius: 999px;
      border: none;
      background: transparent;
      color: var(--text-muted);
      padding: 4px 8px;
      cursor: pointer;
    }

    .modal-toggle button.active {
      background: linear-gradient(135deg, #22d38a, #11b16b);
      color: #fff;
    }

    .modal-close {
      border-radius: 50%;
      border: 1px solid rgba(255, 255, 255, 0.1);
      background: transparent;
      width: 22px;
      height: 22px;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      color: var(--text-muted);
      font-size: 13px;
    }

    .modal-field {
      margin-bottom: 8px;
      display: flex;
      flex-direction: column;
      gap: 3px;
    }

    .modal-field label {
      font-size: 12px;
      color: var(--text-muted);
    }

    .modal-field input {
      border-radius: 999px;
      border: 1px solid rgba(255, 255, 255, 0.08);
      background: #060b14;
      padding: 7px 10px;
      font-size: 13px;
      color: var(--text-main);
      outline: none;
    }

    .modal-field input:focus {
      border-color: rgba(30, 204, 124, 0.8);
      box-shadow: 0 0 0 1px rgba(30, 204, 124, 0.5);
    }

    .modal-footer {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-top: 10px;
      font-size: 11px;
      color: var(--text-muted);
    }

    .modal-error {
      font-size: 11px;
      color: var(--danger);
      min-height: 14px;
      margin-top: 4px;
    }

    /* Trade modal */

    .trade-modal .modal {
      max-width: 380px;
    }

    .trade-asset {
      font-size: 13px;
      color: var(--text-muted);
      margin-bottom: 4px;
    }

    .trade-asset strong {
      color: var(--text-main);
    }

    .trade-row {
      display: flex;
      justify-content: space-between;
      font-size: 12px;
      margin-bottom: 6px;
      color: var(--text-muted);
    }

    .trade-row span:last-child {
      color: var(--text-main);
    }

    .trade-qty-input {
      display: flex;
      align-items: center;
      gap: 6px;
      margin: 8px 0 6px;
    }

    .trade-qty-input input {
      width: 80px;
      border-radius: 999px;
      border: 1px solid rgba(255, 255, 255, 0.08);
      background: #060b14;
      padding: 6px 8px;
      font-size: 13px;
      color: var(--text-main);
      outline: none;
    }

    .trade-qty-input button {
      border-radius: 999px;
      border: none;
      background: rgba(255, 255, 255, 0.06);
      color: var(--text-main);
      padding: 3px 8px;
      font-size: 11px;
      cursor: pointer;
    }

    .trade-info {
      font-size: 11px;
      color: var(--text-muted);
      margin-bottom: 6px;
    }

    .trade-summary {
      font-size: 12px;
      margin: 6px 0;
    }

    .trade-summary span {
      color: var(--accent);
      font-weight: 500;
    }

    .trade-error {
      font-size: 11px;
      color: var(--danger);
      min-height: 14px;
      margin-top: 4px;
    }

    /* Positions */

    .positions-list {
      margin-top: 8px;
      border-radius: 10px;
      border: 1px solid rgba(255, 255, 255, 0.04);
      overflow: hidden;
      font-size: 11px;
    }

    .position-row {
      display: grid;
      grid-template-columns: 1.7fr 0.8fr 0.9fr 0.7fr;
      padding: 6px 8px;
      background: rgba(4, 10, 18, 0.96);
      border-bottom: 1px solid rgba(11, 18, 30, 0.9);
    }

    .position-row:nth-child(even) {
      background: rgba(6, 10, 20, 0.96);
    }

    .position-row:last-child {
      border-bottom: none;
    }

    .position-symbol {
      font-size: 11px;
      color: var(--text-muted);
    }

    .position-empty {
      padding: 6px 8px;
      color: var(--text-muted);
      font-size: 11px;
    }

    /* Auth hint badge */

    .auth-hint {
      font-size: 11px;
      color: var(--text-muted);
    }

    .auth-hint span {
      color: var(--accent);
      font-weight: 500;
    }

    /* Responsive */

    @media (max-width: 900px) {
      .main-grid {
        grid-template-columns: 1fr;
      }

      .side-column {
        order: -1;
      }

      header {
        flex-wrap: wrap;
        align-items: flex-start;
      }

      nav {
        width: 100%;
        justify-content: flex-end;
        flex-wrap: wrap;
      }

      .hero-card {
        padding: 18px 14px;
      }

      .hero-header {
        flex-direction: column;
      }
    }

    @media (max-width: 640px) {
      header {
        flex-direction: column;
        align-items: flex-start;
      }

      nav {
        flex-direction: column;
        align-items: flex-start;
        gap: 10px;
      }

      .nav-cta {
        width: 100%;
      }

      .nav-cta a,
      .nav-cta button {
        flex: 1;
        justify-content: center;
      }

      .market-row {
        grid-template-columns: 1.6fr 1fr 0.8fr;
      }

      .market-actions {
        display: none;
      }

      .positions-list {
        font-size: 10px;
      }

      .position-row {
        grid-template-columns: 1.6fr 0.7fr 0.8fr 0.7fr;
      }
    }
  </style>
</head>
<body>
  <div class="page">
    <!-- HEADER -->
    <header>
      <div class="logo">
        <div class="logo-icon"></div>
        <div class="logo-text">
          <span>NovaTrade</span>
          <span>Invest · Trade · Grow</span>
        </div>
      </div>

      <nav>
        <div class="nav-links">
          <a href="#" class="active">Trading</a>
          <a href="#">Markets</a>
          <a href="#">Pricing</a>
          <a href="#">Education</a>
        </div>
        <div class="nav-cta">
          <span id="navUser" class="auth-hint"></span>
          <button id="btnLogin" class="btn btn-ghost">Log in / Sign up</button>
          <button id="btnLogout" class="btn btn-text" style="display:none;">Log out</button>
        </div>
      </nav>
    </header>

    <!-- MAIN CONTENT -->
    <main class="main-grid">
      <!-- LEFT: HERO & CHART -->
      <section class="hero-card">
        <div class="hero-header">
          <div class="hero-title">
            <div class="hero-title-badge">
              <span class="hero-title-badge-dot"></span>
              Zero-commission demo · Real-time prices
            </div>
            <h1>Trade global markets with a clean, simple interface.</h1>
            <p>
              Practice on a free demo account and explore CFDs on stocks, forex, indices, and crypto on one modern web
              platform.
            </p>
          </div>

          <div class="hero-kpis">
            <div class="kpi">
              <div class="kpi-label">Demo balance</div>
              <div class="kpi-value" id="kpiBalance">$50,000.00</div>
              <div class="kpi-trend" id="kpiToday">+ $0.00 today</div>
            </div>
            <div class="kpi">
              <div class="kpi-label">Open P&L</div>
              <div class="kpi-value" id="kpiPnL">$0.00</div>
              <div class="kpi-trend negative" id="kpiOvernight">– $0.00 overnight</div>
            </div>
          </div>
        </div>

        <article class="chart-card">
          <div class="chart-header">
            <div>
              <div class="asset-name">US Tech 100</div>
              <div class="asset-symbol">NAS100 · Index CFD</div>
            </div>
            <div>
              <span class="asset-price" id="assetPrice">18,245.12</span>
              <span class="asset-price-change" id="assetChange">+0.86% (day)</span>
            </div>
          </div>

          <div class="chart-timeframe">
            <button class="active">1D</button>
            <button>1W</button>
            <button>1M</button>
            <button>6M</button>
            <button>1Y</button>
          </div>

          <div class="chart-body">
            <div class="chart-grid"></div>
            <div class="chart-line"></div>
            <div class="chart-glow"></div>
          </div>

          <div class="chart-footer">
            <div class="chart-legend">
              <div class="legend-item">
                <span class="dot-buy"></span>
                <span>Buy</span>
              </div>
              <div class="legend-item">
                <span class="dot-sell"></span>
                <span>Sell</span>
              </div>
            </div>
            <div>Spread from 0.7 pts · Leverage up to 1:30</div>
          </div>
        </article>
      </section>

      <!-- RIGHT: MARKETS & ACCOUNT -->
      <aside class="side-column">
        <!-- Markets -->
        <section class="side-card">
          <div class="side-header">
            <div>
              <h2>Popular markets</h2>
              <span>Tap buy to open a position</span>
            </div>
            <a href="#" style="font-size: 11px; color: var(--accent);">View all</a>
          </div>

          <div class="markets-list" id="marketsList">
            <!-- Market rows generated by JS -->
          </div>
        </section>

        <!-- Account summary -->
        <section class="side-card">
          <div class="side-header">
            <div>
              <h2>Account overview</h2>
              <span id="accountTypeLabel">Guest · Demo preview</span>
            </div>
          </div>

          <div class="balance-row">
            <span>Equity</span>
            <span id="equityValue">$0.00</span>
          </div>
          <div class="balance-row">
            <span>Available margin</span>
            <span id="availableMarginValue">$0.00</span>
          </div>
          <div class="balance-row">
            <span>Used margin</span>
            <span id="usedMarginValue">$0.00</span>
          </div>

          <div class="progress-wrap">
            <div class="progress-label">
              <span>Risk usage</span>
              <span id="riskUsageLabel">0%</span>
            </div>
            <div class="progress-bar">
              <div class="progress-fill" id="riskUsageFill"></div>
            </div>
          </div>

          <div class="small-pill">
            <span>Leverage</span>
            <strong id="avgLeverage">1 : 0</strong>
            <span>Avg. on open trades</span>
          </div>

          <div class="account-footer">
            <div class="risk-status" id="riskStatus">
              <span class="risk-dot"></span>
              <span id="riskStatusText">No open positions</span>
            </div>
            <button class="btn-text" id="manageFundsBtn">Manage funds</button>
          </div>

          <!-- Positions -->
          <h3 style="font-size: 12px; margin-top: 10px; color: var(--text-muted);">
            Open positions
          </h3>
          <div class="positions-list" id="positionsList">
            <div class="position-empty">No open positions. Buy a market to get started.</div>
          </div>
        </section>
      </aside>
    </main>

    <!-- TICKER -->
    <section class="ticker">
      <span class="ticker-label">Live snapshot</span>
      <div class="ticker-track">
        <div class="ticker-item">
          <span class="ticker-symbol">DAX40</span>
          <span class="ticker-price">18,950.4</span>
          <span class="ticker-change positive">+0.55%</span>
        </div>
        <div class="ticker-item">
          <span class="ticker-symbol">GBP / USD</span>
          <span class="ticker-price">1.2741</span>
          <span class="ticker-change negative">–0.18%</span>
        </div>
        <div class="ticker-item">
          <span class="ticker-symbol">TSLA</span>
          <span class="ticker-price">241.32</span>
          <span class="ticker-change positive">+1.02%</span>
        </div>
        <div class="ticker-item">
          <span class="ticker-symbol">OIL</span>
          <span class="ticker-price">81.42</span>
          <span class="ticker-change negative">–0.41%</span>
        </div>
        <div class="ticker-item">
          <span class="ticker-symbol">NIKKEI</span>
          <span class="ticker-price">39,210.6</span>
          <span class="ticker-change positive">+0.77%</span>
        </div>
        <!-- Duplicate for smooth scroll -->
        <div class="ticker-item">
          <span class="ticker-symbol">DAX40</span>
          <span class="ticker-price">18,950.4</span>
          <span class="ticker-change positive">+0.55%</span>
        </div>
        <div class="ticker-item">
          <span class="ticker-symbol">GBP / USD</span>
          <span class="ticker-price">1.2741</span>
          <span class="ticker-change negative">–0.18%</span>
        </div>
        <div class="ticker-item">
          <span class="ticker-symbol">TSLA</span>
          <span class="ticker-price">241.32</span>
          <span class="ticker-change positive">+1.02%</span>
        </div>
        <div class="ticker-item">
          <span class="ticker-symbol">OIL</span>
          <span class="ticker-price">81.42</span>
          <span class="ticker-change negative">–0.41%</span>
        </div>
        <div class="ticker-item">
          <span class="ticker-symbol">NIKKEI</span>
          <span class="ticker-price">39,210.6</span>
          <span class="ticker-change positive">+0.77%</span>
        </div>
      </div>
    </section>
  </div>

  <footer>
    <span>NovaTrade is a fictional demo UI for practice and design purposes only.</span>
    <span>All data is stored locally in your browser using localStorage.</span>
  </footer>

  <!-- AUTH MODAL -->
  <div class="backdrop auth-modal" id="authBackdrop">
    <div class="modal">
      <div class="modal-header">
        <h2 id="authTitle">Welcome to NovaTrade</h2>
        <button class="modal-close" id="authClose">×</button>
      </div>
      <div class="modal-toggle">
        <button id="tabSignIn" class="active">Sign in</button>
        <button id="tabSignUp">Sign up</button>
      </div>

      <div style="margin-top: 10px;">
        <div class="modal-field">
          <label for="authEmail">Email</label>
          <input type="email" id="authEmail" placeholder="you@example.com" />
        </div>
        <div class="modal-field">
          <label for="authPassword">Password</label>
          <input type="password" id="authPassword" placeholder="••••••••" />
        </div>
        <div class="modal-error" id="authError"></div>
        <button class="btn btn-primary" style="width:100%; margin-top:6px;" id="authSubmit">
          Continue
        </button>
      </div>

      <div class="modal-footer">
        <span>Demo only · No real money</span>
      </div>
    </div>
  </div>

  <!-- TRADE MODAL -->
  <div class="backdrop trade-modal" id="tradeBackdrop">
    <div class="modal">
      <div class="modal-header">
        <h2>Open buy position</h2>
        <button class="modal-close" id="tradeClose">×</button>
      </div>
      <div id="tradeContent">
        <div class="trade-asset" id="tradeAssetLabel"></div>

        <div class="trade-row">
          <span>Current price</span>
          <span id="tradePrice">0.00</span>
        </div>
        <div class="trade-row">
          <span>Max position (based on margin)</span>
          <span id="tradeMaxSize">0 units</span>
        </div>

        <div class="trade-qty-input">
          <label for="tradeQty" style="font-size:12px; color:var(--text-muted);">Quantity</label>
          <input type="number" id="tradeQty" min="1" step="1" value="10" />
          <button data-q="10">10</button>
          <button data-q="50">50</button>
          <button data-q="100">100</button>
        </div>

        <div class="trade-info">
          Approx. margin required:
          <span id="tradeMargin">0.00</span>
        </div>

        <div class="trade-summary">
          You are about to buy
          <span id="tradeQtySummary">10</span>
          units of
          <span id="tradeSymbolSummary"></span>.
        </div>

        <div class="trade-error" id="tradeError"></div>

        <button class="btn btn-primary" style="width:100%; margin-top:6px;" id="tradeSubmit">
          Confirm buy
        </button>
      </div>
    </div>
  </div>

  <script>
    // ---------------------------
    // SIMPLE "BACKEND" DATA MODEL
    // stored in localStorage
    // ---------------------------

    const STORAGE_KEY_USERS = "novatrade_users";
    const STORAGE_KEY_SESSION = "novatrade_session";

    const INITIAL_BALANCE = 50000;

    const MARKETS = [
      {
        id: "eurusd",
        name: "EUR / USD",
        symbol: "EURUSD",
        type: "Forex · Major",
        price: 1.0852,
        spread: 0.2,
        change: 0.23
      },
      {
        id: "aapl",
        name: "Apple",
        symbol: "AAPL",
        type: "Stock CFD",
        price: 196.7,
        spread: 0.4,
        change: -1.32
      },
      {
        id: "btc",
        name: "Bitcoin",
        symbol: "BTCUSD",
        type: "Crypto CFD",
        price: 62480,
        spread: 32,
        change: 3.14
      },
      {
        id: "xauusd",
        name: "Gold",
        symbol: "XAUUSD",
        type: "Gold · Spot",
        price: 2356.2,
        spread: 0.35,
        change: 0.45
      }
    ];

    function loadUsers() {
      try {
        const raw = localStorage.getItem(STORAGE_KEY_USERS);
        return raw ? JSON.parse(raw) : {};
      } catch (e) {
        return {};
      }
    }

    function saveUsers(users) {
      localStorage.setItem(STORAGE_KEY_USERS, JSON.stringify(users));
    }

    function loadSession() {
      try {
        const raw = localStorage.getItem(STORAGE_KEY_SESSION);
        return raw ? JSON.parse(raw) : null;
      } catch (e) {
        return null;
      }
    }

    function saveSession(session) {
      if (session) {
        localStorage.setItem(STORAGE_KEY_SESSION, JSON.stringify(session));
      } else {
        localStorage.removeItem(STORAGE_KEY_SESSION);
      }
    }

    function getCurrentUser() {
      const session = loadSession();
      if (!session) return null;
      const users = loadUsers();
      return users[session.email] || null;
    }

    function setCurrentUser(user) {
      const users = loadUsers();
      users[user.email] = user;
      saveUsers(users);
      saveSession({ email: user.email });
    }

    function createUser(email, password) {
      return {
        email,
        password,
        balance: INITIAL_BALANCE,
        usedMargin: 0,
        positions: [], // {id, marketId, symbol, name, qty, price, margin}
        history: [] // {time, action, symbol, qty, price}
      };
    }

    // ---------------------------
    // AUTH MODAL LOGIC
    // ---------------------------

    const authBackdrop = document.getElementById("authBackdrop");
    const authClose = document.getElementById("authClose");
    const btnLogin = document.getElementById("btnLogin");
    const btnLogout = document.getElementById("btnLogout");
    const navUser = document.getElementById("navUser");
    const authTitle = document.getElementById("authTitle");
    const tabSignIn = document.getElementById("tabSignIn");
    const tabSignUp = document.getElementById("tabSignUp");
    const authEmail = document.getElementById("authEmail");
    const authPassword = document.getElementById("authPassword");
    const authError = document.getElementById("authError");
    const authSubmit = document.getElementById("authSubmit");

    let authMode = "signin"; // or "signup"

    function openAuthModal(mode = "signin") {
      authMode = mode;
      authBackdrop.classList.add("show");
      setAuthMode(mode);
      authEmail.value = "";
      authPassword.value = "";
      authError.textContent = "";
      setTimeout(() => authEmail.focus(), 10);
    }

    function closeAuthModal() {
      authBackdrop.classList.remove("show");
    }

    function setAuthMode(mode) {
      authMode = mode;
      const isSignIn = mode === "signin";
      tabSignIn.classList.toggle("active", isSignIn);
      tabSignUp.classList.toggle("active", !isSignIn);
      authTitle.textContent = isSignIn ? "Sign in to continue" : "Create a demo account";
      authSubmit.textContent = isSignIn ? "Sign in" : "Create account";
      authError.textContent = "";
    }

    btnLogin.addEventListener("click", () => openAuthModal("signin"));
    authClose.addEventListener("click", closeAuthModal);
    tabSignIn.addEventListener("click", () => setAuthMode("signin"));
    tabSignUp.addEventListener("click", () => setAuthMode("signup"));
    authBackdrop.addEventListener("click", (e) => {
      if (e.target === authBackdrop) closeAuthModal();
    });

    authSubmit.addEventListener("click", handleAuthSubmit);
    authPassword.addEventListener("keydown", (e) => {
      if (e.key === "Enter") {
        handleAuthSubmit();
      }
    });

    function handleAuthSubmit() {
      const email = authEmail.value.trim().toLowerCase();
      const password = authPassword.value;

      if (!email || !password) {
        authError.textContent = "Please enter both email and password.";
        return;
      }
      const users = loadUsers();
      if (authMode === "signup") {
        if (users[email]) {
          authError.textContent = "An account with this email already exists.";
          return;
        }
        const user = createUser(email, password);
        users[email] = user;
        saveUsers(users);
        saveSession({ email });
        closeAuthModal();
        updateUI();
      } else {
        const user = users[email];
        if (!user || user.password !== password) {
          authError.textContent = "Invalid credentials. Try again.";
          return;
        }
        saveSession({ email });
        closeAuthModal();
        updateUI();
      }
    }

    btnLogout.addEventListener("click", () => {
      saveSession(null);
      updateUI();
    });

    // ---------------------------
    // MARKETS RENDERING & TRADING
    // ---------------------------

    const marketsListEl = document.getElementById("marketsList");
    const positionsListEl = document.getElementById("positionsList");

    function renderMarkets() {
      marketsListEl.innerHTML = "";
      MARKETS.forEach((m) => {
        const row = document.createElement("div");
        row.className = "market-row";
        row.innerHTML = `
          <div class="market-name">
            <span>${m.name}</span>
            <span class="market-symbol">${m.symbol} · ${m.type}</span>
          </div>
          <div>
            ${m.price.toFixed(4).replace(/\.?0+$/, "")}
            <div class="market-spread">Spread ${m.spread}</div>
          </div>
          <div class="market-change ${m.change >= 0 ? "positive" : "negative"}">
            ${m.change >= 0 ? "+" : ""}${m.change.toFixed(2)}%
          </div>
          <div class="market-actions">
            <button class="btn-buy" data-market="${m.id}">Buy</button>
            <button class="btn-sell" disabled>Sell</button>
          </div>
        `;
        marketsListEl.appendChild(row);
      });

      marketsListEl.querySelectorAll(".btn-buy").forEach((btn) => {
        btn.addEventListener("click", () => {
          const id = btn.getAttribute("data-market");
          openTradeModal(id);
        });
      });
    }

    // ---------------------------
    // TRADE MODAL
    // ---------------------------

    const tradeBackdrop = document.getElementById("tradeBackdrop");
    const tradeClose = document.getElementById("tradeClose");
    const tradeAssetLabel = document.getElementById("tradeAssetLabel");
    const tradePriceEl = document.getElementById("tradePrice");
    const tradeMaxSizeEl = document.getElementById("tradeMaxSize");
    const tradeMarginEl = document.getElementById("tradeMargin");
    const tradeQtyInput = document.getElementById("tradeQty");
    const tradeQtySummary = document.getElementById("tradeQtySummary");
    const tradeSymbolSummary = document.getElementById("tradeSymbolSummary");
    const tradeError = document.getElementById("tradeError");
    const tradeSubmit = document.getElementById("tradeSubmit");

    let currentTradeMarket = null;

    function openTradeModal(marketId) {
      const user = getCurrentUser();
      if (!user) {
        // require login
        openAuthModal("signin");
        return;
      }
      currentTradeMarket = MARKETS.find((m) => m.id === marketId);
      if (!currentTradeMarket) return;

      tradeBackdrop.classList.add("show");
      tradeError.textContent = "";
      tradeQtyInput.value = 10;

      tradeAssetLabel.innerHTML = `
        You are placing a <strong>BUY</strong> order on
        <strong>${currentTradeMarket.name} (${currentTradeMarket.symbol})</strong>.
      `;
      tradePriceEl.textContent = currentTradeMarket.price.toFixed(4).replace(/\.?0+$/, "");
      tradeSymbolSummary.textContent = currentTradeMarket.symbol;

      updateTradeCalculations();
    }

    function closeTradeModal() {
      tradeBackdrop.classList.remove("show");
      currentTradeMarket = null;
    }

    tradeClose.addEventListener("click", closeTradeModal);
    tradeBackdrop.addEventListener("click", (e) => {
      if (e.target === tradeBackdrop) closeTradeModal();
    });

    document.querySelectorAll(".trade-qty-input button[data-q]").forEach((btn) => {
      btn.addEventListener("click", () => {
        tradeQtyInput.value = btn.getAttribute("data-q");
        updateTradeCalculations();
      });
    });

    tradeQtyInput.addEventListener("input", updateTradeCalculations);

    function updateTradeCalculations() {
      const user = getCurrentUser();
      if (!user || !currentTradeMarket) return;

      const qty = Math.max(1, parseInt(tradeQtyInput.value || "1", 10));
      tradeQtyInput.value = qty;
      tradeQtySummary.textContent = qty;

      const price = currentTradeMarket.price;
      const notional = qty * price;
      // very simple margin: 5% of notional
      const marginRequired = notional * 0.05;
      tradeMarginEl.textContent = "$" + marginRequired.toFixed(2);

      // approximate max size from free margin
      const freeMargin = user.balance - user.usedMargin;
      const maxSize = freeMargin > 0 ? Math.floor((freeMargin / 0.05) / price) : 0;
      tradeMaxSizeEl.textContent = `${maxSize} units`;
    }

    tradeSubmit.addEventListener("click", () => {
      const user = getCurrentUser();
      if (!user || !currentTradeMarket) {
        tradeError.textContent = "You must be logged in to trade.";
        return;
      }
      const qty = Math.max(1, parseInt(tradeQtyInput.value || "1", 10));
      const price = currentTradeMarket.price;
      const notional = qty * price;
      const marginRequired = notional * 0.05;

      const freeMargin = user.balance - user.usedMargin;
      if (marginRequired > freeMargin + 1e-6) {
        tradeError.textContent = "Not enough margin. Reduce quantity or add funds.";
        return;
      }

      const position = {
        id: Date.now().toString(),
        marketId: currentTradeMarket.id,
        symbol: currentTradeMarket.symbol,
        name: currentTradeMarket.name,
        qty,
        price,
        margin: marginRequired
      };

      user.usedMargin += marginRequired;
      user.positions.push(position);
      user.history.push({
        time: new Date().toISOString(),
        action: "BUY",
        symbol: position.symbol,
        qty,
        price
      });

      setCurrentUser(user);
      closeTradeModal();
      updateUI();
    });

    // ---------------------------
    // ACCOUNT UI UPDATE
    // ---------------------------

    const kpiBalance = document.getElementById("kpiBalance");
    const kpiToday = document.getElementById("kpiToday");
    const kpiPnL = document.getElementById("kpiPnL");
    const kpiOvernight = document.getElementById("kpiOvernight");

    const equityValue = document.getElementById("equityValue");
    const availableMarginValue = document.getElementById("availableMarginValue");
    const usedMarginValue = document.getElementById("usedMarginValue");

    const riskUsageLabel = document.getElementById("riskUsageLabel");
    const riskUsageFill = document.getElementById("riskUsageFill");
    const avgLeverage = document.getElementById("avgLeverage");
    const riskStatus = document.getElementById("riskStatus");
    const riskStatusText = document.getElementById("riskStatusText");
    const accountTypeLabel = document.getElementById("accountTypeLabel");
    const manageFundsBtn = document.getElementById("manageFundsBtn");

    manageFundsBtn.addEventListener("click", () => {
      const user = getCurrentUser();
      if (!user) {
        openAuthModal("signin");
        return;
      }
      alert("This is a demo. In a real app, this would open a deposit/withdraw funds page.");
    });

    function formatMoney(v) {
      return "$" + v.toFixed(2);
    }

    function updateUI() {
      const user = getCurrentUser();

      if (!user) {
        navUser.innerHTML = `<span>Guest demo</span>`;
        btnLogin.style.display = "inline-flex";
        btnLogout.style.display = "none";
        accountTypeLabel.textContent = "Guest · Log in to unlock full demo";
        // guest preview values
        kpiBalance.textContent = formatMoney(INITIAL_BALANCE);
        kpiToday.textContent = "+ $0.00 today";
        kpiToday.classList.remove("negative");
        kpiPnL.textContent = "$0.00";
        kpiOvernight.textContent = "– $0.00 overnight";
        equityValue.textContent = "$0.00";
        availableMarginValue.textContent = "$0.00";
        usedMarginValue.textContent = "$0.00";
        riskUsageLabel.textContent = "0%";
        riskUsageFill.style.width = "0%";
        riskStatusText.textContent = "No account connected";
        avgLeverage.textContent = "1 : 0";
        renderPositions(null);
        return;
      }

      navUser.innerHTML = `Signed in as <span>${user.email}</span>`;
      btnLogin.style.display = "none";
      btnLogout.style.display = "inline";

      accountTypeLabel.textContent = "Demo · USD";

      // simple P&L & balance logic: assume equity = balance, no mark-to-market yet
      const equity = user.balance; // no floating P&L in this simple version
      const usedMargin = user.usedMargin;
      const freeMargin = Math.max(0, equity - usedMargin);

      kpiBalance.textContent = formatMoney(user.balance);
      kpiToday.textContent = "+ $0.00 today";
      kpiToday.classList.remove("negative");

      kpiPnL.textContent = "$0.00";
      kpiOvernight.textContent = "– $0.00 overnight";

      equityValue.textContent = formatMoney(equity);
      availableMarginValue.textContent = formatMoney(freeMargin);
      usedMarginValue.textContent = formatMoney(usedMargin);

      const riskUsage = equity > 0 ? (usedMargin / equity) * 100 : 0;
      riskUsageLabel.textContent = riskUsage.toFixed(0) + "%";
      riskUsageFill.style.width = Math.min(100, riskUsage).toFixed(0) + "%";

      let avgLev = 0;
      if (user.positions.length > 0) {
        const totalNotional = user.positions.reduce((acc, p) => acc + p.qty * p.price, 0);
        avgLev = totalNotional / equity;
      }
      avgLeverage.textContent = "1 : " + avgLev.toFixed(1);

      if (user.positions.length === 0) {
        riskStatusText.textContent = "No open positions";
      } else if (riskUsage < 30) {
        riskStatusText.textContent = "Low risk usage";
      } else if (riskUsage < 60) {
        riskStatusText.textContent = "Moderate risk usage";
      } else {
        riskStatusText.textContent = "High risk usage";
      }

      renderPositions(user);
    }

    function renderPositions(user) {
      positionsListEl.innerHTML = "";
      if (!user || user.positions.length === 0) {
        positionsListEl.innerHTML =
          '<div class="position-empty">No open positions. Buy a market to get started.</div>';
        return;
      }

      user.positions.forEach((p) => {
        const row = document.createElement("div");
        row.className = "position-row";
        const notional = p.qty * p.price;

        row.innerHTML = `
          <div>
            <div>${p.name}</div>
            <div class="position-symbol">${p.symbol} · Buy</div>
          </div>
          <div>${p.qty} units</div>
          <div>${formatMoney(p.price)}</div>
          <div>${formatMoney(notional)}</div>
        `;
        positionsListEl.appendChild(row);
      });
    }

    // ---------------------------
    // SIMPLE MAIN CHART PRICE TICK
    // ---------------------------

    (function () {
      const priceEl = document.getElementById("assetPrice");
      const changeEl = document.getElementById("assetChange");

      let basePrice = 18245.12;
      let baseChange = 0.86;

      setInterval(() => {
        const move = (Math.random() - 0.5) * 4;
        basePrice += move;
        baseChange += (Math.random() - 0.5) * 0.08;

        const changeSign = baseChange >= 0 ? "+" : "";
        const isPositive = baseChange >= 0;

        priceEl.textContent = basePrice.toFixed(2);
        changeEl.textContent = `${changeSign}${baseChange.toFixed(2)}% (day)`;
        changeEl.classList.toggle("negative", !isPositive);
      }, 2200);
    })();

    // ---------------------------
    // INIT
    // ---------------------------

    renderMarkets();
    updateUI();
  </script>
</body>
</html>
