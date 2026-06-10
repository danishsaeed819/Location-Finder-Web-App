# Location Finder Web App

A real-time location search tool built with **HTML5**, **CSS3**, and **JavaScript**, integrating third-party geolocation and mapping APIs.

![Stack](https://img.shields.io/badge/JavaScript-ES6+-F7DF1E?style=flat&logo=javascript&logoColor=black)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=css3&logoColor=white)

## Features

| Feature | API / Technology |
|---------|------------------|
| Interactive map | [Leaflet](https://leafletjs.com/) + [OpenStreetMap](https://www.openstreetmap.org/) tiles |
| Address search | [Nominatim](https://nominatim.org/) forward geocoding |
| Click-to-identify | Nominatim reverse geocoding |
| Current location | [HTML5 Geolocation API](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API) |
| Distance measurement | Haversine formula on map clicks |
| Search history | `localStorage` persistence |
| Dark mode | CSS custom properties + `localStorage` |

## Quick Start

No build step or API keys required.

### Option 1 — Open directly

Double-click `index.html` in your browser.

> Some browsers restrict `fetch()` on `file://` URLs. If search fails, use Option 2.

### Option 2 — Local server (recommended)

```bash
# Python 3
python -m http.server 8080

# Node.js (npx)
npx serve .

# PHP
php -S localhost:8080
```

Then open [http://localhost:8080](http://localhost:8080).

## Project Structure

```
Location-Finder-Web-App/
├── index.html          # App shell & semantic markup
├── css/
│   └── styles.css      # Design system, layout, responsive UI
├── js/
│   ├── app.js          # Main orchestrator & event handling
│   ├── config.js       # API endpoints & app settings
│   ├── geolocation.js  # Browser Geolocation API wrapper
│   ├── geocoding.js    # Nominatim search & reverse geocoding
│   ├── map.js          # Leaflet map controller
│   ├── history.js      # Search history (localStorage)
│   └── utils.js        # Helpers (debounce, distance, toasts)
└── README.md
```

## How It Works

### 1. Forward Geocoding (Search)

When you type an address and press search, the app calls Nominatim's `/search` endpoint:

```
GET https://nominatim.openstreetmap.org/search?q=London&format=json&addressdetails=1
```

Results include coordinates, display name, and structured address components.

### 2. Reverse Geocoding (Map Click)

Clicking anywhere on the map sends coordinates to Nominatim's `/reverse` endpoint:

```
GET https://nominatim.openstreetmap.org/reverse?lat=51.5&lon=-0.1&format=json
```

The resolved address is shown in the sidebar and as a map popup.

### 3. Browser Geolocation

The "Use My Current Location" button calls `navigator.geolocation.getCurrentPosition()` with high-accuracy options. The browser prompts for permission; on success, coordinates are reverse-geocoded and marked on the map.

### 4. Distance Calculator

Click two points on the map. The app draws a dashed line and computes the great-circle distance using the Haversine formula.

## API Usage Policy

This project uses free OpenStreetMap services. Please respect their [Nominatim Usage Policy](https://operations.osmfoundation.org/policies/nominatim/):

- Max 1 request per second
- Provide a valid `User-Agent` (configured in `config.js`)
- Do not use for heavy bulk geocoding in production without self-hosting

## Browser Support

- Chrome, Firefox, Safari, Edge (latest)
- Geolocation requires HTTPS or `localhost`
- JavaScript modules (`type="module"`) required

## License

MIT — free to use for learning and portfolio purposes.
