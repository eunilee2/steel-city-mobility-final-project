---
theme: light
title: Mobility Equity
toc: false
---

# Mobility Equity in Pittsburgh

## Two Faces of Pittsburgh Transit Access

```js
// Persona data grounded in real Pittsburgh neighborhood statistics
const personas = {
  jordan: {
    name: "Jordan",
    age: 34,
    demographic: "1-person household",
    neighborhood: "Brentwood, Allegheny County",
    busRoutes: ["51", "Y1"],
    censustract: "Census Tract 4781",
    medianIncome: "$54,446",
    noCarHouseholds: "21.5% (413 households)",
    transitAccess: "Low - 2 routes with 27 stops",
    occupation: "Fast Food/Retail Worker",
    workLocation: "Chipotle at Forbes Avenue, Oakland",
    dailyResponsibilities: [
      "Commute to work via bus (41-60 min total)",
      "Hourly shifts at minimum wage ($22/hr)",
      "No vehicle access - relies on transit",
      "Daily commute navigates high-poverty area"
    ],
    transportationMode: "Bus + Walking",
    // monthlyTransitCost: "$56-60 (monthly transit cost)"
  },
  
  jocelyn: {
    name: "Jocelyn",
    age: 44,
    demographic: "1-person household",
    neighborhood: "Lower Lawrenceville, Pittsburgh",
    busRoutes: ["91", "64", "88", "86", "54"],
    censustract: "Census Tract 603",
    medianIncome: "$86,094",
    noCarHouseholds: "11.3% (174 households)",
    transitAccess: "High- 5 routes with 41 bus stops",
    occupation: "Registered Nurse",
    workLocation: "UPMC University Center Medical Building (University of Pittsburgh)",
    dailyResponsibilities: [
      "Commute to hospital shifts via bus or car",
      "Earns $40/hour salary (~$80,000/year)",
      "Has car access for convenience/optional errands",
      "Chooses bus for commute when possible"
    ],
    transportationMode: "Bus + Car",
    // monthlyTransitCost: "$56-60 (transit choice) or $350-400 (car costs)"
  }
};

// Timeline data for each persona's daily commute
const timelines = {
  jordan: {
    morning: {
      commuteStart: "8:00 AM",
      walkToStop: { duration: "10 min", distance: "0.4 mi" },
      waitTime: { duration: "15 min", frequency: "51 bus" },
      transfer: { duration: "5 min wait", bus: "54 bus" },
      rideDuration: "25 min",
      walkToWork: { duration: "5 min", distance: "0.2 mi" },
      arrival: "9:00 AM"
    },
    evening: {
      commuteStart: "5:00 PM",
      walkToStop: { duration: "5 min", distance: "0.2 mi" },
      waitTime: { duration: "12-20 min", frequency: "54 bus return" },
      rideDuration: "25 min",
      transfer: { duration: "8 min wait", bus: "51 bus" },
      walkHome: { duration: "10 min", distance: "0.4 mi" },
      arrival: "6:20 PM",
      concerns: "Long commute home, limited evening service frequency"
    }
  },
  jocelyn: {
    transit: {
      morning: {
        commuteStart: "8:40 AM",
        walkToStop: { duration: "5 min", distance: "0.2 mi" },
        busRide: { duration: "15 min", bus: "93 bus" },
        walkToWork: { duration: "5 min", distance: "0.2 mi" },
        arrival: "9:05 AM"
      }
    },
    car: {
      morning: {
        commuteStart: "8:30 AM",
        driveDuration: "15-20 min",
        parking: "5 min",
        arrival: "8:50-8:55 AM",
        flexibility: "Can leave anytime"
      }
    }
  }
};
```


Public transit in Pittsburgh is not experienced equally across communities. While many lower-income neighborhoods within the city have moderate to adequate bus access, poorer suburbs farther from the core often face limited routes and are most vulnerable to service reductions. Because residents in lower-income areas rely on transit far more than wealthier neighborhoods, changes to bus frequency, routing, or reliability disproportionately affect them.

This dashboard examines these inequities by exploring: (1) how socioeconomic status relates to transit accessibility, and (2) how different socioeconomic groups experience bus service. Two personas illustrate how neighborhood context shapes daily mobility and transit dependence.

