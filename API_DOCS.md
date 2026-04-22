# 📡 API Documentation - NSE Live Dashboard

Complete reference for all API endpoints and data structures.

---

## Base URL

When running locally:
```
http://localhost:5050
```

When running with ngrok:
```
https://your-subdomain.ngrok-free.dev
```

---

## Authentication

Currently, the API is **public** and requires no authentication.

> **Note:** For production use, consider adding API keys or OAuth.

---

## Endpoints

### 1. Get Stock Data

Fetch comprehensive stock information including price, metrics, charts, and indicators.

**Endpoint:** `GET /api/stock`

**Parameters:**

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| name | string | Yes | Display name of stock | `RELIANCE` |

**Request Example:**
```bash
curl "https://your-url.ngrok-free.dev/api/stock?name=RELIANCE"
```

**Response Schema:**
```json
{
  "name": "string",
  "price": "number",
  "change": "number",
  "change_pct": "number",
  "day_high": "number",
  "day_low": "number",
  "prev_close": "number",
  "market_cap_cr": "string",
  "mcap_class": "string",
  "pe_ratio": "number | 'N/A'",
  "pb_ratio": "number | 'N/A'",
  "eps": "number | 'N/A'",
  "beta": "number | 'N/A'",
  "div_yield": "string",
  "avg_volume": "string",
  "week_52_low": "number",
  "week_52_high": "number",
  "price_trend": {
    "dates": ["string"],
    "close": ["number | null"],
    "ma20": ["number | null"],
    "ma50": ["number | null"],
    "ma200": ["number | null"]
  },
  "volume_data": {
    "dates": ["string"],
    "volume": ["number | null"]
  },
  "rsi": {
    "value": "number | null",
    "label": "string"
  }
}
```

