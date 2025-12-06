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
  marcus: {
    name: "Jordan",
    age: 34,
    demographic: "1-person household",
    neighborhood: "Brentwood, Pittsburgh",
    censustract: "Census Tract 4781",
    medianIncome: "$54,446",
    noCarHouseholds: "21.5% (413 households)",
    transitFrequency: "High - 2 routes (Y1, 51) with 27 stops",
    occupation: "Fast Food/Retail Worker",
    workLocation: "Chipotle at Forbes Avenue, Oakland",
    dailyResponsibilities: [
      "Commute to work via bus (41-60 min total)",
      "Hourly shifts at minimum wage ($22/hr)",
      "No vehicle access - relies on transit",
      "Daily commute navigates high-poverty area"
    ],
    transportationMode: "Bus + Walking",
    monthlyTransitCost: "$56-60 (monthly transit cost)"
  },
  
  jen: {
    name: "Jocelyn",
    age: 44,
    demographic: "1-person household",
    neighborhood: "Lower Lawrenceville, Pittsburgh",
    censustract: "Census Tract 603",
    medianIncome: "$86,094",
    noCarHouseholds: "11.3% (174 households)",
    transitFrequency: "Medium - 5 routes with 41 bus stops",
    occupation: "Registered Nurse",
    workLocation: "UPMC University Center Medical Building (University of Pittsburgh)",
    dailyResponsibilities: [
      "Commute to hospital shifts via bus or car",
      "Earns $40/hour salary (~$80,000/year)",
      "Has car access for convenience/optional errands",
      "Chooses bus for commute when possible"
    ],
    transportationMode: "Bus + Car (optional)",
    monthlyTransitCost: "$56-60 (transit choice) or $350-400 (car costs)"
  }
};