```js
html`
<div class="grid grid-cols-2" style="margin-top: 2rem;">
  <div class="card" style="padding: 2rem;">
    <div style="border-bottom: 3px solid #4e79a7; padding-bottom: 1rem; margin-bottom: 1rem;">
      <h2 style="margin: 0;">${personas.jordan.name}</h2>
      <p style="margin: 0.5rem 0 0 0; font-size: 0.95rem;">${personas.jordan.age} years old • ${personas.jordan.demographic} • ${personas.jordan.neighborhood}</p>
    </div>
    
    <div style="margin-bottom: 1.5rem;">
      <p style="font-weight: 600; margin: 0 0 0.5rem 0;">💼 Work & Responsibilities</p>
      <p style="margin: 0.3rem 0; font-size: 0.9rem;"><strong>${personas.jordan.occupation}</strong></p>
      <p style="margin: 0.3rem 0; font-size: 0.9rem;">${personas.jordan.workLocation}</p>
    </div>
    
    <div style="margin-bottom: 1.5rem;">
      <p style="font-weight: 600; margin: 0 0 0.5rem 0;">📅 Daily Responsibilities</p>
      <ul style="margin: 0; padding-left: 1.2rem; font-size: 0.9rem;">
        ${personas.jordan.dailyResponsibilities.map(r => html`<li style="margin: 0.3rem 0;">${r}</li>`)}
      </ul>
    </div>
  </div>

  <div class="card" style="padding: 2rem;">
    <div style="border-bottom: 3px solid #f28e2c; padding-bottom: 1rem; margin-bottom: 1rem;">
      <h2 style="margin: 0;">${personas.jocelyn.name}</h2>
      <p style="margin: 0.5rem 0 0 0; font-size: 0.95rem;">${personas.jocelyn.age} years old • ${personas.jocelyn.demographic}</p>
    </div>
    
    <div style="margin-bottom: 1.5rem;">
      <p style="font-weight: 600; margin: 0 0 0.5rem 0;">💼 Work & Responsibilities</p>
      <p style="margin: 0.3rem 0; font-size: 0.9rem;"><strong>${personas.jocelyn.occupation}</strong></p>
      <p style="margin: 0.3rem 0; font-size: 0.9rem;">${personas.jocelyn.workLocation}</p>
    </div>
    
    <div style="margin-bottom: 1.5rem;">
      <p style="font-weight: 600; margin: 0 0 0.5rem 0;">📅 Daily Schedule</p>
      <ul style="margin: 0; padding-left: 1.2rem; font-size: 0.9rem;">
        ${personas.jocelyn.dailyResponsibilities.map(r => html`<li style="margin: 0.3rem 0;">${r}</li>`)}
      </ul>
    </div>
  </div>
</div>
`
```
To begin exploring transit accessibility and equity across socioeconomic groups, we follow two personas. Jordan, a car-less fast-food worker, relies entirely on bus service from a higher-poverty neighborhood. Jocelyn, a registered nurse with a car, uses transit by choice. Their narratives reveal how income, location, and vehicle access shape mobility.

## Persona Neighborhood Context

```js
html`
<div class="grid grid-cols-2" style="margin-top: 2rem;">
  <div class="card" style="padding: 2rem;">
    <div style="border-bottom: 3px solid #4e79a7; padding-bottom: 1rem; margin-bottom: 1rem;">
      <h3 style="margin: 0; color: #4e79a7;">📍 ${personas.jordan.neighborhood}</h3>
      <p style="margin: 0.5rem 0 0 0; font-size: 0.9rem;">${personas.jordan.censustract}</p>
    </div>
    
    <div style="font-size: 0.9rem; margin-bottom: 1.5rem;">
      <p style="margin: 0.3rem 0;"><strong>Median Income:</strong> ${personas.jordan.medianIncome}</p>
      <p style="margin: 0.3rem 0;"><strong>No-Vehicle Households:</strong> ${personas.jordan.noCarHouseholds}</p>
      <p style="margin: 0.3rem 0;"><strong>Transit Access:</strong> ${personas.jordan.transitAccess}</p>
      <p style="margin: 0.3rem 0;"><strong>Bus Routes:</strong> ${personas.jordan.busRoutes.join(", ")}</p>
      <p style="margin: 0.3rem 0;"><strong>Primary Transport:</strong> ${personas.jordan.transportationMode}</p>
    </div>
  </div>

  <div class="card" style="padding: 2rem;">
    <div style="border-bottom: 3px solid #f28e2c; padding-bottom: 1rem; margin-bottom: 1rem;">
      <h3 style="margin: 0; color: #f28e2c;">📍 ${personas.jocelyn.neighborhood}</h3>
      <p style="margin: 0.5rem 0 0 0; font-size: 0.9rem;">${personas.jocelyn.censustract}</p>
    </div>
    
    <div style="font-size: 0.9rem;">
      <p style="margin: 0.3rem 0;"><strong>Median Income:</strong> ${personas.jocelyn.medianIncome}</p>
      <p style="margin: 0.3rem 0;"><strong>No-Car Households:</strong> ${personas.jocelyn.noCarHouseholds}</p>
      <p style="margin: 0.3rem 0;"><strong>Transit Access:</strong> ${personas.jocelyn.transitAccess}</p>
      <p style="margin: 0.3rem 0;"><strong>Bus Routes:</strong> ${personas.jocelyn.busRoutes.join(", ")}</p>
      <p style="margin: 0.3rem 0;"><strong>Primary Transport:</strong> ${personas.jocelyn.transportationMode}</p>
    </div>
  </div>