**Response Example:**
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
  "week_52_low": 1298.5,
  "week_52_high": 1608.9,
  "price_trend": {
    "dates": ["2024-01-28", "2024-01-29", "..."],
    "close": [1450.2, 1448.7, null],
    "ma20": [1465.3, 1463.8, null],
    "ma50": [1478.9, 1477.2, null],
    "ma200": [1420.5, 1421.1, null]
  },
  "volume_data": {
    "dates": ["2024-01-28", "2024-01-29"],
    "volume": [8234567, 9123456]
  },
  "rsi": {
    "value": 51,
    "label": "NEUTRAL"
  }
}
```

**Field Descriptions:**

| Field | Type | Description |
|-------|------|-------------|
| name | string | Stock display name |
| price | number | Current trading price (₹) |
| change | number | Price change from previous close (₹) |
| change_pct | number | Percentage change from previous close |
| day_high | number | Today's highest price (₹) |
| day_low | number | Today's lowest price (₹) |
| prev_close | number | Previous closing price (₹) |
| market_cap_cr | string | Market capitalization (formatted) |
| mcap_class | string | Classification: Large/Mid/Small Cap |
| pe_ratio | number\|string | Price-to-Earnings ratio |
| pb_ratio | number\|string | Price-to-Book ratio |
| eps | number\|string | Earnings per share (TTM) |
| beta | number\|string | Volatility vs market |
| div_yield | string | Dividend yield percentage |
| avg_volume | string | Average trading volume |
| week_52_low | number | 52-week low price |
| week_52_high | number | 52-week high price |
| price_trend | object | Historical price and moving averages |
| volume_data | object | Historical volume data |
| rsi | object | Relative Strength Index |

**Status Codes:**

| Code | Description |
|------|-------------|
| 200 | Success |
| 400 | Invalid stock name |
| 500 | Server error / API failure |

---

### 2. Get Extra Financials

Fetch detailed financial statements, shareholding, and corporate actions.

**Endpoint:** `GET /api/extra`

**Parameters:**

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| name | string | Yes | Display name of stock | `INFOSYS` |

**Request Example:**
```bash
curl "https://your-url.ngrok-free.dev/api/extra?name=INFOSYS"
```

**Response Schema:**
```json
{
  "balance_sheet": {
    "Cash": "string",
    "Total Assets": "string",
    "Total Liabilities": "string",
    "Stockholders Equity": "string"
  },
  "financials": {
    "Revenue": "string",
    "Operating Income": "string",
    "Net Income": "string",
    "EBITDA": "string"
  },
  "shareholding": {
    "Promoters": "number",
    "FII": "number",
    "DII": "number",
    "Public": "number"
  },
  "corp_actions": [
    {
      "date": "string",
      "type": "string",
      "value": "string"
    }
  ]
}
```

**Response Example:**
```json
{
  "balance_sheet": {
    "Cash": "₹45,123 Cr",
    "Total Assets": "₹3,45,678 Cr",
    "Total Liabilities": "₹1,23,456 Cr",
    "Stockholders Equity": "₹2,22,222 Cr"
  },
  "financials": {
    "Revenue": "₹6,78,900 Cr",
    "Operating Income": "₹1,45,678 Cr",
    "Net Income": "₹56,789 Cr",
    "EBITDA": "₹1,67,890 Cr"
  },
  "shareholding": {
    "Promoters": 50.52,
    "FII": 22.34,
    "DII": 15.12,
    "Public": 12.02
  },
  "corp_actions": [
    {
      "date": "2024-01-15",
      "type": "Dividend",
      "value": "₹6.5"
    },
    {
      "date": "2023-09-20",
      "type": "Split",
      "value": "1:2"
    },
    {
      "date": "2023-06-10",
      "type": "Bonus",
      "value": "1:1"
    }
  ]
}
```

**Corporate Action Types:**

| Type | Description | Value Format |
|------|-------------|--------------|
| Dividend | Cash dividend | `₹X.XX` |
| Split | Stock split | `X:Y` (e.g., 1:2) |
| Bonus | Bonus shares | `X:Y` (e.g., 1:1) |

**Status Codes:**

| Code | Description |
|------|-------------|
| 200 | Success |
| 400 | Invalid stock name |
| 500 | Server error / API failure |

---

### 3. Home Page

Serves the main dashboard UI.

**Endpoint:** `GET /`

**Parameters:** None

**Response:** HTML page

**Request Example:**
```bash
curl "https://your-url.ngrok-free.dev/"
```

---

## Supported Stocks

Current list of available stocks:

| Display Name | Symbol | NSE Code |
|--------------|--------|----------|
| RELIANCE | RELIANCE.NS | RELIANCE |
| TCS | TCS.NS | TCS |
| HDFC BANK | HDFCBANK.NS | HDFCBANK |
| INFOSYS | INFY.NS | INFY |
| MOTILAL OSWAL | MOTILALOFS.NS | MOTILALOFS |
| BANK OF BARODA | BANKBARODA.NS | BANKBARODA |
| GAIL | GAIL.NS | GAIL |
| VEDANTA | VEDL.NS | VEDL |
| BIRLASOFT | BSOFT.NS | BSOFT |
| NMDC | NMDC.NS | NMDC |

---

## Data Sources

### yfinance API

All stock data comes from the yfinance Python library, which scrapes Yahoo Finance.

**Data includes:**
- Real-time prices
- Historical OHLCV data
- Financial statements
- Company information
- Dividends and splits

**Limitations:**
- Data may have 15-minute delay
- Some stocks may have incomplete data
- API rate limits apply

### Exchange Rate API

USD to INR conversion uses:
```
https://api.exchangerate-api.com/v4/latest/USD
```

**Fallback:** 83.5 if API fails

---

## Rate Limits

**Current:** No rate limiting

**Recommended for production:**
- 100 requests per hour per IP
- 1000 requests per day per IP

**Implementation example:**
```python
from flask_limiter import Limiter

