<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>OrangeVest – Advanced Online Trading Platform</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <script src="https://unpkg.com/lightweight-charts/dist/lightweight-charts.standalone.production.js"></script>
  <style>
    :root {
      --bg-dark: #060b10;
      --bg-card: #0d151f;
      --accent: #ff9f43;
      --accent-soft: rgba(255, 159, 67, 0.15);
      --accent-strong: #ffb257;
      --danger: #ff5c5c;
      --success: #25d586;
      --text-main: #f5f7fb;
      --text-muted: #8a94a7;
      --border-soft: #1a2535;
      --shadow-soft: 0 20px 50px rgba(0, 0, 0, 0.55);
      --radius-lg: 16px;
      --radius-md: 10px;
      --radius-pill: 999px;
    }

    * { box-sizing: border-box; margin: 0; padding: 0; }
    
    /* Custom Scrollbar */
    ::-webkit-scrollbar { width: 6px; height: 6px; }
    ::-webkit-scrollbar-track { background: transparent; }
    ::-webkit-scrollbar-thumb { background: #1a2535; border-radius: 10px; }
    ::-webkit-scrollbar-thumb:hover { background: #2a3545; }

    body {
      font-family: system-ui, -apple-system, sans-serif;
      background: radial-gradient(circle at top, #182a40 0, #060b10 50%, #020408 100%);
      color: var(--text-main);
      min-height: 100vh;
      overflow-x: hidden;
    }

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
      color: inherit; cursor: pointer; transition: 0.2s ease; font-size: 14px;
    }
    .nav-links button:hover { color: var(--text-main); background: rgba(255, 255, 255, 0.04); }
    .nav-links button.active { color: var(--accent); background: var(--accent-soft); }

    .nav-cta { display: flex; gap: 10px; align-items: center; }
    .btn {
      border-radius: var(--radius-pill); padding: 8px 16px; font-size: 13px; border: 1px solid transparent;
      cursor: pointer; background: transparent; color: var(--text-main); transition: 0.2s ease;
      display: inline-flex; align-items: center; justify-content: center; gap: 6px; font-weight: 500;
    }
    .btn-ghost { border-color: var(--border-soft); color: var(--text-muted); }
    .btn-ghost:hover { background: rgba(255, 255, 255, 0.03); color: var(--text-main); }
    .btn-primary { background: linear-gradient(135deg, #ff9f43, #ff6b6b); box-shadow: 0 0 18px rgba(255, 159, 67, 0.4); font-weight: 600; }
    .btn-primary:hover { transform: translateY(-1px); box-shadow: 0 10px 30px rgba(0, 0, 0, 0.6); }
    .btn-text { border: none; background: none; color: var(--text-muted); font-size: 12px; cursor: pointer; }
    .btn-text:hover { color: var(--text-main); }
    
    .btn-buy-green { background: radial-gradient(circle at top left, #27e49b, #16b16b); color: #020309; border: 1px solid rgba(39, 228, 155, 0.8); }
    .btn-sell-red { background: radial-gradient(circle at top left, #ff7a7a, #ff3b3b); color: #fff; border: 1px solid rgba(255, 122, 122, 0.9); }
    .btn-buy-green:hover, .btn-sell-red:hover { transform: translateY(-1px); filter: brightness(1.1); }

    .main-grid { display: grid; grid-template-columns: 1.4fr 1fr; gap: 24px; align-items: flex-start; }
    
    .hero-card {
      background: radial-gradient(circle at top left, rgba(255, 159, 67, 0.08), transparent), linear-gradient(135deg, rgba(17, 25, 39, 0.98), rgba(7, 11, 18, 0.98));
      border-radius: var(--radius-lg); padding: 20px; box-shadow: var(--shadow-soft); border: 1px solid rgba(255, 255, 255, 0.03);
    }
    .hero-header { display: flex; justify-content: space-between; gap: 12px; margin-bottom: 18px; flex-wrap: wrap;}
    .hero-title h1 { font-size: 24px; margin-bottom: 6px; }
    .hero-title p { font-size: 13px; color: var(--text-muted); max-width: 380px;}

    .hero-kpis { display: flex; gap: 10px; font-size: 12px; }
    .kpi { background: rgba(3, 8, 15, 0.8); border-radius: var(--radius-md); border: 1px solid rgba(255, 255, 255, 0.04); padding: 10px 14px; min-width: 140px; }
    .kpi-label { color: var(--text-muted); margin-bottom: 4px; font-size: 11px; text-transform: uppercase; letter-spacing: 0.5px;}
    .kpi-value { font-size: 18px; font-weight: 600; margin-bottom: 2px;}
    .kpi-trend { font-size: 12px; color: var(--success); font-weight: 500;}
    .kpi-trend.negative { color: var(--danger); }

    .chart-card { margin-top: 10px; background: #020307; border-radius: var(--radius-md); padding: 14px; border: 1px solid #171f2a; }
    .chart-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 12px; }
    .asset-name { font-weight: 600; font-size: 16px;}
    .asset-symbol { color: var(--text-muted); font-size: 12px; }
    .asset-price { font-weight: 600; font-size: 18px; margin-right: 8px;}
    .asset-price-change { font-size: 12px; color: var(--success); background: rgba(37, 213, 134, 0.1); padding: 4px 8px; border-radius: var(--radius-pill); }
    .asset-price-change.negative { color: var(--danger); background: rgba(255, 92, 92, 0.1); }
    
    .chart-timeframe { display: flex; gap: 4px; }
    .chart-timeframe button {
      border-radius: 6px; border: none; background: transparent; color: var(--text-muted);
      padding: 4px 10px; cursor: pointer; font-size: 12px; font-weight: 600; transition: 0.2s;
    }
    .chart-timeframe button.active { background: #1a2535; color: var(--text-main); }
    .chart-timeframe button:hover:not(.active) { background: rgba(255,255,255,0.05); }

    .chart-body { height: 350px; width: 100%; position: relative; }

    .side-column { display: flex; flex-direction: column; gap: 16px; }
    .side-card {
      background: linear-gradient(145deg, #050a11, #090f18); border-radius: var(--radius-lg);
      padding: 16px; border: 1px solid rgba(255, 255, 255, 0.03); box-shadow: 0 16px 40px rgba(0, 0, 0, 0.7);
    }
    .side-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 14px; }
    .side-header h2 { font-size: 16px; }
    .side-header span { font-size: 12px; color: var(--text-muted); }

    .markets-list { border-radius: 12px; border: 1px solid rgba(255, 255, 255, 0.04); overflow: hidden; }
    .market-row {
      display: grid; grid-template-columns: 1.2fr 1fr 1fr; align-items: center; padding: 10px;
      background: rgba(7, 11, 20, 0.9); border-bottom: 1px solid rgba(15, 23, 37, 0.9); cursor: pointer; transition: 0.2s;
    }
    .market-row:hover { background: rgba(15, 23, 37, 0.9); }
    .market-name { display: flex; flex-direction: column; gap: 2px; font-size: 13px; font-weight: 500;}
    .market-symbol { font-size: 11px; color: var(--text-muted); }
    .market-change { font-size: 12px; text-align: right; font-weight: 500;}
    .market-change.positive { color: var(--success); }
    .market-change.negative { color: var(--danger); }

    .balance-row { display: flex; justify-content: space-between; margin-bottom: 8px; font-size: 13px;}
    .balance-row span:first-child { color: var(--text-muted); }
    .balance-row span:last-child { font-weight: 600; }
    
    .progress-wrap { margin: 16px 0 12px; }
    .progress-label { display: flex; justify-content: space-between; font-size: 12px; color: var(--text-muted); margin-bottom: 6px; }
    .progress-bar { width: 100%; height: 6px; border-radius: 99px; background: #0f1724; overflow: hidden; }
    .progress-fill { height: 100%; width: 0%; background: linear-gradient(90deg, var(--success), var(--accent)); transition: width 0.4s ease; }

    .positions-list { margin-top: 12px; border-radius: 10px; border: 1px solid rgba(255, 255, 255, 0.04); overflow: hidden; font-size: 12px; }
    .position-row {
      display: grid; grid-template-columns: 1.5fr 1fr 1fr 0.8fr; padding: 10px;
      background: rgba(4, 10, 18, 0.96); border-bottom: 1px solid rgba(11, 18, 30, 0.9); align-items: center;
    }
    .position-row .pnl { font-weight: 600; }
    .position-row .pnl.positive { color: var(--success); }
    .position-row .pnl.negative { color: var(--danger); }
    .pos-sell-btn {
      border-radius: 6px; border: none; background: rgba(255, 92, 92, 0.15); color: var(--danger);
      padding: 6px 12px; cursor: pointer; font-weight: 600; transition: 0.2s; width: 100%;
    }
    .pos-sell-btn:hover { background: var(--danger); color: #fff; }

    .ticker { margin-top: 24px; background: #050910; border-radius: var(--radius-pill); border: 1px solid rgba(255,255,255,0.05); padding: 8px 16px; display: flex; align-items: center; gap: 14px; overflow: hidden; }
    .ticker-label { text-transform: uppercase; font-size: 11px; color: var(--text-muted); border-right: 1px solid rgba(255,255,255,0.1); padding-right: 14px; white-space: nowrap; font-weight: 600;}
    .ticker-track { display: flex; gap: 30px; animation: ticker-scroll 30s linear infinite; white-space: nowrap; }
    .ticker-item { display: inline-flex; gap: 8px; font-size: 13px;}
    .ticker-item .positive { color: var(--success); }
    .ticker-item .negative { color: var(--danger); }

    @keyframes ticker-scroll { 0% { transform: translateX(0); } 100% { transform: translateX(-50%); } }

    /* Modals & Toasts */
    .backdrop { position: fixed; inset: 0; background: rgba(0, 0, 0, 0.75); backdrop-filter: blur(4px); display: none; align-items: center; justify-content: center; z-index: 50; }
    .backdrop.show { display: flex; }
    .modal { background: #0a111a; border-radius: 16px; padding: 24px; width: 90%; max-width: 400px; border: 1px solid rgba(255, 255, 255, 0.1); box-shadow: 0 24px 48px rgba(0,0,0,0.8); }
    .modal-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px; font-size: 18px; font-weight: 600;}
    .modal-close { background: none; border: none; color: var(--text-muted); font-size: 24px; cursor: pointer; }
    .modal-close:hover { color: #fff; }
    
    .trade-input-group { background: #05080c; border: 1px solid #1a2535; border-radius: 8px; padding: 12px; margin-bottom: 16px; }
    .trade-input-group label { display: block; font-size: 12px; color: var(--text-muted); margin-bottom: 8px; }
    .trade-input-group input { width: 100%; background: transparent; border: none; color: #fff; font-size: 20px; font-weight: 600; outline: none; }
    
    /* Toast System */
    #toast-container { position: fixed; bottom: 20px; right: 20px; display: flex; flex-direction: column; gap: 10px; z-index: 100; }
    .toast { background: #0d151f; border-left: 4px solid var(--accent); color: #fff; padding: 16px 20px; border-radius: 8px; box-shadow: 0 8px 24px rgba(0,0,0,0.5); font-size: 14px; animation: slideIn 0.3s ease forwards; min-width: 250px;}
    .toast.success { border-color: var(--success); }
    .toast.error { border-color: var(--danger); }
    @keyframes slideIn { from { transform: translateX(100%); opacity: 0; } to { transform: translateX(0); opacity: 1; } }
    @keyframes fadeOut { to { opacity: 0; transform: translateY(10px); } }

    /* Hide other sections for brevity, focusing on trading */
    .section { display: none; }
    .section.active { display: block; }
  </style>
</head>
<body>
  <div class="page">
    <header>
      <div class="logo">
        <div class="logo-icon"></div>
        <div class="logo-text"><span>OrangeVest</span><span>Pro Simulator</span></div>
      </div>
      <nav>
        <div class="nav-links"><button class="active">Trading Desk</button></div>
        <div class="nav-cta">
          <span id="navUser" class="auth-hint">Guest</span>
          <button id="btnReset" class="btn btn-ghost">Reset Account</button>
        </div>
      </nav>
    </header>

    <section id="section-trading" class="section active">
      <main class="main-grid">
        <div>
          <div class="hero-header">
            <div class="hero-title">
              <h1>Advanced Trading Interface</h1>
              <p>Practice with real-time Binance WebSocket data and professional charting tools.</p>
            </div>
            <div class="hero-kpis">
              <div class="kpi">
                <div class="kpi-label">Available Equity</div>
                <div class="kpi-value" id="kpiEquity">$10,000.00</div>
              </div>
              <div class="kpi">
                <div class="kpi-label">Floating P&L</div>
                <div class="kpi-value" id="kpiPnL">$0.00</div>
                <div class="kpi-trend" id="kpiPnLPercent">0.00%</div>
              </div>
            </div>
          </div>

          <article class="chart-card">
            <div class="chart-header">
              <div>
                <div class="asset-name" id="heroAssetName">Bitcoin</div>
                <div class="asset-symbol" id="heroAssetSymbol">BTCUSDT</div>
              </div>
              <div style="text-align: right;">
                <span class="asset-price" id="assetPrice">...</span>
                <span class="asset-price-change" id="assetChange">...</span>
              </div>
            </div>
            <div class="chart-timeframe" id="heroTimeframeButtons">
              <button data-tf="15m" class="active">15m</button>
              <button data-tf="1h">1H</button>
              <button data-tf="4h">4H</button>
              <button data-tf="1d">1D</button>
            </div>
            <div class="chart-body" id="tvChartContainer"></div>
          </article>
        </div>

        <aside class="side-column">
          <section class="side-card">
            <div class="side-header">
              <h2>Quick Trade</h2>
              <span id="tradeContextSymbol">BTCUSDT</span>
            </div>
            <div class="trade-input-group">
              <label>Amount (Units)</label>
              <input type="number" id="quickTradeQty" value="1" step="0.01" min="0.01">
            </div>
            <div style="display: flex; gap: 10px;">
              <button class="btn btn-buy-green" style="flex: 1; padding: 12px; font-size: 16px;" id="btnBuy">Buy Long</button>
            </div>
          </section>

          <section class="side-card">
            <div class="side-header">
              <h2>Open Positions</h2>
              <span id="activePositionsCount">0 Active</span>
            </div>
            <div class="positions-list" id="positionsList">
              <div style="padding: 16px; text-align: center; color: var(--text-muted);">No open positions.</div>
            </div>
          </section>

          <section class="side-card">
            <div class="side-header">
              <h2>Live Markets</h2>
              <span style="color: var(--success); display:flex; align-items:center; gap:4px;">
                <span style="width:8px;height:8px;background:var(--success);border-radius:50%;display:inline-block;"></span> Live
              </span>
            </div>
            <div class="markets-list" id="marketsList"></div>
          </section>
        </aside>
      </main>

      <section class="ticker">
        <span class="ticker-label">Live Stream</span>
        <div class="ticker-track" id="tickerTrack"></div>
      </section>
    </section>
  </div>

  <div id="toast-container"></div>

  <script>
    // --- 1. CONFIG & STATE ---
    const BINANCE_REST = "https://api.binance.com";
    const BINANCE_WS = "wss://stream.binance.com:9443/ws/!ticker@arr";
    
    let state = {
      balance: 10000,
      positions: [], // { symbol, name, totalQty, avgEntryPrice }
    };

    const MARKETS = [
      { id: "BTCUSDT", name: "Bitcoin", price: 0, change: 0 },
      { id: "ETHUSDT", name: "Ethereum", price: 0, change: 0 },
      { id: "SOLUSDT", name: "Solana", price: 0, change: 0 },
      { id: "BNBUSDT", name: "Binance Coin", price: 0, change: 0 },
      { id: "XRPUSDT", name: "Ripple", price: 0, change: 0 },
      { id: "DOGEUSDT", name: "Dogecoin", price: 0, change: 0 }
    ];

    let activeSymbol = "BTCUSDT";
    let chart, candleSeries;

    // --- 2. UTILS ---
    const formatMoney = (val) => new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD' }).format(val);
    const formatPrice = (val) => val < 1 ? val.toFixed(4) : val.toFixed(2);
    
    function showToast(msg, type = 'success') {
      const container = document.getElementById('toast-container');
      const toast = document.createElement('div');
      toast.className = `toast ${type}`;
      toast.innerText = msg;
      container.appendChild(toast);
      setTimeout(() => { toast.style.animation = 'fadeOut 0.3s ease forwards'; setTimeout(() => toast.remove(), 300); }, 3000);
    }

    // --- 3. TRADINGVIEW CHART SETUP ---
    function initChart() {
      const container = document.getElementById('tvChartContainer');
      chart = LightweightCharts.createChart(container, {
        width: container.clientWidth,
        height: 350,
        layout: { background: { type: 'solid', color: 'transparent' }, textColor: '#8a94a7' },
        grid: { vertLines: { color: '#1a2535' }, horzLines: { color: '#1a2535' } },
        crosshair: { mode: LightweightCharts.CrosshairMode.Normal },
        rightPriceScale: { borderColor: '#1a2535' },
        timeScale: { borderColor: '#1a2535', timeVisible: true }
      });
      candleSeries = chart.addCandlestickSeries({
        upColor: '#25d586', downColor: '#ff5c5c', borderVisible: false, wickUpColor: '#25d586', wickDownColor: '#ff5c5c'
      });

      new ResizeObserver(() => { chart.applyOptions({ width: container.clientWidth }); }).observe(container);
    }

    async function loadChartData(symbol, interval) {
      const res = await fetch(`${BINANCE_REST}/api/v3/klines?symbol=${symbol}&interval=${interval}&limit=500`);
      const data = await res.json();
      const formatted = data.map(d => ({
        time: d[0] / 1000, open: parseFloat(d[1]), high: parseFloat(d[2]), low: parseFloat(d[3]), close: parseFloat(d[4])
      }));
      candleSeries.setData(formatted);
    }

    // --- 4. WEBSOCKETS (LIVE DATA) ---
    function initWebSocket() {
      const ws = new WebSocket(BINANCE_WS);
      ws.onmessage = (event) => {
        const data = JSON.parse(event.data);
        let activeMarketUpdated = false;

        data.forEach(tick => {
          const market = MARKETS.find(m => m.id === tick.s);
          if (market) {
            market.price = parseFloat(tick.c);
            market.change = parseFloat(tick.P);
            if (market.id === activeSymbol) activeMarketUpdated = true;
          }
        });

        updateMarketsSidebar();
        updateTicker();
        updatePortfolio();
        
        if (activeMarketUpdated) {
          const activeM = MARKETS.find(m => m.id === activeSymbol);
          document.getElementById('assetPrice').innerText = formatMoney(activeM.price);
          const changeEl = document.getElementById('assetChange');
          changeEl.innerText = `${activeM.change > 0 ? '+' : ''}${activeM.change.toFixed(2)}%`;
          changeEl.className = `asset-price-change ${activeM.change < 0 ? 'negative' : ''}`;
        }
      };
    }

    // --- 5. TRADING LOGIC ---
    document.getElementById('btnBuy').addEventListener('click', () => {
      const qty = parseFloat(document.getElementById('quickTradeQty').value);
      const market = MARKETS.find(m => m.id === activeSymbol);
      const cost = qty * market.price;

      if (state.balance < cost) return showToast("Insufficient equity!", "error");

      state.balance -= cost;
      
      let pos = state.positions.find(p => p.symbol === market.id);
      if (pos) {
        // Average down/up
        const totalCost = (pos.totalQty * pos.avgEntryPrice) + cost;
        pos.totalQty += qty;
        pos.avgEntryPrice = totalCost / pos.totalQty;
      } else {
        state.positions.push({ symbol: market.id, name: market.name, totalQty: qty, avgEntryPrice: market.price });
      }

      showToast(`Bought ${qty} ${market.id} at ${formatPrice(market.price)}`);
      updatePortfolio();
    });

    window.closePosition = function(symbol) {
      const posIndex = state.positions.findIndex(p => p.symbol === symbol);
      if (posIndex === -1) return;
      const pos = state.positions[posIndex];
      const market = MARKETS.find(m => m.id === symbol);
      
      const revenue = pos.totalQty * market.price;
      const pnl = revenue - (pos.totalQty * pos.avgEntryPrice);
      
      state.balance += revenue;
      state.positions.splice(posIndex, 1);
      
      showToast(`Closed ${symbol}. P&L: ${formatMoney(pnl)}`, pnl >= 0 ? 'success' : 'error');
      updatePortfolio();
    };

    // --- 6. UI UPDATES ---
    function updatePortfolio() {
      let totalFloatingPnL = 0;
      let openPosHTML = '';

      state.positions.forEach(pos => {
        const currentPrice = MARKETS.find(m => m.id === pos.symbol).price;
        const currentVal = pos.totalQty * currentPrice;
        const entryVal = pos.totalQty * pos.avgEntryPrice;
        const pnl = currentVal - entryVal;
        const pnlPct = (pnl / entryVal) * 100;
        
        totalFloatingPnL += pnl;

        openPosHTML += `
          <div class="position-row">
            <div>
              <div style="font-weight:600">${pos.symbol}</div>
              <div style="font-size:10px; color:var(--text-muted)">Avg: ${formatPrice(pos.avgEntryPrice)}</div>
            </div>
            <div>${pos.totalQty.toFixed(4)}</div>
            <div class="pnl ${pnl >= 0 ? 'positive' : 'negative'}">
              ${pnl >= 0 ? '+' : ''}${formatMoney(pnl)} <br>
              <span style="font-size:10px">(${pnlPct.toFixed(2)}%)</span>
            </div>
            <button class="pos-sell-btn" onclick="closePosition('${pos.symbol}')">Close</button>
          </div>
        `;
      });

      document.getElementById('positionsList').innerHTML = openPosHTML || '<div style="padding: 16px; text-align: center; color: var(--text-muted);">No open positions.</div>';
      document.getElementById('activePositionsCount').innerText = `${state.positions.length} Active`;

      document.getElementById('kpiEquity').innerText = formatMoney(state.balance);
      
      const pnlEl = document.getElementById('kpiPnL');
      const pnlPctEl = document.getElementById('kpiPnLPercent');
      
      pnlEl.innerText = `${totalFloatingPnL >= 0 ? '+' : ''}${formatMoney(totalFloatingPnL)}`;
      pnlPctEl.innerText = `Floating`;
      pnlEl.style.color = totalFloatingPnL >= 0 ? 'var(--success)' : 'var(--danger)';
    }

    function updateMarketsSidebar() {
      const html = MARKETS.map(m => `
        <div class="market-row" onclick="changeActiveMarket('${m.id}', '${m.name}')">
          <div class="market-name">${m.name}<span class="market-symbol">${m.id}</span></div>
          <div style="text-align:right">${formatPrice(m.price)}</div>
          <div class="market-change ${m.change >= 0 ? 'positive' : 'negative'}">${m.change > 0 ? '+' : ''}${m.change.toFixed(2)}%</div>
        </div>
      `).join('');
      document.getElementById('marketsList').innerHTML = html;
    }

    function updateTicker() {
      const html = MARKETS.map(m => `
        <div class="ticker-item">
          <strong>${m.id}</strong> ${formatPrice(m.price)} 
          <span class="${m.change >= 0 ? 'positive' : 'negative'}">${m.change > 0 ? '+' : ''}${m.change.toFixed(2)}%</span>
        </div>
      `).join(' • ');
      document.getElementById('tickerTrack').innerHTML = html + ' • ' + html;
    }

    window.changeActiveMarket = function(symbol, name) {
      activeSymbol = symbol;
      document.getElementById('heroAssetName').innerText = name;
      document.getElementById('heroAssetSymbol').innerText = symbol;
      document.getElementById('tradeContextSymbol').innerText = symbol;
      
      // Reset active button
      document.querySelectorAll('#heroTimeframeButtons button').forEach(b => b.classList.remove('active'));
      document.querySelector('#heroTimeframeButtons button[data-tf="15m"]').classList.add('active');
      
      loadChartData(symbol, '15m');
    };

    // Timeframe listeners
    document.querySelectorAll('#heroTimeframeButtons button').forEach(btn => {
      btn.addEventListener('click', (e) => {
        document.querySelectorAll('#heroTimeframeButtons button').forEach(b => b.classList.remove('active'));
        e.target.classList.add('active');
        loadChartData(activeSymbol, e.target.getAttribute('data-tf'));
      });
    });

    document.getElementById('btnReset').addEventListener('click', () => {
      state = { balance: 10000, positions: [] };
      showToast("Account Reset to $10,000");
      updatePortfolio();
    });

    // --- 7. BOOTSTRAP ---
    initChart();
    loadChartData(activeSymbol, '15m');
    initWebSocket();
    updatePortfolio();

  </script>
</body>
</html>