</div>
`
```
### Poverty Level by Tracts
Click on the tract with the marker to see details about poverty level in each persona's neighborhood.
Poverty levels are broken down into age groups: children (under 18), working-age adults (18-64), and seniors (65+).
```js
html`
<div class="grid grid-cols-2" style="margin-top: 2rem;">
    <iframe width="100%" height="400" allow="local-network-access; geolocation" title="Neighborhood-Level Visual Snapshot - Poverty Level" src="https://carnegiemellon.maps.arcgis.com/apps/mapviewer/index.html?configurableview=true&webmap=bafd1bfe129149c7851502ae9b77c2d9&theme=light&bookmarks=true&legend=true&scroll=false&center=-79.99695270247207,40.36826072127577&scale=36111.909643" ></iframe>
    <iframe width="100%" height="400" allow="local-network-access; geolocation" title="Neighborhood-Level Visual Snapshot - Poverty Level" src="https://carnegiemellon.maps.arcgis.com/apps/mapviewer/index.html?configurableview=true&webmap=bafd1bfe129149c7851502ae9b77c2d9&theme=light&bookmarks=true&legend=true&share=true&scroll=false&center=-79.96877964851696,40.45971867043966&scale=36111.909643" ></iframe>
</div>
`
```
### % of Households with No Vehicle Access by Tracts
Click on the tract with the marker to see details about % of households with no vehicle access in each persona's neighborhood. % of vehicle access is broken down into number of people in the household: 1-person, 2-person, 3-person, 4+ person.
```js
html`
<div class="grid grid-cols-2" style="margin-top: 2rem;">
    <iframe width="100%" height="400" allow="local-network-access; geolocation" title="Neighborhood-Level Visual Snapshot - No Vehicle Access" src="https://carnegiemellon.maps.arcgis.com/apps/mapviewer/index.html?configurableview=true&webmap=c849f620805c44e5b354c858d14ff306&theme=light&bookmarks=true&legend=true&scroll=false&center=-79.97536628432029,40.36999364431445&scale=72223.819286" ></iframe>
    <iframe width="100%" height="400" allow="local-network-access; geolocation" title="Neighborhood-Level Visual Snapshot - No Vehicle Access" src="https://carnegiemellon.maps.arcgis.com/apps/mapviewer/index.html?configurableview=true&webmap=c849f620805c44e5b354c858d14ff306&theme=light&bookmarks=true&legend=true&scroll=false&center=-79.95809372780174,40.45668190346116&scale=36111.909643" ></iframe>
</div>
`
```
Brentwood reflects a community where many residents lack vehicles and rely heavily on a small number of bus routes, making daily travel long and burdensome. In contrast, Lower Lawrenceville offers stronger economic stability and far denser transit coverage, giving residents more flexibility and shorter, more reliable trips. Together, these neighborhoods illustrate how location and transit access shape mobility options, time costs, and overall quality of life for Pittsburgh residents.

## Daily Commute Timeline Comparison

Jordan’s commute from Brentwood reflects the reality of a transit-dependent rider: long walks to limited bus routes, a required transfer, and nearly an hour of travel before reaching work. His morning is shaped by fixed schedules and little room for error.
Jocelyn’s trip from Lower Lawrenceville looks entirely different. With stronger transit coverage, her bus ride is quick and predictable. When transit isn’t convenient, she can simply drive. Her mobility is defined by choice, while Jordan’s is defined by necessity. Their timelines reveal how neighborhood context directly influences time, flexibility, and daily stress.

