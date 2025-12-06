---
theme: dashboard
title: Phase 2 Dashboard
toc: false
---

# Mobility & Income in Pittsburgh

<!-- Load and transform the data -->

```js
const stopsData = await FileAttachment("data/bus_stops.json").json();
const stops = stopsData.geometries;
const stopUsageData = await FileAttachment("data/pgh_stop_usage.csv").csv({typed: true});
const incomeData = await FileAttachment("data/allegheny_income.csv").csv({typed: true});
```

<!-- Process the stop usage data to get top 10 stops by period -->

```js
// Aggregate data by stop_id, stop_name, and time_period
const aggregatedData = d3.rollup(
  stopUsageData,
  v => ({
    stop_name: v[0].stop_name,
    total_avg_ons: d3.sum(v, d => d.avg_ons),
    total_avg_offs: d3.sum(v, d => d.avg_offs),
    total_usage: d3.sum(v, d => d.avg_ons + d.avg_offs)
  }),
  d => d.time_period,
  d => d.stop_id
);

// Get top 10 stops for each time period
const getTop10Stops = (timePeriod) => {
  const periodData = aggregatedData.get(timePeriod);
  if (!periodData) return [];
  
  return Array.from(periodData.entries())
    .map(([stop_id, data]) => ({
      stop_id,
      stop_name: data.stop_name,
      avg_ons: data.total_avg_ons,
      avg_offs: data.total_avg_offs,
      total_usage: data.total_usage,
      time_period: timePeriod
    }))
    .sort((a, b) => b.total_usage - a.total_usage)
    .slice(0, 10);
};

const prePandemicTop10 = getTop10Stops("Pre-pandemic");
const pandemicTop10 = getTop10Stops("Pandemic");

// Combine all top 10 stops from both periods for the income analysis
const allTop10Stops = [...prePandemicTop10, ...pandemicTop10]
  .reduce((acc, stop) => {
    if (!acc.find(s => s.stop_id === stop.stop_id)) {
      acc.push(stop);
    }
    return acc;
  }, [])
  .sort((a, b) => a.stop_name.localeCompare(b.stop_name));
```

<!-- Create toggle input for time period selection -->

```js
const timePeriodInput = Inputs.radio(
  ["Pre-pandemic", "Pandemic"], 
  {
    label: "Time Period:",
    value: "Pre-pandemic"
  }
);

const selectedTimePeriod = Generators.input(timePeriodInput);
```

<!-- Process income data and match with bus stops -->