// Timeline data for each persona's daily commute
const timelines = {
  marcus: {
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
  jen: {
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

```js
html`
<div class="grid grid-cols-2">
  <div class="card" style="padding: 2rem;">
    <div style="border-bottom: 3px solid #4e79a7; padding-bottom: 1rem; margin-bottom: 1rem;">
      <h2 style="margin: 0;">${personas.marcus.name}</h2>
      <p style="margin: 0.5rem 0 0 0; font-size: 0.95rem;">${personas.marcus.age} years old • ${personas.marcus.demographic}</p>
    </div>
    
    <div style="margin-bottom: 1.5rem;">
      <p style="font-weight: 600; margin: 0 0 0.5rem 0;">💼 Work & Responsibilities</p>
      <p style="margin: 0.3rem 0; font-size: 0.9rem;"><strong>${personas.marcus.occupation}</strong></p>
      <p style="margin: 0.3rem 0; font-size: 0.9rem;">${personas.marcus.workLocation}</p>
    </div>
    
    <div style="margin-bottom: 1.5rem;">
      <p style="font-weight: 600; margin: 0 0 0.5rem 0;">📅 Daily Responsibilities</p>
      <ul style="margin: 0; padding-left: 1.2rem; font-size: 0.9rem;">
        ${personas.marcus.dailyResponsibilities.map(r => html`<li style="margin: 0.3rem 0;">${r}</li>`)}
      </ul>
    </div>
    
    <div style="margin-bottom: 1.5rem; padding: 1rem; background: rgba(78, 121, 167, 0.08); border-radius: 0.5rem;">
      <p style="font-weight: 600; margin: 0 0 0.5rem 0;">📍 Neighborhood</p>
      <p style="margin: 0;">${personas.marcus.neighborhood}</p>
      <p style="margin: 0; font-size: 0.9rem;">${personas.marcus.censustract}</p>
    </div>
    
    <div style="margin-bottom: 1.5rem; padding: 1rem; background: rgba(78, 121, 167, 0.08); border-radius: 0.5rem;">
      <p style="font-weight: 600; margin: 0 0 0.5rem 0;">Neighborhood Statistics</p>
      <div style="font-size: 0.9rem;">
        <p style="margin: 0.3rem 0;"><strong>Median Income:</strong> ${personas.marcus.medianIncome}</p>
        <p style="margin: 0.3rem 0;"><strong>No-Vehicle Households:</strong> ${personas.marcus.noCarHouseholds}</p>
        <p style="margin: 0.3rem 0;"><strong>Transit Access:</strong> ${personas.marcus.transitFrequency}</p>
        <p style="margin: 0.3rem 0;"><strong>Primary Transport:</strong> ${personas.marcus.transportationMode}</p>
        <p style="margin: 0.3rem 0;"><strong>Monthly Transit Cost:</strong> ${personas.marcus.monthlyTransitCost}</p>
      </div>
    </div>
  </div>

  <div class="card" style="padding: 2rem;">
    <div style="border-bottom: 3px solid #f28e2c; padding-bottom: 1rem; margin-bottom: 1rem;">
      <h2 style="margin: 0;">${personas.jen.name}</h2>
      <p style="margin: 0.5rem 0 0 0; font-size: 0.95rem;">${personas.jen.age} years old • ${personas.jen.demographic}</p>
    </div>
    
    <div style="margin-bottom: 1.5rem;">
      <p style="font-weight: 600; margin: 0 0 0.5rem 0;">💼 Work & Responsibilities</p>
      <p style="margin: 0.3rem 0; font-size: 0.9rem;"><strong>${personas.jen.occupation}</strong></p>
      <p style="margin: 0.3rem 0; font-size: 0.9rem;">${personas.jen.workLocation}</p>
    </div>
    
    <div style="margin-bottom: 1.5rem;">
      <p style="font-weight: 600; margin: 0 0 0.5rem 0;">📅 Daily Schedule</p>
      <ul style="margin: 0; padding-left: 1.2rem; font-size: 0.9rem;">
        ${personas.jen.dailyResponsibilities.map(r => html`<li style="margin: 0.3rem 0;">${r}</li>`)}
      </ul>
    </div>
    
    <div style="margin-bottom: 1.5rem; padding: 1rem; background: rgba(78, 121, 167, 0.08); border-radius: 0.5rem;">
      <p style="font-weight: 600; margin: 0 0 0.5rem 0;">📍 Neighborhood</p>
      <p style="margin: 0;">${personas.jen.neighborhood}</p>
      <p style="margin: 0; font-size: 0.9rem;">${personas.jen.censustract}</p>
    </div>
    
    <div style="margin-bottom: 1.5rem; padding: 1rem; background: rgba(78, 121, 167, 0.08); border-radius: 0.5rem;">
      <p style="font-weight: 600; margin: 0 0 0.5rem 0;">Neighborhood Statistics</p>
      <div style="font-size: 0.9rem;">
        <p style="margin: 0.3rem 0;"><strong>Median Income:</strong> ${personas.jen.medianIncome}</p>
        <p style="margin: 0.3rem 0;"><strong>No-Car Households:</strong> ${personas.jen.noCarHouseholds}</p>
        <p style="margin: 0.3rem 0;"><strong>Transit Frequency:</strong> ${personas.jen.transitFrequency}</p>
        <p style="margin: 0.3rem 0;"><strong>Primary Transport:</strong> ${personas.jen.transportationMode}</p>
        <p style="margin: 0.3rem 0;"><strong>Transit Cost/Month:</strong> ${personas.jen.monthlyTransitCost}</p>
      </div>
    </div>
  </div>
</div>
`
```

## Daily Commute Timeline Comparison

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
          <p style="margin: 0; font-weight: 600;">${timelines.marcus.morning.commuteStart}</p>
          <p style="margin: 0.2rem 0 0 0; font-size: 0.85rem;">Leaves home in Brentwood</p>
        </div>
        
        <div style="margin-bottom: 1rem; position: relative;">
          <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #4e79a7; border-radius: 50%; border: 2px solid #fff;"></div>
          <p style="margin: 0; font-weight: 600;">Walk to 51 bus stop</p>
          <p style="margin: 0.2rem 0 0 0; font-size: 0.85rem;">⏱️ ${timelines.marcus.morning.walkToStop.duration} • 📍 ${timelines.marcus.morning.walkToStop.distance}</p>
        </div>
        
        <div style="margin-bottom: 1rem; position: relative;">
          <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #4e79a7; border-radius: 50%; border: 2px solid #fff;"></div>
          <p style="margin: 0; font-weight: 600;">51 Bus ride</p>
          <p style="margin: 0.2rem 0 0 0; font-size: 0.85rem;">⏱️ ${timelines.marcus.morning.waitTime.duration}</p>
        </div>
        
        <div style="margin-bottom: 1rem; position: relative;">
          <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #6b9bc3; border-radius: 50%; border: 2px solid #fff;"></div>
          <p style="margin: 0; font-weight: 600;">Wait & Transfer</p>
          <p style="margin: 0.2rem 0 0 0; font-size: 0.85rem;">⏱️ ${timelines.marcus.morning.transfer.duration} for 54 bus</p>
        </div>
        
        <div style="margin-bottom: 1rem; position: relative;">
          <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #6b9bc3; border-radius: 50%; border: 2px solid #fff;"></div>
          <p style="margin: 0; font-weight: 600;">54 Bus to Oakland</p>
          <p style="margin: 0.2rem 0 0 0; font-size: 0.85rem;">⏱️ ${timelines.marcus.morning.rideDuration}</p>
        </div>
        
        <div style="margin-bottom: 1rem; position: relative;">
          <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #4e79a7; border-radius: 50%; border: 2px solid #fff;"></div>
          <p style="margin: 0; font-weight: 600;">Walk to Chipotle</p>
          <p style="margin: 0.2rem 0 0 0; font-size: 0.85rem;">⏱️ ${timelines.marcus.morning.walkToWork.duration} down Craig Street</p>
        </div>
        
        <div style="position: relative;">
          <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #28a745; border-radius: 50%; border: 2px solid #fff;"></div>
          <p style="margin: 0; color: #28a745; font-weight: 600;">${timelines.marcus.morning.arrival}</p>
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
            <p style="margin: 0; font-weight: 600;">${timelines.jen.transit.morning.commuteStart}</p>
            <p style="margin: 0.2rem 0 0 0; font-size: 0.85rem;">Leaves home in Lawrenceville</p>
          </div>
          
          <div style="margin-bottom: 1rem; position: relative;">
            <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #4e79a7; border-radius: 50%; border: 2px solid #fff;"></div>
            <p style="margin: 0; font-weight: 600;">Walk to 93 bus stop</p>
            <p style="margin: 0.2rem 0 0 0; font-size: 0.85rem;">⏱️ ${timelines.jen.transit.morning.walkToStop.duration} • 📍 ${timelines.jen.transit.morning.walkToStop.distance}</p>
          </div>
          
          <div style="margin-bottom: 1rem; position: relative;">
            <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #4e79a7; border-radius: 50%; border: 2px solid #fff;"></div>
            <p style="margin: 0; font-weight: 600;">93 Bus to UPMC</p>
            <p style="margin: 0.2rem 0 0 0; font-size: 0.85rem;">⏱️ ${timelines.jen.transit.morning.busRide.duration}</p>
          </div>
          
          <div style="margin-bottom: 1rem; position: relative;">
            <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #4e79a7; border-radius: 50%; border: 2px solid #fff;"></div>
            <p style="margin: 0; font-weight: 600;">Walk to Medical Building</p>
            <p style="margin: 0.2rem 0 0 0; font-size: 0.85rem;">⏱️ ${timelines.jen.transit.morning.walkToWork.duration} • 📍 ${timelines.jen.transit.morning.walkToWork.distance}</p>
          </div>
          
          <div style="position: relative;">
            <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #28a745; border-radius: 50%; border: 2px solid #fff;"></div>
            <p style="margin: 0; color: #28a745; font-weight: 600;">${timelines.jen.transit.morning.arrival}</p>
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
            <p style="margin: 0; font-weight: 600;">${timelines.jen.car.morning.commuteStart}</p>
            <p style="margin: 0.2rem 0 0 0; font-size: 0.85rem;">Flexible departure time</p>
          </div>
          
          <div style="margin-bottom: 1rem; position: relative;">
            <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #28a745; border-radius: 50%; border: 2px solid #fff;"></div>
            <p style="margin: 0; font-weight: 600;">Drive to UPMC</p>
            <p style="margin: 0.2rem 0 0 0; font-size: 0.85rem;">⏱️ ${timelines.jen.car.morning.driveDuration}</p>
            <p style="margin: 0.2rem 0 0 0; font-size: 0.8rem;">Direct route, no transfers</p>
          </div>
          
          <div style="position: relative;">
            <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #28a745; border-radius: 50%; border: 2px solid #fff;"></div>
            <p style="margin: 0; font-weight: 600;">Parking</p>
            <p style="margin: 0.2rem 0 0 0; font-size: 0.85rem;">⏱️ ${timelines.jen.car.morning.parking}</p>
          </div>
          
          <div style="position: relative; margin-bottom: 1rem;">
            <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #28a745; border-radius: 50%; border: 2px solid #fff;"></div>
            <p style="margin: 0; color: #28a745; font-weight: 600;">${timelines.jen.car.morning.arrival}</p>
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
`
```


## Neighborhood Infrastructure Comparison

```js
html`
<div class="grid grid-cols-2" style="margin-top: 2rem; margin-bottom: 2rem; gap: 2rem;">
  <--trace Neighborhood Mini-Map A: Jordan's Transit-Dependent Area -->
  <div class="card" style="padding: 2rem;">
    <h3 style="margin: 0 0 1.5rem 0; color: #4e79a7;">📍 Map A: Transit-Dependent Neighborhood (Jordan - Brentwood)</h3>
    <p style="margin: 0 0 1.5rem 0; font-size: 0.9rem;">Low-income with transit access: Median income $54,446 • 21.5% no-vehicle households</p>
    
    <svg width="100%" height="300" viewBox="0 0 400 300" style="border: 2px solid #ddd; border-radius: 0.5rem; background: #fff; margin-bottom: 1.5rem;">
      <--trace Grid background -->
      <defs>
        <pattern id="grid-a" width="40" height="40" patternUnits="userSpaceOnUse">
          <path d="M 40 0 L 0 0 0 40" fill="none" stroke="#e0e0e0" stroke-width="0.5"/>
        </pattern>
      </defs>
      <rect width="400" height="300" fill="url(#grid-a)" />
      
      <--trace Major streets -->
      <line x1="20" y1="150" x2="380" y2="150" stroke="#bbb" stroke-width="3"/>
      <line x1="200" y1="20" x2="200" y2="280" stroke="#bbb" stroke-width="3"/>
      
      <--trace Bus routes (multiple, frequent) -->
      <line x1="20" y1="100" x2="380" y2="100" stroke="#4e79a7" stroke-width="2" stroke-dasharray="5,5"/>
      <line x1="20" y1="200" x2="380" y2="200" stroke="#4e79a7" stroke-width="2" stroke-dasharray="5,5"/>
      <line x1="100" y1="20" x2="100" y2="280" stroke="#4e79a7" stroke-width="2" stroke-dasharray="5,5"/>
      <line x1="300" y1="20" x2="300" y2="280" stroke="#4e79a7" stroke-width="2" stroke-dasharray="5,5"/>
      
      <--trace Bus stops (many, dense) -->
      <circle cx="60" cy="100" r="5" fill="#4e79a7"/>
      <circle cx="120" cy="100" r="5" fill="#4e79a7"/>
      <circle cx="180" cy="100" r="5" fill="#4e79a7"/>
      <circle cx="240" cy="100" r="5" fill="#4e79a7"/>
      <circle cx="300" cy="100" r="5" fill="#4e79a7"/>
      <circle cx="340" cy="100" r="5" fill="#4e79a7"/>
      
      <circle cx="100" cy="150" r="5" fill="#4e79a7"/>
      <circle cx="200" cy="150" r="5" fill="#4e79a7"/>
      <circle cx="300" cy="150" r="5" fill="#4e79a7"/>
      
      <circle cx="60" cy="200" r="5" fill="#4e79a7"/>
      <circle cx="120" cy="200" r="5" fill="#4e79a7"/>
      <circle cx="180" cy="200" r="5" fill="#4e79a7"/>
      <circle cx="240" cy="200" r="5" fill="#4e79a7"/>
      <circle cx="300" cy="200" r="5" fill="#4e79a7"/>
      <circle cx="340" cy="200" r="5" fill="#4e79a7"/>
      
      <--trace Walking distance circles (short) -->
      <circle cx="180" cy="150" r="40" fill="none" stroke="#28a745" stroke-width="1" stroke-dasharray="3,3" opacity="0.5"/>
      
      <--trace Home location -->
      <rect x="165" y="135" width="30" height="30" fill="#fff" stroke="#28a745" stroke-width="2" rx="2"/>
      <text x="180" y="155" text-anchor="middle" fill="#000" font-weight="bold" font-size="16">🏠</text>
      
      <--trace Safety features -->
      <circle cx="80" cy="180" r="3" fill="#ffc107"/>
      <circle cx="250" cy="120" r="3" fill="#ffc107"/>
      <circle cx="320" cy="170" r="3" fill="#ffc107"/>
      <text x="380" y="290" text-anchor="end" fill="#ffc107" font-size="10">�� Street lights</text>
    </svg>
    
    <div style="background: rgba(78, 121, 167, 0.15); padding: 1rem; border-radius: 0.5rem; border-left: 3px solid #4e79a7;">
      <h4 style="margin: 0 0 0.5rem 0; color: #4e79a7;">✓ Transit-Dependent Access</h4>
      <ul style="margin: 0; padding-left: 1.5rem; font-size: 0.9rem;">
        <li style="margin: 0.3rem 0;">27 bus stops within area (routes Y1, 51)</li>
        <li style="margin: 0.3rem 0;">2 bus routes provide coverage to downtown</li>
        <li style="margin: 0.3rem 0;">Average walk: 10-15 minutes to transit</li>
        <li style="margin: 0.3rem 0;">Service frequency: Every 15-20 min during peak</li>
        <li style="margin: 0.3rem 0;">High transit reliance: 21.5% no-vehicle access</li>
        <li style="margin: 0.3rem 0;">Commute time to employment: 41-60 minutes</li>
      </ul>
    </div>
  </div>

  <--trace Neighborhood Mini-Map B: Middle-Income Mixed Access -->
  <div class="card" style="padding: 2rem;">
    <h3 style="margin: 0 0 1.5rem 0; color: #f28e2c;">📍 Map B: Mixed-Access Neighborhood (Jocelyn - Lower Lawrenceville)</h3>
    <p style="margin: 0 0 1.5rem 0; font-size: 0.9rem;">Middle-income with both transit and car access: Median income $86,094 • 11.3% no-vehicle households</p>
    
    <svg width="100%" height="300" viewBox="0 0 400 300" style="border: 2px solid #ddd; border-radius: 0.5rem; background: #fff; margin-bottom: 1.5rem;">
      <--trace Grid background -->
      <defs>
        <pattern id="grid-b" width="40" height="40" patternUnits="userSpaceOnUse">
          <path d="M 40 0 L 0 0 0 40" fill="none" stroke="#e0e0e0" stroke-width="0.5"/>
        </pattern>
      </defs>
      <rect width="400" height="300" fill="url(#grid-b)" />
      
      <--trace Major streets (mixed use) -->
      <line x1="20" y1="150" x2="380" y2="150" stroke="#bbb" stroke-width="3"/>
      <line x1="200" y1="20" x2="200" y2="280" stroke="#bbb" stroke-width="3"/>
      <line x1="80" y1="20" x2="80" y2="280" stroke="#ccc" stroke-width="2"/>
      <line x1="320" y1="20" x2="320" y2="280" stroke="#ccc" stroke-width="2"/>
      
      <--trace Bus routes (multiple, reasonable coverage) -->
      <line x1="20" y1="100" x2="380" y2="100" stroke="#f28e2c" stroke-width="2" stroke-dasharray="8,5"/>
      <line x1="20" y1="200" x2="380" y2="200" stroke="#f28e2c" stroke-width="2" stroke-dasharray="8,5"/>
      <line x1="80" y1="20" x2="80" y2="280" stroke="#f28e2c" stroke-width="2" stroke-dasharray="8,5"/>
      <line x1="320" y1="20" x2="320" y2="280" stroke="#f28e2c" stroke-width="2" stroke-dasharray="8,5"/>
      <line x1="200" y1="50" x2="200" y2="250" stroke="#f28e2c" stroke-width="2" stroke-dasharray="8,5"/>
      
      <--trace Bus stops (moderate density, good access) -->
      <circle cx="50" cy="100" r="5" fill="#f28e2c"/>
      <circle cx="120" cy="100" r="5" fill="#f28e2c"/>
      <circle cx="200" cy="100" r="5" fill="#f28e2c"/>
      <circle cx="280" cy="100" r="5" fill="#f28e2c"/>
      <circle cx="350" cy="100" r="5" fill="#f28e2c"/>
      
      <circle cx="80" cy="150" r="5" fill="#f28e2c"/>
      <circle cx="200" cy="150" r="5" fill="#f28e2c"/>
      <circle cx="320" cy="150" r="5" fill="#f28e2c"/>
      
      <circle cx="50" cy="200" r="5" fill="#f28e2c"/>
      <circle cx="120" cy="200" r="5" fill="#f28e2c"/>
      <circle cx="200" cy="200" r="5" fill="#f28e2c"/>
      <circle cx="280" cy="200" r="5" fill="#f28e2c"/>
      <circle cx="350" cy="200" r="5" fill="#f28e2c"/>
      
      <circle cx="200" cy="70" r="5" fill="#f28e2c"/>
      <circle cx="200" cy="230" r="5" fill="#f28e2c"/>
      
      <--trace Walking distance circles (moderate) -->
      <circle cx="180" cy="150" r="50" fill="none" stroke="#f28e2c" stroke-width="1" stroke-dasharray="3,3" opacity="0.5"/>
      
      <--trace Home location -->
      <rect x="155" y="125" width="50" height="50" fill="#fff" stroke="#f28e2c" stroke-width="2" rx="2"/>
      <text x="180" y="165" text-anchor="middle" fill="#000" font-weight="bold" font-size="24">🏠</text>
      
      <--trace Parking availability -->
      <rect x="30" y="240" width="40" height="30" fill="#ddd" opacity="0.4" stroke="#999" stroke-width="1"/>
      <text x="50" y="260" text-anchor="middle" fill="#999" font-size="9">P</text>
      
      <--trace Good walkability indicators -->
      <circle cx="320" cy="80" r="3" fill="#28a745"/>
      <circle cx="80" cy="220" r="3" fill="#28a745"/>
      <text x="380" y="290" text-anchor="end" fill="#28a745" font-size="10">✓ Walkable/Safe</text>
    </svg>
    
    <div style="background: rgba(242, 142, 44, 0.15); padding: 1rem; border-radius: 0.5rem; border-left: 3px solid #f28e2c;">
      <h4 style="margin: 0 0 0.5rem 0; color: #f28e2c;">✓ Transit + Car Flexibility</h4>
      <ul style="margin: 0; padding-left: 1.5rem; font-size: 0.9rem;">
        <li style="margin: 0.3rem 0;">41 bus stops within area (5 routes including 93)</li>
        <li style="margin: 0.3rem 0;">Multiple route options provide coverage</li>
        <li style="margin: 0.3rem 0;">Average walk: 5-10 minutes to transit</li>
        <li style="margin: 0.3rem 0;">Service frequency: Every 10-15 min during peak</li>
        <li style="margin: 0.3rem 0;">Good vehicle access: 11.3% no-vehicle households</li>
        <li style="margin: 0.3rem 0;">Commute time by transit: ~25 minutes (choice)</li>
        <li style="margin: 0.3rem 0;">Can use car for flexibility/errands when needed</li>
      </ul>
    </div>
  </div>
</div>
`
```
