# Live-Stock-Market-Dashboard

# ⚡ NSE Live Dashboard

<div align="center">

![NSE Live Dashboard](https://img.shields.io/badge/NSE-Live%20Dashboard-7c3aed?style=for-the-badge&logo=lightning&logoColor=white)
![Python](https://img.shields.io/badge/Python-3.8+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-000000?style=for-the-badge&logo=flask&logoColor=white)
![Status](https://img.shields.io/badge/Status-Live-00d4ff?style=for-the-badge)

**Real-time NSE Stock Market Dashboard with Beautiful Analytics & Live Public URL**

[🚀 Live Demo](https://savor-cabdriver-grapple.ngrok-free.dev/) 

</div>

---

## 🌟 Overview

A **production-ready** real-time stock market dashboard that fetches live NSE data and serves it through a stunning web interface. Built with Flask, yfinance, and Chart.js, deployed instantly via ngrok with zero configuration.

### ✨ What Makes This Special?

- 📊 **Real-time Data** - Auto-refreshes every 30 seconds
- 🎨 **Beautiful UI** - Dark-themed, responsive design with gradient accents
- 📈 **Advanced Charts** - Interactive price trends, volume analysis, RSI indicators
- 💼 **10 Major Stocks** - RELIANCE, TCS, HDFC, INFOSYS, and more
- 🔍 **Deep Analytics** - Balance sheets, financials, shareholding patterns
- 🌐 **Instant Deploy** - Get a live public URL in seconds with ngrok
- 📱 **Mobile Friendly** - Responsive design works on all devices

---

## 🎯 Features

### Core Functionality
✅ **Live Stock Prices** - Real-time price updates from NSE  
✅ **Price Trends** - 60-day moving averages (MA-20, MA-50, MA-200)  
✅ **Technical Indicators** - RSI (14), Volume Analysis, 52-week range  
✅ **Key Metrics** - P/E Ratio, P/B Ratio, EPS, Beta, Dividend Yield  
✅ **Market Cap Classification** - Auto-categorized (Large/Mid/Small Cap)  

### Advanced Features
📊 **Financial Statements** - Balance sheet, P&L statements  
👥 **Shareholding Patterns** - Promoter, FII, DII, Public holdings  
💰 **Corporate Actions** - Dividends, splits, bonus shares  
📉 **Volume Analysis** - Color-coded volume bars (60-day history)  
💱 **USD-INR Rates** - Live currency conversion  

### Developer Features
🔌 **RESTful API** - `/api/stock` and `/api/extra` endpoints  
🔄 **Auto-refresh** - Configurable refresh intervals  
🛠️ **Easy Setup** - One-click deploy in Google Colab  
📦 **Minimal Dependencies** - Flask, yfinance, pyngrok, requests  

---

## 🚀 Quick Start

### Option 1: Google Colab (Recommended)

1. **Open the Notebook**  
   [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/yourusername/nse-live-dashboard/blob/main/NSE_LIVE_DASHBOARD_final.ipynb)

2. **Run All Cells**  
   ```
   Runtime → Run all
   ```

3. **Get Your ngrok Token**  
   - Sign up at [ngrok.com](https://ngrok.com) (free)
   - Copy your authtoken from [dashboard](https://dashboard.ngrok.com/get-started/your-authtoken)
   - Paste in Cell 2

4. **Get Your Live URL**  
   Your dashboard will be live at: `https://xxxxx.ngrok-free.dev`

### Option 2: Local Setup

```bash
# Clone the repository
git clone https://github.com/yourusername/nse-live-dashboard.git
cd nse-live-dashboard

# Install dependencies
pip install yfinance flask pyngrok requests

# Set your ngrok token
export NGROK_TOKEN="your_token_here"

# Run the server
python app.py

# In a new terminal, create the tunnel
ngrok http 5050
```

---

## 📖 Documentation

### API Endpoints

#### `GET /api/stock?name=STOCK_NAME`
Returns comprehensive stock data including price, metrics, and charts.

**Response Structure:**
```json
{
  "name": "RELIANCE",
  "price": 1353.3,
  "change": -10.5,
  "change_pct": -0.77,
  "day_high": 1369.8,
  "day_low": 1350.1,
  "prev_close": 1363.8,
  "market_cap_cr": "₹1,843,258 Cr",
  "mcap_class": "Large Cap",
  "pe_ratio": 22.17,
  "pb_ratio": 2.1,
  "eps": 61.44,
  "beta": 0.22,
  "div_yield": "0%",
  "avg_volume": "12.31M",
  "price_trend": [...],
  "volume_data": [...],
  "rsi": {"value": 51, "label": "NEUTRAL"}
}
```

#### `GET /api/extra?name=STOCK_NAME`
Returns additional financial data.

**Response Structure:**
```json
{
  "balance_sheet": {
    "Cash": "₹45,123 Cr",
    "Total Assets": "₹3,45,678 Cr",
    ...
  },
  "financials": {
    "Revenue": "₹6,78,900 Cr",
    "Net Income": "₹56,789 Cr",
    ...
  },
  "shareholding": {
    "Promoters": 50.5,
    "FII": 22.3,
    "DII": 15.1,
    "Public": 12.1
  },
  "corp_actions": [
    {"date": "2024-01-15", "type": "Dividend", "value": "₹6.5"},
    ...
  ]
}
```

### Supported Stocks

| Display Name | NSE Symbol | Sector |
|--------------|------------|--------|
| RELIANCE | RELIANCE.NS | Energy |
| TCS | TCS.NS | IT Services |
| HDFC BANK | HDFCBANK.NS | Banking |
| INFOSYS | INFY.NS | IT Services |
| MOTILAL OSWAL | MOTILALOFS.NS | Financial Services |
| BANK OF BARODA | BANKBARODA.NS | Banking |
| GAIL | GAIL.NS | Oil & Gas |
| VEDANTA | VEDL.NS | Metals & Mining |
| BIRLASOFT | BSOFT.NS | IT Services |
| NMDC | NMDC.NS | Metals & Mining |

### Configuration

**Refresh Interval** (default: 30 seconds)
```javascript
// In the HTML template, find:
setInterval(loadData, 30000); // Change to your desired milliseconds
```

**Add New Stocks**
```python
# In the STOCKS dictionary:
STOCKS = {
    "YOUR STOCK": "SYMBOL.NS",
    # ... existing stocks
}
```

**Change Port**
```python
# In run_flask():
app.run(port=5050, ...)  # Change to your desired port
```

---

## 🎨 UI Components

### Tabs & Sections

1. **Overview Tab** 📊
   - Price trend with 3 moving averages
   - Key metrics grid (PE, PB, EPS, Beta)
   - RSI indicator with visual gauge
   - 52-week range slider
   - Dividend information
   - Volume analysis chart (60-day bars)

2. **Financials Tab** 💰
   - Latest balance sheet items
   - Revenue, expenses, net income
   - Clean tabular layout

3. **Balance Sheet Tab** 📄
   - Total assets, liabilities
   - Cash, inventory, debt
   - Auto-formatted in crores

4. **Shareholding Tab** 👥
   - Interactive doughnut chart
   - Promoter, FII, DII, Public percentages
   - Color-coded legend

5. **Corporate Actions Tab** 🎯
   - Dividend history
   - Stock splits
   - Bonus issues
   - Date, type, value columns

### Design System

**Color Palette:**
```css
--primary: #7c3aed      /* Purple accent */
--secondary: #00d4ff    /* Cyan highlights */
--green: #10b981        /* Positive changes */
--red: #ef4444          /* Negative changes */
--bg: #0b1120           /* Dark background */
--panel: #111827        /* Panel background */
--text: #f9fafb         /* Primary text */
--muted: #9ca3af        /* Muted text */
```

**Typography:**
- Headings: **Inter** (500, 600, 700 weights)
- Monospace: **DM Mono** (for numbers, tickers)

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| **Backend** | Flask (Python) |
| **Data Source** | yfinance API |
| **Tunneling** | ngrok |
| **Frontend** | Vanilla JS + Chart.js |
| **Styling** | Custom CSS (Dark Theme) |
| **Charts** | Chart.js v3.9.1 |
| **Deployment** | Google Colab / Local |

---

## 📊 Architecture

```
┌─────────────────┐
│  Google Colab   │  (or Local Machine)
│   Jupyter NB    │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Flask Server   │  Port 5050
│  (app.py)       │
└────────┬────────┘
         │
         ├─► yfinance API ──► NSE Data
         │
         ▼
┌─────────────────┐
│  ngrok Tunnel   │  Public HTTPS URL
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   Browser UI    │  Auto-refresh every 30s
│  (HTML/JS/CSS)  │
└─────────────────┘
```

**Data Flow:**
1. User selects stock from nav bar
2. Frontend calls `/api/stock?name=STOCK`
3. Backend fetches from yfinance
4. Data processed (NaN cleaning, formatting)
5. JSON response sent to frontend
6. Charts & UI updated dynamically
7. Process repeats every 30 seconds

---

## 🔧 Customization Guide

### Adding Custom Stocks

1. **Get NSE Symbol**  
   Find your stock symbol on [nseindia.com](https://www.nseindia.com)

2. **Update STOCKS Dictionary**
   ```python
   STOCKS = {
       "TATA MOTORS": "TATAMOTORS.NS",
       "WIPRO": "WIPRO.NS",
       # ... add your stocks
   }
   ```

3. **Restart Server**  
   Rerun Cell 3 in Colab or restart `app.py`

### Customizing UI Colors

Edit the CSS variables in the HTML template:

```css
:root {
  --primary: #your-color;
  --secondary: #your-color;
  --green: #your-color;
  --red: #your-color;
}
```

### Changing Refresh Rate

```javascript
// Faster updates (10 seconds)
setInterval(loadData, 10000);

// Slower updates (1 minute)
setInterval(loadData, 60000);
```

### Custom Metrics

Add new metrics in `get_stock_data()`:

```python
def get_stock_data(symbol):
    # ... existing code ...
    
    # Add your custom metric
    data["your_metric"] = inf.get("yourField", "N/A")
    
    return data
```

---

## 🚨 Troubleshooting

### Common Issues

**❌ "Port 5050 is in use"**
```python
# Change port in run_flask():
app.run(port=5051, ...)  # Use a different port

# Update ngrok tunnel:
tunnel = ngrok.connect(5051)
```

**❌ "ngrok authentication failed"**
- Verify your token at [ngrok dashboard](https://dashboard.ngrok.com/get-started/your-authtoken)
- Make sure no quotes/spaces when pasting
- Token should start with numbers/letters (not with "Basic")

**❌ "No data for stock XYZ"**
- Verify NSE symbol ends with `.NS`
- Check if trading hours (9:15 AM - 3:30 PM IST)
- Some stocks may have insufficient yfinance data

**❌ Chart not rendering**
- Clear browser cache
- Check browser console for errors
- Ensure Chart.js CDN is accessible

**❌ 502 Bad Gateway on ngrok URL**
- Wait 30 seconds for Flask to fully start
- Rerun Cell 4 to refresh tunnel
- Check Colab runtime hasn't disconnected

---

## 📈 Performance Tips

1. **Reduce API Calls**  
   Increase refresh interval for less frequent updates

2. **Cache Static Data**  
   Balance sheets don't change daily - cache them

3. **Optimize Chart Data**  
   Reduce `period` in yfinance calls:
   ```python
   hist = ticker.history(period="30d")  # Instead of 60d
   ```

4. **Lazy Load Tabs**  
   Load financials only when tab is clicked

---

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

1. **Fork the Repository**
2. **Create Feature Branch**  
   ```bash
   git checkout -b feature/AmazingFeature
   ```
3. **Commit Changes**  
   ```bash
   git commit -m 'Add some AmazingFeature'
   ```
4. **Push to Branch**  
   ```bash
   git push origin feature/AmazingFeature
   ```
5. **Open Pull Request**

### Ideas for Contributions
- [ ] Add more NSE stocks
- [ ] Implement watchlist feature
- [ ] Add comparison mode (2+ stocks)
- [ ] Export data to CSV/Excel
- [ ] Historical data viewer
- [ ] Price alerts system
- [ ] Dark/Light theme toggle
- [ ] Authentication layer
- [ ] Database integration for data caching

---

## 📜 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- **yfinance** - For providing free stock market data
- **ngrok** - For instant public URLs
- **Chart.js** - For beautiful interactive charts
- **NSE India** - For market data
- **Exchange Rate API** - For USD-INR conversion

---

## 📞 Support
- **Email:** mansukhute@iitbhilai.ac.in

---

<div align="center">

**Built with ❤️ by [Mansu Khute]**

⭐ **Star this repo if you find it useful!** ⭐

[🚀 Live Demo](https://savor-cabdriver-grapple.ngrok-free.dev/) • [📚 Docs](#documentation) • [🐛 Report Bug](https://github.com/yourusername/nse-live-dashboard/issues) • [💡 Request Feature](https://github.com/yourusername/nse-live-dashboard/issues)

</div>
