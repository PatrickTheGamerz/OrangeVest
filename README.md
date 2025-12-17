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

    /* Layout */

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

    /* Logo */

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
      background: radial-gradient(circle at 30% 20%, rgba(255, 255, 255, 0.2), transparent 60%),
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

    /* Nav */

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

    /* Main layout */

    .main-grid {
      display: grid;
      grid-template-columns: 1.35fr 1fr;
      gap: 24px;
      align-items: flex-start;
    }

    /* Left: hero + chart */

    .hero-card {
      background: radial-gradient(circle at top left, rgba(30, 204, 124, 0.1), transparent),
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

    /* Fake chart */

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
      background-image: linear-gradient(to right, rgba(255, 255, 255, 0.04) 1px, transparent 1px),
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

    /* Right: markets & account */

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
      grid-template-columns: 1.5fr 1fr 0.9fr 0.6fr;
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
    }

    /* Account summary */

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
      width: 46%;
      border-radius: inherit;
      background: linear-gradient(90deg, #1ecc7c, #27a3e4);
      box-shadow: 0 0 12px rgba(30, 204, 124, 0.75);
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

    /* Ticker */

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

    /* Footer */

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

      .markets-list {
        font-size: 12px;
      }

      .market-row {
        grid-template-columns: 1.6fr 1fr 0.8fr;
      }

      .market-actions {
        display: none;
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
          <button class="btn btn-ghost">Log in</button>
          <a href="#" class="btn btn-primary">Start demo</a>
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
              <div class="kpi-value">$50,000.00</div>
              <div class="kpi-trend">+ $1,274.23 today</div>
            </div>
            <div class="kpi">
              <div class="kpi-label">Open P&L</div>
              <div class="kpi-value">$312.64</div>
              <div class="kpi-trend negative">– $18.20 overnight</div>
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
            <!-- simple fake chart visuals -->
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
              <span>Tap to open a position</span>
            </div>
            <a href="#" style="font-size: 11px; color: var(--accent);">View all</a>
          </div>

          <div class="markets-list">
            <div class="market-row">
              <div class="market-name">
                <span>EUR / USD</span>
                <span class="market-symbol">Forex · Major</span>
              </div>
              <div>
                1.0852
                <div class="market-spread">Spread 0.2</div>
              </div>
              <div class="market-change positive">+0.23%</div>
              <div class="market-actions">
                <button class="btn-buy">Buy</button>
                <button class="btn-sell">Sell</button>
              </div>
            </div>

            <div class="market-row">
              <div class="market-name">
                <span>Apple</span>
                <span class="market-symbol">AAPL · Stock CFD</span>
              </div>
              <div>
                196.70
                <div class="market-spread">Spread 0.4</div>
              </div>
              <div class="market-change negative">–1.32%</div>
              <div class="market-actions">
                <button class="btn-buy">Buy</button>
                <button class="btn-sell">Sell</button>
              </div>
            </div>

            <div class="market-row">
              <div class="market-name">
                <span>Bitcoin</span>
                <span class="market-symbol">BTC · Crypto CFD</span>
              </div>
              <div>
                62,480
                <div class="market-spread">Spread 32</div>
              </div>
              <div class="market-change positive">+3.14%</div>
              <div class="market-actions">
                <button class="btn-buy">Buy</button>
                <button class="btn-sell">Sell</button>
              </div>
            </div>

            <div class="market-row">
              <div class="market-name">
                <span>Gold</span>
                <span class="market-symbol">XAU / USD</span>
              </div>
              <div>
                2,356.20
                <div class="market-spread">Spread 0.35</div>
              </div>
              <div class="market-change positive">+0.45%</div>
              <div class="market-actions">
                <button class="btn-buy">Buy</button>
                <button class="btn-sell">Sell</button>
              </div>
            </div>
          </div>
        </section>

        <!-- Account summary -->
        <section class="side-card">
          <div class="side-header">
            <div>
              <h2>Account overview</h2>
              <span>Demo · USD</span>
            </div>
          </div>

          <div class="balance-row">
            <span>Equity</span>
            <span>$50,312.64</span>
          </div>
          <div class="balance-row">
            <span>Available margin</span>
            <span>$42,110.22</span>
          </div>
          <div class="balance-row">
            <span>Used margin</span>
            <span>$8,202.42</span>
          </div>

          <div class="progress-wrap">
            <div class="progress-label">
              <span>Risk usage</span>
              <span>46%</span>
            </div>
            <div class="progress-bar">
              <div class="progress-fill"></div>
            </div>
          </div>

          <div class="small-pill">
            <span>Leverage</span>
            <strong>1 : 20</strong>
            <span>Avg. on open trades</span>
          </div>

          <div class="account-footer">
            <div class="risk-status">
              <span class="risk-dot"></span>
              <span>Moderate risk profile</span>
            </div>
            <a href="#" style="color: var(--accent);">Manage funds</a>
          </div>
        </section>
      </aside>
    </main>

    <!-- TICKER -->
    <section class="ticker">
      <span class="ticker-label">Live snapshot</span>
      <div class="ticker-track" id="tickerTrack">
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

        <!-- Duplicate items for smooth scrolling -->
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
    <span>CFD trading involves risk. This layout is just sample front‑end code.</span>
  </footer>

  <script>
    // Simple fake price fluctuation for the main asset
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
  </script>
</body>
</html>