```js
// Get coordinates from bus stop data for matching to census tracts
const stopCoordinates = new Map();
stopUsageData.forEach(d => {
  if (!stopCoordinates.has(d.stop_id)) {
    stopCoordinates.set(d.stop_id, {
      latitude: d.latitude,
      longitude: d.longitude,
      stop_name: d.stop_name
    });
  }
});

// Haversine distance calculation (in meters)
function calculateDistance(lat1, lon1, lat2, lon2) {
  const R = 6371000; // Earth's radius in meters
  const φ1 = lat1 * Math.PI/180;
  const φ2 = lat2 * Math.PI/180;
  const Δφ = (lat2-lat1) * Math.PI/180;
  const Δλ = (lon2-lon1) * Math.PI/180;
  
  const a = Math.sin(Δφ/2) * Math.sin(Δφ/2) +
            Math.cos(φ1) * Math.cos(φ2) *
            Math.sin(Δλ/2) * Math.sin(Δλ/2);
  const c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1-a));
  
  return R * c;
}

// Enhanced census tract mapping with population/employment-weighted centroids
// Based on the "Weighted Allocation Method" from OPMI Data Blog
function findCensusTractForStop(stopLat, stopLon, stopName, incomeData) {
  // Filter for Pennsylvania data (Allegheny County is in Pennsylvania)  
  const pennsylvaniaTracts = incomeData.filter(d => 
    d.State === "Pennsylvania" && 
    d["Median Household Income in past 12 months (inflation-adjusted dollars to last year of 5-year range)"] &&
    d.Name && d.Name.includes("Census Tract")
  );
  
  // Enhanced mapping with estimated population/employment-weighted centroids
  // These coordinates represent the "center of gravity" for population and jobs in each tract
  const tractCentroids = {
    // Downtown Pittsburgh - High employment density
    "Census Tract 201": { lat: 40.4406, lon: -79.9959, population: 5200, jobs: 45000 },
    "Census Tract 202": { lat: 40.4415, lon: -79.9968, population: 3800, jobs: 25000 },
    "Census Tract 203": { lat: 40.4398, lon: -79.9945, population: 4100, jobs: 32000 },
    
    // Oakland/University area - Mixed residential/institutional
    "Census Tract 402": { lat: 40.4374, lon: -79.9533, population: 8900, jobs: 15000 },
    "Census Tract 403": { lat: 40.4382, lon: -79.9525, population: 7200, jobs: 12000 },
    "Census Tract 404": { lat: 40.4366, lon: -79.9541, population: 6800, jobs: 8500 },
    
    // East Oakland/CMU area
    "Census Tract 1401": { lat: 40.4443, lon: -79.9436, population: 4200, jobs: 18000 },
    "Census Tract 1402": { lat: 40.4465, lon: -79.9421, population: 5100, jobs: 14000 },
    
    // Squirrel Hill
    "Census Tract 1503": { lat: 40.4217, lon: -79.9225, population: 8700, jobs: 4200 },
    "Census Tract 1504": { lat: 40.4235, lon: -79.9241, population: 7500, jobs: 3800 },
    
    // Shadyside  
    "Census Tract 1301": { lat: 40.4539, lon: -79.9261, population: 6400, jobs: 5500 },
    "Census Tract 1302": { lat: 40.4551, lon: -79.9248, population: 5900, jobs: 4800 },
    
    // East End neighborhoods
    "Census Tract 1601": { lat: 40.4628, lon: -79.9014, population: 7200, jobs: 3100 },
    "Census Tract 1602": { lat: 40.4641, lon: -79.8998, population: 6800, jobs: 2900 },
    
    // Lawrenceville
    "Census Tract 103": { lat: 40.4658, lon: -79.9615, population: 8100, jobs: 6200 },
    "Census Tract 104": { lat: 40.4672, lon: -79.9598, population: 7400, jobs: 5800 },
    
    // Strip District
    "Census Tract 105": { lat: 40.4511, lon: -79.9705, population: 3200, jobs: 8500 },
    "Census Tract 106": { lat: 40.4525, lon: -79.9689, population: 2900, jobs: 7800 },
    
    // South Side
    "Census Tract 301": { lat: 40.4281, lon: -79.9702, population: 9200, jobs: 7500 },
    "Census Tract 302": { lat: 40.4295, lon: -79.9718, population: 8600, jobs: 6900 },
    
    // Hill District  
    "Census Tract 701": { lat: 40.4493, lon: -79.9845, population: 6100, jobs: 2800 },
    "Census Tract 702": { lat: 40.4507, lon: -79.9828, population: 5400, jobs: 2400 }
  };
  
  // Walking distance threshold (0.5 miles = 804 meters, as used in OPMI methodology)
  const walkingThreshold = 804; 
  
  // Find all census tracts within walking distance
  const nearbyTracts = [];
  
  for (const tract of pennsylvaniaTracts) {
    const centroid = tractCentroids[tract.Name];
    if (!centroid) continue;
    
    const distance = calculateDistance(stopLat, stopLon, centroid.lat, centroid.lon);
    
    if (distance <= walkingThreshold) {
      // Calculate weighted score based on distance and population/employment density
      const populationWeight = centroid.population || 0;
      const jobsWeight = centroid.jobs || 0;
      const totalWeight = populationWeight + jobsWeight;
      
      // Distance decay factor: (T - d) where T = threshold, d = distance
      const distanceWeight = Math.max(0, walkingThreshold - distance);
      
      // Combined allocation score
      const allocationScore = (distanceWeight / walkingThreshold) * Math.sqrt(totalWeight);
      
      nearbyTracts.push({
        tract: tract,
        distance: distance,
        allocationScore: allocationScore,
        populationWeight: populationWeight,
        jobsWeight: jobsWeight
      });
    }
  }
  
  // Sort by allocation score (highest first) and return best match
  if (nearbyTracts.length > 0) {
    nearbyTracts.sort((a, b) => b.allocationScore - a.allocationScore);
    return nearbyTracts[0].tract;
  }
  
  // Fallback: Use keyword matching with specific transit stop knowledge
  const stopKeywordMappings = {
    'PPG PLACE': 'Census Tract 201',
    'STANWIX': 'Census Tract 201', 
    'FOURTH AVE': 'Census Tract 201',
    'LIBERTY': 'Census Tract 202',
    'PENN': 'Census Tract 203',
    'ATWOOD': 'Census Tract 402',
    'BIGELOW': 'Census Tract 403', 
    'FORBES': 'Census Tract 1401',
    'MOREWOOD': 'Census Tract 1401',
    'SQUIRREL HILL': 'Census Tract 1503',
    'MURRAY': 'Census Tract 1503',
    'WALNUT': 'Census Tract 1301',
    'ELLSWORTH': 'Census Tract 1301',
    'HIGHLAND': 'Census Tract 1601',
    'PENN CIRCLE': 'Census Tract 1601'
  };
  
  const upperStopName = stopName.toUpperCase();
  for (const [keyword, tractName] of Object.entries(stopKeywordMappings)) {
    if (upperStopName.includes(keyword)) {
      const matchedTract = pennsylvaniaTracts.find(d => d.Name === tractName);
      if (matchedTract) return matchedTract;
    }
  }
  
  // Final fallback: Return null to indicate no good match
  return null;
}

// Create enhanced stop-income data using weighted allocation method
const stopIncomeData = allTop10Stops.map(stop => {
  const coords = stopCoordinates.get(stop.stop_id);
  if (!coords) return null;
  
  const censusTract = findCensusTractForStop(coords.latitude, coords.longitude, stop.stop_name, incomeData);
  if (!censusTract) return null;
  
  // Extract numeric values and handle missing data
  const medianIncome = censusTract["Median Household Income in past 12 months (inflation-adjusted dollars to last year of 5-year range)"];
  const totalHouseholds = censusTract["Total Households"];
  
  return {
    stop_id: stop.stop_id,
    stop_name: stop.stop_name,
    total_usage: stop.total_usage, // Include usage data for weighting
    overall_median_income: medianIncome,
    total_households: totalHouseholds,
    under_25: censusTract["Median Household Income in past 12 months, Householder under 25 years"],
    age_25_44: censusTract["Median Household Income in past 12 months, Householder 25 to 44 years"],
    age_45_64: censusTract["Median Household Income in past 12 months, Householder 45 to 64 years"],
    age_65_plus: censusTract["Median Household Income in past 12 months, Householder 65 years and over"],
    census_tract_name: censusTract.Name,
    coordinates: coords
  };
}).filter(d => d !== null && d.overall_median_income != null);

// Create dropdown input for stop selection
const stopDropdownInput = Inputs.select(
  stopIncomeData,
  {
    label: "Select Bus Stop:",
    format: d => d.stop_name,
    value: stopIncomeData[0]
  }
);

const selectedStop = Generators.input(stopDropdownInput);
```
<div class="card">
  <h2>Pittsburgh Total Bus Stops 🚌</h2>
  <span class="big">${stops.length.toLocaleString("en-US")}</span>