limiter = Limiter(
    app,
    key_func=lambda: request.remote_addr,
    default_limits=["100 per hour"]
)
```

---

## Error Handling

### Error Response Format

```json
{
  "error": "string",
  "message": "string",
  "status": "number"
}
```

### Common Errors

**Invalid Stock Name:**
```json
{
  "error": "Invalid Stock",
  "message": "Stock name not found in STOCKS dictionary",
  "status": 400
}
```

**API Failure:**
```json
{
  "error": "API Error",
  "message": "Failed to fetch data from yfinance",
  "status": 500
}
```

**Missing Parameters:**
```json
{
  "error": "Bad Request",
  "message": "Missing required parameter: name",
  "status": 400
}
```

---

## Special Data Handling

### NaN/Infinity Values

The API handles NaN and Infinity values gracefully:

1. **Numbers:** Replaced with `null` in JSON
2. **Strings:** Replaced with `"N/A"`

**Example:**
```python
# Input
pe_ratio = float('nan')

# Output
{
  "pe_ratio": null  # or "N/A" depending on context
}
```

### Market Cap Formatting

Values are converted from raw INR to crores:

```python
# Input (raw value)
market_cap = 184325800000000  # ₹184,325,800,000,000

# Output (formatted)
{
  "market_cap_cr": "₹1,843,258 Cr"
}
```

### Date Formatting

All dates are in `YYYY-MM-DD` format:

```python
# Example
"2024-01-28"
```

---

## Usage Examples

### Python

```python
import requests

# Get stock data
response = requests.get(
    "https://your-url.ngrok-free.dev/api/stock",
    params={"name": "RELIANCE"}
)
data = response.json()

print(f"Price: ₹{data['price']}")
print(f"Change: {data['change_pct']}%")
```

### JavaScript

```javascript
// Fetch stock data
async function getStock(name) {
  const response = await fetch(
    `https://your-url.ngrok-free.dev/api/stock?name=${encodeURIComponent(name)}`
  );
  const data = await response.json();
  return data;
}

// Usage
const stock = await getStock('INFOSYS');
console.log(stock.price);
```

### cURL

```bash
# Get stock data
curl -X GET "https://your-url.ngrok-free.dev/api/stock?name=TCS"

# Get extra financials
curl -X GET "https://your-url.ngrok-free.dev/api/extra?name=HDFC%20BANK"

# Pretty print with jq
curl -s "https://your-url.ngrok-free.dev/api/stock?name=RELIANCE" | jq '.'
```

---

## CORS Configuration

**Current:** CORS is not enabled

**Enable for production:**

```python
from flask_cors import CORS

CORS(app, resources={
    r"/api/*": {
        "origins": ["https://your-frontend.com"],
        "methods": ["GET", "POST"],
        "allow_headers": ["Content-Type"]
    }
})
```

---

## Caching Strategy

**Recommended:**

1. **Client-side:** Cache for 30 seconds
2. **Server-side:** Use Redis/Memcached
3. **CDN:** Cache static assets

**Example implementation:**

```python
from flask_caching import Cache

cache = Cache(app, config={
    'CACHE_TYPE': 'redis',
    'CACHE_REDIS_URL': 'redis://localhost:6379/0',
    'CACHE_DEFAULT_TIMEOUT': 300
})

@app.route('/api/stock')
@cache.cached(timeout=30, query_string=True)
def api_stock():
    # ... existing code
```

---

## Versioning

**Current version:** v1 (no version prefix)

**Future versions:**
- `/api/v2/stock`
- `/api/v2/extra`

---

## Webhooks (Planned)

Future feature to receive real-time updates:

```json
POST https://your-callback-url.com/webhook

{
  "event": "price_change",
  "stock": "RELIANCE",
  "old_price": 1350.0,
  "new_price": 1353.3,
  "timestamp": "2024-01-28T14:30:00Z"
}
```

---

## Support

For API issues or questions:

- **GitHub Issues:** [Report here](https://github.com/yourusername/nse-live-dashboard/issues)
- **Email:** your.email@example.com

---

**Last Updated:** April 23, 2024
