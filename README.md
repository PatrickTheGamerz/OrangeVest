<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>OrangeVest – Online Trading Platform</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <script src="https://unpkg.com/lightweight-charts/dist/lightweight-charts.standalone.production.js"></script>
  <style>
    /* YOUR EXACT ORIGINAL CSS */
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

    * { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
      background: radial-gradient(circle at top, #182a40 0, #060b10 50%, #020408 100%);
      color: var(--text-main);
      min-height: 100vh;
    }

    a { color: inherit; text-decoration: none; }

    .page { max-width: 1200px; margin: 0 auto; padding: 20px 18px 60px; }

    header { display: flex; align-items: center; justify-content: space-between; margin-bottom: 24px; gap: 16px; }

    .logo { display: flex; align-items: center; gap: 10px; }

    .logo-icon {
      width: 32px; height: 32px; border-radius: 10px;
      background: conic-gradient(from 120deg, #ff9f43, #ff6b6b, #ffd86b, #ff9f43);
      position: relative; box-shadow: 0 0 18px rgba(255, 159, 67, 0.6);
    }

    .logo-icon::after {
      content: ""; position: absolute; inset: 4px; border-radius: inherit;
      background: radial-gradient(circle at 30% 20%, rgba(255, 255, 255, 0.2), transparent 60%), radial-gradient(circle at 80% 80%, rgba(0, 0, 0, 0.8), #050910);
    }

    .logo-text { display: flex; flex-direction: column; line-height: 1.1; }
    .logo-text span:first-child { font-weight: 700; letter-spacing: 0.05em; font-size: 18px; }
    .logo-text span:last-child { font-size: 11px; color: var(--text-muted); text-transform: uppercase; }

    nav { display: flex; align-items: center; gap: 18px; font-size: 14px; }
    .nav-links { display: flex; gap: 14px; color: var(--text-muted); }
    .nav-links button {
      padding: 6px 10px; border-radius: 999px; border: none; background: transparent;
      color: inherit; cursor: pointer; transition: color 0.2s ease, background 0.2s ease; font-size: 14px;
    }
    .nav-links button:hover { color: var(--text-main); background: rgba(255, 255, 255, 0.04); }
    .nav-links button.active { color: var(--accent); background: var(--accent-soft); }

    .nav-cta { display: flex; gap: 10px; align-items: center; }

    .btn {
      border-radius: var(--radius-pill); padding: 8px 16px; font-size: 13px; border: 1px solid transparent;
      cursor: pointer; background: transparent; color: var(--text-main); transition: background 0.2s ease, border 0.2s ease, transform 0.1s ease, box-shadow 0.1s ease;
      display: inline-flex; align-items: center; gap: 6px; text-decoration: none;
    }

    .btn-ghost { border-color: var(--border-soft); color: var(--text-muted); }
    .btn-ghost:hover { background: rgba(255, 255, 255, 0.03); color: var(--text-main); }
    .btn-primary { background: linear-gradient(135deg, #ff9f43, #ff6b6b); border-color: transparent; box-shadow: 0 0 18px rgba(255, 159, 67, 0.65); font-weight: 600; }
    .btn-primary:hover { transform: translateY(-1px); box-shadow: 0 10px 30px rgba(0, 0, 0, 0.8); }
    .btn-text { border: none; background: none; color: var(--text-muted); font-size: 12px; cursor: pointer; }
    .btn-text:hover { color: var(--text-main); }

    .btn-buy-green { background: radial-gradient(circle at top left, #27e49b, #16b16b); border: 1px solid rgba(39, 228, 155, 0.8); box-shadow: 0 0 12px rgba(39, 228, 155, 0.25); color: #020309; }
    .btn-sell-red { background: radial-gradient(circle at top left, #ff7a7a, #ff3b3b); border: 1px solid rgba(255, 122, 122, 0.9); box-shadow: 0 0 12px rgba(255, 122, 122, 0.25); color: #fff8f8; }
    .btn-buy-green:hover, .btn-sell-red:hover { transform: translateY(-0.5px); box-shadow: 0 8px 24px rgba(0, 0, 0, 0.7); }

    .main-grid { display: grid; grid-template-columns: 1.35fr 1fr; gap: 24px; align-items: flex-start; }

    .hero-card {
      background: radial-gradient(circle at top left, rgba(255, 159, 67, 0.12), transparent), linear-gradient(135deg, rgba(17, 25, 39, 0.98), rgba(7, 11, 18, 0.98));
      border-radius: var(--radius-lg); padding: 20px 20px 18px; box-shadow: var(--shadow-soft); border: 1px solid rgba(255, 255, 255, 0.03);
    }

    .hero-header { display: flex; justify-content: space-between; gap: 12px; margin-bottom: 18px; }
    .hero-title { max-width: 360px; }
    .hero-title-badge {
      font-size: 11px; letter-spacing: 0.08em; text-transform: uppercase; color: var(--accent-strong); background: rgba(255, 159, 67, 0.12);
      border-radius: var(--radius-pill); padding: 4px 10px; display: inline-flex; align-items: center; gap: 6px; margin-bottom: 8px; border: 1px solid rgba(255, 159, 67, 0.25);
    }
    .hero-title-badge-dot { width: 6px; height: 6px; border-radius: 50%; background: var(--accent-strong); box-shadow: 0 0 10px rgba(255, 159, 67, 0.9); }
    .hero-title h1 { font-size: 26px; margin-bottom: 6px; }
    .hero-title p { font-size: 13px; color: var(--text-muted); }

    .hero-kpis { display: grid; grid-auto-flow: column; gap: 10px; font-size: 12px; }
    .kpi { background: rgba(3, 8, 15, 0.8); border-radius: var(--radius-md); border: 1px solid rgba(255, 255, 255, 0.04); padding: 8px 10px; min-width: 120px; }
    .kpi-label { color: var(--text-muted); margin-bottom: 4px; font-size: 11px; }
    .kpi-value { font-size: 13px; font-weight: 600; }
    .kpi-trend { font-size: 11px; color: var(--accent-strong); }
    .kpi-trend.negative { color: var(--danger); }
    .kpi-trend.positive { color: #25d586; }

    .chart-card { margin-top: 10px; background: linear-gradient(180deg, #050912, #020307); border-radius: var(--radius-md); padding: 14px 14px 12px; border: 1px solid #171f2a; position: relative; overflow: hidden; }
    .chart-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 12px; font-size: 12px; }
    .asset-name { font-weight: 600; }
    .asset-symbol { color: var(--text-muted); font-size: 11px; }
    .asset-price { font-weight: 600; font-size: 14px; }
    .asset-price-change { font-size: 11px; color: var(--accent-strong); background: rgba(255, 159, 67, 0.1); padding: 2px 8px; border-radius: var(--radius-pill); margin-left: 6px; }
    .asset-price-change.negative { color: var(--danger); background: rgba(255, 92, 92, 0.12); }

    .chart-timeframe { display: flex; gap: 6px; font-size: 11px; }
    .chart-timeframe button { border-radius: 999px; border: 1px solid transparent; background: transparent; color: var(--text-muted); padding: 4px 8px; cursor: pointer; font-size: inherit; transition: 0.15s ease background, 0.15s ease color, 0.15s ease border; }
    .chart-timeframe button.active { background: rgba(255, 159, 67, 0.14); color: var(--accent-strong); border-color: rgba(255, 159, 67, 0.65); }
    .chart-timeframe button:hover { color: var(--text-main); background: rgba(255, 255, 255, 0.03); }

    /* New TV Chart Container */
    .chart-body { position: relative; height: 300px; width: 100%; }

    .chart-footer { display: flex; justify-content: space-between; align-items: center; padding-top: 10px; border-top: 1px solid rgba(17, 24, 38, 0.8); margin-top: 8px; font-size: 11px; color: var(--text-muted); }
    .chart-legend { display: flex; gap: 12px; }
    .legend-item { display: flex; align-items: center; gap: 4px; }
    .dot-buy, .dot-sell { width: 8px; height: 8px; border-radius: 50%; }
    .dot-buy { background: #25d586; }
    .dot-sell { background: var(--danger); }

    .side-column { display: flex; flex-direction: column; gap: 14px; }
    .side-card { background: linear-gradient(145deg, #050a11, #090f18); border-radius: var(--radius-lg); padding: 16px 14px 14px; border: 1px solid rgba(255, 255, 255, 0.03); box-shadow: 0 16px 40px rgba(0, 0, 0, 0.7); font-size: 13px; }
    .side-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px; }
    .side-header h2 { font-size: 15px; }
    .side-header span { font-size: 11px; color: var(--text-muted); }

    .markets-list { margin-top: 4px; border-radius: 12px; border: 1px solid rgba(255, 255, 255, 0.04); overflow: hidden; }
    .market-row { display: grid; grid-template-columns: 1.5fr 1fr 0.9fr 0.9fr; align-items: center; padding: 8px 10px; background: rgba(7, 11, 20, 0.9); border-bottom: 1px solid rgba(15, 23, 37, 0.9); }
    .market-row:nth-child(even) { background: rgba(4, 8, 15, 0.92); }
    .market-row:last-child { border-bottom: none; }
    .market-name { display: flex; flex-direction: column; gap: 2px; }
    .market-symbol { font-size: 11px; color: var(--text-muted); }
    .market-spread { font-size: 11px; color: var(--text-muted); }
    .market-change.positive { color: #25d586; }
    .market-change.negative { color: var(--danger); }
    .market-actions { display: flex; gap: 6px; justify-content: flex-end; }

    .balance-row { display: flex; justify-content: space-between; margin-bottom: 6px; }
    .balance-row span:first-child { color: var(--text-muted); font-size: 12px; }
    .balance-row span:last-child { font-weight: 500; font-size: 13px; }

    .progress-wrap { margin: 10px 0 6px; }
    .progress-label { display: flex; justify-content: space-between; font-size: 11px; color: var(--text-muted); margin-bottom: 4px; }
    .progress-bar { width: 100%; height: 7px; border-radius: 99px; background: #050910; overflow: hidden; border: 1px solid #151d2a; }
    .progress-fill { height: 100%; width: 0%; border-radius: inherit; background: linear-gradient(90deg, #25d586, #ff9f43); box-shadow: 0 0 12px rgba(255, 159, 67, 0.75); transition: width 0.2s ease; }

    .small-pill { display: inline-flex; align-items: center; gap: 6px; border-radius: 999px; padding: 3px 9px; font-size: 11px; background: rgba(9, 16, 26, 0.96); border: 1px solid rgba(255, 255, 255, 0.06); color: var(--text-muted); margin-top: 4px; }
    .small-pill strong { color: var(--accent-strong); font-weight: 600; font-size: 11px; }

    .account-footer { display: flex; justify-content: space-between; align-items: center; margin-top: 10px; border-top: 1px dashed rgba(255, 255, 255, 0.06); padding-top: 8px; font-size: 11px; color: var(--text-muted); }
    .risk-status { display: inline-flex; align-items: center; gap: 6px; border-radius: 999px; padding: 3px 8px; background: rgba(4, 12, 24, 0.95); border: 1px solid rgba(255, 255, 255, 0.04); }
    .risk-dot { width: 7px; height: 7px; border-radius: 50%; background: #ffb020; box-shadow: 0 0 10px rgba(255, 176, 32, 0.7); }

    .ticker { margin-top: 18px; background: linear-gradient(90deg, #050910, #081120); border-radius: var(--radius-pill); border: 1px solid rgba(255, 255, 255, 0.05); box-shadow: 0 10px 30px rgba(0, 0, 0, 0.7); padding: 6px 12px; font-size: 12px; display: flex; align-items: center; gap: 14px; overflow: hidden; position: relative; }
    .ticker-label { text-transform: uppercase; letter-spacing: 0.1em; font-size: 10px; color: var(--text-muted); border-right: 1px solid rgba(255, 255, 255, 0.06); padding-right: 10px; }
    .ticker-track { display: flex; gap: 20px; animation: ticker-scroll 22s linear infinite; white-space: nowrap; }
    .ticker-item { display: inline-flex; gap: 6px; align-items: baseline; }
    .ticker-symbol { font-size: 11px; color: var(--text-muted); }
    .ticker-price { font-size: 12px; font-weight: 500; }
    .ticker-change { font-size: 11px; }
    .ticker-change.positive { color: #25d586; }
    .ticker-change.negative { color: var(--danger); }
    @keyframes ticker-scroll { 0% { transform: translateX(0); } 100% { transform: translateX(-50%); } }

    footer { max-width: 1200px; margin: 24px auto 0; padding: 0 18px; font-size: 11px; color: var(--text-muted); display: flex; flex-wrap: wrap; gap: 10px; justify-content: space-between; }

    /* Modals */
    .backdrop { position: fixed; inset: 0; background: rgba(0, 0, 0, 0.65); display: none; align-items: center; justify-content: center; z-index: 20; }
    .backdrop.show { display: flex; }
    .modal { background: #050910; border-radius: 18px; padding: 18px 18px 16px; width: 92%; max-width: 380px; border: 1px solid rgba(255, 255, 255, 0.08); box-shadow: 0 18px 40px rgba(0, 0, 0, 0.8); position: relative; }
    .modal-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px; }
    .modal-header h2 { font-size: 18px; }
    .modal-toggle { display: flex; gap: 4px; background: #070d18; border-radius: 999px; padding: 2px; border: 1px solid rgba(255, 255, 255, 0.06); font-size: 11px; }
    .modal-toggle button { flex: 1; border-radius: 999px; border: none; background: transparent; color: var(--text-muted); padding: 4px 8px; cursor: pointer; }
    .modal-toggle button.active { background: linear-gradient(135deg, #ff9f43, #ff6b6b); color: #fff; }
    .modal-close { border-radius: 50%; border: 1px solid rgba(255, 255, 255, 0.1); background: transparent; width: 22px; height: 22px; display: inline-flex; align-items: center; justify-content: center; cursor: pointer; color: var(--text-muted); font-size: 13px; }
    .modal-field { margin-bottom: 8px; display: flex; flex-direction: column; gap: 3px; }
    .modal-field label { font-size: 12px; color: var(--text-muted); }
    .modal-field input, .modal-field select { border-radius: 999px; border: 1px solid rgba(255, 255, 255, 0.08); background: #060b14; padding: 7px 10px; font-size: 13px; color: var(--text-main); outline: none; }
    .modal-field input:focus, .modal-field select:focus { border-color: rgba(255, 159, 67, 0.8); box-shadow: 0 0 0 1px rgba(255, 159, 67, 0.5); }
    .modal-error { font-size: 11px; color: var(--danger); min-height: 14px; margin-top: 4px; }
    .modal-footer { display: flex; justify-content: space-between; align-items: center; margin-top: 10px; font-size: 11px; color: var(--text-muted); }

    .trade-asset { font-size: 13px; color: var(--text-muted); margin-bottom: 4px; }
    .trade-asset strong { color: var(--text-main); }
    .trade-row { display: flex; justify-content: space-between; font-size: 12px; margin-bottom: 6px; color: var(--text-muted); }
    .trade-row span:last-child { color: var(--text-main); }
    .trade-qty-input { display: flex; align-items: center; gap: 6px; margin: 8px 0 6px; }
    .trade-qty-input input { width: 80px; border-radius: 999px; border: 1px solid rgba(255, 255, 255, 0.08); background: #060b14; padding: 6px 8px; font-size: 13px; color: var(--text-main); outline: none; }
    .trade-qty-input button { border-radius: 999px; border: none; background: rgba(255, 255, 255, 0.06); color: var(--text-main); padding: 3px 8px; font-size: 11px; cursor: pointer; }
    .trade-info { font-size: 11px; color: var(--text-muted); margin-bottom: 6px; }
    .trade-summary { font-size: 12px; margin: 6px 0; }
    .trade-summary span { color: var(--accent-strong); font-weight: 500; }
    .trade-error { font-size: 11px; color: var(--danger); min-height: 14px; margin-top: 4px; }

    .positions-list { margin-top: 8px; border-radius: 10px; border: 1px solid rgba(255, 255, 255, 0.04); overflow: hidden; font-size: 11px; }
    .position-row { display: grid; grid-template-columns: 1.7fr 0.8fr 0.9fr 0.8fr 0.6fr; padding: 6px 8px; background: rgba(4, 10, 18, 0.96); border-bottom: 1px solid rgba(11, 18, 30, 0.9); align-items: center; gap: 4px; }
    .position-row:nth-child(even) { background: rgba(6, 10, 20, 0.96); }
    .position-row:last-child { border-bottom: none; }
    .position-symbol { font-size: 11px; color: var(--text-muted); }
    .position-empty { padding: 6px 8px; color: var(--text-muted); font-size: 11px; }
    .pos-sell-btn { border-radius: 999px; border: none; background: radial-gradient(circle at top left, #ff7a7a, #ff3b3b); color: #fff; font-size: 10px; padding: 3px 8px; cursor: pointer; box-shadow: 0 0 8px rgba(255, 122, 122, 0.4); }

    .section { display: none; }
    .section.active { display: block; }
    .section-shell { background: radial-gradient(circle at top left, rgba(255, 159, 67, 0.06), transparent 60%), linear-gradient(135deg, #050a10, #060c18); border-radius: 18px; border: 1px solid rgba(255, 255, 255, 0.05); padding: 18px 16px 16px; box-shadow: 0 18px 40px rgba(0, 0, 0, 0.75); margin-top: 4px; }
    .section-header-row { display: flex; justify-content: space-between; align-items: center; gap: 10px; margin-bottom: 10px; }
    .section-title { font-size: 18px; display: flex; align-items: center; gap: 8px; }
    .section-title-pill { font-size: 10px; text-transform: uppercase; letter-spacing: 0.08em; border-radius: 999px; padding: 2px 8px; border: 1px solid rgba(255, 255, 255, 0.12); color: var(--text-muted); }
    .section-subtitle { font-size: 13px; color: var(--text-muted); margin-bottom: 12px; }

    .markets-page-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 16px; }
    .market-card { background: linear-gradient(150deg, #050a11, #0c1320); border-radius: var(--radius-lg); border: 1px solid rgba(255, 255, 255, 0.05); padding: 12px 12px 10px; box-shadow: 0 14px 30px rgba(0, 0, 0, 0.7); font-size: 12px; }
    .market-card-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 6px; }
    .market-card-name { font-weight: 600; }
    .market-card-symbol { font-size: 11px; color: var(--text-muted); }
    .market-card-price { font-size: 14px; font-weight: 600; }
    .market-card-change { font-size: 11px; padding: 2px 6px; border-radius: 999px; margin-top: 2px; display: inline-block; }
    .market-card-change.positive { color: #25d586; background: rgba(37, 213, 134, 0.1); }
    .market-card-change.negative { color: var(--danger); background: rgba(255, 92, 92, 0.12); }
    .market-card-chart { margin-top: 6px; position: relative; height: 80px; border-radius: 10px; border: 1px solid rgba(255, 255, 255, 0.05); overflow: hidden; background: radial-gradient(circle at top left, rgba(255, 159, 67, 0.1), transparent 60%), #050910; padding: 4px; }
    .market-card-canvas { width: 100%; height: 100%; display: block; }
    .markets-page-actions { margin-top: 8px; display: flex; gap: 6px; justify-content: flex-end; }

    .pill-row { display: flex; flex-wrap: wrap; gap: 6px; margin-bottom: 10px; }
    .pill { font-size: 11px; border-radius: 999px; padding: 2px 8px; border: 1px solid rgba(255, 255, 255, 0.12); color: var(--text-muted); cursor: pointer; }
    .pill-accent { border-color: rgba(255, 159, 67, 0.7); color: var(--accent-strong); }
    .pill.active { background: rgba(255, 159, 67, 0.18); border-color: rgba(255, 159, 67, 0.9); color: var(--accent-strong); }

    .profile-grid { display: grid; grid-template-columns: minmax(0, 1.2fr) minmax(0, 1fr); gap: 16px; }
    .profile-card { background: rgba(4, 10, 18, 0.96); border-radius: 14px; border: 1px solid rgba(255, 255, 255, 0.08); padding: 12px 12px 10px; font-size: 12px; box-shadow: 0 14px 30px rgba(0, 0, 0, 0.7); }
    .profile-card h3 { font-size: 14px; margin-bottom: 5px; }
    .profile-card p { font-size: 12px; color: var(--text-muted); }
    .profile-row { display: flex; justify-content: space-between; margin-bottom: 4px; font-size: 12px; }
    .profile-row span:first-child { color: var(--text-muted); }
    .profile-stat-pill { display: inline-flex; align-items: center; gap: 6px; border-radius: 999px; padding: 3px 8px; border: 1px solid rgba(255, 255, 255, 0.15); font-size: 11px; color: var(--text-muted); margin-right: 4px; margin-top: 4px; }
    .settings-field { margin-top: 6px; }
    .settings-field label { font-size: 11px; color: var(--text-muted); display: block; margin-bottom: 2px; }
    .settings-field input { width: 100%; border-radius: 999px; border: 1px solid rgba(255, 255, 255, 0.12); background: #060b14; padding: 6px 9px; font-size: 12px; color: var(--text-main); outline: none; }
    .mode-toggle { display: flex; gap: 6px; margin-top: 6px; }
    .mode-toggle button { flex: 1; font-size: 11px; border-radius: 999px; border: 1px solid rgba(255, 255, 255, 0.12); background: rgba(7, 10, 18, 0.98); color: var(--text-muted); padding: 4px 8px; cursor: pointer; }
    .mode-toggle button.active { border-color: rgba(255, 159, 67, 0.9); color: var(--accent-strong); background: rgba(255, 159, 67, 0.14); }
    .settings-error { font-size: 11px; color: var(--danger); margin-top: 4px; min-height: 14px; }
    .settings-success { font-size: 11px; color: var(--accent-strong); margin-top: 4px; min-height: 14px; }

    .education-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 16px; }
    .education-card { background: rgba(4, 10, 18, 0.96); border-radius: 14px; border: 1px solid rgba(255, 255, 255, 0.08); padding: 12px 12px 10px; font-size: 12px; box-shadow: 0 14px 30px rgba(0, 0, 0, 0.7); }
    .education-card h3 { font-size: 14px; margin-bottom: 5px; }
    .education-card p { font-size: 12px; color: var(--text-muted); }
    .education-step-label { font-size: 11px; text-transform: uppercase; letter-spacing: 0.08em; color: var(--accent-strong); margin-bottom: 2px; }
    .education-caption { font-size: 11px; color: var(--text-muted); margin-top: 4px; }

    /* New Toast Notifications */
    #toast-container { position: fixed; bottom: 20px; right: 20px; display: flex; flex-direction: column; gap: 10px; z-index: 100; pointer-events: none;}
    .toast { background: #0d151f; border-left: 4px solid var(--accent); color: #fff; padding: 14px 18px; border-radius: 8px; box-shadow: 0 8px 24px rgba(0,0,0,0.5); font-size: 13px; animation: slideIn 0.3s ease forwards; min-width: 250px;}
    .toast.success { border-color: #25d586; }
    .toast.error { border-color: var(--danger); }
    @keyframes slideIn { from { transform: translateX(100%); opacity: 0; } to { transform: translateX(0); opacity: 1; } }
    @keyframes fadeOut { to { opacity: 0; transform: translateY(10px); } }

    @media (max-width: 900px) { .main-grid { grid-template-columns: 1fr; } .side-column { order: -1; } header { flex-wrap: wrap; align-items: flex-start; } nav { width: 100%; justify-content: flex-end; flex-wrap: wrap; } .hero-header { flex-direction: column; } .profile-grid { grid-template-columns: 1fr; } }
    @media (max-width: 640px) { header { flex-direction: column; align-items: flex-start; } nav { flex-direction: column; align-items: flex-start; gap: 10px; } .nav-cta { width: 100%; } .nav-cta button { flex: 1; justify-content: center; } .market-row { grid-template-columns: 1.6fr 1fr 0.8fr; } .market-actions { display: none; } .position-row { grid-template-columns: 1.6fr 0.7fr 0.8fr 0.8fr 0.7fr; } }
  </style>
</head>
<body>
  <div class="page">
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
          <button data-section="pricing">Profile</button>
          <button data-section="education">Education</button>
        </div>
        <div class="nav-cta">
          <span id="navUser" class="auth-hint"></span>
          <button id="btnLogin" class="btn btn-ghost">Log in / Sign up</button>
          <button id="btnLogout" class="btn btn-text" style="display:none;">Log out</button>
        </div>
      </nav>
    </header>

    <section id="section-trading" class="section active">
      <main class="main-grid">
        <div class="hero-card">
          <div class="hero-header">
            <div class="hero-title">
              <div class="hero-title-badge">
                <span class="hero-title-badge-dot" id="liveIndicator"></span>
                Live feed · Binance markets
              </div>
              <h1>Trade major crypto pairs with a clean, simple interface.</h1>
              <p>Watch real-time WebSocket data from Binance. Practice entries, exits, and risk management.</p>
            </div>
            <div class="hero-kpis">
              <div class="kpi">
                <div class="kpi-label">Balance</div>
                <div class="kpi-value" id="kpiBalance">$100.00</div>
              </div>
              <div class="kpi">
                <div class="kpi-label">Live P&L</div>
                <div class="kpi-value" id="kpiPnL">$0.00</div>
                <div class="kpi-trend" id="kpiPnLPercent">0.00%</div>
              </div>
            </div>
          </div>

          <article class="chart-card">
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
              <button data-tf="15m" class="active">15m</button>
              <button data-tf="1h">1H</button>
              <button data-tf="4h">4H</button>
              <button data-tf="1d">1D</button>
            </div>

            <div class="chart-body" id="tvChartContainer"></div>

            <div class="chart-footer">
              <div id="heroFooterInfo">Live Candles from Binance.</div>
            </div>
          </article>
        </div>

        <aside class="side-column">
          <section class="side-card">
            <div class="side-header">
              <div>
                <h2>Popular markets</h2>
                <span>Top 4 movers (24h)</span>
              </div>
              <button class="btn-text" id="viewAllMarketsBtn" style="color: var(--accent-strong);">View all</button>
            </div>
            <div class="markets-list" id="marketsList"></div>
          </section>

          <section class="side-card">
            <div class="side-header">
              <div>
                <h2>Account overview</h2>
                <span id="accountTypeLabel">Guest · Connect to start tracking</span>
              </div>
              <span id="currencyLabel" style="font-size:11px; color:var(--accent-strong);"></span>
            </div>

            <div class="balance-row">
              <span>Equity (Live)</span>
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

            <div class="account-footer">
              <div class="risk-status">
                <span class="risk-dot"></span>
                <span id="riskStatusText">No account connected</span>
              </div>
              <button class="btn-text" id="manageFundsBtn">Manage funds</button>
            </div>

            <h3 style="font-size: 12px; margin-top: 10px; color: var(--text-muted);">Open positions</h3>
            <div class="positions-list" id="positionsList">
              <div class="position-empty">No open positions. Buy a market to get started.</div>
            </div>
          </section>
        </aside>
      </main>

      <section class="ticker">
        <span class="ticker-label">Live snapshot</span>
        <div class="ticker-track" id="tickerTrack"></div>
      </section>
    </section>

    <section id="section-markets" class="section">
      <div class="section-shell">
        <div class="section-header-row">
          <div>
            <div class="section-title">
              Markets board <span class="section-title-pill">Binance spot</span>
            </div>
            <p class="section-subtitle">Filter and trade straight from here. Sparklines update live.</p>
          </div>
          <div class="pill-row" id="marketsFilters">
            <span class="pill pill-accent active" data-filter="all">All</span>
            <span class="pill" data-filter="volatile">Most volatile</span>
            <span class="pill" data-filter="majors">Majors</span>
            <span class="pill" data-filter="altcoins">Altcoins</span>
            <span class="pill" data-filter="meme">Meme</span>
          </div>
        </div>
        <div class="markets-page-grid" id="marketsPageGrid"></div>
      </div>
    </section>

    <section id="section-pricing" class="section">
      <div class="section-shell">
        <div class="section-header-row">
          <div>
            <div class="section-title">Profile <span class="section-title-pill">Your footprint</span></div>
            <p class="section-subtitle" id="profileSubtitle">Connect an account or switch to Test mode.</p>
          </div>
        </div>

        <div class="profile-grid">
          <div class="profile-card">
            <h3>Account snapshot</h3>
            <p id="profileGuestHint">You're currently browsing as a guest in Normal mode. Sign in or switch to Test mode.</p>
            <div id="profileOverviewDetails" style="display:none; margin-top:8px;">
              <div class="profile-row"><span>Display name</span><span id="profileDisplayName"></span></div>
              <div class="profile-row"><span>Email</span><span id="profileEmail"></span></div>
              <div class="profile-row"><span>Live Equity</span><span id="profileBalance">$0.00</span></div>
              <div class="profile-row"><span>Open positions</span><span id="profileOpenPositions">0</span></div>
              <div style="margin-top:6px;">
                <span class="profile-stat-pill">Sessions <strong id="profileSessions">0</strong></span>
                <span class="profile-stat-pill">Trades <strong id="profileTrades">0</strong></span>
              </div>
            </div>
          </div>

          <div class="profile-card">
            <h3>Settings & modes</h3>
            <div class="mode-toggle">
              <button id="modeNormalBtn" class="active">Normal mode</button>
              <button id="modeTestBtn">Test mode</button>
            </div>
            <div style="font-size:11px; color:var(--text-muted); margin-top:4px;" id="modeDescription">
              Normal: saves to profile. Test: sandbox mode.
            </div>

            <div class="settings-field" style="margin-top:8px;">
              <label>Display name</label>
              <input id="displayNameInput" type="text" placeholder="Your name" />
            </div>
            <button class="btn btn-primary" style="margin-top:6px; padding:6px 12px;" id="saveDisplayNameBtn">Save name</button>

            <div class="settings-success" id="settingsSuccess"></div>
            <div class="settings-error" id="settingsError"></div>
          </div>
        </div>
      </div>
    </section>

    <section id="section-education" class="section">
      <div class="section-shell">
        <div class="section-header-row">
          <div>
            <div class="section-title">Education corner <span class="section-title-pill">Habits over hype</span></div>
            <p class="section-subtitle">Practise execution and risk management.</p>
          </div>
        </div>
        <div class="education-grid">
          <div class="education-card">
            <div class="education-step-label">Module 1</div>
            <h3>Risk per trade</h3>
            <p>Decide in advance how much of your equity you risk on an idea.</p>
          </div>
          <div class="education-card">
            <div class="education-step-label">Module 2</div>
            <h3>Leverage awareness</h3>
            <p>Watching “used margin” and “risk usage” keeps exposure visible.</p>
          </div>
          <div class="education-card">
            <div class="education-step-label">Module 3</div>
            <h3>Plan before placing</h3>
            <p>A trade idea is clearer when you know where you’d scale out or exit.</p>
          </div>
          <div class="education-card">
            <div class="education-step-label">Module 4</div>
            <h3>Journal decisions</h3>
            <p>Recording why you entered turns the platform into a feedback loop.</p>
          </div>
        </div>
      </div>
    </section>
  </div>

  <footer>
    <span>OrangeVest</span>
    <span>Trade, review, and refine your approach.</span>
  </footer>

  <div id="toast-container"></div>

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
          <label>Email</label>
          <input type="email" id="authEmail" placeholder="you@example.com" />
        </div>
        <div class="modal-field">
          <label>Password</label>
          <input type="password" id="authPassword" placeholder="At least 5 chars" />
        </div>
        <div class="modal-error" id="authError"></div>
        <button class="btn btn-primary" style="width:100%; margin-top:6px;" id="authSubmit">Continue</button>
      </div>
    </div>
  </div>

  <div class="backdrop trade-modal" id="tradeBackdrop">
    <div class="modal">
      <div class="modal-header">
        <h2>Open buy position</h2>
        <button class="modal-close" id="tradeClose">×</button>
      </div>
      <div id="tradeContent">
        <div class="trade-asset" id="tradeAssetLabel"></div>
        <div class="trade-row"><span>Current price</span><span id="tradePrice">0.00</span></div>
        <div class="trade-qty-input">
          <label style="font-size:12px; color:var(--text-muted);">Quantity</label>
          <input type="number" id="tradeQty" min="0.01" step="0.01" value="1" />
          <button data-q="1">1</button>
          <button data-q="10">10</button>
          <button data-q="50">50</button>
        </div>
        <div class="trade-info">Approx. cost: <span id="tradeMargin">0.00</span></div>
        <div class="trade-error" id="tradeError"></div>
        <button class="btn btn-buy-green" style="width:100%; margin-top:6px;" id="tradeSubmit">Confirm buy</button>
      </div>
    </div>
  </div>

  <div class="backdrop trade-modal" id="sellBackdrop">
    <div class="modal">
      <div class="modal-header">
        <h2>Close position</h2>
        <button class="modal-close" id="sellClose">×</button>
      </div>
      <div id="sellContent">
        <div class="trade-asset" id="sellAssetLabel"></div>
        <div class="trade-row"><span>Current price</span><span id="sellPrice">0.00</span></div>
        <div class="trade-row"><span>Total quantity open</span><span id="sellTotalQty">0</span></div>
        <div class="trade-qty-input">
          <label style="font-size:12px; color:var(--text-muted);">Qty to close</label>
          <input type="number" id="sellQty" min="0.01" step="0.01" value="1" />
          <button data-sq="50">50%</button>
          <button data-sq="100">100%</button>
        </div>
        <div class="trade-error" id="sellError"></div>
        <button class="btn btn-sell-red" style="width:100%; margin-top:6px;" id="sellSubmit">Confirm sell</button>
      </div>
    </div>
  </div>

  <div class="backdrop" id="fundsBackdrop">
    <div class="modal">
      <div class="modal-header">
        <h2>Manage funds & currency</h2>
        <button class="modal-close" id="fundsClose">×</button>
      </div>
      <div>
        <div class="modal-field">
          <label>Display currency</label>
          <select id="currencySelect">
            <option value="USD">$ USD</option>
            <option value="EUR">€ EUR</option>
          </select>
        </div>
        <button class="btn btn-primary" style="width:100%; margin-top:8px;" id="fundsSave">Apply</button>
      </div>
    </div>
  </div>

  <script>
    // --- APP CORE & WEBSOCKETS ---
    const BINANCE_REST = "https://api.binance.com";
    const BINANCE_WS = "wss://stream.binance.com:9443/ws/!ticker@arr";

    const MARKETS = [
      { id: "BTCUSDT", name: "Bitcoin", symbol: "BTCUSDT", group: "majors", lastPrice: 0, change24h: 0, candles: [] },
      { id: "ETHUSDT", name: "Ethereum", symbol: "ETHUSDT", group: "majors", lastPrice: 0, change24h: 0, candles: [] },
      { id: "BNBUSDT", name: "BNB", symbol: "BNBUSDT", group: "majors", lastPrice: 0, change24h: 0, candles: [] },
      { id: "SOLUSDT", name: "Solana", symbol: "SOLUSDT", group: "altcoins", lastPrice: 0, change24h: 0, candles: [] },
      { id: "XRPUSDT", name: "XRP", symbol: "XRPUSDT", group: "altcoins", lastPrice: 0, change24h: 0, candles: [] },
      { id: "DOGEUSDT", name: "Dogecoin", symbol: "DOGEUSDT", group: "meme", lastPrice: 0, change24h: 0, candles: [] },
      { id: "LINKUSDT", name: "Chainlink", symbol: "LINKUSDT", group: "defi", lastPrice: 0, change24h: 0, candles: [] },
      { id: "UNIUSDT", name: "Uniswap", symbol: "UNIUSDT", group: "defi", lastPrice: 0, change24h: 0, candles: [] }
    ];

    let appCurrency = "USD";
    const CURRENCY_RATES = { USD: 1, EUR: 0.92 };
    function formatMoney(amountUSD) {
      const val = amountUSD * CURRENCY_RATES[appCurrency];
      return (appCurrency === "EUR" ? "€" : "$") + (val < 1 ? val.toFixed(4) : val.toFixed(2));
    }
    function formatPriceRaw(val) { return val < 1 ? val.toFixed(4) : val.toFixed(2); }

    // --- TOAST NOTIFICATIONS ---
    function showToast(msg, type = 'success') {
      const container = document.getElementById('toast-container');
      const toast = document.createElement('div');
      toast.className = `toast ${type}`;
      toast.innerText = msg;
      container.appendChild(toast);
      setTimeout(() => { toast.style.animation = 'fadeOut 0.3s ease forwards'; setTimeout(() => toast.remove(), 300); }, 3000);
    }

    // --- STATE MANAGEMENT ---
    let mode = "normal"; 
    let testState = null;
    const START_BAL = 10000;

    function loadSession() { try { return JSON.parse(localStorage.getItem("ov_session")); } catch { return null; } }
    function saveSession(s) { if(s) localStorage.setItem("ov_session", JSON.stringify(s)); else localStorage.removeItem("ov_session"); }
    function loadUsers() { try { return JSON.parse(localStorage.getItem("ov_users")) || {}; } catch { return {}; } }
    function saveUsers(u) { localStorage.setItem("ov_users", JSON.stringify(u)); }

    function getCurrentUser() {
      const session = loadSession();
      return session ? loadUsers()[session.email] || null : null;
    }

    function getActiveState() {
      if (mode === "test") {
        if (!testState) testState = { balance: START_BAL, positions: [], history: [] };
        return testState;
      }
      return getCurrentUser();
    }

    function saveActiveState(state) {
      if (mode === "test") testState = state;
      else {
        const users = loadUsers();
        users[state.email] = state;
        saveUsers(users);
      }
      updateUI();
    }

    // --- CHARTING ENGINE (Lightweight Charts) ---
    let tvChart, tvSeries, heroMarketId = "BTCUSDT";

    function initTVChart() {
      const container = document.getElementById('tvChartContainer');
      tvChart = LightweightCharts.createChart(container, {
        width: container.clientWidth, height: 300,
        layout: { background: { type: 'solid', color: 'transparent' }, textColor: '#8a94a7' },
        grid: { vertLines: { color: 'rgba(255,255,255,0.05)' }, horzLines: { color: 'rgba(255,255,255,0.05)' } },
        timeScale: { timeVisible: true }
      });
      tvSeries = tvChart.addCandlestickSeries({
        upColor: '#25d586', downColor: '#ff5c5c', borderVisible: false, wickUpColor: '#25d586', wickDownColor: '#ff5c5c'
      });
      new ResizeObserver(() => tvChart.applyOptions({ width: container.clientWidth })).observe(container);
    }

    async function loadHeroChartData(interval) {
      try {
        const res = await fetch(`${BINANCE_REST}/api/v3/klines?symbol=${heroMarketId}&interval=${interval}&limit=200`);
        const data = await res.json();
        const formatted = data.map(d => ({ time: d[0]/1000, open: parseFloat(d[1]), high: parseFloat(d[2]), low: parseFloat(d[3]), close: parseFloat(d[4]) }));
        tvSeries.setData(formatted);
      } catch (e) { console.error("Chart load failed", e); }
    }

    document.getElementById("heroTimeframeButtons").addEventListener("click", e => {
      if(e.target.tagName !== "BUTTON") return;
      document.querySelectorAll("#heroTimeframeButtons button").forEach(b => b.classList.remove("active"));
      e.target.classList.add("active");
      loadHeroChartData(e.target.dataset.tf);
    });

    // --- SPARKLINE CANVAS ---
    function drawSparkline(canvas, data) {
      if(!canvas || !data || data.length < 2) return;
      const ctx = canvas.getContext("2d");
      const w = canvas.width = canvas.clientWidth, h = canvas.height = canvas.clientHeight;
      ctx.clearRect(0,0,w,h);
      const min = Math.min(...data), max = Math.max(...data), range = max - min || 1;
      const stroke = data[data.length-1] >= data[0] ? "#25d586" : "#ff5c5c";
      
      ctx.lineWidth = 1.5; ctx.strokeStyle = stroke; ctx.beginPath();
      data.forEach((v, i) => ctx[i===0?'moveTo':'lineTo'](i*(w/(data.length-1)), h - ((v-min)/range)*(h*0.8) - h*0.1));
      ctx.stroke();
    }

    // --- LIVE WEBSOCKETS ---
    function initWS() {
      const ws = new WebSocket(BINANCE_WS);
      const indicator = document.getElementById("liveIndicator");
      
      ws.onopen = () => indicator.style.background = "#25d586";
      ws.onclose = () => { indicator.style.background = "var(--danger)"; setTimeout(initWS, 3000); };
      
      ws.onmessage = (e) => {
        const data = JSON.parse(e.data);
        data.forEach(t => {
          const m = MARKETS.find(x => x.id === t.s);
          if(m) { m.lastPrice = parseFloat(t.c); m.change24h = parseFloat(t.P); }
        });
        updateLiveDOM();
      };
    }

    function updateLiveDOM() {
      const heroM = MARKETS.find(m => m.id === heroMarketId);
      document.getElementById("assetPrice").textContent = formatMoney(heroM.lastPrice);
      const chgEl = document.getElementById("assetChange");
      chgEl.textContent = `${heroM.change24h > 0 ? '+' : ''}${heroM.change24h.toFixed(2)}%`;
      chgEl.className = `asset-price-change ${heroM.change24h < 0 ? 'negative' : ''}`;

      // Efficient DOM updates for lists
      MARKETS.forEach(m => {
        document.querySelectorAll(`.price-${m.id}`).forEach(el => el.textContent = formatMoney(m.lastPrice));
        document.querySelectorAll(`.change-${m.id}`).forEach(el => {
          el.textContent = `${m.change24h > 0 ? '+' : ''}${m.change24h.toFixed(2)}%`;
          el.className = `market-change change-${m.id} ${m.change24h < 0 ? 'negative' : 'positive'}`;
        });
      });
      calculateLivePnL();
    }

    // --- TRADING LOGIC ---
    let tradeContext = null;

    window.openTrade = (id) => {
      const state = getActiveState();
      if(!state) return document.getElementById("btnLogin").click();
      tradeContext = MARKETS.find(m => m.id === id);
      document.getElementById("tradeAssetLabel").innerHTML = `Buy <strong>${tradeContext.name}</strong>`;
      document.getElementById("tradePrice").textContent = formatMoney(tradeContext.lastPrice);
      document.getElementById("tradeBackdrop").classList.add("show");
    };

    document.getElementById("tradeSubmit").onclick = () => {
      const state = getActiveState();
      const qty = parseFloat(document.getElementById("tradeQty").value);
      const cost = qty * tradeContext.lastPrice;
      
      if(state.balance < cost) {
        document.getElementById("tradeError").textContent = "Insufficient funds!";
        return;
      }
      
      state.balance -= cost;
      let pos = state.positions.find(p => p.symbol === tradeContext.id);
      if(pos) {
        const totalCost = (pos.qty * pos.entry) + cost;
        pos.qty += qty;
        pos.entry = totalCost / pos.qty;
      } else {
        state.positions.push({ symbol: tradeContext.id, name: tradeContext.name, qty, entry: tradeContext.lastPrice });
      }
      
      document.getElementById("tradeBackdrop").classList.remove("show");
      showToast(`Bought ${qty} ${tradeContext.id} at ${formatMoney(tradeContext.lastPrice)}`);
      saveActiveState(state);
    };

    window.openSell = (id) => {
      const state = getActiveState();
      if(!state) return;
      tradeContext = MARKETS.find(m => m.id === id);
      const pos = state.positions.find(p => p.symbol === id);
      if(!pos) return showToast("No open position for " + id, "error");

      document.getElementById("sellAssetLabel").innerHTML = `Close <strong>${tradeContext.name}</strong>`;
      document.getElementById("sellTotalQty").textContent = pos.qty.toFixed(4);
      document.getElementById("sellQty").value = pos.qty;
      document.getElementById("sellBackdrop").classList.add("show");
    };

    document.getElementById("sellSubmit").onclick = () => {
      const state = getActiveState();
      const qtyToClose = parseFloat(document.getElementById("sellQty").value);
      const posIndex = state.positions.findIndex(p => p.symbol === tradeContext.id);
      const pos = state.positions[posIndex];

      if(qtyToClose > pos.qty) return document.getElementById("sellError").textContent = "Exceeds holding qty!";

      const revenue = qtyToClose * tradeContext.lastPrice;
      const costBasis = qtyToClose * pos.entry;
      const pnl = revenue - costBasis;

      state.balance += revenue;
      pos.qty -= qtyToClose;
      if(pos.qty <= 0.0001) state.positions.splice(posIndex, 1);

      document.getElementById("sellBackdrop").classList.remove("show");
      showToast(`Sold ${qtyToClose} ${tradeContext.id}. P&L: ${formatMoney(pnl)}`, pnl >= 0 ? 'success' : 'error');
      saveActiveState(state);
    };

    function calculateLivePnL() {
      const state = getActiveState();
      if(!state) return;
      
      let floatPnL = 0;
      let currentEquity = state.balance;
      let usedMargin = 0;

      let posHTML = "";
      state.positions.forEach(p => {
        const livePrice = MARKETS.find(m => m.id === p.symbol).lastPrice;
        const currentVal = p.qty * livePrice;
        const entryVal = p.qty * p.entry;
        const pnl = currentVal - entryVal;
        
        floatPnL += pnl;
        currentEquity += currentVal;
        usedMargin += entryVal;

        posHTML += `
          <div class="position-row">
            <div>${p.name}<div class="position-symbol">Avg: ${formatPriceRaw(p.entry)}</div></div>
            <div>${p.qty.toFixed(4)}</div>
            <div style="color:${pnl>=0?'#25d586':'var(--danger)'}">${pnl>0?'+':''}${formatMoney(pnl)}</div>
            <div><button class="pos-sell-btn" onclick="openSell('${p.symbol}')">Sell</button></div>
          </div>
        `;
      });

      document.getElementById("kpiPnL").textContent = `${floatPnL>0?'+':''}${formatMoney(floatPnL)}`;
      document.getElementById("kpiPnLPercent").textContent = "Floating";
      document.getElementById("kpiPnLPercent").className = `kpi-trend ${floatPnL<0?'negative':''}`;
      document.getElementById("kpiBalance").textContent = formatMoney(currentEquity);
      
      document.getElementById("equityValue").textContent = formatMoney(currentEquity);
      document.getElementById("usedMarginValue").textContent = formatMoney(usedMargin);
      document.getElementById("availableMarginValue").textContent = formatMoney(state.balance);

      const risk = currentEquity > 0 ? (usedMargin / currentEquity)*100 : 0;
      document.getElementById("riskUsageLabel").textContent = risk.toFixed(1) + "%";
      document.getElementById("riskUsageFill").style.width = Math.min(risk, 100) + "%";
      
      document.getElementById("positionsList").innerHTML = posHTML || `<div class="position-empty">No open positions.</div>`;
    }

    // --- UI & NAVIGATION RE-WIRING ---
    function updateUI() {
      const state = getActiveState();
      const user = getCurrentUser();

      if(user) {
        document.getElementById("navUser").textContent = user.displayName || user.email;
        document.getElementById("btnLogin").style.display = "none";
        document.getElementById("btnLogout").style.display = "inline";
        document.getElementById("accountTypeLabel").textContent = "Profile connected";
      } else if(mode === "test") {
        document.getElementById("navUser").textContent = "Test Mode";
        document.getElementById("btnLogin").style.display = "inline";
      } else {
        document.getElementById("navUser").textContent = "Guest";
        document.getElementById("btnLogin").style.display = "inline";
        document.getElementById("btnLogout").style.display = "none";
      }

      // Profile Panel
      if(state && mode === "normal") {
        document.getElementById("profileGuestHint").style.display = "none";
        document.getElementById("profileOverviewDetails").style.display = "block";
        document.getElementById("profileDisplayName").textContent = state.displayName || state.email;
        document.getElementById("profileEmail").textContent = state.email;
      }

      renderLists();
      calculateLivePnL();
    }

    function renderLists() {
      // Sidebar top 4
      const sorted = [...MARKETS].sort((a,b) => Math.abs(b.change24h) - Math.abs(a.change24h));
      document.getElementById("marketsList").innerHTML = sorted.slice(0,4).map(m => `
        <div class="market-row">
          <div class="market-name" style="cursor:pointer" onclick="heroMarketId='${m.id}'; document.getElementById('heroAssetName').textContent='${m.name}'; document.getElementById('heroAssetSymbol').textContent='${m.symbol}'; loadHeroChartData('15m');">${m.name}<span class="market-symbol">${m.symbol}</span></div>
          <div class="price-${m.id}" style="font-size:13px">${formatMoney(m.lastPrice)}</div>
          <div class="market-change change-${m.id} ${m.change24h>=0?'positive':'negative'}">${m.change24h.toFixed(2)}%</div>
          <div class="market-actions"><button class="btn btn-buy-green" style="padding:4px 8px;font-size:10px" onclick="openTrade('${m.id}')">Buy</button></div>
        </div>
      `).join("");

      // Main Markets Grid
      document.getElementById("marketsPageGrid").innerHTML = MARKETS.map(m => `
        <div class="market-card">
          <div class="market-card-header">
            <div><div class="market-card-name">${m.name}</div><div class="market-card-symbol">${m.symbol}</div></div>
            <div style="text-align:right">
              <div class="price-${m.id} market-card-price">${formatMoney(m.lastPrice)}</div>
              <div class="change-${m.id} market-card-change ${m.change24h>=0?'positive':'negative'}">${m.change24h.toFixed(2)}%</div>
            </div>
          </div>
          <div class="market-card-chart"><canvas id="spark-${m.id}" class="market-card-canvas"></canvas></div>
          <div class="markets-page-actions">
            <button class="btn btn-buy-green" onclick="openTrade('${m.id}')">Buy</button>
            <button class="btn btn-sell-red" onclick="openSell('${m.id}')">Sell</button>
          </div>
        </div>
      `).join("");
      
      // Draw static sparklines (fetch once)
      MARKETS.forEach(async m => {
        try {
          const res = await fetch(`${BINANCE_REST}/api/v3/klines?symbol=${m.id}&interval=1h&limit=50`);
          const data = await res.json();
          drawSparkline(document.getElementById(`spark-${m.id}`), data.map(d => parseFloat(d[4])));
        } catch(e){}
      });

      // Ticker
      document.getElementById("tickerTrack").innerHTML = MARKETS.map(m => `<div class="ticker-item"><span class="ticker-symbol">${m.symbol}</span><span class="ticker-price price-${m.id}">${formatMoney(m.lastPrice)}</span></div>`).join(" • ") + " • " + MARKETS.map(m => `<div class="ticker-item"><span class="ticker-symbol">${m.symbol}</span><span class="ticker-price price-${m.id}">${formatMoney(m.lastPrice)}</span></div>`).join(" • ");
    }

    // Modal Events
    document.querySelectorAll(".modal-close").forEach(btn => btn.onclick = function() { this.closest('.backdrop').classList.remove('show'); });
    document.getElementById("btnLogin").onclick = () => document.getElementById("authBackdrop").classList.add("show");
    document.getElementById("btnLogout").onclick = () => { saveSession(null); updateUI(); };
    document.getElementById("manageFundsBtn").onclick = () => document.getElementById("fundsBackdrop").classList.add("show");
    document.getElementById("fundsSave").onclick = () => { appCurrency = document.getElementById("currencySelect").value; updateUI(); updateLiveDOM(); document.getElementById("fundsBackdrop").classList.remove("show"); };
    
    // Auth Logic
    document.getElementById("authSubmit").onclick = () => {
      const email = document.getElementById("authEmail").value;
      const pwd = document.getElementById("authPassword").value;
      if(!email || pwd.length < 5) return document.getElementById("authError").textContent = "Invalid info";
      const users = loadUsers();
      if(!users[email]) users[email] = { email, password: pwd, balance: START_BAL, positions: [], history: [] };
      saveUsers(users);
      saveSession({ email });
      document.getElementById("authBackdrop").classList.remove("show");
      updateUI();
    };

    // Mode Toggle
    document.getElementById("modeTestBtn").onclick = () => { mode="test"; document.getElementById("modeNormalBtn").classList.remove("active"); document.getElementById("modeTestBtn").classList.add("active"); updateUI(); };
    document.getElementById("modeNormalBtn").onclick = () => { mode="normal"; document.getElementById("modeTestBtn").classList.remove("active"); document.getElementById("modeNormalBtn").classList.add("active"); updateUI(); };

    // Navigation
    document.querySelectorAll(".nav-links button").forEach(btn => {
      btn.onclick = () => {
        document.querySelectorAll(".section").forEach(s => s.classList.remove("active"));
        document.querySelectorAll(".nav-links button").forEach(b => b.classList.remove("active"));
        document.getElementById(`section-${btn.dataset.section}`).classList.add("active");
        btn.classList.add("active");
      };
    });

    // Boot
    async function boot() {
      initTVChart();
      await fetch(`${BINANCE_REST}/api/v3/ticker/24hr?symbols=${encodeURIComponent(JSON.stringify(MARKETS.map(m=>m.id)))}`)
        .then(r=>r.json()).then(d => {
          d.forEach(t => { const m = MARKETS.find(x => x.id === t.symbol); if(m){ m.lastPrice=parseFloat(t.lastPrice); m.change24h=parseFloat(t.priceChangePercent); }});
        });
      document.getElementById('heroAssetName').textContent = MARKETS[0].name;
      document.getElementById('heroAssetSymbol').textContent = MARKETS[0].symbol;
      updateUI();
      loadHeroChartData("15m");
      initWS();
    }
    boot();
  </script>
</body>
</html>