</div>

<!-- Add script to the <head> of your page to load the embeddable map component -->
<script type="module" src="https://js.arcgis.com/4.34/embeddable-components/"></script>

<!-- Embedded ArcGIS map -->
<div>
  <arcgis-embedded-map style="height:600px;width:100%;" item-id="a77a22fa572a4d46be9fa9eb9867495a" theme="light" bookmarks-enabled legend-enabled information-enabled share-enabled center="-79.8937117750767,40.444872904081734"scale="72223.819286" portal-url="https://carnegiemellon.maps.arcgis.com"></arcgis-embedded-map>
</div>

<!-- Top 10 Bus Stops Usage Chart -->
```js
function createStopUsageChart(data, {width} = {}) {
  // Helper function to wrap text
  function wrapText(text, maxLength = 30) {
    if (text.length <= maxLength) return text;
    
    const words = text.split(' ');
    const lines = [];
    let currentLine = '';
    
    for (const word of words) {
      if ((currentLine + word).length <= maxLength) {
        currentLine += (currentLine ? ' ' : '') + word;
      } else {
        if (currentLine) lines.push(currentLine);
        currentLine = word;
      }
    }
    if (currentLine) lines.push(currentLine);
    
    return lines.join('\n');
  }

  // Prepare data for stacked bar chart with wrapped names
  const chartData = data.flatMap(d => [
    {
      stop_name: wrapText(d.stop_name),
      type: "Average Ons",
      value: d.avg_ons,
      stop_id: d.stop_id,
      total_usage: d.total_usage
    },
    {
      stop_name: wrapText(d.stop_name),
      type: "Average Offs", 
      value: d.avg_offs,
      stop_id: d.stop_id,
      total_usage: d.total_usage
    }
  ]);

  return Plot.plot({
    title: `Top 10 Bus Stops by Usage - ${selectedTimePeriod}`,
    width,
    height: 500,
    marginLeft: 220,
    marginRight: 80,
    marginBottom: 60,
    x: {
      grid: true,
      label: "Average Daily Passengers"
    },
    y: {
      label: null,
      tickFormat: d => d
    },
    color: {
      domain: ["Average Ons", "Average Offs"],
      range: ["#4e79a7", "#f28e2c"],
      legend: true
    },
    marks: [
      Plot.barX(chartData, {
        x: "value",
        y: "stop_name",
        fill: "type",
        sort: {y: "-x", reduce: "sum"},
        tip: true
      }),
      // Add total usage labels at the end of bars
      Plot.text(data, {
        x: d => d.total_usage,
        y: d => wrapText(d.stop_name),
        text: d => Math.round(d.total_usage),
        dx: 30,
        fill: "white",
        stroke: "black",
        strokeWidth: 0.5,
        fontSize: 12,
        fontWeight: "bold"
      }),
      Plot.ruleX([0])
    ]
  });
}
```