```js
html`
<div class="grid grid-cols-2" style="margin-top: 2rem;">
  <div class="card" style="padding: 2rem;">
    <h3 style="margin: 0 0 1.5rem 0; color: #4e79a7;">Jordan's Morning Commute to Work</h3>
    
    <!-- Morning Commute -->
    <div style="margin-bottom: 2rem;">
      
      <!-- Commute Time Breakdown Chart -->
      <div style="margin-bottom: 1.5rem; padding: 1rem 1.5rem 1rem 0.8rem; background: rgba(78, 121, 167, 0.08); border-radius: 0.5rem;">
        <p style="margin: 0 0 0.75rem 0; font-weight: 600; font-size: 0.9rem;">⏱️ Time Breakdown: 60 minutes total</p>
        <div style="display: grid; grid-template-columns: 16.67% 25% 8.33% 41.67% 8.33%; gap: 2px; height: 32px; margin-bottom: 0.75rem;">
          <div style="background: linear-gradient(135deg, #4e79a7, #5a88b5); display: flex; align-items: center; justify-content: center; border-radius: 0.25rem;">
            <span style="font-size: 0.7rem; font-weight: 600; color: #fff; text-shadow: 0 1px 2px rgba(0,0,0,0.3); text-align: center;">10 min</span>
          </div>
          <div style="background: linear-gradient(135deg, #6b9bc3, #7ba8d0); display: flex; align-items: center; justify-content: center; border-radius: 0.25rem;">
            <span style="font-size: 0.7rem; font-weight: 600; color: #fff; text-shadow: 0 1px 2px rgba(0,0,0,0.3); text-align: center;">15 min</span>
          </div>
          <div style="background: linear-gradient(135deg, #ffc107, #ffcd39); display: flex; align-items: center; justify-content: center; border-radius: 0.25rem;">
            <span style="font-size: 0.65rem; font-weight: 600; color: #000; text-shadow: 0 1px 1px rgba(255,255,255,0.5); text-align: center; white-space: nowrap;">5 m</span>
          </div>
          <div style="background: linear-gradient(135deg, #6b9bc3, #7ba8d0); display: flex; align-items: center; justify-content: center; border-radius: 0.25rem;">
            <span style="font-size: 0.7rem; font-weight: 600; color: #fff; text-shadow: 0 1px 2px rgba(0,0,0,0.3); text-align: center;">25 min</span>
          </div>
          <div style="background: linear-gradient(135deg, #4e79a7, #5a88b5); display: flex; align-items: center; justify-content: center; border-radius: 0.25rem;">
            <span style="font-size: 0.65rem; font-weight: 600; color: #fff; text-shadow: 0 1px 2px rgba(0,0,0,0.3); text-align: center; white-space: nowrap;">5 m</span>
          </div>
        </div>
        <div style="display: grid; grid-template-columns: 16.67% 25% 8.33% 41.67% 8.33%; gap: 2px; font-size: 0.75rem;">
          <div style="text-align: center;">
            <div style="color: #4e79a7; font-weight: 600;">Walk</div>
            <div style="color: #666;">10 min (16.7%)</div>
          </div>
          <div style="text-align: center;">
            <div style="color: #6b9bc3; font-weight: 600;">51 Bus</div>
            <div style="color: #666;">15 min (25%)</div>
          </div>
          <div style="text-align: center;">
            <div style="color: #ffc107; font-weight: 600;">Wait</div>
            <div style="color: #666;">5 min (8.3%)</div>
          </div>
          <div style="text-align: center;">
            <div style="color: #6b9bc3; font-weight: 600;">54 Bus</div>
            <div style="color: #666;">25 min (41.7%)</div>
          </div>
          <div style="text-align: center;">
            <div style="color: #4e79a7; font-weight: 600;">Walk</div>
            <div style="color: #666;">5 min (8.3%)</div>
          </div>
        </div>
      </div>
      
      <h4 style="margin: 0 0 1rem 0;">🚌 By Bus </h4>

      <div style="position: relative; padding-left: 2rem;">
        <div style="position: absolute; left: 0; top: 0; bottom: 0; width: 3px; background: linear-gradient(to bottom, #4e79a7, #6b9bc3);"></div>
        
        <div style="margin-bottom: 1rem; position: relative;">
          <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #4e79a7; border-radius: 50%; border: 2px solid #fff;"></div>
          <p style="margin: 0; font-weight: 600;">${timelines.jordan.morning.commuteStart}</p>
          <p style="margin: 0.2rem 0 0 0; font-size: 0.85rem;">Leaves home in Brentwood</p>
        </div>
        
        <div style="margin-bottom: 1rem; position: relative;">
          <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #4e79a7; border-radius: 50%; border: 2px solid #fff;"></div>
          <p style="margin: 0; font-weight: 600;">Walk to 51 bus stop</p>
          <p style="margin: 0.2rem 0 0 0; font-size: 0.85rem;">⏱️ ${timelines.jordan.morning.walkToStop.duration} • 📍 ${timelines.jordan.morning.walkToStop.distance}</p>
        </div>
        
        <div style="margin-bottom: 1rem; position: relative;">
          <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #4e79a7; border-radius: 50%; border: 2px solid #fff;"></div>
          <p style="margin: 0; font-weight: 600;">51 Bus ride</p>
          <p style="margin: 0.2rem 0 0 0; font-size: 0.85rem;">⏱️ ${timelines.jordan.morning.waitTime.duration}</p>
        </div>
        
        <div style="margin-bottom: 1rem; position: relative;">
          <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #6b9bc3; border-radius: 50%; border: 2px solid #fff;"></div>
          <p style="margin: 0; font-weight: 600;">Wait & Transfer</p>
          <p style="margin: 0.2rem 0 0 0; font-size: 0.85rem;">⏱️ ${timelines.jordan.morning.transfer.duration} for 54 bus</p>
        </div>
        
        <div style="margin-bottom: 1rem; position: relative;">
          <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #6b9bc3; border-radius: 50%; border: 2px solid #fff;"></div>
          <p style="margin: 0; font-weight: 600;">54 Bus to Oakland</p>
          <p style="margin: 0.2rem 0 0 0; font-size: 0.85rem;">⏱️ ${timelines.jordan.morning.rideDuration}</p>
        </div>
        
        <div style="margin-bottom: 1rem; position: relative;">
          <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #4e79a7; border-radius: 50%; border: 2px solid #fff;"></div>
          <p style="margin: 0; font-weight: 600;">Walk to Chipotle</p>
          <p style="margin: 0.2rem 0 0 0; font-size: 0.85rem;">⏱️ ${timelines.jordan.morning.walkToWork.duration} down Craig Street</p>
        </div>
        
        <div style="position: relative;">
          <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #28a745; border-radius: 50%; border: 2px solid #fff;"></div>
          <p style="margin: 0; color: #28a745; font-weight: 600;">${timelines.jordan.morning.arrival}</p>
          <p style="margin: 0.2rem 0 0 0; font-size: 0.85rem;">Arrives at work</p>
          <p style="margin: 0.5rem 0 0 0; font-size: 0.8rem; font-style: italic;">Total: ~60 minutes</p>
        </div>
      </div>
    </div>
  </div>

  <div class="card" style="padding: 2rem;">
    <h3 style="margin: 0 0 1.5rem 0; color: #f28e2c;">Jocelyn's Morning Commute to Work</h3>
    
    <!-- Time Breakdown Comparison Card -->
    <div style="margin-bottom: 2rem; padding: 1rem 1.5rem 1rem 0.8rem; background: rgba(242, 142, 44, 0.08); border-radius: 0.5rem;">
      <!-- Transit Chart -->
      <div style="margin-bottom: 2rem;">
        <p style="margin: 0 0 0.75rem 0; font-weight: 600; font-size: 0.9rem;">🚌 Transit: 25 minutes total</p>
        <div style="display: grid; grid-template-columns: 20% 60% 20%; gap: 2px; height: 32px; margin-bottom: 0.75rem;">
          <div style="background: linear-gradient(135deg, #4e79a7, #5a88b5); display: flex; align-items: center; justify-content: center; border-radius: 0.25rem;">
            <span style="font-size: 0.7rem; font-weight: 600; color: #fff; text-shadow: 0 1px 2px rgba(0,0,0,0.3); text-align: center;">5 min</span>
          </div>
          <div style="background: linear-gradient(135deg, #6b9bc3, #7ba8d0); display: flex; align-items: center; justify-content: center; border-radius: 0.25rem;">
            <span style="font-size: 0.7rem; font-weight: 600; color: #fff; text-shadow: 0 1px 2px rgba(0,0,0,0.3); text-align: center;">15 min</span>
          </div>
          <div style="background: linear-gradient(135deg, #4e79a7, #5a88b5); display: flex; align-items: center; justify-content: center; border-radius: 0.25rem;">
            <span style="font-size: 0.7rem; font-weight: 600; color: #fff; text-shadow: 0 1px 2px rgba(0,0,0,0.3); text-align: center;">5 min</span>
          </div>
        </div>
        <div style="display: grid; grid-template-columns: 20% 60% 20%; gap: 2px; font-size: 0.75rem;">
          <div style="text-align: center;">
            <div style="color: #4e79a7; font-weight: 600;">Walk</div>
            <div style="color: #666;">5 min (20%)</div>
          </div>
          <div style="text-align: center;">
            <div style="color: #6b9bc3; font-weight: 600;">93 Bus</div>
            <div style="color: #666;">15 min (60%)</div>
          </div>
          <div style="text-align: center;">
            <div style="color: #4e79a7; font-weight: 600;">Walk</div>
            <div style="color: #666;">5 min (20%)</div>
          </div>
        </div>
      </div>
      
      <!-- Car Chart -->
      <div>
        <p style="margin: 0 0 0.75rem 0; font-weight: 600; font-size: 0.9rem;">🚗 Car: 20-25 minutes total</p>
        <div style="display: grid; grid-template-columns: 60% 25%; gap: 2px; height: 32px; margin-bottom: 0.75rem;">
          <div style="background: linear-gradient(135deg, #28a745, #2ecc71); display: flex; align-items: center; justify-content: center; border-radius: 0.25rem;">
            <span style="font-size: 0.7rem; font-weight: 600; color: #fff; text-shadow: 0 1px 2px rgba(0,0,0,0.3); text-align: center;">15-20 min</span>
          </div>
          <div style="background: linear-gradient(135deg, #20c997, #38b6a8); display: flex; align-items: center; justify-content: center; border-radius: 0.25rem;">
            <span style="font-size: 0.7rem; font-weight: 600; color: #fff; text-shadow: 0 1px 2px rgba(0,0,0,0.3); text-align: center;">5 min</span>
          </div>
        </div>
        <div style="display: grid; grid-template-columns: 60% 25%; gap: 2px; font-size: 0.75rem;">
          <div style="text-align: center;">
            <div style="color: #28a745; font-weight: 600;">Drive</div>
            <div style="color: #666;">15-20 min (75%)</div>
          </div>
          <div style="text-align: center;">
            <div style="color: #20c997; font-weight: 600;">Parking</div>
            <div style="color: #666;">5 min (25%)</div>
          </div>
        </div>
      </div>
    </div>
    
    <!-- Timelines below charts -->
    <div class="grid grid-cols-2" style="gap: 2rem;">
      <!-- Transit Option (Left) -->
      <div>
        <h4 style="margin: 0 0 1rem 0;">🚌 By Bus (Choice/Convenience)</h4>
        
        <div style="position: relative; padding-left: 2rem;">
          <div style="position: absolute; left: 0; top: 0; bottom: 0; width: 3px; background: linear-gradient(to bottom, #4e79a7, #6b9bc3);"></div>
          
          <div style="margin-bottom: 1rem; position: relative;">
            <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #4e79a7; border-radius: 50%; border: 2px solid #fff;"></div>
            <p style="margin: 0; font-weight: 600;">${timelines.jocelyn.transit.morning.commuteStart}</p>
            <p style="margin: 0.2rem 0 0 0; font-size: 0.85rem;">Leaves home in Lawrenceville</p>
          </div>
          
          <div style="margin-bottom: 1rem; position: relative;">
            <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #4e79a7; border-radius: 50%; border: 2px solid #fff;"></div>
            <p style="margin: 0; font-weight: 600;">Walk to 93 bus stop</p>
            <p style="margin: 0.2rem 0 0 0; font-size: 0.85rem;">⏱️ ${timelines.jocelyn.transit.morning.walkToStop.duration} • 📍 ${timelines.jocelyn.transit.morning.walkToStop.distance}</p>
          </div>
          
          <div style="margin-bottom: 1rem; position: relative;">
            <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #4e79a7; border-radius: 50%; border: 2px solid #fff;"></div>
            <p style="margin: 0; font-weight: 600;">93 Bus to UPMC</p>
            <p style="margin: 0.2rem 0 0 0; font-size: 0.85rem;">⏱️ ${timelines.jocelyn.transit.morning.busRide.duration}</p>
          </div>
          
          <div style="margin-bottom: 1rem; position: relative;">
            <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #4e79a7; border-radius: 50%; border: 2px solid #fff;"></div>
            <p style="margin: 0; font-weight: 600;">Walk to Medical Building</p>
            <p style="margin: 0.2rem 0 0 0; font-size: 0.85rem;">⏱️ ${timelines.jocelyn.transit.morning.walkToWork.duration} • 📍 ${timelines.jocelyn.transit.morning.walkToWork.distance}</p>
          </div>
          
          <div style="position: relative;">
            <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #28a745; border-radius: 50%; border: 2px solid #fff;"></div>
            <p style="margin: 0; color: #28a745; font-weight: 600;">${timelines.jocelyn.transit.morning.arrival}</p>
            <p style="margin: 0.2rem 0 0 0; font-size: 0.85rem;">Arrives at work</p>
            <p style="margin: 0.5rem 0 0 0; font-size: 0.8rem; font-style: italic;">Total: ~25 minutes</p>
          </div>
          
          <div style="margin-top: 1rem; padding: 0.75rem; background: rgba(78, 121, 167, 0.15); border-left: 3px solid #4e79a7; border-radius: 0.25rem;">
            <p style="margin: 0; color: #4e79a7; font-weight: 600; font-size: 0.85rem;">✓ Reliable transit option</p>
            <p style="margin: 0.3rem 0 0 0; font-size: 0.8rem;">1 transfer, well-served by 93 bus, good for reducing transit costs</p>
          </div>
        </div>
      </div>
      
      <!-- Car Option (Right) -->
      <div>
        <h4 style="margin: 0 0 1rem 0;">🚗 By Car (Optional/Flexible)</h4>
        
        <div style="position: relative; padding-left: 2rem;">
          <div style="position: absolute; left: 0; top: 0; bottom: 0; width: 3px; background: linear-gradient(to bottom, #28a745, #20c997);"></div>
          
          <div style="margin-bottom: 1rem; position: relative;">
            <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #28a745; border-radius: 50%; border: 2px solid #fff;"></div>
            <p style="margin: 0; font-weight: 600;">${timelines.jocelyn.car.morning.commuteStart}</p>
            <p style="margin: 0.2rem 0 0 0; font-size: 0.85rem;">Flexible departure time</p>
          </div>
          
          <div style="margin-bottom: 1rem; position: relative;">
            <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #28a745; border-radius: 50%; border: 2px solid #fff;"></div>
            <p style="margin: 0; font-weight: 600;">Drive to UPMC</p>
            <p style="margin: 0.2rem 0 0 0; font-size: 0.85rem;">⏱️ ${timelines.jocelyn.car.morning.driveDuration}</p>
            <p style="margin: 0.2rem 0 0 0; font-size: 0.8rem;">Direct route, no transfers</p>
          </div>
          
          <div style="position: relative;">
            <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #28a745; border-radius: 50%; border: 2px solid #fff;"></div>
            <p style="margin: 0; font-weight: 600;">Parking</p>
            <p style="margin: 0.2rem 0 0 0; font-size: 0.85rem;">⏱️ ${timelines.jocelyn.car.morning.parking}</p>
          </div>
          
          <div style="position: relative; margin-bottom: 1rem;">
            <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #28a745; border-radius: 50%; border: 2px solid #fff;"></div>
            <p style="margin: 0; color: #28a745; font-weight: 600;">${timelines.jocelyn.car.morning.arrival}</p>
            <p style="margin: 0.2rem 0 0 0; font-size: 0.85rem;">Arrives at work</p>
            <p style="margin: 0.5rem 0 0 0; font-size: 0.8rem; font-style: italic;">Total: ~20-25 minutes</p>
          </div>
          
          <div style="margin-top: 1rem; padding: 0.75rem; background: rgba(40, 167, 69, 0.15); border-left: 3px solid #28a745; border-radius: 0.25rem;">
            <p style="margin: 0; color: #28a745; font-weight: 600; font-size: 0.85rem;">✓ Optional flexibility</p>
            <p style="margin: 0.3rem 0 0 0; font-size: 0.8rem;">Can adjust timing, run errands, useful for spontaneous needs</p>
          </div>
        </div>
      </div>
    </div>
    
  </div>
