<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>OrangeVest | Pro Trading Terminal</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <script src="https://unpkg.com/lightweight-charts/dist/lightweight-charts.standalone.production.js"></script>
  <style>
    /* --- PROFESSIONAL EXCHANGE THEME --- */
    :root {
      --bg-base: #0b0e11;
      --bg-panel: #181a20;
      --bg-hover: #2b3139;
      --border: #2b3139;
      --text-main: #eaecef;
      --text-muted: #848e9c;
      --up: #0ecb81;
      --up-bg: rgba(14, 203, 129, 0.1);
      --down: #f6465d;
      --down-bg: rgba(246, 70, 93, 0.1);
      --accent: #fcd535;
      --accent-dark: #c9a92a;
    }

    * { box-sizing: border-box; margin: 0; padding: 0; font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif; }
    
    body { background-color: var(--bg-base); color: var(--text-main); height: 100vh; display: flex; flex-direction: column; overflow: hidden; }
    
    /* Scrollbars */
    ::-webkit-scrollbar { width: 4px; height: 4px; }
    ::-webkit-scrollbar-track { background: var(--bg-base); }
    ::-webkit-scrollbar-thumb { background: var(--border); border-radius: 4px; }
    ::-webkit-scrollbar-thumb:hover { background: var(--text-muted); }

    /* --- TOP NAVBAR --- */
    header { height: 56px; background-color: var(--bg-panel); border-bottom: 1px solid var(--border); display: flex; align-items: center; justify-content: space-between; padding: 0 16px; flex-shrink: 0; }
    .brand { display: flex; align-items: center; gap: 8px; font-weight: 700; font-size: 18px; color: var(--accent); }
    .brand-icon { width: 24px; height: 24px; background: linear-gradient(135deg, var(--accent), #ff9f43); border-radius: 4px; }
    .nav-links { display: flex; gap: 20px; font-size: 14px; font-weight: 500; }
    .nav-links a { color: var(--text-muted); text-decoration: none; cursor: pointer; transition: 0.2s; }
    .nav-links a:hover, .nav-links a.active { color: var(--text-main); }
    .account-info { display: flex; align-items: center; gap: 16px; font-size: 14px; }
    .btn-reset { background: var(--border); border: none; color: var(--text-main); padding: 6px 12px; border-radius: 4px; cursor: pointer; font-weight: 500; }
    .btn-reset:hover { background: var(--text-muted); }

    /* --- MAIN LAYOUT GRID --- */
    .terminal-layout { display: grid; grid-template-columns: 280px 1fr 300px; grid-template-rows: 1fr 250px; height: calc(100vh - 56px); gap: 1px; background-color: var(--border); }
    .panel { background-color: var(--bg-panel); display: flex; flex-direction: column; overflow: hidden; }
    
    /* --- LEFT: MARKETS --- */
    .market-list-panel { grid-column: 1; grid-row: 1 / 3; }
    .panel-header { padding: 12px 16px; font-size: 14px; font-weight: 600; border-bottom: 1px solid var(--border); display: flex; justify-content: space-between; align-items: center; flex-shrink: 0;}
    .search-bar { padding: 8px 16px; border-bottom: 1px solid var(--border); }
    .search-bar input { width: 100%; background: var(--bg-base); border: 1px solid var(--border); color: var(--text-main); padding: 6px 10px; border-radius: 4px; outline: none; }
    .search-bar input:focus { border-color: var(--accent); }
    .market-table { flex: 1; overflow-y: auto; }
    .market-row { display: grid; grid-template-columns: 1fr 1fr 1fr; padding: 8px 16px; font-size: 12px; cursor: pointer; border-bottom: 1px solid rgba(255,255,255,0.02); }
    .market-row:hover, .market-row.active { background-color: var(--bg-hover); }
    .market-symbol { font-weight: 600; }
    .market-price { text-align: right; font-variant-numeric: tabular-nums; }
    .market-change { text-align: right; font-weight: 500; }
    .up { color: var(--up); }
    .down { color: var(--down); }

    /* --- CENTER: CHART --- */
    .chart-panel { grid-column: 2; grid-row: 1; display: flex; flex-direction: column; }
    .ticker-header { display: flex; align-items: center; gap: 24px; padding: 12px 16px; border-bottom: 1px solid var(--border); flex-shrink: 0; }
    .ticker-main { display: flex; flex-direction: column; }
    .ticker-title { font-size: 20px; font-weight: 700; }
    .ticker-link { font-size: 12px; color: var(--text-muted); text-decoration: underline; cursor: pointer; }
    .ticker-stat { display: flex; flex-direction: column; gap: 2px; }
    .ticker-stat-label { font-size: 11px; color: var(--text-muted); }
    .ticker-stat-value { font-size: 14px; font-weight: 500; font-variant-numeric: tabular-nums; }
    
    .chart-controls { padding: 8px 16px; border-bottom: 1px solid var(--border); display: flex; gap: 8px; flex-shrink: 0; }
    .tf-btn { background: transparent; border: none; color: var(--text-muted); font-size: 12px; cursor: pointer; padding: 4px 8px; border-radius: 4px; }
    .tf-btn:hover { color: var(--text-main); }
    .tf-btn.active { background: var(--bg-hover); color: var(--accent); }
    
    #tvchart { flex: 1; width: 100%; height: 100%; }

    /* --- RIGHT: ORDER ENTRY & BOOK --- */
    .order-panel { grid-column: 3; grid-row: 1 / 3; display: flex; flex-direction: column; border-left: 1px solid var(--border); }
    
    /* Order Book Simulation */
    .order-book { flex: 1; display: flex; flex-direction: column; overflow: hidden; border-bottom: 1px solid var(--border); }
    .ob-header { display: grid; grid-template-columns: 1fr 1fr 1fr; padding: 8px 16px; font-size: 11px; color: var(--text-muted); }
    .ob-rows { flex: 1; overflow: hidden; display: flex; flex-direction: column; justify-content: space-around; font-size: 12px; font-variant-numeric: tabular-nums;}
    .ob-row { display: grid; grid-template-columns: 1fr 1fr 1fr; padding: 2px 16px; position: relative; cursor: pointer; }
    .ob-row:hover { background-color: var(--bg-hover); }
    .ob-bg { position: absolute; right: 0; top: 0; height: 100%; opacity: 0.15; z-index: 0; }
    .ob-bg.ask { background-color: var(--down); }
    .ob-bg.bid { background-color: var(--up); }
    .ob-val { z-index: 1; }
    .ob-price.ask { color: var(--down); }
    .ob-price.bid { color: var(--up); }
    .ob-mid { text-align: center; padding: 8px 0; font-size: 16px; font-weight: 600; border-top: 1px solid var(--bg-hover); border-bottom: 1px solid var(--bg-hover); }

    /* Order Entry Form */
    .order-entry { padding: 16px; flex-shrink: 0; }
    .oe-tabs { display: flex; margin-bottom: 16px; border-bottom: 1px solid var(--border); }
    .oe-tab { flex: 1; text-align: center; padding: 8px; font-size: 14px; font-weight: 600; color: var(--text-muted); cursor: pointer; border-bottom: 2px solid transparent; }
    .oe-tab.active { color: var(--accent); border-bottom-color: var(--accent); }
    
    .input-group { background: var(--bg-base); border: 1px solid var(--border); border-radius: 4px; display: flex; align-items: center; padding: 0 12px; margin-bottom: 12px; height: 40px; }
    .input-group label { color: var(--text-muted); font-size: 12px; width: 50px; }
    .input-group input { flex: 1; background: transparent; border: none; color: var(--text-main); font-size: 14px; text-align: right; outline: none; font-variant-numeric: tabular-nums; }
    .input-group span { color: var(--text-main); font-size: 12px; margin-left: 8px; }
    
    .slider-container { display: flex; justify-content: space-between; margin-bottom: 16px; }
    .slider-dot { width: 22%; height: 6px; background: var(--bg-hover); cursor: pointer; border-radius: 2px; }
    .slider-dot:hover { background: var(--border); }
    
    .action-btns { display: flex; gap: 8px; }
    .btn-buy, .btn-sell { flex: 1; height: 40px; border: none; border-radius: 4px; font-size: 14px; font-weight: 600; color: #fff; cursor: pointer; transition: 0.2s; }
    .btn-buy { background-color: var(--up); }
    .btn-buy:hover { background-color: #12e092; }
    .btn-sell { background-color: var(--down); }
    .btn-sell:hover { background-color: #ff5b71; }
    .oe-avail { font-size: 12px; color: var(--text-muted); margin-bottom: 12px; display: flex; justify-content: space-between;}

    /* --- BOTTOM: PORTFOLIO --- */
    .portfolio-panel { grid-column: 2; grid-row: 2; border-top: 1px solid var(--border); }
    .port-tabs { display: flex; border-bottom: 1px solid var(--border); }
    .port-tab { padding: 10px 16px; font-size: 13px; font-weight: 500; color: var(--text-muted); cursor: pointer; }
    .port-tab.active { color: var(--accent); border-top: 2px solid var(--accent); background: var(--bg-base); }
    
    .port-table-wrap { height: calc(100% - 40px); overflow-y: auto; }
    .port-table { width: 100%; border-collapse: collapse; font-size: 12px; text-align: right; }
    .port-table th { color: var(--text-muted); font-weight: 400; padding: 8px 16px; border-bottom: 1px solid var(--border); position: sticky; top: 0; background: var(--bg-panel); }
    .port-table td { padding: 10px 16px; border-bottom: 1px solid rgba(255,255,255,0.02); font-variant-numeric: tabular-nums; }
    .port-table th:first-child, .port-table td:first-child { text-align: left; }
    .action-close { background: var(--bg-hover); color: var(--text-main); border: none; padding: 4px 12px; border-radius: 4px; cursor: pointer; font-size: 11px; }
    .action-close:hover { background: var(--border); }

    /* --- RESPONSIVE --- */
    @media (max-width: 1200px) {
      .terminal-layout { grid-template-columns: 250px 1fr; grid-template-rows: 1fr 250px 400px; }
      .order-panel { grid-column: 1 / 3; grid-row: 3; border-left: none; border-top: 1px solid var(--border); flex-direction: row; }
      .order-book { width: 50%; border-right: 1px solid var(--border); border-bottom: none; }
      .order-entry { width: 50%; }
    }
    @media (max-width: 768px) {
      .terminal-layout { display: flex; flex-direction: column; height: auto; overflow-y: auto; }
      .market-list-panel { height: 300px; }
      .chart-panel { height: 400px; }
      .order-panel { flex-direction: column; height: auto; }
      .order-book { width: 100%; height: 300px; border-right: none; border-bottom: 1px solid var(--border); }
      .order-entry { width: 100%; }
      .portfolio-panel { height: 300px; }
      body { overflow-y: auto; }
    }
  </style>
</head>
<body>

  <header>
    <div class="brand">
      <div class="brand-icon"></div>
      OrangeVest Pro
    </div>
    <div class="nav-links">
      <a class="active">Markets</a>
      <a href="https://www.binance.com/en/trade/BTC_USDT" target="_blank">Binance Live</a>
      <a href="https://www.tradingview.com/" target="_blank">TradingView</a>
    </div>
    <div class="account-info">
      <span style="color: var(--text-muted)">Equity:</span>
      <strong id="headerEquity" style="color: var(--accent); font-size: 16px; font-variant-numeric: tabular-nums;">$100,000.00</strong>
      <button class="btn-reset" onclick="resetAccount()">Reset</button>
    </div>
  </header>

  <div class="terminal-layout">
    
    <aside class="panel market-list-panel">
      <div class="panel-header">Markets</div>
      <div class="search-bar">
        <input type="text" id="marketSearch" placeholder="Search pairs..." onkeyup="filterMarkets()">
      </div>
      <div class="ob-header" style="border-bottom: 1px solid var(--border)">
        <span>Pair</span>
        <span style="text-align:right">Price</span>
        <span style="text-align:right">Change</span>
      </div>
      <div class="market-table" id="marketList">
        </div>
    </aside>

    <main class="panel chart-panel">
      <div class="ticker-header">
        <div class="ticker-main">
          <span class="ticker-title" id="chartTitle">BTCUSDT</span>
          <a class="ticker-link" id="chartLink" target="_blank">View on Binance ↗</a>
        </div>
        <div class="ticker-stat">
          <span class="ticker-stat-label">Last Price</span>
          <span class="ticker-stat-value up" id="chartPrice">0.00</span>
        </div>
        <div class="ticker-stat">
          <span class="ticker-stat-label">24h Change</span>
          <span class="ticker-stat-value" id="chartChange">0.00%</span>
        </div>
        <div class="ticker-stat">
          <span class="ticker-stat-label">24h High</span>
          <span class="ticker-stat-value" id="chartHigh">0.00</span>
        </div>
        <div class="ticker-stat">
          <span class="ticker-stat-label">24h Low</span>
          <span class="ticker-stat-value" id="chartLow">0.00</span>
        </div>
      </div>
      <div class="chart-controls" id="timeframes">
        <button class="tf-btn" data-tf="1m">1m</button>
        <button class="tf-btn active" data-tf="15m">15m</button>
        <button class="tf-btn" data-tf="1h">1H</button>
        <button class="tf-btn" data-tf="4h">4H</button>
        <button class="tf-btn" data-tf="1d">1D</button>
      </div>
      <div id="tvchart"></div>
    </main>

    <aside class="panel order-panel">
      <div class="order-book">
        <div class="panel-header">Order Book</div>
        <div class="ob-header">
          <span>Price(USDT)</span>
          <span style="text-align:right">Amount</span>
          <span style="text-align:right">Total</span>
        </div>
        
        <div class="ob-rows" id="obAsks"></div>
        
        <div class="ob-mid" id="obMidPrice">
          <span class="up">0.00</span>
        </div>
        
        <div class="ob-rows" id="obBids"></div>
      </div>

      <div class="order-entry">
        <div class="oe-tabs">
          <div class="oe-tab active">Market</div>
          <div class="oe-tab" style="cursor:not-allowed; opacity:0.5" title="Limit orders coming soon">Limit</div>
        </div>
        
        <div class="oe-avail">
          <span>Avail:</span>
          <strong id="oeAvailBal" style="color:var(--text-main)">100000.00 USDT</strong>
        </div>

        <div class="input-group">
          <label>Price</label>
          <input type="text" value="Market" disabled style="color:var(--text-muted)">
          <span>USDT</span>
        </div>

        <div class="input-group">
          <label>Amount</label>
          <input type="number" id="oeQty" placeholder="0.00" step="0.001">
          <span id="oeBaseSymbol">BTC</span>
        </div>

        <div class="slider-container">
          <div class="slider-dot" onclick="setQtyPct(0.25)"></div>
          <div class="slider-dot" onclick="setQtyPct(0.50)"></div>
          <div class="slider-dot" onclick="setQtyPct(0.75)"></div>
          <div class="slider-dot" onclick="setQtyPct(1.00)"></div>
        </div>

        <div class="action-btns">
          <button class="btn-buy" onclick="executeTrade('BUY')">Buy <span class="base-sym">BTC</span></button>
          <button class="btn-sell" onclick="executeTrade('SELL')">Sell <span class="base-sym">BTC</span></button>
        </div>
      </div>
    </aside>

    <footer class="panel portfolio-panel">
      <div class="port-tabs">
        <div class="port-tab active">Open Positions (<span id="posCount">0</span>)</div>
      </div>
      <div class="port-table-wrap">
        <table class="port-table">
          <thead>
            <tr>
              <th>Symbol</th>
              <th>Size</th>
              <th>Entry Price</th>
              <th>Mark Price</th>
              <th>Margin</th>
              <th>Unrealized PNL</th>
              <th>Action</th>
            </tr>
          </thead>
          <tbody id="portfolioBody">
            <tr><td colspan="7" style="text-align:center; color:var(--text-muted); padding: 30px;">No open positions</td></tr>
          </tbody>
        </table>
      </div>
    </footer>

  </div>

  <script>
    // --- APP CONFIG & STATE ---
    const BINANCE_REST = "https://api.binance.com";
    const BINANCE_WS = "wss://stream.binance.com:9443/ws/!ticker@arr";
    
    // Top volume Binance Pairs
    let MARKETS = [
      { s: "BTCUSDT", b: "BTC", p: 0, c: 0, h: 0, l: 0 },
      { s: "ETHUSDT", b: "ETH", p: 0, c: 0, h: 0, l: 0 },
      { s: "SOLUSDT", b: "SOL", p: 0, c: 0, h: 0, l: 0 },
      { s: "BNBUSDT", b: "BNB", p: 0, c: 0, h: 0, l: 0 },
      { s: "XRPUSDT", b: "XRP", p: 0, c: 0, h: 0, l: 0 },
      { s: "DOGEUSDT", b: "DOGE", p: 0, c: 0, h: 0, l: 0 },
      { s: "ADAUSDT", b: "ADA", p: 0, c: 0, h: 0, l: 0 },
      { s: "AVAXUSDT", b: "AVAX", p: 0, c: 0, h: 0, l: 0 },
      { s: "LINKUSDT", b: "LINK", p: 0, c: 0, h: 0, l: 0 },
      { s: "MATICUSDT", b: "MATIC", p: 0, c: 0, h: 0, l: 0 },
      { s: "SHIBUSDT", b: "SHIB", p: 0, c: 0, h: 0, l: 0 },
      { s: "LTCUSDT", b: "LTC", p: 0, c: 0, h: 0, l: 0 }
    ];

    let activeSymbol = "BTCUSDT";
    let activeBase = "BTC";
    let activePrice = 0;
    
    // Portfolio State
    let balance = parseFloat(localStorage.getItem('ov_balance')) || 100000.00;
    let positions = JSON.parse(localStorage.getItem('ov_positions')) || [];

    // --- UTILS ---
    const formatNum = (num, dec = 2) => num.toLocaleString('en-US', { minimumFractionDigits: dec, maximumFractionDigits: dec });
    const getDecimals = (price) => price < 1 ? 4 : (price < 10 ? 3 : 2);

    function saveState() {
      localStorage.setItem('ov_balance', balance);
      localStorage.setItem('ov_positions', JSON.stringify(positions));
    }

    // --- TRADINGVIEW CHART ---
    let chart, candleSeries;
    let currentCandle = null;

    function initChart() {
      const container = document.getElementById('tvchart');
      chart = LightweightCharts.createChart(container, {
        layout: { background: { type: 'solid', color: 'transparent' }, textColor: '#848e9c' },
        grid: { vertLines: { color: '#2b3139' }, horzLines: { color: '#2b3139' } },
        crosshair: { mode: LightweightCharts.CrosshairMode.Normal },
        rightPriceScale: { borderColor: '#2b3139' },
        timeScale: { borderColor: '#2b3139', timeVisible: true }
      });
      candleSeries = chart.addCandlestickSeries({
        upColor: '#0ecb81', downColor: '#f6465d', borderVisible: false, wickUpColor: '#0ecb81', wickDownColor: '#f6465d'
      });
      new ResizeObserver(() => chart.applyOptions({ width: container.clientWidth, height: container.clientHeight })).observe(container);
    }

    async function loadChartData(interval) {
      try {
        const res = await fetch(`${BINANCE_REST}/api/v3/klines?symbol=${activeSymbol}&interval=${interval}&limit=300`);
        const data = await res.json();
        const formatted = data.map(d => ({
          time: d[0] / 1000, open: parseFloat(d[1]), high: parseFloat(d[2]), low: parseFloat(d[3]), close: parseFloat(d[4])
        }));
        candleSeries.setData(formatted);
        currentCandle = formatted[formatted.length - 1];
      } catch (e) { console.error("Chart load error", e); }
    }

    document.getElementById('timeframes').addEventListener('click', (e) => {
      if(e.target.classList.contains('tf-btn')) {
        document.querySelectorAll('.tf-btn').forEach(b => b.classList.remove('active'));
        e.target.classList.add('active');
        loadChartData(e.target.dataset.tf);
      }
    });

    // --- WEBSOCKET ENGINE (Live Ticker & Chart Ticking) ---
    function initWS() {
      const ws = new WebSocket(BINANCE_WS);
      ws.onmessage = (e) => {
        const data = JSON.parse(e.data);
        let updateUI = false;

        data.forEach(t => {
          const m = MARKETS.find(x => x.s === t.s);
          if (m) {
            m.p = parseFloat(t.c); // Last price
            m.c = parseFloat(t.P); // Price change %
            m.h = parseFloat(t.h); // High
            m.l = parseFloat(t.l); // Low
            updateUI = true;
            
            // If this is the active asset, update chart & header
            if (m.s === activeSymbol) {
              activePrice = m.p;
              updateActiveHeader(m);
              tickChart(m.p);
              renderOrderBook(m.p);
            }
          }
        });

        if (updateUI) {
          renderMarketList();
          renderPortfolio();
        }
      };
      ws.onclose = () => setTimeout(initWS, 2000); // Reconnect
    }

    function tickChart(price) {
      if (!currentCandle) return;
      // Update the current live candle (creates the flashing chart effect)
      currentCandle.close = price;
      if (price > currentCandle.high) currentCandle.high = price;
      if (price < currentCandle.low) currentCandle.low = price;
      candleSeries.update(currentCandle);
    }

    // --- UI RENDERING ---
    function updateActiveHeader(m) {
      const dec = getDecimals(m.p);
      const priceEl = document.getElementById('chartPrice');
      priceEl.innerText = m.p.toFixed(dec);
      priceEl.className = `ticker-stat-value ${m.c >= 0 ? 'up' : 'down'}`;
      
      document.getElementById('chartChange').innerText = `${m.c > 0 ? '+' : ''}${m.c.toFixed(2)}%`;
      document.getElementById('chartChange').className = `ticker-stat-value ${m.c >= 0 ? 'up' : 'down'}`;
      
      document.getElementById('chartHigh').innerText = m.h.toFixed(dec);
      document.getElementById('chartLow').innerText = m.l.toFixed(dec);
      
      document.getElementById('obMidPrice').innerHTML = `<span class="${m.c >= 0 ? 'up' : 'down'}">${m.p.toFixed(dec)}</span>`;
    }

    function renderMarketList() {
      const filter = document.getElementById('marketSearch').value.toUpperCase();
      const html = MARKETS.filter(m => m.s.includes(filter)).map(m => {
        const dec = getDecimals(m.p);
        return `
        <div class="market-row ${m.s === activeSymbol ? 'active' : ''}" onclick="switchMarket('${m.s}', '${m.b}')">
          <div class="market-symbol">${m.b}</div>
          <div class="market-price">${m.p.toFixed(dec)}</div>
          <div class="market-change ${m.c >= 0 ? 'up' : 'down'}">${m.c > 0 ? '+' : ''}${m.c.toFixed(2)}%</div>
        </div>
      `}).join('');
      document.getElementById('marketList').innerHTML = html;
    }

    window.switchMarket = function(symbol, base) {
      activeSymbol = symbol;
      activeBase = base;
      document.getElementById('chartTitle').innerText = symbol;
      document.getElementById('chartLink').href = `https://www.binance.com/en/trade/${base}_USDT`;
      document.getElementById('oeBaseSymbol').innerText = base;
      document.querySelectorAll('.base-sym').forEach(el => el.innerText = base);
      document.getElementById('oeQty').value = '';
      
      const tf = document.querySelector('.tf-btn.active').dataset.tf;
      loadChartData(tf);
      renderMarketList();
    };

    window.filterMarkets = () => renderMarketList();

    // --- ORDER BOOK SIMULATION ---
    // Instead of complex REST calls, we generate a realistic spread around the live price.
    function generateOBRows(midPrice, type) {
      const rows = [];
      const dec = getDecimals(midPrice);
      const step = midPrice * 0.0005; // 0.05% spread steps
      let currentPrice = type === 'ask' ? midPrice + step : midPrice - step;
      let totalAmount = 0;

      for (let i = 0; i < 9; i++) {
        const amount = (Math.random() * (1000 / midPrice) + (10 / midPrice)); // Random size
        totalAmount += amount;
        rows.push({ p: currentPrice, a: amount, t: totalAmount });
        currentPrice = type === 'ask' ? currentPrice + (Math.random() * step) : currentPrice - (Math.random() * step);
      }
      return type === 'ask' ? rows.reverse() : rows;
    }

    function renderOrderBook(price) {
      const dec = getDecimals(price);
      const asks = generateOBRows(price, 'ask');
      const bids = generateOBRows(price, 'bid');
      const maxTotal = Math.max(asks[0].t, bids[bids.length-1].t);

      const renderRow = (r, type) => {
        const pct = (r.t / maxTotal) * 100;
        return `
          <div class="ob-row" onclick="document.getElementById('oeQty').value='${(balance/r.p).toFixed(4)}'">
            <div class="ob-bg ${type}" style="width: ${pct}%"></div>
            <div class="ob-val ob-price ${type}">${r.p.toFixed(dec)}</div>
            <div class="ob-val" style="text-align:right">${r.a.toFixed(4)}</div>
            <div class="ob-val" style="text-align:right">${r.t.toFixed(4)}</div>
          </div>
        `;
      };

      document.getElementById('obAsks').innerHTML = asks.map(r => renderRow(r, 'ask')).join('');
      document.getElementById('obBids').innerHTML = bids.map(r => renderRow(r, 'bid')).join('');
    }

    // --- TRADING EXECUTION ---
    window.setQtyPct = (pct) => {
      if(!activePrice) return;
      const maxQty = balance / activePrice;
      document.getElementById('oeQty').value = (maxQty * pct).toFixed(4);
    };

    window.executeTrade = (side) => {
      const qtyStr = document.getElementById('oeQty').value;
      if (!qtyStr || isNaN(qtyStr) || qtyStr <= 0) return alert('Enter a valid quantity.');
      const qty = parseFloat(qtyStr);
      
      if (side === 'BUY') {
        const cost = qty * activePrice;
        if (cost > balance) return alert('Insufficient USDT balance.');
        
        balance -= cost;
        let pos = positions.find(p => p.sym === activeSymbol);
        if (pos) {
          // Average entry math
          const totalCost = (pos.qty * pos.entry) + cost;
          pos.qty += qty;
          pos.entry = totalCost / pos.qty;
        } else {
          positions.push({ sym: activeSymbol, base: activeBase, qty: qty, entry: activePrice });
        }
      } else if (side === 'SELL') {
        const posIndex = positions.findIndex(p => p.sym === activeSymbol);
        if (posIndex === -1 || positions[posIndex].qty < qty) return alert(`Insufficient ${activeBase} balance. Open a Long position first.`);
        
        const pos = positions[posIndex];
        const revenue = qty * activePrice;
        balance += revenue; // realized
        
        pos.qty -= qty;
        if (pos.qty <= 0.000001) positions.splice(posIndex, 1);
      }

      document.getElementById('oeQty').value = '';
      saveState();
      renderPortfolio();
    };

    window.closePosition = (sym) => {
      const posIndex = positions.findIndex(p => p.sym === sym);
      if (posIndex === -1) return;
      const pos = positions[posIndex];
      const liveMarket = MARKETS.find(m => m.s === sym);
      if(!liveMarket) return;

      const revenue = pos.qty * liveMarket.p;
      balance += revenue;
      positions.splice(posIndex, 1);
      
      saveState();
      renderPortfolio();
    };

    window.resetAccount = () => {
      if(confirm("Reset account to $100,000 USD? All positions will be wiped.")) {
        balance = 100000.00;
        positions = [];
        saveState();
        renderPortfolio();
      }
    };

    // --- PORTFOLIO RENDERING ---
    function renderPortfolio() {
      document.getElementById('oeAvailBal').innerText = `${formatNum(balance)} USDT`;
      
      let floatPnl = 0;
      let totalEquity = balance;
      let usedMargin = 0;

      const html = positions.map(p => {
        const liveMarket = MARKETS.find(m => m.s === p.sym);
        const liveP = liveMarket ? liveMarket.p : p.entry;
        const currentVal = p.qty * liveP;
        const entryVal = p.qty * p.entry;
        const pnl = currentVal - entryVal;
        const pnlPct = (pnl / entryVal) * 100;
        
        floatPnl += pnl;
        totalEquity += currentVal;
        usedMargin += entryVal;

        const dec = getDecimals(liveP);

        return `
          <tr>
            <td style="font-weight:600">${p.sym}</td>
            <td>${p.qty.toFixed(4)} ${p.base}</td>
            <td>${p.entry.toFixed(dec)}</td>
            <td style="color:var(--accent)">${liveP.toFixed(dec)}</td>
            <td>${formatNum(entryVal)}</td>
            <td class="${pnl >= 0 ? 'up' : 'down'}">${pnl > 0 ? '+' : ''}${formatNum(pnl)} (${pnlPct.toFixed(2)}%)</td>
            <td><button class="action-close" onclick="closePosition('${p.sym}')">Close</button></td>
          </tr>
        `;
      }).join('');

      document.getElementById('portfolioBody').innerHTML = positions.length ? html : `<tr><td colspan="7" style="text-align:center; color:var(--text-muted); padding: 30px;">No open positions</td></tr>`;
      document.getElementById('posCount').innerText = positions.length;
      document.getElementById('headerEquity').innerText = `$${formatNum(totalEquity)}`;
    }

    // --- BOOTSTRAP ---
    initChart();
    renderMarketList();
    renderPortfolio();
    
    // Initial fetch to paint the board before WS connects
    fetch(`${BINANCE_REST}/api/v3/ticker/24hr?symbols=["BTCUSDT","ETHUSDT","SOLUSDT","BNBUSDT","XRPUSDT","DOGEUSDT","ADAUSDT","AVAXUSDT","LINKUSDT","MATICUSDT","SHIBUSDT","LTCUSDT"]`)
      .then(r => r.json()).then(data => {
        data.forEach(t => {
          const m = MARKETS.find(x => x.s === t.symbol);
          if (m) { m.p = parseFloat(t.lastPrice); m.c = parseFloat(t.priceChangePercent); m.h = parseFloat(t.highPrice); m.l = parseFloat(t.lowPrice); }
        });
        activePrice = MARKETS[0].p;
        updateActiveHeader(MARKETS[0]);
        renderMarketList();
        renderOrderBook(activePrice);
        loadChartData('15m');
        initWS(); // Connect live stream
      });

  </script>
</body>
</html>