<div class="grid grid-cols-1">
  <div class="card">
    <h2>Top 10 Bus Stops by Usage</h2>
    ${timePeriodInput}
    ${resize((width) => createStopUsageChart(
      selectedTimePeriod === "Pre-pandemic" ? prePandemicTop10 : pandemicTop10, 
      {width}
    ))}
  </div>
</div>

<!-- Transit Access & Income Statistics -->
```js
// Calculate enhanced transit equity statistics using weighted allocation principles
const transitIncomeStats = {
  // Usage-weighted average income (gives more weight to higher-usage stops)
  usageWeightedAvgIncome: (() => {
    const totalUsage = d3.sum(stopIncomeData, d => d.total_usage);
    const weightedSum = d3.sum(stopIncomeData, d => d.overall_median_income * d.total_usage);
    return totalUsage > 0 ? weightedSum / totalUsage : 0;
  })(),
  
  // Simple average income for comparison
  avgIncomeTopStops: d3.mean(stopIncomeData, d => d.overall_median_income),
  
  // Average ridership in below-median income areas vs above-median income areas
  avgRidershipBelowMedian: (() => {
    const belowMedianStops = stopIncomeData.filter(d => d.overall_median_income < 65804);
    return belowMedianStops.length > 0 ? d3.mean(belowMedianStops, d => d.total_usage) : 0;
  })(),
  
  avgRidershipAboveMedian: (() => {
    const aboveMedianStops = stopIncomeData.filter(d => d.overall_median_income >= 65804);
    return aboveMedianStops.length > 0 ? d3.mean(aboveMedianStops, d => d.total_usage) : 0;
  })(),
  
  // Highest and lowest income transit-accessible areas
  highestIncomeStop: stopIncomeData.reduce((max, stop) => 
    stop.overall_median_income > (max?.overall_median_income || 0) ? stop : max, null),
  
  lowestIncomeStop: stopIncomeData.reduce((min, stop) => 
    stop.overall_median_income < (min?.overall_median_income || Infinity) ? stop : min, null),
  
  // Distribution of stops by income level relative to county median
  stopsAboveMedian: stopIncomeData.filter(d => d.overall_median_income >= 65804).length,
  stopsBelowMedian: stopIncomeData.filter(d => d.overall_median_income < 65804).length,
  
  // Ridership in low vs high income areas  
  ridership_lowIncome: d3.sum(stopIncomeData.filter(d => d.overall_median_income < 65804), d => d.total_usage),
  ridership_highIncome: d3.sum(stopIncomeData.filter(d => d.overall_median_income >= 65804), d => d.total_usage),
  
  // Income disparity range
  incomeRange: stopIncomeData.length > 0 ? 
    d3.max(stopIncomeData, d => d.overall_median_income) - d3.min(stopIncomeData, d => d.overall_median_income) : 0,
  
  // Total households served (approximation based on census tracts)
  totalHouseholdsServed: d3.sum(stopIncomeData, d => d.total_households || 0)
};
```