</div>
<div>
    <iframe width="100%" height="600" allow="local-network-access; geolocation" title="Neighborhood-Level Visual Snapshot - Time on Transit to Oakland" src="https://carnegiemellon.maps.arcgis.com/apps/mapviewer/index.html?configurableview=true&webmap=de62d2d1668548329d7bae60e1768061&theme=light&scroll=false&center=-79.94770734495785,40.47197766398784&scale=577790.554289" ></iframe>
</div>
`
```
The map above visualizes estimated travel times from each persona’s neighborhood to Oakland, and these estimates align closely with the commute timelines shown below. For Jocelyn, living in a well-connected neighborhood with multiple reliable routes, her estimated and actual travel times remain short and flexible.

For Jordan, however, the same travel-time map tells only part of the story. Although the estimated 41–60 minute commute from Brentwood matches his timeline, real conditions (such as delays, missed transfers, or reductions to key routes) can significantly extend his travel time. Because he has no car and relies solely on two critical bus lines, any service disruption disproportionately affects him.

Together, the map and timelines highlight how transit accessibility is not only about distance, but also about reliability and how changes to service can deepen inequities for riders who depend on the system most.

## Summary Comparison Table 

```js
html`
<div style="margin-top: 2rem;">
  <table style="width: 100%; border-collapse: collapse; font-size: 0.9rem; table-layout: fixed;">
    <thead>
      <tr style="background: #f5f5f5;">
        <th style="border: 1px solid #ddd; padding: 1rem; text-align: left; font-weight: 600;">Factor</th>
        <th style="border: 1px solid #ddd; padding: 1rem; text-align: left; font-weight: 600; color: #4e79a7;">Jordan (Brentwood)</th>
        <th style="border: 1px solid #ddd; padding: 1rem; text-align: left; font-weight: 600; color: #f28e2c;">Jocelyn (Lower Lawrenceville)</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td style="border: 1px solid #ddd; padding: 1rem; font-weight: 600;">Income Level</td>
        <td style="border: 1px solid #ddd; padding: 1rem;">$54,446 (Low)</td>
        <td style="border: 1px solid #ddd; padding: 1rem;">$86,094 (Higher)</td>
      </tr>
      <tr style="background: #fafafa;">
        <td style="border: 1px solid #ddd; padding: 1rem; font-weight: 600;">Vehicle Access</td>
        <td style="border: 1px solid #ddd; padding: 1rem;">None (21.5% of households)</td>
        <td style="border: 1px solid #ddd; padding: 1rem;">Yes (11.3% of households)</td>
      </tr>
      <tr>
        <td style="border: 1px solid #ddd; padding: 1rem; font-weight: 600;">Transit Routes</td>
        <td style="border: 1px solid #ddd; padding: 1rem;">2 routes (51, Y1)</td>
        <td style="border: 1px solid #ddd; padding: 1rem;">5 routes (91, 64, 88, 86, 54)</td>
      </tr>
      <tr style="background: #fafafa;">
        <td style="border: 1px solid #ddd; padding: 1rem; font-weight: 600;">Transit Access</td>
        <td style="border: 1px solid #ddd; padding: 1rem;">Low (27 stops)</td>
        <td style="border: 1px solid #ddd; padding: 1rem;">High (41 stops)</td>
      </tr>
      <tr>
        <td style="border: 1px solid #ddd; padding: 1rem; font-weight: 600;">Morning Commute Time</td>
        <td style="border: 1px solid #ddd; padding: 1rem;"><strong style="color: #d9534f;">60 minutes</strong></td>
        <td style="border: 1px solid #ddd; padding: 1rem;"><strong style="color: #28a745;">25 minutes (transit) or 20-25 (car)</strong></td>
      </tr>
      <tr style="background: #fafafa;">
        <td style="border: 1px solid #ddd; padding: 1rem; font-weight: 600;">Transfers Required</td>
        <td style="border: 1px solid #ddd; padding: 1rem;">1 transfer (51 → 54 bus)</td>
        <td style="border: 1px solid #ddd; padding: 1rem;">0 transfers (direct route available)</td>
      </tr>
      <tr>
        <td style="border: 1px solid #ddd; padding: 1rem; font-weight: 600;">Transportation Mode</td>
        <td style="border: 1px solid #ddd; padding: 1rem;">Bus + Walking (only option)</td>
        <td style="border: 1px solid #ddd; padding: 1rem;">Bus + Car (choice)</td>
      </tr>
      <tr style="background: #fafafa;">
        <td style="border: 1px solid #ddd; padding: 1rem; font-weight: 600;">Commute Flexibility</td>
        <td style="border: 1px solid #ddd; padding: 1rem;">Fixed (depends on bus schedule)</td>
        <td style="border: 1px solid #ddd; padding: 1rem;">High (can choose transit or drive)</td>
      </tr>
      <tr>
        <td style="border: 1px solid #ddd; padding: 1rem; font-weight: 600;">Daily Time Burden</td>
        <td style="border: 1px solid #ddd; padding: 1rem;"><strong style="color: #d9534f;">~2 hours round-trip</strong></td>
        <td style="border: 1px solid #ddd; padding: 1rem;"><strong style="color: #28a745;">~50 minutes round-trip</strong></td>
      </tr>
      <tr style="background: #fafafa;">
        <td style="border: 1px solid #ddd; padding: 1rem; font-weight: 600;">Equity Issue</td>
        <td style="border: 1px solid #ddd; padding: 1rem;">Transport-dependent; limited choices</td>
        <td style="border: 1px solid #ddd; padding: 1rem;">Transport-advantaged; multiple options</td>
      </tr>
    </tbody>
  </table>
  
  <div style="margin-top: 2rem; padding: 1.5rem; background: rgba(217, 83, 79, 0.1); border-left: 4px solid #d9534f; border-radius: 0.5rem;">
    <h4 style="margin: 0 0 0.5rem 0; color: #d9534f;">Key Takeaway</h4>
    <p style="margin: 0; font-size: 0.95rem;">
      Jordan spends <strong>60 minutes commuting to work</strong> due to limited transit options and required transfers, while Jocelyn can reach the same destination in <strong>25 minutes by bus or 20-25 minutes by car</strong>. This inequality reveals how neighborhood infrastructure and vehicle access create vastly different mobility experiences—and significantly different quality-of-life outcomes for Pittsburgh residents.
    </p>
  </div>
</div>
`
```

---

*Built with Observable and ArcGIS Online (Dec 2025)*

*Data Sources Used*
- *ACS Vehicle Availability Variables - Boundaries, ArcGIS, https://carnegiemellon.maps.arcgis.com/home/item.html?id=9a9e43ec1603446880c50d4ed1df2207*
- *ACS Poverty Status Variables - Boundaries, ArcGIS, https://carnegiemellon.maps.arcgis.com/home/item.html?id=0e468b75bca545ee8dc4b039cbb5aff6*
- *ACS Median Household Income Variables - Boundaries, ArcGIS, https://carnegiemellon.maps.arcgis.com/home/item.html?id=45ede6d6ff7e4cbbbffa60d34227e462*
- *PRT Routes - Current (full system), Pittsburgh Regional Transit Open Geospatial Data, https://carnegiemellon.maps.arcgis.com/home/item.html?id=9483dc3e6dc8495badef05a3f7f38dff*
- *PRT Stops - Current (full system), Pittsburgh Regional Transit Open Geospatial Data, https://carnegiemellon.maps.arcgis.com/home/item.html?id=a29f37608eb34c3895332ff99eea9b17*
