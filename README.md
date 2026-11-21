🚇 YatraCompare India

A single-file web app that compares estimated fares and travel times across cabs, autos, bike taxis, metro, city buses and a hybrid auto + metro option for trips between popular landmarks in major Indian cities.

🔗 Live Demo

YatraCompare India screenshot

⚠️ Estimates only. Fares and durations are calculated from simple formulas, not live data from Uber, Ola, Rapido or any transit authority. Always confirm the real price in the provider's app before booking.
⸻
Features

- Multimodal comparison – Rapido Bike Taxi, Auto Rickshaw, Uber Go, Ola Prime, Uber XL, Metro, City Bus and a Smart Mix (Auto + Metro).
- Passenger-aware results – options appear or disappear based on group size (1–8 passengers). Bike taxis are solo only, autos up to 3, hatchback/sedan cabs up to 4, and SUV/MUV cabs for 4 or more.
- Time-aware pricing – a 25% night surcharge on autos and 15% on cabs between 11 PM and 5 AM. Metro is marked closed outside 6 AM–11 PM, and buses are marked limited outside 5 AM–11 PM.
- Smart badges – CHEAPEST, FASTEST and BEST BALANCED tags on the best operating options.
- Filter and sort – filter by All / Cabs & Autos / Metro & Bus, sort by Cheapest / Fastest / Balanced.
- Step-by-step itinerary – a modal showing each leg of the trip (walk, auto, metro, bus, etc.) with distance and time.
- Real-fare override – type the actual fare you see in the app for any option; it replaces the estimate and is remembered for 30 minutes.
- Deep links – "Book / Open App" buttons pass pickup and drop coordinates to Uber, Ola and Rapido where supported.
- Route overview – a self-contained inline SVG schematic of pickup and drop (no map tiles or API keys needed).
- GPS pickup – optionally use your current location as the pickup point.
- Responsive UI – works on desktop and mobile, with safe-area support for notched phones.

Getting Started

There is no build step and no dependencies to install.

1. Clone the repo or download index.html.
2. Open it in any modern browser (double-click, or drag it into a browser window).

An internet connection is needed only to load the Tailwind CSS script from its CDN (https://cdn.tailwindcss.com/3.4.17). Without it the page will load unstyled.

How to Use

1. Choose a Pickup and Destination. Start typing (2+ characters) and pick a landmark from the suggestions. The defaults are Connaught Place → IGI Airport Terminal 3, Delhi.
2. Set the Departure Time and number of Passengers.
3. Click Compare All Routes. Changing passengers or departure time also refreshes results automatically.
4. Use the filter and sort toggles to narrow down the list.
5. Open Step Itinerary for the leg-by-leg breakdown, or Book / Open App to jump to the provider.
6. Optionally enter the real fare you see in an app to correct the estimate.

Supported Locations

The app uses a built-in list of 27 landmarks (airports, railway stations, tech parks and metro hubs) across:
Region	Examples
Delhi NCR	Connaught Place, IGI Airport T3, New Delhi Railway Station, Cyber Hub (Gurugram), Noida Sector 62, Hauz Khas, Anand Vihar
Bengaluru	Majestic, Kempegowda Airport, Indiranagar, Whitefield ITPL, Koramangala, Electronic City
Mumbai	CSMT, Airport T2, BKC, Dadar, Andheri Metro
Hyderabad	Rajiv Gandhi Airport, Hitec City, Secunderabad Junction
Chennai	Chennai Central, Chennai Airport
Kolkata	Howrah Station, NSCBI Airport
Pune	Pune Junction, Hinjawadi IT Park

Free-text addresses are not geocoded. If you type something that isn't in the list, the app asks you to pick a suggestion.

How Estimates Are Calculated

Distance is the straight-line (haversine) distance between the two points. Everything else is derived from it.
Mode	Approach
Drive time	max(12, distance / 22 km/h + 4 min)
Bike taxi	Base ₹25 + ₹11/km after 1.5 km; ~72% of drive time
Auto	Base ₹30 + ₹16.5/km after 1.5 km (+25% at night)
Uber Go	65 + 15.5/km + 1.5/min (+15% at night)
Ola Prime	85 + 18/km + 1.8/min (+15% at night)
Uber XL / SUV	130 + 25/km + 2/min
Metro	Distance-slab fare (₹20 / 30 / 50 / 60) per person, available for trips ≥ 3 km
City Bus	₹15–₹45 per person based on distance, available for trips ≥ 2 km
Smart Mix	₹45 auto leg + metro fare per person, for trips ≥ 6 km while metro is running

The Balanced score weights cost at 45% and time at 55%.

Tech Stack

- HTML, CSS and vanilla JavaScript (single file, no framework)
- Tailwind CSS via CDN
- Inline SVG for the route map
- localStorage for saving fare overrides
- Browser Geolocation API for "Use My GPS"

Project Structure

index.html               # Entire app: markup, styles and logic
screenshots/
  screenshot.png         # Preview image used in this README
LICENSE
README.md

Key parts inside the script:

- LOCS – the landmark dataset (name, latitude, longitude, address)
- haversine() – distance calculation
- calculateRoutes() – fare, duration and itinerary logic for every mode
- assignBadges() – picks cheapest / fastest / best-balanced
- renderResults() / openModal() – UI rendering
- updateMap() – SVG route schematic

Limitations

- Fares and times are formula-based estimates; there is no live pricing, traffic, surge or availability data.
- Distance is straight-line, not road distance, so real trips will usually be longer.
- The route map is a schematic, not a road map.
- Metro and bus fares and the metro booking link are generic and not tailored per city. The metro link points to Delhi Metro for all cities.
- The Ola and Rapido deep-link formats are best-effort and may not open the right screen in every app or region.
- Only the built-in landmarks are searchable. Picking locations from different cities will produce a long-distance result that isn't realistic for local transport.
- Saved fare overrides live in your browser's localStorage and expire after 30 minutes.

Ideas for Future Work

- Integrate a geocoding API for any address search
- Use a routing API for real road distance and traffic-based durations
- City-specific metro and bus fare tables
- Live fare data via official partner APIs
- More cities and landmarks

License

Released under the MIT License.

Author

Aryan Singh 
B.Tech CSE (AI/ML), Bosscoder School of Technology

- GitHub: aryansingh8793-art
- LinkedIn: https://www.linkedin.com/in/aryan-singh-411ab8309/

Disclaimer

YatraCompare India is not affiliated with Uber, Ola, Rapido, or any metro or bus authority. All brand names belong to their respective owners.
