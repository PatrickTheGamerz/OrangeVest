<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>OrangeVest – Online Trading Platform</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <style>
    :root {
      --bg-dark: #060b10;
      --bg-card: #0d151f;
      --bg-card-alt: #101927;
      --accent: #ff9f43;
      --accent-soft: rgba(255, 159, 67, 0.15);
      --accent-strong: #ffb257;
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
      background: conic-gradient(
        from 120deg,
        #ff9f43,
        #ff6b6b,
        #ffd86b,
        #ff9f43
      );
      position: relative;
      box-shadow: 0 0 18px rgba(255, 159, 67, 0.6);
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

    .nav-links button {
      padding: 6px 10px;
      border-radius: 999px;
      border: none;
      background: transparent;
      color: inherit;
      cursor: pointer;
      transition: color 0.2s ease, background 0.2s ease;
      font-size: 14px;
    }

    .nav-links button:hover {
      color: var(--text-main);
      background: rgba(255, 255, 255, 0.04);
    }

    .nav-links button.active {
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
      background: linear-gradient(135deg, #ff9f43, #ff6b6b);
      border-color: transparent;
      box-shadow: 0 0 18px rgba(255, 159, 67, 0.65);
      font-weight: 600;
    }

    .btn-primary:hover {
      transform: translateY(-1px);
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.8);
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
        radial-gradient(circle at top left, rgba(255, 159, 67, 0.12), transparent),
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
      color: var(--accent-strong);
      background: rgba(255, 159, 67, 0.12);
      border-radius: var(--radius-pill);
      padding: 4px 10px;
      display: inline-flex;
      align-items: center;
      gap: 6px;
      margin-bottom: 8px;
      border: 1px solid rgba(255, 159, 67, 0.25);
    }

    .hero-title-badge-dot {
      width: 6px;
      height: 6px;
      border-radius: 50%;
      background: var(--accent-strong);
      box-shadow: 0 0 10px rgba(255, 159, 67, 0.9);
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
      color: var(--accent-strong);
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
      color: var(--accent-strong);
      background: rgba(255, 159, 67, 0.1);
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
      background: rgba(255, 159, 67, 0.14);
      color: var(--accent-strong);
      border-color: rgba(255, 159, 67, 0.65);
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
      inset: 20px 10px 20px 0;
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
      background: var(--accent-strong);
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
      grid-template-columns: 1.5fr 1fr 0.9fr 0.9fr;
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
      color: var(--accent-strong);
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
      background: linear-gradient(90deg, #25d586, #ff9f43);
      box-shadow: 0 0 12px rgba(255, 159, 67, 0.75);
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
      color: var(--accent-strong);
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
      color: var(--accent-strong);
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

    .auth-hint {
      font-size: 11px;
      color: var(--text-muted);
    }

    .auth-hint span {
      color: var(--accent-strong);
      font-weight: 500;
    }

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
      background: linear-gradient(135deg, #ff9f43, #ff6b6b);
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
      border-color: rgba(255, 159, 67, 0.8);
      box-shadow: 0 0 0 1px rgba(255, 159, 67, 0.5);
    }

    .modal-error {
      font-size: 11px;
      color: var(--danger);
      min-height: 14px;
      margin-top: 4px;
    }

    .modal-footer {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-top: 10px;
      font-size: 11px;
      color: var(--text-muted);
    }

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
      color: var(--accent-strong);
      font-weight: 500;
    }

    .trade-error {
      font-size: 11px;
      color: var(--danger);
      min-height: 14px;
      margin-top: 4px;
    }

    .positions-list {
      margin-top: 8px;
      border-radius: 10px;
      border: 1px solid rgba(255, 255, 255, 0.04);
      overflow: hidden;
      font-size: 11px;
    }

    .position-row {
      display: grid;
      grid-template-columns: 1.7fr 0.8fr 0.9fr 0.8fr 0.6fr;
      padding: 6px 8px;
      background: rgba(4, 10, 18, 0.96);
      border-bottom: 1px solid rgba(11, 18, 30, 0.9);
      align-items: center;
      gap: 4px;
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

    .pos-sell-btn {
      border-radius: 999px;
      border: none;
      background: linear-gradient(135deg, #ff6b6b, #ff3b3b);
      color: #fff;
      font-size: 10px;
      padding: 3px 8px;
      cursor: pointer;
    }

    .section {
      display: none;
    }

    .section.active {
      display: block;
    }

    .section-shell {
      background:
        radial-gradient(circle at top left, rgba(255, 159, 67, 0.06), transparent 60%),
        linear-gradient(135deg, #050a10, #060c18);
      border-radius: 18px;
      border: 1px solid rgba(255, 255, 255, 0.05);
      padding: 18px 16px 16px;
      box-shadow: 0 18px 40px rgba(0, 0, 0, 0.75);
      margin-top: 4px;
    }

    .section-header-row {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 10px;
      margin-bottom: 10px;
    }

    .section-title {
      font-size: 18px;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .section-title-pill {
      font-size: 10px;
      text-transform: uppercase;
      letter-spacing: 0.08em;
      border-radius: 999px;
      padding: 2px 8px;
      border: 1px solid rgba(255, 255, 255, 0.12);
      color: var(--text-muted);
    }

    .section-subtitle {
      font-size: 13px;
      color: var(--text-muted);
      margin-bottom: 12px;
    }

    .markets-page-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
      gap: 16px;
    }

    .market-card {
      background: linear-gradient(150deg, #050a11, #0c1320);
      border-radius: var(--radius-lg);
      border: 1px solid rgba(255, 255, 255, 0.05);
      padding: 12px 12px 10px;
      box-shadow: 0 14px 30px rgba(0, 0, 0, 0.7);
      font-size: 12px;
    }

    .market-card-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 6px;
    }

    .market-card-name {
      font-weight: 600;
    }

    .market-card-symbol {
      font-size: 11px;
      color: var(--text-muted);
    }

    .market-card-price {
      font-size: 14px;
      font-weight: 600;
    }

    .market-card-change {
      font-size: 11px;
      padding: 2px 6px;
      border-radius: 999px;
      margin-top: 2px;
      display: inline-block;
    }

    .market-card-change.positive {
      color: var(--accent-strong);
      background: rgba(255, 159, 67, 0.1);
    }

    .market-card-change.negative {
      color: var(--danger);
      background: rgba(255, 92, 92, 0.12);
    }

    .market-card-chart {
      margin-top: 6px;
      position: relative;
      height: 80px;
      border-radius: 10px;
      border: 1px solid rgba(255, 255, 255, 0.05);
      overflow: hidden;
      background: radial-gradient(circle at top left, rgba(255, 159, 67, 0.1), transparent 60%),
        #050910;
      padding: 4px;
    }

    .market-card-canvas {
      width: 100%;
      height: 100%;
      display: block;
    }

    .markets-page-actions {
      margin-top: 8px;
      display: flex;
      gap: 6px;
      justify-content: flex-end;
    }

    .info-box {
      background: rgba(4, 10, 18, 0.96);
      border-radius: 12px;
      border: 1px solid rgba(255, 255, 255, 0.08);
      padding: 10px 12px;
      font-size: 12px;
      color: var(--text-muted);
      margin-bottom: 14px;
    }

    .info-box strong {
      color: var(--accent-strong);
      font-weight: 600;
    }

    .pill-row {
      display: flex;
      flex-wrap: wrap;
      gap: 6px;
      margin-bottom: 10px;
    }

    .pill {
      font-size: 11px;
      border-radius: 999px;
      padding: 2px 8px;
      border: 1px solid rgba(255, 255, 255, 0.12);
      color: var(--text-muted);
    }

    .pill-accent {
      border-color: rgba(255, 159, 67, 0.7);
      color: var(--accent-strong);
    }

    .pricing-grid,
    .education-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
      gap: 16px;
    }

    .pricing-card,
    .education-card {
      background: rgba(4, 10, 18, 0.96);
      border-radius: 14px;
      border: 1px solid rgba(255, 255, 255, 0.08);
      padding: 12px 12px 10px;
      font-size: 12px;
      box-shadow: 0 14px 30px rgba(0, 0, 0, 0.7);
    }

    .pricing-card h3,
    .education-card h3 {
      font-size: 14px;
      margin-bottom: 5px;
    }

    .pricing-card p,
    .education-card p {
      font-size: 12px;
      color: var(--text-muted);
    }

    .pricing-highlight {
      font-size: 18px;
      font-weight: 600;
      color: var(--accent-strong);
      margin-bottom: 4px;
    }

    .pricing-tagline {
      font-size: 11px;
      color: var(--text-muted);
      margin-bottom: 8px;
    }

    .check-row {
      font-size: 12px;
      color: var(--text-muted);
      margin-bottom: 4px;
      display: flex;
      gap: 6px;
      align-items: flex-start;
    }

    .check-bullet {
      width: 6px;
      height: 6px;
      border-radius: 50%;
      background: var(--accent-strong);
      margin-top: 4px;
    }

    .badge {
      display: inline-flex;
      align-items: center;
      gap: 4px;
      border-radius: 999px;
      padding: 3px 8px;
      font-size: 10px;
      border: 1px solid rgba(255, 255, 255, 0.15);
      color: var(--text-muted);
      margin-bottom: 6px;
    }

    .badge-accent {
      border-color: rgba(255, 159, 67, 0.6);
      color: var(--accent-strong);
    }

    .education-step-label {
      font-size: 11px;
      text-transform: uppercase;
      letter-spacing: 0.08em;
      color: var(--accent-strong);
      margin-bottom: 2px;
    }

    .education-caption {
      font-size: 11px;
      color: var(--text-muted);
      margin-top: 4px;
    }

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

      .nav-cta button,
      .nav-cta .btn-ghost {
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
        grid-template-columns: 1.6fr 0.7fr 0.8fr 0.8fr 0.7fr;
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
          <span>OrangeVest</span>
          <span>Invest · Trade · Grow</span>
        </div>
      </div>

      <nav>
        <div class="nav-links">
          <button data-section="trading" class="active">Trading</button>
          <button data-section="markets">Markets</button>
          <button data-section="pricing">Pricing</button>
          <button data-section="education">Education</button>
        </div>
        <div class="nav-cta">
          <span id="navUser" class="auth-hint"></span>
          <button id="btnLogin" class="btn btn-ghost">Log in / Sign up</button>
          <button id="btnLogout" class="btn btn-text" style="display:none;">Log out</button>
        </div>
      </nav>
    </header>

    <!-- SECTION: TRADING -->
    <section id="section-trading" class="section active">
      <main class="main-grid">
        <!-- LEFT -->
        <div class="hero-card">
          <div class="hero-header">
            <div class="hero-title">
              <div class="hero-title-badge">
                <span class="hero-title-badge-dot"></span>
                Zero-commission demo · Live-style feed
              </div>
              <h1>Trade global markets with a clean, simple interface.</h1>
              <p>
                Practice on a free demo account and explore CFDs on stocks, forex, indices, and crypto in one place with
                OrangeVest.
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
                <div class="asset-name" id="heroAssetName">US Tech 100</div>
                <div class="asset-symbol" id="heroAssetSymbol">NAS100 · Index CFD</div>
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
              <canvas id="heroChartCanvas" class="chart-line"></canvas>
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
        </div>

        <!-- RIGHT -->
        <aside class="side-column">
          <!-- Markets -->
          <section class="side-card">
            <div class="side-header">
              <div>
                <h2>Popular markets</h2>
                <span>Tap buy or sell on your demo</span>
              </div>
              <button class="btn-text" id="viewAllMarketsBtn" style="color: var(--accent-strong);">View all</button>
            </div>

            <div class="markets-list" id="marketsList">
              <!-- Filled by JS -->
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
                <span id="riskStatusText">No account connected</span>
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
    </section>

    <!-- SECTION: MARKETS -->
    <section id="section-markets" class="section">
      <div class="section-shell">
        <div class="section-header-row">
          <div>
            <div class="section-title">
              Markets board
              <span class="section-title-pill">Live-style demo</span>
            </div>
            <p class="section-subtitle">
              Track every instrument OrangeVest simulates. Watch the mini charts breathe as prices move, then open or close
              positions directly from here.
            </p>
          </div>
          <div class="pill-row">
            <span class="pill pill-accent">Forex</span>
            <span class="pill">Stocks</span>
            <span class="pill">Crypto</span>
            <span class="pill">Metals</span>
          </div>
        </div>

        <div class="markets-page-grid" id="marketsPageGrid">
          <!-- Filled by JS -->
        </div>
      </div>
    </section>

    <!-- SECTION: PRICING -->
    <section id="section-pricing" class="section">
      <div class="section-shell">
        <div class="section-header-row">
          <div>
            <div class="section-title">
              Pricing & costs
              <span class="section-title-pill">Demo-only numbers</span>
            </div>
            <p class="section-subtitle">
              These are fictional pricing examples that show how spreads, leverage and overnight costs could be presented in
              a real platform.
            </p>
          </div>
        </div>

        <div class="pricing-grid">
          <div class="pricing-card">
            <div class="badge badge-accent">Forex majors</div>
            <div class="pricing-highlight>From 0.2 pips</div>
            <div class="pricing-tagline">Learn how tight spreads feel on a liquid pair.</div>
            <div class="check-row">
              <div class="check-bullet"></div>
              <div>EURUSD, GBPUSD and other majors at up to 1:30 leverage in this demo.</div>
            </div>
            <div class="check-row">
              <div class="check-bullet"></div>
              <div>No separate commission; the spread itself is the primary displayed cost.</div>
            </div>
          </div>

          <div class="pricing-card">
            <div class="badge">Indices</div>
            <div class="pricing-highlight">Index snapshots</div>
            <div class="pricing-tagline">Practice index trading without touching real markets.</div>
            <div class="check-row">
              <div class="check-bullet"></div>
              <div>Simulated spreads on NAS100, DAX40 and more for learning volatility.</div>
            </div>
            <div class="check-row">
              <div class="check-bullet"></div>
              <div>Moderate leverage shows how overnight and gap risk can affect a portfolio.</div>
            </div>
          </div>

          <div class="pricing-card">
            <div class="badge">Crypto</div>
            <div class="pricing-highlight">High-volatility demo</div>
            <div class="pricing-tagline">Crypto CFDs with wider spreads to emphasize risk.</div>
            <div class="check-row">
              <div class="check-bullet"></div>
              <div>BTCUSD and similar assets simulate sudden price bursts and deeper drawdowns.</div>
            </div>
            <div class="check-row">
              <div class="check-bullet"></div>
              <div>Reduced leverage in the demo encourages smaller, controlled position sizes.</div>
            </div>
          </div>

          <div class="pricing-card">
            <div class="badge">Metals</div>
            <div class="pricing-highlight">Gold & more</div>
            <div class="pricing-tagline">Practice defensive and hedge-style positions.</div>
            <div class="check-row">
              <div class="check-bullet"></div>
              <div>Gold (XAUUSD) and other metals shown with relatively stable simulated pricing.</div>
            </div>
            <div class="check-row">
              <div class="check-bullet"></div>
              <div>Lower leverage to help you see how diversification might feel in a portfolio.</div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- SECTION: EDUCATION -->
    <section id="section-education" class="section">
      <div class="section-shell">
        <div class="section-header-row">
          <div>
            <div class="section-title">
              Education corner
              <span class="section-title-pill">Learn in demo</span>
            </div>
            <p class="section-subtitle">
              Use OrangeVest’s demo environment to build habits: how you size trades, handle losses, and protect your
              balance matters more than any single entry.
            </p>
          </div>
        </div>

        <div class="education-grid">
          <div class="education-card">
            <div class="education-step-label">Module 1</div>
            <h3>Risk per trade</h3>
            <p>
              Decide in advance how much of your equity you’re willing to risk per idea. Many traders keep this number
              small so a series of losses is survivable.
            </p>
            <div class="education-caption">
              Try: place a few demo trades where the margin used stays below a percentage you choose.
            </div>
          </div>

          <div class="education-card">
            <div class="education-step-label">Module 2</div>
            <h3>Leverage awareness</h3>
            <p>
              Leverage magnifies both profits and losses. Watching “used margin” and “risk usage” in the account widget
              teaches you how quickly positions stack up.
            </p>
            <div class="education-caption">
              Try: deliberately open several small positions and see how overall risk usage changes.
            </div>
          </div>

          <div class="education-card">
            <div class="education-step-label">Module 3</div>
            <h3>Plan before placing</h3>
            <p>
              A trade idea is clearer when you know your invalidation level, target and time horizon before clicking
              “buy.”
            </p>
            <div class="education-caption">
              Try: write your entry plan in a note, then compare it to what actually happens on the chart.
            </div>
          </div>

          <div class="education-card">
            <div class="education-step-label">Module 4</div>
            <h3>Journal your decisions</h3>
            <p>
              Capturing why you entered or exited positions helps you see patterns in your reactions, not just in the
              market.
            </p>
            <div class="education-caption">
              Try: after you close a demo trade, jot down what felt easy and what felt uncomfortable.
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>

  <footer>
    <span>OrangeVest is a fictional demo UI for practice and design purposes only.</span>
    <span>All data is stored locally in your browser using localStorage.</span>
  </footer>

  <!-- AUTH MODAL -->
  <div class="backdrop auth-modal" id="authBackdrop">
    <div class="modal">
      <div class="modal-header">
        <h2 id="authTitle">Welcome to OrangeVest</h2>
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
          <input
            type="password"
            id="authPassword"
            placeholder="At least 5 chars, 1 number, 1 uppercase"
          />
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
    // DATA MODEL & STORAGE
    // ---------------------------

    const STORAGE_KEY_USERS = "orangevest_users";
    const STORAGE_KEY_SESSION = "orangevest_session";

    const INITIAL_BALANCE = 50000;

    const MARKETS = [
      {
        id: "eurusd",
        name: "EUR / USD",
        symbol: "EURUSD",
        type: "Forex · Major",
        price: 1.0852,
        spread: 0.2,
        change: 0.23,
        history: []
      },
      {
        id: "aapl",
        name: "Apple",
        symbol: "AAPL",
        type: "Stock CFD",
        price: 196.7,
        spread: 0.4,
        change: -1.32,
        history: []
      },
      {
        id: "btc",
        name: "Bitcoin",
        symbol: "BTCUSD",
        type: "Crypto CFD",
        price: 62480,
        spread: 32,
        change: 3.14,
        history: []
      },
      {
        id: "xauusd",
        name: "Gold",
        symbol: "XAUUSD",
        type: "Gold · Spot",
        price: 2356.2,
        spread: 0.35,
        change: 0.45,
        history: []
      }
    ];

    function seedHistories() {
      MARKETS.forEach((m) => {
        if (!m.history || !m.history.length) {
          m.history = [];
          for (let i = 0; i < 40; i++) {
            m.history.push(m.price * (1 + (Math.random() - 0.5) * 0.01));
          }
        }
      });
    }

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
        positions: [],
        history: []
      };
    }

    // ---------------------------
    // AUTH LOGIC
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

    let authMode = "signin";

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

    function validatePassword(pw) {
      if (pw.length < 5) return "Password must be at least 5 characters long.";
      if (!/[A-Z]/.test(pw)) return "Password must contain at least one uppercase letter.";
      if (!/[0-9]/.test(pw)) return "Password must contain at least one number.";
      return null;
    }

    function handleAuthSubmit() {
      const email = authEmail.value.trim().toLowerCase();
      const password = authPassword.value;

      if (!email || !password) {
        authError.textContent = "Please enter both email and password.";
        return;
      }
      const users = loadUsers();
      if (authMode === "signup") {
        const pwError = validatePassword(password);
        if (pwError) {
          authError.textContent = pwError;
          return;
        }
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
    // NAVIGATION
    // ---------------------------

    const navButtons = document.querySelectorAll(".nav-links button");
    const sections = {
      trading: document.getElementById("section-trading"),
      markets: document.getElementById("section-markets"),
      pricing: document.getElementById("section-pricing"),
      education: document.getElementById("section-education")
    };

    function setActiveSection(sectionId) {
      Object.keys(sections).forEach((id) => {
        sections[id].classList.toggle("active", id === sectionId);
      });
      navButtons.forEach((btn) => {
        btn.classList.toggle("active", btn.dataset.section === sectionId);
      });
    }

    navButtons.forEach((btn) => {
      btn.addEventListener("click", () => {
        const target = btn.dataset.section;
        if (target !== "trading" && !getCurrentUser()) {
          openAuthModal("signin");
          return;
        }
        setActiveSection(target);
      });
    });

    const viewAllMarketsBtn = document.getElementById("viewAllMarketsBtn");
    viewAllMarketsBtn.addEventListener("click", () => {
      if (!getCurrentUser()) {
        openAuthModal("signin");
        return;
      }
      setActiveSection("markets");
    });

    // ---------------------------
    // MARKETS RENDERING
    // ---------------------------

    const marketsListEl = document.getElementById("marketsList");
    const marketsPageGrid = document.getElementById("marketsPageGrid");
    const positionsListEl = document.getElementById("positionsList");

    function formatPrice(value) {
      if (value < 10) return value.toFixed(4).replace(/\.?0+$/, "");
      if (value < 1000) return value.toFixed(2).replace(/\.?0+$/, "");
      return value.toFixed(0);
    }

    function renderMarketsSidebar() {
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
            <span class="market-price" data-price="${m.id}">${formatPrice(m.price)}</span>
            <div class="market-spread">Spread ${m.spread}</div>
          </div>
          <div class="market-change ${m.change >= 0 ? "positive" : "negative"}" data-change="${m.id}">
            ${m.change >= 0 ? "+" : ""}${m.change.toFixed(2)}%
          </div>
          <div class="market-actions">
            <button class="btn-buy" data-market="${m.id}">Buy</button>
            <button class="btn-sell" data-market-sell="${m.id}">Sell</button>
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

      marketsListEl.querySelectorAll(".btn-sell").forEach((btn) => {
        btn.addEventListener("click", () => {
          const id = btn.getAttribute("data-market-sell");
          attemptQuickSell(id);
        });
      });
    }

    function renderMarketsPage() {
      marketsPageGrid.innerHTML = "";
      MARKETS.forEach((m) => {
        const card = document.createElement("div");
        card.className = "market-card";
        card.innerHTML = `
          <div class="market-card-header">
            <div>
              <div class="market-card-name">${m.name}</div>
              <div class="market-card-symbol">${m.symbol} · ${m.type}</div>
            </div>
            <div style="text-align:right;">
              <div class="market-card-price" data-price="${m.id}-page">${formatPrice(m.price)}</div>
              <div class="market-card-change ${m.change >= 0 ? "positive" : "negative"}" data-change="${m.id}-page">
                ${m.change >= 0 ? "+" : ""}${m.change.toFixed(2)}%
              </div>
            </div>
          </div>
          <div class="market-card-chart">
            <canvas class="market-card-canvas" data-canvas="${m.id}"></canvas>
          </div>
          <div class="markets-page-actions">
            <button class="btn-buy" data-market="${m.id}">Buy</button>
            <button class="btn-sell" data-market-sell="${m.id}">Sell</button>
          </div>
        `;
        marketsPageGrid.appendChild(card);
      });

      marketsPageGrid.querySelectorAll(".btn-buy").forEach((btn) => {
        btn.addEventListener("click", () => {
          const id = btn.getAttribute("data-market");
          openTradeModal(id);
        });
      });

      marketsPageGrid.querySelectorAll(".btn-sell").forEach((btn) => {
        btn.addEventListener("click", () => {
          const id = btn.getAttribute("data-market-sell");
          attemptQuickSell(id);
        });
      });

      drawAllSparklines();
    }

    // ---------------------------
    // TRADE MODAL & BUY
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
      tradePriceEl.textContent = formatPrice(currentTradeMarket.price);
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
      const marginRequired = notional * 0.05;
      tradeMarginEl.textContent = "$" + marginRequired.toFixed(2);

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
    // SELL / CLOSE
    // ---------------------------

    function attemptQuickSell(marketId) {
      const user = getCurrentUser();
      if (!user) {
        openAuthModal("signin");
        return;
      }

      const remaining = [];
      let marginReleased = 0;
      let closedCount = 0;
      let pnl = 0;

      const market = MARKETS.find((m) => m.id === marketId);
      const currentPrice = market ? market.price : 0;

      user.positions.forEach((p) => {
        if (p.marketId === marketId) {
          marginReleased += p.margin;
          closedCount++;
          const notional = p.qty * p.price;
          const delta = (currentPrice - p.price) / p.price;
          const realised = notional * delta;
          pnl += realised;
          user.history.push({
            time: new Date().toISOString(),
            action: "SELL",
            symbol: p.symbol,
            qty: p.qty,
            price: currentPrice
          });
        } else {
          remaining.push(p);
        }
      });

      if (!closedCount) {
        alert("No open positions in this market to sell.");
        return;
      }

      user.positions = remaining;
      user.usedMargin = Math.max(0, user.usedMargin - marginReleased);
      user.balance += pnl;

      setCurrentUser(user);
      updateUI();
      alert(
        `Closed ${closedCount} position(s) in ${market.symbol || marketId.toUpperCase()}.\nRealised P&L: ${
          pnl >= 0 ? "+" : ""
        }$${pnl.toFixed(2)}`
      );
    }

    function closeSinglePosition(positionId) {
      const user = getCurrentUser();
      if (!user) {
        openAuthModal("signin");
        return;
      }
      const pos = user.positions.find((p) => p.id === positionId);
      if (!pos) return;
      const market = MARKETS.find((m) => m.id === pos.marketId);
      const currentPrice = market ? market.price : pos.price;
      const notional = pos.qty * pos.price;
      const delta = (currentPrice - pos.price) / pos.price;
      const pnl = notional * delta;

      user.positions = user.positions.filter((p) => p.id !== positionId);
      user.usedMargin = Math.max(0, user.usedMargin - pos.margin);
      user.balance += pnl;
      user.history.push({
        time: new Date().toISOString(),
        action: "SELL",
        symbol: pos.symbol,
        qty: pos.qty,
        price: currentPrice
      });

      setCurrentUser(user);
      updateUI();
    }

    // ---------------------------
    // ACCOUNT UI
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
    const riskStatusText = document.getElementById("riskStatusText");
    const accountTypeLabel = document.getElementById("accountTypeLabel");
    const manageFundsBtn = document.getElementById("manageFundsBtn");

    manageFundsBtn.addEventListener("click", () => {
      const user = getCurrentUser();
      if (!user) {
        openAuthModal("signin");
        return;
      }
      alert("Demo mode: in a real app this would open deposit/withdraw options.");
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

      const equity = user.balance;
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
          <div style="text-align:right;">
            <button class="pos-sell-btn" data-pos-id="${p.id}">Sell</button>
          </div>
        `;
        positionsListEl.appendChild(row);
      });

      positionsListEl.querySelectorAll(".pos-sell-btn").forEach((btn) => {
        btn.addEventListener("click", () => {
          const id = btn.getAttribute("data-pos-id");
          closeSinglePosition(id);
        });
      });
    }

    // ---------------------------
    // HERO CHART
    // ---------------------------

    const heroCanvas = document.getElementById("heroChartCanvas");
    const assetPriceEl = document.getElementById("assetPrice");
    const assetChangeEl = document.getElementById("assetChange");
    let heroHistory = [];

    function initHeroHistory() {
      heroHistory = [];
      let base = 18245.12;
      for (let i = 0; i < 60; i++) {
        base *= 1 + (Math.random() - 0.5) * 0.002;
        heroHistory.push(base);
      }
    }

    function drawLineChart(canvas, data, colorUp, colorDown) {
      if (!canvas || !data || data.length < 2) return;
      const ctx = canvas.getContext("2d");
      const dpr = window.devicePixelRatio || 1;
      const rect = canvas.getBoundingClientRect();
      canvas.width = rect.width * dpr;
      canvas.height = rect.height * dpr;
      ctx.scale(dpr, dpr);

      const w = rect.width;
      const h = rect.height;
      ctx.clearRect(0, 0, w, h);

      const min = Math.min(...data);
      const max = Math.max(...data);
      const range = max - min || 1;

      const step = w / (data.length - 1);

      const lastChange = data[data.length - 1] - data[0];
      const stroke = lastChange >= 0 ? colorUp : colorDown;

      ctx.lineWidth = 1.6;
      ctx.strokeStyle = stroke;
      ctx.beginPath();
      data.forEach((v, i) => {
        const x = i * step;
        const y = h - ((v - min) / range) * (h * 0.9) - h * 0.05;
        if (i === 0) ctx.moveTo(x, y);
        else ctx.lineTo(x, y);
      });
      ctx.stroke();

      const grad = ctx.createLinearGradient(0, 0, 0, h);
      grad.addColorStop(0, stroke + "55");
      grad.addColorStop(1, "transparent");

      ctx.fillStyle = grad;
      ctx.lineTo(w, h);
      ctx.lineTo(0, h);
      ctx.closePath();
      ctx.fill();
    }

    function tickHeroChart() {
      const last = heroHistory[heroHistory.length - 1];
      const move = last * ((Math.random() - 0.5) * 0.0025);
      const next = last + move;
      heroHistory.push(next);
      if (heroHistory.length > 60) heroHistory.shift();

      const changePct = ((heroHistory[heroHistory.length - 1] - heroHistory[0]) / heroHistory[0]) * 100;
      const sign = changePct >= 0 ? "+" : "";
      assetPriceEl.textContent = heroHistory[heroHistory.length - 1].toFixed(2);
      assetChangeEl.textContent = `${sign}${changePct.toFixed(2)}% (day)`;
      assetChangeEl.classList.toggle("negative", changePct < 0);

      drawLineChart(heroCanvas, heroHistory, "#25d586", "#ff6b6b");
    }

    // ---------------------------
    // MINI MARKET CHARTS
    // ---------------------------

    function updateMarketHistory() {
      MARKETS.forEach((m) => {
        if (!m.history) m.history = [];
        const last = m.history.length ? m.history[m.history.length - 1] : m.price;
        const drift = m.id === "btc" ? 0.004 : 0.0015;
        const vol = m.id === "btc" ? 0.015 : 0.008;
        const move = last * (drift + (Math.random() - 0.5) * vol);
        const next = Math.max(0.0001, last + move);
        m.history.push(next);
        if (m.history.length > 40) m.history.shift();
        m.price = next;
        const rel = (m.price - m.history[0]) / m.history[0];
        m.change = rel * 100;
      });
    }

    function drawAllSparklines() {
      MARKETS.forEach((m) => {
        const canvas = document.querySelector(`canvas[data-canvas="${m.id}"]`);
        if (!canvas) return;
        drawLineChart(canvas, m.history, "#25d586", "#ff6b6b");
      });
    }

    function updateMarketDisplays() {
      MARKETS.forEach((m) => {
        const priceSpan = document.querySelector(`.market-price[data-price="${m.id}"]`);
        const changeSpan = document.querySelector(`.market-change[data-change="${m.id}"]`);
        if (priceSpan) priceSpan.textContent = formatPrice(m.price);
        if (changeSpan) {
          changeSpan.textContent = `${m.change >= 0 ? "+" : ""}${m.change.toFixed(2)}%`;
          changeSpan.classList.toggle("positive", m.change >= 0);
          changeSpan.classList.toggle("negative", m.change < 0);
        }

        const pagePriceSpan = document.querySelector(`.market-card-price[data-price="${m.id}-page"]`);
        const pageChangeSpan = document.querySelector(`.market-card-change[data-change="${m.id}-page"]`);
        if (pagePriceSpan) pagePriceSpan.textContent = formatPrice(m.price);
        if (pageChangeSpan) {
          pageChangeSpan.textContent = `${m.change >= 0 ? "+" : ""}${m.change.toFixed(2)}%`;
          pageChangeSpan.classList.toggle("positive", m.change >= 0);
          pageChangeSpan.classList.toggle("negative", m.change < 0);
        }
      });
      drawAllSparklines();
    }

    function tickMarkets() {
      updateMarketHistory();
      updateMarketDisplays();
    }

    // ---------------------------
    // INIT
    // ---------------------------

    function init() {
      seedHistories();
      renderMarketsSidebar();
      renderMarketsPage();
      initHeroHistory();
      updateUI();
      tickHeroChart();
      tickMarkets();
      setInterval(tickHeroChart, 2200);
      setInterval(tickMarkets, 2600);
    }

    init();
  </script>
</body>
</html>
