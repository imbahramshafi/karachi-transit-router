# Karachi Transit Router

An open-source public transport router for Karachi. Plan a journey across BRT lines and Peoples Bus Service routes, with step-by-step directions, walking legs, and flag-down boarding for non-BRT buses.

**Live demo:** https://YOURUSERNAME.github.io/karachi-transit-router

## Why this exists

Karachi has no working transit routing app. Google Maps doesn't know our routes. The official Breeze app only covers BRT. Daily commuters rely on memory, word of mouth, and asking conductors.

This is a prototype to see if a community-built alternative could work. The data started as 3 routes hand-encoded from the Think Transportation map and has grown from there. The goal is to make it accurate enough that real commuters can use it.

## Features

- **Step-by-step directions** for any A to B journey
- **Walking legs** at start and end (up to ~15 min)
- **Flag-down boarding** for non-BRT buses (walk to the road, wave the bus down)
- **Use My Location** to plan from where you are
- **Road-snapped routes** drawn on a dark Karachi map
- **Transfer detection** when no direct route exists
- **Autocomplete** for stop names

## Routes covered

- **BRT Green Line** — Surjani Chowrangi to Numaish (22 stations)
- **BRT Orange Line** — TMA Orangi to Board Office (5 stations)
- **R9** — Gulshan-e-Hadeed to Tower (flag-down)
- **R2** — Power House to Indus Hospital (flag-down)

More routes need adding. See "Contribute" below.

## Tech

- Single static HTML file. No build step, no backend.
- Leaflet.js for the map, CartoDB dark tiles for the basemap.
- OSRM public API for road snapping and walking paths.
- Browser geolocation for "use my location".
- Plain JavaScript graph search for routing.

## Run it locally

```
git clone https://github.com/YOURUSERNAME/karachi-transit-router.git
cd karachi-transit-router
python -m http.server 8000
```

Open http://localhost:8000 in your browser.

## Contribute

The data is the bottleneck, not the code. If you ride a route I haven't added, you can help by submitting it.

**Add a route in 3 steps:**

1. Open `index.html` and find the `STOP_COORDS` object. Add each stop on your route as `"Stop Name": [longitude, latitude]`. Get coordinates by right-clicking on Google Maps.

2. Find the `ROUTE_STOPS` object. Add your route in order of stops: `"R3-Power House to Nasir Jump": ["Stop A", "Stop B", ...]`

3. Find the `ROUTE_COLORS`, `ROUTE_SHORT`, and `FLAG_DOWN` objects. Add your route to each (use any free color, a short name, and `true` for flag-down or `false` for BRT-style fixed-stop).

Open a Pull Request and tag what you've ridden. I'll verify with the Think Transportation map and merge.

## Known limitations

- Some R2 intermediate stops are best-guess. Verified by riding the route would improve them.
- Maximum 2 buses per journey (1 transfer). Most Karachi trips don't need more.
- No real-time bus tracking. This is a static router.
- Walking distance capped at 1.2 km. Beyond that the app says no route found.
- No fares yet.

## License

MIT. Use it, fork it, ship it.
