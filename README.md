<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>OrangeVest – Investing Platform</title>
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

    .btn-buy-green {
      background: radial-gradient(circle at top left, #27e49b, #16b16b);
      border: 1px solid rgba(39, 228, 155, 0.8);
      box-shadow: 0 0 12px rgba(39, 228, 155, 0.25);
      color: #020309;
    }

    .btn-sell-red {
      background: radial-gradient(circle at top left, #ff7a7a, #ff3b3b);
      border: 1px solid rgba(255, 122, 122, 0.9);
      box-shadow: 0 0 12px rgba(255, 122, 122, 0.25);
      color: #fff8f8;
    }

    .btn-buy-green:hover,
    .btn-sell-red:hover {
      transform: translateY(-0.5px);
      box-shadow: 0 8px 24px rgba(0, 0, 0, 0.7);
    }

    .main-grid {
      display: grid;
      grid-template-columns: 1.2fr 1fr;
      gap: 24px;
      align-items: flex-start;
    }

    .hero-card {
      background:
        radial-gradient(circle at top left, rgba(255, 159, 67, 0.12), transparent),
        linear-gradient(135deg, rgba(17, 25, 39, 0.98), rgba(7, 11, 18, 0.98));
      border-radius: var(--radius-lg);
      padding: 20px 20px 16px;
      box-shadow: var(--shadow-soft);
      border: 1px solid rgba(255, 255, 255, 0.03);
    }

    .portfolio-header {
      display: flex;
      justify-content: space-between;
      align-items: flex-start;
      gap: 14px;
      margin-bottom: 16px;
    }

    .portfolio-main-title {
      font-size: 20px;
      margin-bottom: 4px;
    }

    .portfolio-subtitle {
      font-size: 12px;
      color: var(--text-muted);
    }

    .portfolio-pills {
      display: flex;
      gap: 6px;
      flex-wrap: wrap;
      margin-top: 6px;
    }

    .portfolio-pill {
      border-radius: 999px;
      border: 1px solid rgba(255, 255, 255, 0.12);
      font-size: 10px;
      padding: 3px 8px;
      color: var(--text-muted);
      background: rgba(4, 10, 18, 0.9);
    }

    .portfolio-balance-block {
      background: rgba(3, 8, 15, 0.9);
      border-radius: var(--radius-md);
      border: 1px solid rgba(255, 255, 255, 0.05);
      padding: 8px 10px;
      font-size: 12px;
      min-width: 160px;
    }

    .portfolio-balance-label {
      font-size: 11px;
      color: var(--text-muted);
      margin-bottom: 2px;
    }

    .portfolio-balance-value {
      font-size: 16px;
      font-weight: 600;
    }

    .portfolio-balance-note {
      font-size: 11px;
      color: var(--text-muted);
      margin-top: 2px;
    }

    .portfolio-body {
      display: grid;
      grid-template-columns: 1.1fr 1fr;
      gap: 16px;
      align-items: stretch;
    }

    .portfolio-alloc-card {
      background: rgba(5, 10, 18, 0.95);
      border-radius: var(--radius-md);
      border: 1px solid rgba(255, 255, 255, 0.04);
      padding: 10px 10px 8px;
      font-size: 12px;
    }

    .portfolio-alloc-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 8px;
    }

    .portfolio-alloc-header h3 {
      font-size: 13px;
    }

    .portfolio-alloc-pie {
      height: 140px;
      border-radius: 12px;
      background:
        radial-gradient(circle at 30% 20%, rgba(255, 255, 255, 0.1), transparent 60%),
        conic-gradient(
          #27e49b 0 18%,
          #ff9f43 18% 36%,
          #4f46e5 36% 52%,
          #ff6b6b 52% 66%,
          #a855f7 66% 82%,
          #14b8a6 82% 100%
        );
      position: relative;
      overflow: hidden;
      border: 1px solid rgba(255, 255, 255, 0.06);
    }

    .portfolio-alloc-pie::after {
      content: "";
      position: absolute;
      inset: 18px;
      border-radius: inherit;
      background: rgba(5, 10, 18, 0.96);
    }

    .portfolio-alloc-center {
      position: absolute;
      inset: 28px;
      border-radius: inherit;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      font-size: 11px;
      color: var(--text-muted);
    }

    .portfolio-alloc-center strong {
      font-size: 14px;
      color: var(--accent-strong);
    }

    .portfolio-alloc-legend {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 4px;
      margin-top: 8px;
      font-size: 11px;
    }

    .portfolio-alloc-item {
      display: flex;
      align-items: center;
      gap: 4px;
    }

    .alloc-dot {
      width: 8px;
      height: 8px;
      border-radius: 999px;
    }

    .alloc-dot-core {
      background: #27e49b;
    }

    .alloc-dot-alt {
      background: #ff9f43;
    }

    .alloc-dot-defi {
      background: #4f46e5;
    }

    .alloc-dot-meme {
      background: #ff6b6b;
    }

    .alloc-dot-stable {
      background: #a855f7;
    }

    .alloc-dot-other {
      background: #14b8a6;
    }

    .portfolio-alloc-label {
      color: var(--text-muted);
    }

    .hero-chart-card {
      background: rgba(3, 8, 15, 0.95);
      border-radius: var(--radius-md);
      border: 1px solid rgba(255, 255, 255, 0.05);
      padding: 10px 10px 8px;
    }

    .chart-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 8px;
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
      margin-bottom: 6px;
    }

    .chart-timeframe button {
      border-radius: 999px;
      border: 1px solid transparent;
      background: transparent;
      color: var(--text-muted);
      padding: 3px 7px;
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
      height: 150px;
    }

    .chart-grid {
      position: absolute;
      inset: 0;
      background-image:
        linear-gradient(to right, rgba(255, 255, 255, 0.04) 1px, transparent 1px),
        linear-gradient(to top, rgba(255, 255, 255, 0.04) 1px, transparent 1px);
      background-size: 40px 40px;
      opacity: 0.4;
    }

    .chart-line {
      position: absolute;
      inset: 18px 8px 18px 0;
      pointer-events: none;
    }

    .chart-footer {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding-top: 6px;
      border-top: 1px solid rgba(17, 24, 38, 0.8);
      margin-top: 6px;
      font-size: 11px;
      color: var(--text-muted);
    }

    .chart-legend {
      display: flex;
      gap: 10px;
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
      background: #25d586;
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
      max-height: 260px;
      overflow-y: auto;
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
      max-width: 380px;
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

    .modal-field input,
    .modal-field select {
      border-radius: 999px;
      border: 1px solid rgba(255, 255, 255, 0.08);
      background: #060b14;
      padding: 7px 10px;
      font-size: 13px;
      color: var(--text-main);
      outline: none;
    }

    .modal-field input:focus,
    .modal-field select:focus {
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
      background: radial-gradient(circle at top left, #ff7a7a, #ff3b3b);
      color: #fff;
      font-size: 10px;
      padding: 3px 8px;
      cursor: pointer;
      box-shadow: 0 0 8px rgba(255, 122, 122, 0.4);
    }

    .pos-sell-btn:hover {
      transform: translateY(-0.5px);
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.7);
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
      cursor: pointer;
    }

    .pill-accent {
      border-color: rgba(255, 159, 67, 0.7);
      color: var(--accent-strong);
    }

    .pill.active {
      background: rgba(255, 159, 67, 0.18);
      border-color: rgba(255, 159, 67, 0.9);
      color: var(--accent-strong);
    }

    .profile-grid {
      display: grid;
      grid-template-columns: minmax(0, 1.2fr) minmax(0, 1fr);
      gap: 16px;
    }

    .profile-card {
      background: rgba(4, 10, 18, 0.96);
      border-radius: 14px;
      border: 1px solid rgba(255, 255, 255, 0.08);
      padding: 12px 12px 10px;
      font-size: 12px;
      box-shadow: 0 14px 30px rgba(0, 0, 0, 0.7);
    }

    .profile-card h3 {
      font-size: 14px;
      margin-bottom: 5px;
    }

    .profile-card p {
      font-size: 12px;
      color: var(--text-muted);
    }

    .profile-row {
      display: flex;
      justify-content: space-between;
      margin-bottom: 4px;
      font-size: 12px;
    }

    .profile-row span:first-child {
      color: var(--text-muted);
    }

    .profile-stat-pill {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      border-radius: 999px;
      padding: 3px 8px;
      border: 1px solid rgba(255, 255, 255, 0.15);
      font-size: 11px;
      color: var(--text-muted);
      margin-right: 4px;
      margin-top: 4px;
    }

    .settings-field {
      margin-top: 6px;
    }

    .settings-field label {
      font-size: 11px;
      color: var(--text-muted);
      display: block;
      margin-bottom: 2px;
    }

    .settings-field input {
      width: 100%;
      border-radius: 999px;
      border: 1px solid rgba(255, 255, 255, 0.12);
      background: #060b14;
      padding: 6px 9px;
      font-size: 12px;
      color: var(--text-main);
      outline: none;
    }

    .settings-field input:focus {
      border-color: rgba(255, 159, 67, 0.8);
      box-shadow: 0 0 0 1px rgba(255, 159, 67, 0.5);
    }

    .mode-toggle {
      display: flex;
      gap: 6px;
      margin-top: 6px;
    }

    .mode-toggle button {
      flex: 1;
      font-size: 11px;
      border-radius: 999px;
      border: 1px solid rgba(255, 255, 255, 0.12);
      background: rgba(7, 10, 18, 0.98);
      color: var(--text-muted);
      padding: 4px 8px;
      cursor: pointer;
    }

    .mode-toggle button.active {
      border-color: rgba(255, 159, 67, 0.9);
      color: var(--accent-strong);
      background: rgba(255, 159, 67, 0.14);
    }

    .settings-error {
      font-size: 11px;
      color: var(--danger);
      margin-top: 4px;
      min-height: 14px;
    }

    .settings-success {
      font-size: 11px;
      color: var(--accent-strong);
      margin-top: 4px;
      min-height: 14px;
    }

    .insights-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
      gap: 16px;
    }

    .insight-card {
      background: rgba(4, 10, 18, 0.96);
      border-radius: 14px;
      border: 1px solid rgba(255, 255, 255, 0.08);
      padding: 12px 12px 10px;
      font-size: 12px;
      box-shadow: 0 14px 30px rgba(0, 0, 0, 0.7);
    }

    .insight-card h3 {
      font-size: 14px;
      margin-bottom: 5px;
    }

    .insight-card p {
      font-size: 12px;
      color: var(--text-muted);
    }

    .insight-badge {
      font-size: 10px;
      text-transform: uppercase;
      letter-spacing: 0.08em;
      color: var(--accent-strong);
      margin-bottom: 4px;
    }

    .insight-caption {
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

      .portfolio-body {
        grid-template-columns: 1fr;
      }

      .profile-grid {
        grid-template-columns: 1fr;
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
          <button data-section="trading" class="active">Portfolio</button>
          <button data-section="markets">Markets</button>
          <button data-section="pricing">Profile</button>
          <button data-section="education">Insights</button>
        </div>
        <div class="nav-cta">
          <span id="navUser" class="auth-hint"></span>
          <button id="btnLogin" class="btn btn-ghost">Log in / Sign up</button>
          <button id="btnLogout" class="btn btn-text" style="display:none;">Log out</button>
        </div>
      </nav>
    </header>

    <!-- SECTION: PORTFOLIO (HOME) -->
    <section id="section-trading" class="section active">
      <main class="main-grid">
        <!-- LEFT: PORTFOLIO -->
        <div class="hero-card">
          <div class="portfolio-header">
            <div>
              <h1 class="portfolio-main-title">Your portfolio</h1>
              <p class="portfolio-subtitle" id="portfolioSubtitle">
                Live crypto prices from global exchanges. Build positions, manage exposure, and track performance in one place.
              </p>
              <div class="portfolio-pills">
                <span class="portfolio-pill">Spot only</span>
                <span class="portfolio-pill">No leverage</span>
                <span class="portfolio-pill">Auto-close after 30 days</span>
              </div>
            </div>
            <div class="portfolio-balance-block">
              <div class="portfolio-balance-label">Total portfolio value</div>
              <div class="portfolio-balance-value" id="portfolioValue">$0.00</div>
              <div class="portfolio-balance-note" id="portfolioChange">0.00% today</div>
            </div>
          </div>

          <div class="portfolio-body">
            <div class="portfolio-alloc-card">
              <div class="portfolio-alloc-header">
                <h3>Allocation snapshot</h3>
                <span style="font-size:11px; color:var(--text-muted);" id="allocHint">
                  Based on current holdings
                </span>
              </div>
              <div class="portfolio-alloc-pie">
                <div class="portfolio-alloc-center" id="allocCenter">
                  <span style="font-size:11px; color:var(--text-muted);">Total</span>
                  <strong id="allocCenterValue">$0.00</strong>
                </div>
              </div>
              <div class="portfolio-alloc-legend" id="allocLegend">
                <div class="portfolio-alloc-item">
                  <span class="alloc-dot alloc-dot-core"></span>
                  <span class="portfolio-alloc-label">Core</span>
                </div>
                <div class="portfolio-alloc-item">
                  <span class="alloc-dot alloc-dot-alt"></span>
                  <span class="portfolio-alloc-label">Altcoins</span>
                </div>
                <div class="portfolio-alloc-item">
                  <span class="alloc-dot alloc-dot-defi"></span>
                  <span class="portfolio-alloc-label">DeFi</span>
                </div>
                <div class="portfolio-alloc-item">
                  <span class="alloc-dot alloc-dot-meme"></span>
                  <span class="portfolio-alloc-label">Meme</span>
                </div>
                <div class="portfolio-alloc-item">
                  <span class="alloc-dot alloc-dot-stable"></span>
                  <span class="portfolio-alloc-label">Stablecoins</span>
                </div>
                <div class="portfolio-alloc-item">
                  <span class="alloc-dot alloc-dot-other"></span>
                  <span class="portfolio-alloc-label">Other</span>
                </div>
              </div>
            </div>

            <div class="hero-chart-card">
              <div class="chart-header">
                <div>
                  <div class="asset-name" id="heroAssetName">Loading...</div>
                  <div class="asset-symbol" id="heroAssetSymbol"></div>
                </div>
                <div>
                  <span class="asset-price" id="assetPrice">0.00</span>
                  <span class="asset-price-change" id="assetChange">0.00% (24h)</span>
                </div>
              </div>

              <div class="chart-timeframe" id="heroTimeframeButtons">
                <button data-tf="1D" class="active">1D</button>
                <button data-tf="1W">1W</button>
                <button data-tf="1M">1M</button>
                <button data-tf="6M">6M</button>
                <button data-tf="1Y">1Y</button>
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
                <div id="heroFooterInfo">
                  Timeframe candles based on live prices. Positions auto-close after 30 days.
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- RIGHT: ACCOUNT OVERVIEW + POPULAR -->
        <aside class="side-column">
          <section class="side-card">
            <div class="side-header">
              <div>
                <h2>Account overview</h2>
                <span id="accountTypeLabel">Guest · Normal mode</span>
              </div>
              <span id="currencyLabel" style="font-size:11px; color:var(--accent-strong);"></span>
            </div>

            <div class="balance-row">
              <span>Equity</span>
              <span id="equityValue">$0.00</span>
            </div>
            <div class="balance-row">
              <span>Cash available</span>
              <span id="availableMarginValue">$0.00</span>
            </div>
            <div class="balance-row">
              <span>Invested</span>
              <span id="usedMarginValue">$0.00</span>
            </div>

            <div class="progress-wrap">
              <div class="progress-label">
                <span>Exposure vs equity</span>
                <span id="riskUsageLabel">0%</span>
              </div>
              <div class="progress-bar">
                <div class="progress-fill" id="riskUsageFill"></div>
              </div>
            </div>

            <div class="small-pill">
              <span>Positions</span>
              <strong id="positionsCount">0</strong>
              <span>open</span>
            </div>

            <div class="account-footer">
              <div class="risk-status">
                <span class="risk-dot"></span>
                <span id="riskStatusText">No account connected</span>
              </div>
              <button class="btn-text" id="manageFundsBtn">Manage funds</button>
            </div>
          </section>

          <section class="side-card">
            <div class="side-header">
              <div>
                <h2>Popular markets</h2>
                <span>Top movers (24h)</span>
              </div>
              <button class="btn-text" id="viewAllMarketsBtn" style="color: var(--accent-strong);">View all</button>
            </div>

            <div class="markets-list" id="marketsList">
              <!-- Filled by JS -->
            </div>
          </section>
        </aside>
      </main>

      <section class="ticker">
        <span class="ticker-label">Live snapshot</span>
        <div class="ticker-track" id="tickerTrack">
          <!-- Filled by JS -->
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
              <span class="section-title-pill">Crypto universe</span>
            </div>
            <p class="section-subtitle">
              Scan major and niche coins, grouped by category. Prices are live; trades are simulated, positions expire
              automatically after 30 days.
            </p>
          </div>
          <div class="pill-row" id="marketsFilters">
            <span class="pill pill-accent active" data-filter="all">All</span>
            <span class="pill" data-filter="volatile">Most volatile</span>
            <span class="pill" data-filter="core">Core</span>
            <span class="pill" data-filter="alt">Altcoins</span>
            <span class="pill" data-filter="defi">DeFi</span>
            <span class="pill" data-filter="meme">Meme</span>
            <span class="pill" data-filter="stable">Stablecoins</span>
            <span class="pill" data-filter="infra">Infrastructure</span>
            <span class="pill" data-filter="ai">AI & new narratives</span>
          </div>
        </div>

        <div class="markets-page-grid" id="marketsPageGrid">
          <!-- Filled by JS -->
        </div>
      </div>
    </section>

    <!-- SECTION: PROFILE -->
    <section id="section-pricing" class="section">
      <div class="section-shell">
        <div class="section-header-row">
          <div>
            <div class="section-title">
              Profile
              <span class="section-title-pill">Your investing footprint</span>
            </div>
            <p class="section-subtitle" id="profileSubtitle">
              Switch between Normal and Test mode, change your display name, choose your currency, and keep an eye on
              how you use this platform.
            </p>
          </div>
        </div>

        <div class="profile-grid">
          <div class="profile-card">
            <h3>Account snapshot</h3>
            <p id="profileGuestHint">
              You're currently browsing as a guest in Normal mode. Sign in or switch to Test mode to explore further.
            </p>
            <div id="profileOverviewDetails" style="display:none; margin-top:8px;">
              <div class="profile-row">
                <span>Display name</span>
                <span id="profileDisplayName"></span>
              </div>
              <div class="profile-row">
                <span>Email</span>
                <span id="profileEmail"></span>
              </div>
              <div class="profile-row">
                <span>Balance</span>
                <span id="profileBalance">$0.00</span>
              </div>
              <div class="profile-row">
                <span>Portfolio value</span>
                <span id="profilePortfolio">$0.00</span>
              </div>
              <div class="profile-row">
                <span>Open positions</span>
                <span id="profileOpenPositions">0</span>
              </div>
              <div class="profile-row">
                <span>Sessions</span>
                <span id="profileSessions">0</span>
              </div>
              <div class="profile-row">
                <span>Trades taken</span>
                <span id="profileTrades">0</span>
              </div>
            </div>
          </div>

          <div class="profile-card">
            <h3>Settings & modes</h3>
            <p style="margin-bottom:6px;">
              Configure how OrangeVest behaves for you: mode, display name, password, and display currency.
            </p>

            <div class="mode-toggle">
              <button id="modeNormalBtn" class="active">Normal</button>
              <button id="modeTestBtn">Test (1 000 000)</button>
            </div>
            <div style="font-size:11px; color:var(--text-muted); margin-top:4px;" id="modeDescription">
              Normal: internal balance 100 (base USD), trades and balance are saved to your profile.
            </div>

            <div class="settings-field" style="margin-top:8px;">
              <label for="displayNameInput">Display name</label>
              <input id="displayNameInput" type="text" placeholder="Your name / nickname" />
            </div>
            <button class="btn btn-primary" style="margin-top:6px; padding:6px 12px;" id="saveDisplayNameBtn">
              Save display name
            </button>

            <div class="settings-field" style="margin-top:10px;">
              <label for="newPasswordInput">Change password</label>
              <input id="newPasswordInput" type="password" placeholder="New password" />
            </div>
            <button class="btn btn-ghost" style="margin-top:6px; padding:6px 12px;" id="changePasswordBtn">
              Update password
            </button>

            <div class="settings-success" id="settingsSuccess"></div>
            <div class="settings-error" id="settingsError"></div>
          </div>
        </div>
      </div>
    </section>

    <!-- SECTION: INSIGHTS -->
    <section id="section-education" class="section">
      <div class="section-shell">
        <div class="section-header-row">
          <div>
            <div class="section-title">
              Insights
              <span class="section-title-pill">Tools for calmer investing</span>
            </div>
            <p class="section-subtitle">
              Use this space as your investing checklist: from position sizing to diversification and how long you hold
              ideas before exiting.
            </p>
          </div>
        </div>

        <div class="insights-grid">
          <div class="insight-card">
            <div class="insight-badge">Sizing</div>
            <h3>Position size vs account size</h3>
            <p>
              A single coin rarely deserves your whole account. Many investors limit each position to a small fraction
              of equity so one mistake doesn't end the story.
            </p>
            <div class="insight-caption">
              Try: keep any single position below a percentage you choose (e.g. 5–10% of total portfolio).
            </div>
          </div>

          <div class="insight-card">
            <div class="insight-badge">Concentration</div>
            <h3>How many ideas at once</h3>
            <p>
              Holding too many coins can feel noisy, but holding only one can feel fragile. The sweet spot depends on
              how closely you monitor markets.
            </p>
            <div class="insight-caption">
              Try: cap open positions and only add a new one when you close an old one.
            </div>
          </div>

          <div class="insight-card">
            <div class="insight-badge">Time</div>
            <h3>Holding time vs thesis</h3>
            <p>
              A 5-minute impulse and a 30-day thesis shouldn't be managed the same way. OrangeVest auto-closes after
              30 days so you revisit your reasoning.
            </p>
            <div class="insight-caption">
              Try: before buying, write a one-line reason and how long you expect to hold.
            </div>
          </div>

          <div class="insight-card">
            <div class="insight-badge">Diversification</div>
            <h3>Not all bets on one story</h3>
            <p>
              If all your coins depend on the same narrative, they often move together. Mixing narratives can smooth
              the ride even if total exposure is similar.
            </p>
            <div class="insight-caption">
              Try: hold at least two different “types” of projects (e.g. L1, DeFi, infrastructure).
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>

  <footer>
    <span>OrangeVest</span>
    <span>Built for practising real investing decisions.</span>
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
        <span>Secure sign-in for your OrangeVest profile.</span>
      </div>
    </div>
  </div>

  <!-- MANAGE FUNDS / CURRENCY MODAL -->
  <div class="backdrop" id="fundsBackdrop">
    <div class="modal">
      <div class="modal-header">
        <h2>Manage funds & currency</h2>
        <button class="modal-close" id="fundsClose">×</button>
      </div>
      <div>
        <div class="modal-field">
          <label for="currencySelect">Display currency</label>
          <select id="currencySelect">
            <option value="USD">$ USD</option>
            <option value="EUR">€ EUR</option>
            <option value="PLN">zł PLN</option>
            <option value="GBP">£ GBP</option>
            <option value="CHF">CHF</option>
            <option value="JPY">¥ JPY</option>
            <option value="AUD">$ AUD</option>
            <option value="CAD">$ CAD</option>
            <option value="SEK">kr SEK</option>
            <option value="NOK">kr NOK</option>
            <option value="DKK">kr DKK</option>
            <option value="CZK">Kč CZK</option>
            <option value="HUF">Ft HUF</option>
          </select>
        </div>
        <div class="modal-field">
          <label>Approx. FX rates</label>
          <div style="font-size:11px; color:var(--text-muted);">
            Static demo FX rates. Real platforms would update these in real time.
          </div>
        </div>
        <div class="modal-field">
          <label>Note</label>
          <div style="font-size:11px; color:var(--text-muted);">
            Changing display currency affects all balances, positions and P&L views. Internal accounting stays in USD.
          </div>
        </div>
        <button class="btn btn-primary" style="width:100%; margin-top:8px;" id="fundsSave">
          Apply currency
        </button>
      </div>
    </div>
  </div>

  <!-- BUY MODAL -->
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
          <span>Available cash</span>
          <span id="tradeCashAvailable">0.00</span>
        </div>

        <div class="trade-qty-input">
          <label for="tradeQty" style="font-size:12px; color:var(--text-muted);">Quantity</label>
          <input type="number" id="tradeQty" min="0.0001" step="0.0001" value="1" />
          <button data-q="0.1">0.1</button>
          <button data-q="0.5">0.5</button>
          <button data-q="1">1</button>
        </div>

        <div class="trade-info">
          Approx. cost at current price:
          <span id="tradeCost">0.00</span>
        </div>
        <div class="trade-info" style="margin-top:2px;">
          Positions auto-close after 30 days at then-current price.
        </div>

        <div class="trade-summary">
          You are about to buy
          <span id="tradeQtySummary">1</span>
          units of
          <span id="tradeSymbolSummary"></span>.
        </div>

        <div class="trade-error" id="tradeError"></div>

        <button class="btn btn-buy-green" style="width:100%; margin-top:6px;" id="tradeSubmit">
          Confirm buy
        </button>
      </div>
    </div>
  </div>

  <!-- SELL MODAL -->
  <div class="backdrop trade-modal" id="sellBackdrop">
    <div class="modal">
      <div class="modal-header">
        <h2>Close positions</h2>
        <button class="modal-close" id="sellClose">×</button>
      </div>
      <div id="sellContent">
        <div class="trade-asset" id="sellAssetLabel"></div>

        <div class="trade-row">
          <span>Current price</span>
          <span id="sellPrice">0.00</span>
        </div>

        <div class="trade-row">
          <span>Total quantity open</span>
          <span id="sellTotalQty">0</span>
        </div>

        <div class="trade-qty-input">
          <label for="sellQty" style="font-size:12px; color:var(--text-muted);">Quantity to close</label>
          <input type="number" id="sellQty" min="0.0001" step="0.0001" value="1" />
          <button data-sq="25">25%</button>
          <button data-sq="50">50%</button>
          <button data-sq="100">100%</button>
        </div>

        <div class="trade-info">
          Approx. realised gain/loss is calculated at the time of closing.
        </div>

        <div class="trade-summary">
          You are about to sell up to
          <span id="sellQtySummary">0</span>
          units of
          <span id="sellSymbolSummary"></span>.
        </div>

        <div class="trade-error" id="sellError"></div>

        <button class="btn btn-sell-red" style="width:100%; margin-top:6px;" id="sellSubmit">
          Confirm sell
        </button>
      </div>
    </div>
  </div>


  <!-- AUTH / TRADE / FUNDS LOGIC AND MARKET DATA WILL CONTINUE IN PART 2 -->
  <script>
    // ===============================
    // MARKET UNIVERSE (symbols as on Binance)
    // ===============================
    const SYMBOL_GROUPS = {
      core: [
        "BTC", "ETH", "BNB", "SOL", "XRP", "ADA", "MATIC", "LTC"
      ],
      meme: [
        "DOGE", "SHIB", "PEPE", "FLOKI"
      ],
      defi: [
        "LINK", "UNI", "AAVE", "CRV", "SNX", "LDO", "GMX", "DYDX",
        "INJ", "CAKE", "SUSHI", "BAL", "MKR", "COMP", "FXS"
      ],
      stable: [
        "USDT", "USDC", "DAI", "FDUSD"
      ],
      infra: [
        "DOT", "AVAX", "TON", "TRX", "XLM", "NEAR", "ATOM", "HBAR",
        "ALGO", "VET", "RUNE", "KAVA", "ONE", "EGLD", "MINA",
        "ICP", "FIL", "EOS", "XTZ", "XMR", "DASH", "ZEC",
        "KAS", "BTT", "LUNC", "LUNA", "HNT"
      ],
      gaming: [
        "SAND", "MANA", "AXS", "GALA", "ILV", "GMT", "CHZ", "ENJ"
      ],
      ai: [
        "OCEAN", "AGIX", "FET", "WLD"
      ],
      wallet: [
        "SFP", "TWT"
      ],
      other: [
        "IMX", "OP", "ARB", "WAVES", "ONT", "QTUM", "CELO",
        "FLOW", "TIA", "SEI", "STRK", "MNT", "CORE",
        "ANKR", "BAND", "ONG", "RSR", "SNT", "POWR",
        "DENT", "CVC", "AR"
      ]
    };

    const ALL_SYMBOLS = [
      "BTC","ETH","BNB","SOL","XRP","ADA","DOGE","SHIB","DOT","AVAX","MATIC",
      "TON","TRX","XLM","LTC","LINK","UNI","APT","NEAR","ATOM","HBAR","ALGO",
      "VET","RNDR","IMX","OP","ARB","LDO","AAVE","CRV","SNX","SAND","MANA",
      "AXS","GALA","PEPE","FLOKI","FDUSD","USDT","USDC","DAI","FTM","ICP",
      "FIL","EOS","XTZ","XMR","DASH","ZEC","RUNE","KAVA","ONE","EGLD","MINA",
      "DYDX","INJ","GMX","CAKE","SUSHI","BAL","MKR","COMP","FXS","WAVES","NEO",
      "ONT","QTUM","CHZ","ENJ","ILV","BLUR","GMT","SFP","TWT","CELO","FLOW",
      "OCEAN","AGIX","FET","WLD","TIA","SEI","STRK","MNT","CORE","KAS","BTT",
      "LUNC","LUNA","HNT","ANKR","BAND","ONG","RSR","SNT","POWR","DENT","CVC",
      "AR"
    ];

    // symbol -> {price, change, lastUpdate}
    let MARKET_DATA = {};
    let HERO_SYMBOL = "BTC";
    let HERO_TIMEFRAME = "1D";

    // ===============================
    // USER STATE
    // ===============================
    const STORAGE_KEY = "orangevest_state_v2";

    let USER = {
      loggedIn: false,
      email: null,
      displayName: "Guest",
      mode: "normal", // normal | test
      currency: "USD",
      balanceUSD: 100,
      testBalanceUSD: 1000000,
      positions: [], // {id, symbol, qty, entry, openedAt, autoCloseAt}
      sessions: 0,
      trades: 0
    };

    function loadState() {
      const raw = localStorage.getItem(STORAGE_KEY);
      if (!raw) return;
      try {
        const parsed = JSON.parse(raw);
        USER = { ...USER, ...parsed };
      } catch {}
    }

    function saveState() {
      const copy = { ...USER };
      localStorage.setItem(STORAGE_KEY, JSON.stringify(copy));
    }

    loadState();

    // ===============================
    // FX / CURRENCY
    // ===============================
    const FX = {
      USD: 1,
      EUR: 0.92,
      PLN: 4.1,
      GBP: 0.79,
      CHF: 0.88,
      JPY: 150,
      AUD: 1.5,
      CAD: 1.35,
      SEK: 10.5,
      NOK: 10.8,
      DKK: 6.8,
      CZK: 23.5,
      HUF: 360
    };

    const currencyLabelEl = document.getElementById("currencyLabel");
    const fundsBackdrop = document.getElementById("fundsBackdrop");
    const fundsClose = document.getElementById("fundsClose");
    const fundsSave = document.getElementById("fundsSave");
    const currencySelect = document.getElementById("currencySelect");

    function formatCurrency(valueUSD) {
      const fx = FX[USER.currency] || 1;
      const converted = valueUSD * fx;

      const symbol = {
        USD: "$",
        EUR: "€",
        PLN: "zł",
        GBP: "£",
        CHF: "CHF ",
        JPY: "¥",
        AUD: "$",
        CAD: "$",
        SEK: "kr ",
        NOK: "kr ",
        DKK: "kr ",
        CZK: "Kč ",
        HUF: "Ft "
      }[USER.currency] || "$";

      return symbol + converted.toFixed(2);
    }

    function openFundsModal() {
      fundsBackdrop.classList.add("show");
      currencySelect.value = USER.currency;
    }

    function closeFundsModal() {
      fundsBackdrop.classList.remove("show");
    }

    fundsClose.addEventListener("click", closeFundsModal);
    fundsBackdrop.addEventListener("click", (e) => {
      if (e.target === fundsBackdrop) closeFundsModal();
    });

    fundsSave.addEventListener("click", () => {
      USER.currency = currencySelect.value || "USD";
      saveState();
      updateUI();
      closeFundsModal();
    });

    document.getElementById("manageFundsBtn").addEventListener("click", openFundsModal);

    // ===============================
    // AUTH
    // ===============================
    const authBackdrop = document.getElementById("authBackdrop");
    const authClose = document.getElementById("authClose");
    const authEmail = document.getElementById("authEmail");
    const authPassword = document.getElementById("authPassword");
    const authError = document.getElementById("authError");
    const authSubmit = document.getElementById("authSubmit");
    const tabSignIn = document.getElementById("tabSignIn");
    const tabSignUp = document.getElementById("tabSignUp");
    const btnLogin = document.getElementById("btnLogin");
    const btnLogout = document.getElementById("btnLogout");
    const navUser = document.getElementById("navUser");
    const authTitle = document.getElementById("authTitle");

    let authMode = "signin";

    function openAuth(mode = "signin") {
      authMode = mode;
      authBackdrop.classList.add("show");
      authEmail.value = "";
      authPassword.value = "";
      authError.textContent = "";
      tabSignIn.classList.toggle("active", mode === "signin");
      tabSignUp.classList.toggle("active", mode === "signup");
      authTitle.textContent =
        mode === "signin" ? "Sign in to your profile" : "Create an OrangeVest profile";
    }

    function closeAuth() {
      authBackdrop.classList.remove("show");
    }

    authClose.addEventListener("click", closeAuth);
    authBackdrop.addEventListener("click", (e) => {
      if (e.target === authBackdrop) closeAuth();
    });

    btnLogin.addEventListener("click", () => openAuth("signin"));
    btnLogout.addEventListener("click", () => {
      USER.loggedIn = false;
      USER.email = null;
      USER.displayName = "Guest";
      saveState();
      updateUI();
    });

    tabSignIn.addEventListener("click", () => openAuth("signin"));
    tabSignUp.addEventListener("click", () => openAuth("signup"));

    authSubmit.addEventListener("click", handleAuthSubmit);

    function handleAuthSubmit() {
      const email = authEmail.value.trim();
      const pw = authPassword.value.trim();

      if (!email || !pw) {
        authError.textContent = "Please enter email and password.";
        return;
      }

      // simplified "auth" – local only
      if (authMode === "signup") {
        USER.loggedIn = true;
        USER.email = email;
        USER.displayName = email.split("@")[0];
        USER.sessions += 1;
        saveState();
        closeAuth();
        updateUI();
      } else {
        USER.loggedIn = true;
        USER.email = email;
        if (!USER.displayName || USER.displayName === "Guest") {
          USER.displayName = email.split("@")[0];
        }
        USER.sessions += 1;
        saveState();
        closeAuth();
        updateUI();
      }
    }

    // ===============================
    // NAVIGATION
    // ===============================
    const sections = {
      trading: document.getElementById("section-trading"),
      markets: document.getElementById("section-markets"),
      pricing: document.getElementById("section-pricing"),
      education: document.getElementById("section-education")
    };

    document.querySelectorAll(".nav-links button").forEach((btn) => {
      btn.addEventListener("click", () => {
        const target = btn.dataset.section;
        Object.keys(sections).forEach((id) => {
          sections[id].classList.toggle("active", id === target);
        });
        document.querySelectorAll(".nav-links button").forEach((b) =>
          b.classList.toggle("active", b.dataset.section === target)
        );
      });
    });

    document.getElementById("viewAllMarketsBtn").addEventListener("click", () => {
      Object.keys(sections).forEach((id) => {
        sections[id].classList.toggle("active", id === "markets");
      });
      document.querySelectorAll(".nav-links button").forEach((b) =>
        b.classList.toggle("active", b.dataset.section === "markets")
      );
    });

    // ===============================
    // MODES (NORMAL / TEST)
    // ===============================
    const modeNormalBtn = document.getElementById("modeNormalBtn");
    const modeTestBtn = document.getElementById("modeTestBtn");
    const modeDescription = document.getElementById("modeDescription");

    function updateModeUI() {
      modeNormalBtn.classList.toggle("active", USER.mode === "normal");
      modeTestBtn.classList.toggle("active", USER.mode === "test");
      modeDescription.textContent =
        USER.mode === "normal"
          ? "Normal: internal balance 100 (base USD), trades and balance are saved to your profile."
          : "Test: internal balance 1 000 000 (base USD), trades reset when you clear your browser data.";
    }

    modeNormalBtn.addEventListener("click", () => {
      USER.mode = "normal";
      saveState();
      updateModeUI();
      updateUI();
    });

    modeTestBtn.addEventListener("click", () => {
      USER.mode = "test";
      saveState();
      updateModeUI();
      updateUI();
    });

    // ===============================
    // PROFILE SETTINGS
    // ===============================
    const profileGuestHint = document.getElementById("profileGuestHint");
    const profileOverviewDetails = document.getElementById("profileOverviewDetails");
    const profileDisplayName = document.getElementById("profileDisplayName");
    const profileEmail = document.getElementById("profileEmail");
    const profileBalance = document.getElementById("profileBalance");
    const profilePortfolio = document.getElementById("profilePortfolio");
    const profileOpenPositions = document.getElementById("profileOpenPositions");
    const profileSessions = document.getElementById("profileSessions");
    const profileTrades = document.getElementById("profileTrades");

    const displayNameInput = document.getElementById("displayNameInput");
    const saveDisplayNameBtn = document.getElementById("saveDisplayNameBtn");
    const newPasswordInput = document.getElementById("newPasswordInput");
    const changePasswordBtn = document.getElementById("changePasswordBtn");
    const settingsSuccess = document.getElementById("settingsSuccess");
    const settingsError = document.getElementById("settingsError");

    saveDisplayNameBtn.addEventListener("click", () => {
      const val = displayNameInput.value.trim();
      settingsSuccess.textContent = "";
      settingsError.textContent = "";
      if (!val) {
        settingsError.textContent = "Display name cannot be empty.";
        return;
      }
      USER.displayName = val;
      saveState();
      updateUI();
      settingsSuccess.textContent = "Display name updated.";
    });

    changePasswordBtn.addEventListener("click", () => {
      settingsSuccess.textContent = "";
      settingsError.textContent = "";
      if (!USER.loggedIn) {
        settingsError.textContent = "Sign in first to change password.";
        return;
      }
      const pw = newPasswordInput.value.trim();
      if (!pw || pw.length < 5) {
        settingsError.textContent = "Use at least 5 characters.";
        return;
      }
      newPasswordInput.value = "";
      settingsSuccess.textContent = "Password updated (locally).";
    });

    // ===============================
    // BUY / SELL MODALS
    // ===============================
    const tradeBackdrop = document.getElementById("tradeBackdrop");
    const tradeClose = document.getElementById("tradeClose");
    const tradeAssetLabel = document.getElementById("tradeAssetLabel");
    const tradePriceEl = document.getElementById("tradePrice");
    const tradeCashAvailableEl = document.getElementById("tradeCashAvailable");
    const tradeQtyInput = document.getElementById("tradeQty");
    const tradeCostEl = document.getElementById("tradeCost");
    const tradeQtySummary = document.getElementById("tradeQtySummary");
    const tradeSymbolSummary = document.getElementById("tradeSymbolSummary");
    const tradeError = document.getElementById("tradeError");
    const tradeSubmit = document.getElementById("tradeSubmit");

    let currentBuySymbol = null;

    tradeClose.addEventListener("click", closeTradeModal);
    tradeBackdrop.addEventListener("click", (e) => {
      if (e.target === tradeBackdrop) closeTradeModal();
    });

    function openTradeModal(symbol) {
      currentBuySymbol = symbol;
      const m = MARKET_DATA[symbol];
      if (!m) return;

      tradeAssetLabel.innerHTML = `
        You are opening a simulated <strong>BUY</strong> position in
        <strong>${symbol}/USDT</strong>.`;
      tradePriceEl.textContent = formatCurrency(m.price);
      tradeSymbolSummary.textContent = symbol;
      tradeQtyInput.value = 1;
      tradeError.textContent = "";

      const cashUSD = USER.mode === "normal" ? USER.balanceUSD : USER.testBalanceUSD;
      tradeCashAvailableEl.textContent = formatCurrency(cashUSD);
      updateTradeCost();

      tradeBackdrop.classList.add("show");
    }

    function closeTradeModal() {
      tradeBackdrop.classList.remove("show");
      currentBuySymbol = null;
    }

    document.querySelectorAll('.trade-qty-input button[data-q]').forEach((btn) => {
      btn.addEventListener("click", () => {
        tradeQtyInput.value = btn.getAttribute("data-q");
        updateTradeCost();
      });
    });

    tradeQtyInput.addEventListener("input", updateTradeCost);

    function updateTradeCost() {
      if (!currentBuySymbol) return;
      const m = MARKET_DATA[currentBuySymbol];
      if (!m) return;
      const qty = Math.max(0, parseFloat(tradeQtyInput.value || "0"));
      const costUSD = qty * m.price;
      tradeQtySummary.textContent = qty.toFixed(4);
      tradeCostEl.textContent = formatCurrency(costUSD);
    }

    tradeSubmit.addEventListener("click", () => {
      if (!currentBuySymbol) return;
      const m = MARKET_DATA[currentBuySymbol];
      if (!m) return;
      const qty = Math.max(0, parseFloat(tradeQtyInput.value || "0"));
      if (qty <= 0) return;

      const costUSD = qty * m.price;
      const cashUSD = USER.mode === "normal" ? USER.balanceUSD : USER.testBalanceUSD;

      // if cannot afford full cost, do nothing at all (silent)
      if (costUSD > cashUSD + 1e-8) {
        return;
      }

      const now = Date.now();
      const autoCloseAt = now + 30 * 24 * 60 * 60 * 1000;

      const position = {
        id: now + "-" + currentBuySymbol,
        symbol: currentBuySymbol,
        qty,
        entry: m.price,
        openedAt: now,
        autoCloseAt
      };

      if (USER.mode === "normal") {
        USER.balanceUSD -= costUSD;
      } else {
        USER.testBalanceUSD -= costUSD;
      }

      USER.positions.push(position);
      USER.trades += 1;
      saveState();
      closeTradeModal();
      updateUI();
    });

    // SELL MODAL
    const sellBackdrop = document.getElementById("sellBackdrop");
    const sellClose = document.getElementById("sellClose");
    const sellAssetLabel = document.getElementById("sellAssetLabel");
    const sellPriceEl = document.getElementById("sellPrice");
    const sellTotalQtyEl = document.getElementById("sellTotalQty");
    const sellQtyInput = document.getElementById("sellQty");
    const sellQtySummary = document.getElementById("sellQtySummary");
    const sellSymbolSummary = document.getElementById("sellSymbolSummary");
    const sellError = document.getElementById("sellError");
    const sellSubmit = document.getElementById("sellSubmit");

    let currentSellSymbol = null;

    sellClose.addEventListener("click", closeSellModal);
    sellBackdrop.addEventListener("click", (e) => {
      if (e.target === sellBackdrop) closeSellModal();
    });

    function openSellModal(symbol) {
      currentSellSymbol = symbol;
      const m = MARKET_DATA[symbol];
      if (!m) return;

      const totalQty = USER.positions
        .filter((p) => p.symbol === symbol)
        .reduce((s, p) => s + p.qty, 0);

      sellAssetLabel.innerHTML = `
        You are closing simulated <strong>BUY</strong> positions in
        <strong>${symbol}/USDT</strong>.`;
      sellPriceEl.textContent = formatCurrency(m.price);
      sellTotalQtyEl.textContent = totalQty.toFixed(4);
      sellQtyInput.value = totalQty > 0 ? totalQty.toFixed(4) : 0;
      sellQtySummary.textContent = sellQtyInput.value;
      sellSymbolSummary.textContent = symbol;
      sellError.textContent = "";

      sellBackdrop.classList.add("show");
    }

    function closeSellModal() {
      sellBackdrop.classList.remove("show");
      currentSellSymbol = null;
    }

    document.querySelectorAll('.trade-qty-input button[data-sq]').forEach((btn) => {
      btn.addEventListener("click", () => {
        if (!currentSellSymbol) return;
        const totalQty = USER.positions
          .filter((p) => p.symbol === currentSellSymbol)
          .reduce((s, p) => s + p.qty, 0);
        const pct = parseInt(btn.getAttribute("data-sq"), 10) / 100;
        const qty = totalQty * pct;
        sellQtyInput.value = qty.toFixed(4);
        sellQtySummary.textContent = sellQtyInput.value;
      });
    });

    sellQtyInput.addEventListener("input", () => {
      const q = Math.max(0, parseFloat(sellQtyInput.value || "0"));
      sellQtyInput.value = q;
      sellQtySummary.textContent = q;
    });

    sellSubmit.addEventListener("click", () => {
      if (!currentSellSymbol) return;
      const m = MARKET_DATA[currentSellSymbol];
      if (!m) return;

      const totalQty = USER.positions
        .filter((p) => p.symbol === currentSellSymbol)
        .reduce((s, p) => s + p.qty, 0);

      let qtyToClose = Math.max(0, parseFloat(sellQtyInput.value || "0"));
      if (qtyToClose <= 0 || qtyToClose > totalQty + 1e-8) {
        // soft fail, do nothing
        return;
      }

      let remaining = qtyToClose;
      const newPositions = [];
      let cashBackUSD = 0;

      for (const p of USER.positions) {
        if (p.symbol !== currentSellSymbol || remaining <= 0) {
          newPositions.push(p);
          continue;
        }
        const closing = Math.min(remaining, p.qty);
        const sellValue = closing * m.price;
        const costValue = closing * p.entry;
        const pnl = sellValue - costValue;

        cashBackUSD += sellValue; // full proceeds back
        remaining -= closing;

        if (closing < p.qty - 1e-8) {
          newPositions.push({
            ...p,
            qty: p.qty - closing
          });
        }
      }

      USER.positions = newPositions;
      if (USER.mode === "normal") {
        USER.balanceUSD += cashBackUSD;
      } else {
        USER.testBalanceUSD += cashBackUSD;
      }
      USER.trades += 1;
      saveState();
      closeSellModal();
      updateUI();
    });

    // ===============================
    // AUTO-EXPIRY (30 DAYS)
    // ===============================
    function autoCloseExpiredPositions() {
      const now = Date.now();
      const kept = [];
      let cashBackUSD = 0;

      for (const p of USER.positions) {
        if (now >= p.autoCloseAt) {
          const m = MARKET_DATA[p.symbol];
          if (!m) continue;
          const sellValue = p.qty * m.price;
          cashBackUSD += sellValue;
        } else {
          kept.push(p);
        }
      }

      USER.positions = kept;
      if (cashBackUSD > 0) {
        if (USER.mode === "normal") USER.balanceUSD += cashBackUSD;
        else USER.testBalanceUSD += cashBackUSD;
      }
      if (cashBackUSD > 0) saveState();
    }

    setInterval(autoCloseExpiredPositions, 30 * 1000); // demo: check often

    // ===============================
    // MARKETS FILTER (TABS)
    // ===============================
    const marketsFilters = document.getElementById("marketsFilters");

    marketsFilters.addEventListener("click", (e) => {
      const pill = e.target.closest(".pill");
      if (!pill) return;
      marketsFilters.querySelectorAll(".pill").forEach((p) =>
        p.classList.remove("active")
      );
      pill.classList.add("active");
      const filter = pill.dataset.filter;
      renderFilteredMarkets(filter);
    });

    function renderFilteredMarkets(filter) {
      const grid = document.getElementById("marketsPageGrid");
      grid.innerHTML = "";

      let list = [...MARKET_LIST];

      if (filter === "volatile") {
        list = list.slice(0, 50);
      } else if (filter === "core") {
        list = list.filter((m) => SYMBOL_GROUPS.core.includes(m.symbol));
      } else if (filter === "alt") {
        list = list.filter((m) => SYMBOL_GROUPS.infra.includes(m.symbol) || SYMBOL_GROUPS.altcoins?.includes(m.symbol));
      } else if (filter === "defi") {
        list = list.filter((m) => SYMBOL_GROUPS.defi.includes(m.symbol));
      } else if (filter === "meme") {
        list = list.filter((m) => SYMBOL_GROUPS.meme.includes(m.symbol));
      } else if (filter === "stable") {
        list = list.filter((m) => SYMBOL_GROUPS.stable.includes(m.symbol));
      } else if (filter === "infra") {
        list = list.filter((m) => SYMBOL_GROUPS.infra.includes(m.symbol));
      } else if (filter === "ai") {
        list = list.filter((m) => SYMBOL_GROUPS.ai.includes(m.symbol));
      }

      list.forEach((m) => {
        const card = document.createElement("div");
        card.className = "market-card";

        card.innerHTML = `
          <div class="market-card-header">
            <div>
              <div class="market-card-name">${m.symbol}</div>
              <div class="market-card-symbol">${m.symbol}/USDT</div>
            </div>
            <div>
              <div class="market-card-price">${formatCurrency(m.price)}</div>
              <div class="market-card-change ${m.change < 0 ? "negative" : "positive"}">
                ${m.change.toFixed(2)}%
              </div>
            </div>
          </div>
          <div class="market-card-chart">
            <canvas class="market-card-canvas" data-symbol="${m.symbol}"></canvas>
          </div>
          <div class="markets-page-actions">
            <button class="btn-buy-green" data-buy="${m.symbol}">Buy</button>
            <button class="btn-sell-red" data-sell="${m.symbol}">Sell</button>
          </div>
        `;
        grid.appendChild(card);
      });

      drawAllMiniCharts();

      grid.querySelectorAll("[data-buy]").forEach((btn) => {
        btn.addEventListener("click", () => openTradeModal(btn.dataset.buy));
      });
      grid.querySelectorAll("[data-sell]").forEach((btn) => {
        btn.addEventListener("click", () => openSellModal(btn.dataset.sell));
      });
    }

    // ===============================
    // GLOBAL BUY/SELL BUTTON BINDING
    // ===============================
    function bindGlobalBuySellButtons() {
      document.querySelectorAll("[data-buy]").forEach((btn) => {
        btn.addEventListener("click", () => openTradeModal(btn.dataset.buy));
      });
      document.querySelectorAll("[data-sell]").forEach((btn) => {
        btn.addEventListener("click", () => openSellModal(btn.dataset.sell));
      });
    }

    // ===============================
    // FETCH PRICES FROM BINANCE
    // ===============================
    async function fetchBinancePrices() {
      try {
        const res = await fetch("https://api.binance.com/api/v3/ticker/24hr");
        const data = await res.json();

        MARKET_DATA = {};
        MARKET_LIST = [];

        data.forEach((item) => {
          if (!item.symbol.endsWith("USDT")) return;
          const sym = item.symbol.replace("USDT", "");
          if (!ALL_SYMBOLS.includes(sym)) return;

          const price = parseFloat(item.lastPrice);
          const change = parseFloat(item.priceChangePercent);

          MARKET_DATA[sym] = { symbol: sym, price, change };
          MARKET_LIST.push({ symbol: sym, price, change });
        });

        MARKET_LIST.sort((a, b) => Math.abs(b.change) - Math.abs(a.change));

        updateHeroIfNeeded();
        updatePopularMarketsSidebar();
        updateTickerBar();
        updateMarketsPageInitial();
        updatePortfolioValuesAndAlloc();
        autoCloseExpiredPositions();
        bindGlobalBuySellButtons();
      } catch (err) {
        console.error("Binance fetch error", err);
      }
    }

    function updateHeroIfNeeded() {
      if (!MARKET_DATA[HERO_SYMBOL]) {
        HERO_SYMBOL = MARKET_LIST[0]?.symbol || "BTC";
      }
      const d = MARKET_DATA[HERO_SYMBOL];
      if (!d) return;
      document.getElementById("heroAssetName").textContent = d.symbol;
      document.getElementById("heroAssetSymbol").textContent = d.symbol + "/USDT";
      document.getElementById("assetPrice").textContent = formatCurrency(d.price);
      const ch = document.getElementById("assetChange");
      ch.textContent = d.change.toFixed(2) + "% (24h)";
      ch.classList.toggle("negative", d.change < 0);
      drawHeroChart();
    }

    async function drawHeroChart() {
      const d = MARKET_DATA[HERO_SYMBOL];
      if (!d) return;
      const canvas = document.getElementById("heroChartCanvas");
      const ctx = canvas.getContext("2d");
      canvas.width = canvas.clientWidth;
      canvas.height = canvas.clientHeight;

      const intervalMap = {
        "1D": "1h",
        "1W": "4h",
        "1M": "1d",
        "6M": "1d",
        "1Y": "1w"
      };
      const interval = intervalMap[HERO_TIMEFRAME] || "1h";

      let prices = [];
      try {
        const res = await fetch(
          `https://api.binance.com/api/v3/klines?symbol=${HERO_SYMBOL}USDT&interval=${interval}&limit=120`
        );
        const data = await res.json();
        prices = data.map((c) => parseFloat(c[4]));
      } catch {
        prices = [];
      }

      if (prices.length < 2) {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        return;
      }

      const min = Math.min(...prices);
      const max = Math.max(...prices);
      const range = max - min || 1;

      ctx.clearRect(0, 0, canvas.width, canvas.height);
      ctx.beginPath();
      ctx.lineWidth = 2;
      ctx.strokeStyle = prices[prices.length - 1] >= prices[0] ? "#27e49b" : "#ff6b6b";

      prices.forEach((p, i) => {
        const x = (i / (prices.length - 1)) * canvas.width;
        const y =
          canvas.height - ((p - min) / range) * (canvas.height * 0.8) - canvas.height * 0.1;
        if (i === 0) ctx.moveTo(x, y);
        else ctx.lineTo(x, y);
      });
      ctx.stroke();
    }

    document.querySelectorAll("#heroTimeframeButtons button").forEach((btn) => {
      btn.addEventListener("click", () => {
        document.querySelectorAll("#heroTimeframeButtons button").forEach((b) =>
          b.classList.remove("active")
        );
        btn.classList.add("active");
        HERO_TIMEFRAME = btn.dataset.tf;
        drawHeroChart();
      });
    });

    function updatePopularMarketsSidebar() {
      const list = document.getElementById("marketsList");
      list.innerHTML = "";
      MARKET_LIST.slice(0, 20).forEach((m) => {
        const row = document.createElement("div");
        row.className = "market-row";
        row.innerHTML = `
          <div class="market-name">
            <strong>${m.symbol}</strong>
            <span class="market-symbol">${m.symbol}/USDT</span>
          </div>
          <div>${formatCurrency(m.price)}</div>
          <div class="market-change ${m.change < 0 ? "negative" : "positive"}">
            ${m.change.toFixed(2)}%
          </div>
          <div class="market-actions">
            <button class="btn-buy-green" data-buy="${m.symbol}">Buy</button>
            <button class="btn-sell-red" data-sell="${m.symbol}">Sell</button>
          </div>
        `;
        list.appendChild(row);
      });
    }

    function updateTickerBar() {
      const track = document.getElementById("tickerTrack");
      track.innerHTML = "";
      MARKET_LIST.slice(0, 40).forEach((m) => {
        const item = document.createElement("div");
        item.className = "ticker-item";
        item.innerHTML = `
          <span class="ticker-symbol">${m.symbol}</span>
          <span class="ticker-price">${formatCurrency(m.price)}</span>
          <span class="ticker-change ${m.change < 0 ? "negative" : "positive"}">
            ${m.change.toFixed(2)}%
          </span>
        `;
        track.appendChild(item);
      });
    }

    function updateMarketsPageInitial() {
      renderFilteredMarkets("all");
    }

    async function drawAllMiniCharts() {
      const canvases = document.querySelectorAll(".market-card-canvas");
      for (const canvas of canvases) {
        const sym = canvas.dataset.symbol;
        const ctx = canvas.getContext("2d");
        canvas.width = canvas.clientWidth;
        canvas.height = canvas.clientHeight;

        let prices = [];
        try {
          const res = await fetch(
            `https://api.binance.com/api/v3/klines?symbol=${sym}USDT&interval=1h&limit=60`
          );
          const data = await res.json();
          prices = data.map((c) => parseFloat(c[4]));
        } catch {
          prices = [];
        }
        if (prices.length < 2) continue;

        const min = Math.min(...prices);
        const max = Math.max(...prices);
        const range = max - min || 1;

        ctx.clearRect(0, 0, canvas.width, canvas.height);
        ctx.beginPath();
        ctx.lineWidth = 1.5;
        ctx.strokeStyle = prices[prices.length - 1] >= prices[0] ? "#27e49b" : "#ff6b6b";

        prices.forEach((p, i) => {
          const x = (i / (prices.length - 1)) * canvas.width;
          const y =
            canvas.height - ((p - min) / range) * (canvas.height * 0.8) - canvas.height * 0.1;
          if (i === 0) ctx.moveTo(x, y);
          else ctx.lineTo(x, y);
        });
        ctx.stroke();
      }
    }

    // ===============================
    // PORTFOLIO & ALLOCATION
    // ===============================
    function updatePortfolioValuesAndAlloc() {
      let totalUSD = 0;
      const buckets = {
        core: 0,
        alt: 0,
        defi: 0,
        meme: 0,
        stable: 0,
        infra: 0,
        ai: 0,
        other: 0
      };

      USER.positions.forEach((p) => {
        const m = MARKET_DATA[p.symbol];
        if (!m) return;
        const value = p.qty * m.price;
        totalUSD += value;

        const group =
          SYMBOL_GROUPS.core.includes(p.symbol) ? "core" :
          SYMBOL_GROUPS.meme.includes(p.symbol) ? "meme" :
          SYMBOL_GROUPS.defi.includes(p.symbol) ? "defi" :
          SYMBOL_GROUPS.stable.includes(p.symbol) ? "stable" :
          SYMBOL_GROUPS.infra.includes(p.symbol) ? "infra" :
          SYMBOL_GROUPS.ai.includes(p.symbol) ? "ai" :
          "other";

        buckets[group] += value;
      });

      const cashUSD = USER.mode === "normal" ? USER.balanceUSD : USER.testBalanceUSD;
      const portfolioValueUSD = totalUSD + cashUSD;

      document.getElementById("portfolioValue").textContent = formatCurrency(portfolioValueUSD);
      document.getElementById("equityValue").textContent = formatCurrency(portfolioValueUSD);
      document.getElementById("availableMarginValue").textContent = formatCurrency(cashUSD);
      document.getElementById("usedMarginValue").textContent = formatCurrency(totalUSD);
      document.getElementById("positionsCount").textContent = USER.positions.length;

      const risk = portfolioValueUSD > 0 ? totalUSD / portfolioValueUSD : 0;
      document.getElementById("riskUsageFill").style.width = (risk * 100).toFixed(0) + "%";
      document.getElementById("riskUsageLabel").textContent = (risk * 100).toFixed(0) + "%";

      document.getElementById("allocCenterValue").textContent =
        formatCurrency(portfolioValueUSD);

      const riskStatusText = document.getElementById("riskStatusText");
      if (USER.positions.length === 0) riskStatusText.textContent = "No open positions";
      else if (risk < 0.3) riskStatusText.textContent = "Lightly invested";
      else if (risk < 0.7) riskStatusText.textContent = "Balanced exposure";
      else riskStatusText.textContent = "Heavily invested";
    }

    // ===============================
    // GLOBAL UI UPDATE
    // ===============================
    function updateUI() {
      currencyLabelEl.textContent = `Display currency: ${USER.currency}`;
      updateModeUI();

      // Header
      if (USER.loggedIn) {
        navUser.innerHTML = `Signed in as <span>${USER.displayName}</span>`;
        btnLogin.style.display = "none";
        btnLogout.style.display = "inline-flex";
      } else {
        navUser.innerHTML = `<span>Guest</span>`;
        btnLogin.style.display = "inline-flex";
        btnLogout.style.display = "none";
      }

      // Account label
      accountTypeLabel.textContent =
        USER.mode === "test"
          ? "Test mode · 1 000 000 internal balance"
          : USER.loggedIn
          ? "Normal mode · Profile connected"
          : "Normal mode · Guest";

      // Portfolio / equity & alloc
      updatePortfolioValuesAndAlloc();

      // Profile
      if (!USER.loggedIn) {
        profileGuestHint.style.display = "block";
        profileOverviewDetails.style.display = "none";
      } else {
        profileGuestHint.style.display = "none";
        profileOverviewDetails.style.display = "block";
        profileDisplayName.textContent = USER.displayName;
        profileEmail.textContent = USER.email || "";
        profileBalance.textContent = formatCurrency(
          USER.mode === "normal" ? USER.balanceUSD : USER.testBalanceUSD
        );

        let totalUSD = 0;
        USER.positions.forEach((p) => {
          const m = MARKET_DATA[p.symbol];
          if (!m) return;
          totalUSD += p.qty * m.price;
        });
        profilePortfolio.textContent = formatCurrency(totalUSD);
        profileOpenPositions.textContent = USER.positions.length;
        profileSessions.textContent = USER.sessions;
        profileTrades.textContent = USER.trades;
      }

      displayNameInput.value = USER.displayName === "Guest" ? "" : USER.displayName;
    }

    // ===============================
    // INITIALISE
    // ===============================
    let MARKET_LIST = [];

    function updatePopularMarketsSidebar() {
      const list = document.getElementById("marketsList");
      list.innerHTML = "";
      MARKET_LIST.slice(0, 20).forEach((m) => {
        const row = document.createElement("div");
        row.className = "market-row";
        row.innerHTML = `
          <div class="market-name">
            <strong>${m.symbol}</strong>
            <span class="market-symbol">${m.symbol}/USDT</span>
          </div>
          <div>${formatCurrency(m.price)}</div>
          <div class="market-change ${m.change < 0 ? "negative" : "positive"}">
            ${m.change.toFixed(2)}%
          </div>
          <div class="market-actions">
            <button class="btn-buy-green" data-buy="${m.symbol}">Buy</button>
            <button class="btn-sell-red" data-sell="${m.symbol}">Sell</button>
          </div>
        `;
        list.appendChild(row);
      });
    }

    function updateTickerBar() {
      const track = document.getElementById("tickerTrack");
      track.innerHTML = "";
      MARKET_LIST.slice(0, 40).forEach((m) => {
        const item = document.createElement("div");
        item.className = "ticker-item";
        item.innerHTML = `
          <span class="ticker-symbol">${m.symbol}</span>
          <span class="ticker-price">${formatCurrency(m.price)}</span>
          <span class="ticker-change ${m.change < 0 ? "negative" : "positive"}">
            ${m.change.toFixed(2)}%
          </span>
        `;
        track.appendChild(item);
      });
    }

    function updateMarketsPageInitial() {
      renderFilteredMarkets("all");
    }

    async function refreshAll() {
      await fetchBinancePrices();
      updateUI();
    }

    // 1 second refresh
    setInterval(refreshAll, 1000);
    refreshAll();
  </script>
</body>
</html>