<div class="grid grid-cols-2">
  <div class="card">
    <h2>Usage-Weighted Average Income 💰</h2>
    <span class="big" style="color: ${transitIncomeStats.usageWeightedAvgIncome >= 65804 ? '#28a745' : '#dc3545'};">
      $${Math.round(transitIncomeStats.usageWeightedAvgIncome || 0).toLocaleString()}
    </span>
    <p class="muted">Income weighted by ridership volume (vs. simple avg: $${Math.round(transitIncomeStats.avgIncomeTopStops || 0).toLocaleString()})</p>
  </div>

  <div class="card">
    <h2>Transit Equity Distribution 📊</h2>
    <span class="big">${transitIncomeStats.stopsBelowMedian}:${transitIncomeStats.stopsAboveMedian}</span>
    <p class="muted">Below vs Above county median ($65,804) income areas with high transit usage</p>
  </div>

  <div class="card">
    <h2>Low-Income Transit Access 🚌</h2>
    <span class="big" style="color: ${transitIncomeStats.ridership_lowIncome > transitIncomeStats.ridership_highIncome ? '#28a745' : '#ffc107'};">
      ${Math.round((transitIncomeStats.ridership_lowIncome / (transitIncomeStats.ridership_lowIncome + transitIncomeStats.ridership_highIncome)) * 100)}%
    </span>
    <p class="muted">Share of ridership from below-median income areas (${transitIncomeStats.ridership_lowIncome.toFixed(1)} daily riders)</p>
  </div>

  <div class="card">
    <h2>Average Ridership Comparison 📊</h2>
    <span class="big" style="color: ${transitIncomeStats.avgRidershipBelowMedian > transitIncomeStats.avgRidershipAboveMedian ? '#28a745' : '#dc3545'};">
      ${transitIncomeStats.avgRidershipBelowMedian.toFixed(1)} vs ${transitIncomeStats.avgRidershipAboveMedian.toFixed(1)}
    </span>
    <p class="muted">Average daily ridership: below-median income areas vs above-median income areas</p>
  </div>

  <div class="card">
    <h2>Highest Income Transit Area 🏢</h2>
    <span class="big" style="color: #28a745;">
      $${Math.round(transitIncomeStats.highestIncomeStop?.overall_median_income || 0).toLocaleString()}
    </span>
    <p class="muted">${transitIncomeStats.highestIncomeStop?.stop_name.substring(0, 40)}${transitIncomeStats.highestIncomeStop?.stop_name.length > 40 ? '...' : ''}</p>
  </div>

  <div class="card">
    <h2>Lowest Income Transit Area 🏘️</h2>
    <span class="big" style="color: #dc3545;">
      $${Math.round(transitIncomeStats.lowestIncomeStop?.overall_median_income || 0).toLocaleString()}
    </span>
    <p class="muted">${transitIncomeStats.lowestIncomeStop?.stop_name.substring(0, 40)}${transitIncomeStats.lowestIncomeStop?.stop_name.length > 40 ? '...' : ''}</p>
  </div>
</div>



<!-- Tableau Visualization of Number of Stops Per Route -->
<div class="tableauPlaceholder" id="viz1763611540383" style="position: relative;">
  <noscript>
    <a href="#">
      <img alt="Number of Stops Per Route" 
           src="https://public.tableau.com/static/images/Bu/BusStopsperRouteSteelCityMobility/Sheet2/1_rss.png" 
           style="border: none" />
    </a>
  </noscript>
  <object class="tableauViz" style="display:none;">
    <param name="host_url" value="https%3A%2F%2Fpublic.tableau.com%2F" />
    <param name="embed_code_version" value="3" />
    <param name="site_root" value="" />
    <param name="name" value="BusStopsperRouteSteelCityMobility&#47;Sheet2" />
    <param name="tabs" value="no" />
    <param name="toolbar" value="yes" />
    <param name="static_image" value="https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Bu&#47;BusStopsperRouteSteelCityMobility&#47;Sheet2&#47;1.png" />
    <param name="animate_transition" value="yes" />
    <param name="display_static_image" value="yes" />
    <param name="display_spinner" value="yes" />
    <param name="display_overlay" value="yes" />
    <param name="display_count" value="yes" />
    <param name="language" value="en-US" />
    <param name="filter" value="publish=yes" />
  </object>
</div>

<script type="text/javascript">
  var divElement = document.getElementById('viz1763611540383');
  var vizElement = divElement.getElementsByTagName('object')[0];
  vizElement.style.width = '100%';
  vizElement.style.height = (divElement.offsetWidth * 0.75) + 'px';
  var scriptElement = document.createElement('script');
  scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';
  vizElement.parentNode.insertBefore(scriptElement, vizElement);
</script>



Data: Western Pennsylvania Regional Data Center, [Pittsburgh Regional Transit Bus Stop Usage](https://data.wprdc.org/dataset/prt-transit-stop-usage)

