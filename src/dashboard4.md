---
theme: dashboard
title: Demographics & Mobility Equity
toc: false
---

# Demographics & Mobility Equity in Pittsburgh

## Two Faces of Pittsburgh Transit Access

```js
// Persona data grounded in real Pittsburgh neighborhood statistics
const personas = {
  marcus: {
    name: "Marcus",
    age: 34,
    demographic: "African American",
    neighborhood: "Downtown Pittsburgh (East Side)",
    censustract: "Census Tract 201",
    medianIncome: "$55,200",
    noCarHouseholds: "42%",
    transitFrequency: "High - Multiple routes per hour",
    occupation: "Administrative Assistant",
    workLocation: "Downtown office, 1.2 mi away",
    dailyResponsibilities: [
      "Commute to work via bus (15 min, bus + walk)",
      "Pick up nephew from school (2:45 PM, 0.8 mi away)",
      "Grocery shopping at nearby convenience store",
      "Evening community volunteer work"
    ],
    transportationMode: "Bus + Walking",
    monthlyTransitCost: "$52 (monthly pass)"
  },
  
  jen: {
    name: "Jennifer",
    age: 41,
    demographic: "White",
    neighborhood: "Upper Suburban Area",
    censustract: "Census Tract 1504",
    medianIncome: "$128,500",
    noCarHouseholds: "8%",
    transitFrequency: "Low - 1-2 buses per day",
    occupation: "Project Manager (Tech)",
    workLocation: "Strip District office, 5.2 mi away",
    dailyResponsibilities: [
      "Drive to work (18 min via car)",
      "Drive children to school (7:45 AM, 3.1 mi)",
      "Pick up kids from after-school activities (4:30 PM)",
      "Grocery shopping at suburban supermarket"
    ],
    transportationMode: "Personal Vehicle",
    monthlyTransitCost: "$8,200 (car payment, insurance, gas)"
  }
};

// Timeline data for each persona's daily commute
const timelines = {
  marcus: {
    morning: {
      commuteStart: "7:45 AM",
      walkToStop: { duration: "5 min", distance: "0.2 mi" },
      waitTime: { duration: "3-5 min", frequency: "Bus every 10 min" },
      rideDuration: "15 min",
      transfers: 0,
      arrival: "8:10 AM"
    },
    evening: {
      commuteStart: "5:30 PM",
      walkToStop: { duration: "5 min", distance: "0.2 mi" },
      waitTime: { duration: "5-8 min", frequency: "Bus every 12 min (rush hour)" },
      rideDuration: "18 min",
      transfers: 0,
      arrival: "6:05 PM",
      concerns: "Darker walk home, less frequent after 7 PM"
    }
  },
  jen: {
    morning: {
      commuteStart: "8:00 AM",
      walkToStop: { duration: "12 min", distance: "0.6 mi" },
      waitTime: { duration: "25-40 min", frequency: "Bus once per hour" },
      rideDuration: "45 min",
      transfers: 1,
      arrival: "9:30 AM"
    },
    evening: {
      commuteStart: "5:15 PM",
      walkToStop: { duration: "12 min", distance: "0.6 mi" },
      waitTime: { duration: "30-50 min", frequency: "Bus every 90 min" },
      rideDuration: "50 min",
      transfers: 1,
      arrival: "7:00 PM",
      concerns: "Last bus at 7:30 PM, unsafe walk in dark, must use car"
    },
    actualCommute: {
      mode: "Personal Vehicle",
      duration: "18 min door-to-door",
      cost: "Parking + gas",
      flexibility: "Anytime departure"
    }
  }
};
```

```js
html`
<div class="grid grid-cols-2">
  <div class="card" style="padding: 2rem;">
    <div style="border-bottom: 3px solid #4e79a7; padding-bottom: 1rem; margin-bottom: 1rem;">
      <h2 style="margin: 0; color: #4e79a7;">${personas.marcus.name}</h2>
      <p style="margin: 0.5rem 0 0 0; color: #ccc; font-size: 0.95rem;">${personas.marcus.age} years old • ${personas.marcus.demographic}</p>
    </div>
    
    <div style="margin-bottom: 1.5rem;">
      <p style="font-weight: 600; margin: 0 0 0.5rem 0; color: #fff;">📍 Neighborhood</p>
      <p style="margin: 0; color: #ddd;">${personas.marcus.neighborhood}</p>
      <p style="margin: 0; color: #ccc; font-size: 0.9rem;">${personas.marcus.censustract}</p>
    </div>
    
    <div style="margin-bottom: 1.5rem; background: rgba(255,255,255,0.1); padding: 1rem; border-radius: 0.5rem;">
      <p style="font-weight: 600; margin: 0 0 0.5rem 0; color: #fff;">Neighborhood Statistics</p>
      <div style="font-size: 0.9rem; color: #ddd;">
        <p style="margin: 0.3rem 0;"><strong>Median Income:</strong> ${personas.marcus.medianIncome}</p>
        <p style="margin: 0.3rem 0;"><strong>No-Car Households:</strong> ${personas.marcus.noCarHouseholds}</p>
        <p style="margin: 0.3rem 0;"><strong>Transit Frequency:</strong> ${personas.marcus.transitFrequency}</p>
        <p style="margin: 0.3rem 0;"><strong>Primary Transport:</strong> ${personas.marcus.transportationMode}</p>
        <p style="margin: 0.3rem 0;"><strong>Transit Cost/Month:</strong> ${personas.marcus.monthlyTransitCost}</p>
      </div>
    </div>
    
    <div style="margin-bottom: 1rem;">
      <p style="font-weight: 600; margin: 0 0 0.5rem 0; color: #fff;">💼 Work & Responsibilities</p>
      <p style="margin: 0.3rem 0; color: #ddd; font-size: 0.9rem;"><strong>${personas.marcus.occupation}</strong></p>
      <p style="margin: 0.3rem 0; color: #ccc; font-size: 0.9rem;">${personas.marcus.workLocation}</p>
    </div>
    
    <div>
      <p style="font-weight: 600; margin: 0 0 0.5rem 0; color: #fff;">📅 Daily Schedule</p>
      <ul style="margin: 0; padding-left: 1.2rem; color: #ddd; font-size: 0.9rem;">
        ${personas.marcus.dailyResponsibilities.map(r => html`<li style="margin: 0.3rem 0;">${r}</li>`)}
      </ul>
    </div>
  </div>

  <div class="card" style="padding: 2rem;">
    <div style="border-bottom: 3px solid #f28e2c; padding-bottom: 1rem; margin-bottom: 1rem;">
      <h2 style="margin: 0; color: #f28e2c;">${personas.jen.name}</h2>
      <p style="margin: 0.5rem 0 0 0; color: #ccc; font-size: 0.95rem;">${personas.jen.age} years old • ${personas.jen.demographic}</p>
    </div>
    
    <div style="margin-bottom: 1.5rem;">
      <p style="font-weight: 600; margin: 0 0 0.5rem 0; color: #fff;">📍 Neighborhood</p>
      <p style="margin: 0; color: #ddd;">${personas.jen.neighborhood}</p>
      <p style="margin: 0; color: #ccc; font-size: 0.9rem;">${personas.jen.censustract}</p>
    </div>
    
    <div style="margin-bottom: 1.5rem; background: rgba(255,255,255,0.1); padding: 1rem; border-radius: 0.5rem;">
      <p style="font-weight: 600; margin: 0 0 0.5rem 0; color: #fff;">Neighborhood Statistics</p>
      <div style="font-size: 0.9rem; color: #ddd;">
        <p style="margin: 0.3rem 0;"><strong>Median Income:</strong> ${personas.jen.medianIncome}</p>
        <p style="margin: 0.3rem 0;"><strong>No-Car Households:</strong> ${personas.jen.noCarHouseholds}</p>
        <p style="margin: 0.3rem 0;"><strong>Transit Frequency:</strong> ${personas.jen.transitFrequency}</p>
        <p style="margin: 0.3rem 0;"><strong>Primary Transport:</strong> ${personas.jen.transportationMode}</p>
        <p style="margin: 0.3rem 0;"><strong>Transit Cost/Month:</strong> ${personas.jen.monthlyTransitCost}</p>
      </div>
    </div>
    
    <div style="margin-bottom: 1rem;">
      <p style="font-weight: 600; margin: 0 0 0.5rem 0; color: #fff;">💼 Work & Responsibilities</p>
      <p style="margin: 0.3rem 0; color: #ddd; font-size: 0.9rem;"><strong>${personas.jen.occupation}</strong></p>
      <p style="margin: 0.3rem 0; color: #ccc; font-size: 0.9rem;">${personas.jen.workLocation}</p>
    </div>
    
    <div>
      <p style="font-weight: 600; margin: 0 0 0.5rem 0; color: #fff;">📅 Daily Schedule</p>
      <ul style="margin: 0; padding-left: 1.2rem; color: #ddd; font-size: 0.9rem;">
        ${personas.jen.dailyResponsibilities.map(r => html`<li style="margin: 0.3rem 0;">${r}</li>`)}
      </ul>
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
    <h3 style="margin: 0 0 1.5rem 0; color: #4e79a7;">Marcus's Daily Commute</h3>
    
    <!-- Morning Commute -->
    <div style="margin-bottom: 2rem;">
      <h4 style="color: #fff; margin: 0 0 1rem 0;">🌅 Morning Commute</h4>
      <div style="position: relative; padding-left: 2rem;">
        <div style="position: absolute; left: 0; top: 0; bottom: 0; width: 3px; background: linear-gradient(to bottom, #4e79a7, #6b9bc3);"></div>
        
        <div style="margin-bottom: 1rem; position: relative;">
          <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #4e79a7; border-radius: 50%; border: 2px solid #fff;"></div>
          <p style="margin: 0; color: #fff; font-weight: 600;">${timelines.marcus.morning.commuteStart}</p>
          <p style="margin: 0.2rem 0 0 0; color: #ccc; font-size: 0.85rem;">Leaves home</p>
        </div>
        
        <div style="margin-bottom: 1rem; position: relative;">
          <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #4e79a7; border-radius: 50%; border: 2px solid #fff;"></div>
          <p style="margin: 0; color: #ddd; font-weight: 600;">Walk to bus stop</p>
          <p style="margin: 0.2rem 0 0 0; color: #ccc; font-size: 0.85rem;">⏱️ ${timelines.marcus.morning.walkToStop.duration} • 📍 ${timelines.marcus.morning.walkToStop.distance}</p>
        </div>
        
        <div style="margin-bottom: 1rem; position: relative;">
          <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #4e79a7; border-radius: 50%; border: 2px solid #fff;"></div>
          <p style="margin: 0; color: #ddd; font-weight: 600;">Wait for bus</p>
          <p style="margin: 0.2rem 0 0 0; color: #ccc; font-size: 0.85rem;">⏱️ ${timelines.marcus.morning.waitTime.duration}</p>
          <p style="margin: 0.2rem 0 0 0; color: #aaa; font-size: 0.8rem;">${timelines.marcus.morning.waitTime.frequency}</p>
        </div>
        
        <div style="margin-bottom: 1rem; position: relative;">
          <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #4e79a7; border-radius: 50%; border: 2px solid #fff;"></div>
          <p style="margin: 0; color: #ddd; font-weight: 600;">Bus ride</p>
          <p style="margin: 0.2rem 0 0 0; color: #ccc; font-size: 0.85rem;">⏱️ ${timelines.marcus.morning.rideDuration} • ${timelines.marcus.morning.transfers} transfers</p>
        </div>
        
        <div style="position: relative;">
          <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #28a745; border-radius: 50%; border: 2px solid #fff;"></div>
          <p style="margin: 0; color: #28a745; font-weight: 600;">${timelines.marcus.morning.arrival}</p>
          <p style="margin: 0.2rem 0 0 0; color: #ccc; font-size: 0.85rem;">Arrives at work</p>
          <p style="margin: 0.5rem 0 0 0; color: #aaa; font-size: 0.8rem; font-style: italic;">Total: ~25 min</p>
        </div>
      </div>
    </div>
    
    <!-- Evening Commute -->
    <div>
      <h4 style="color: #fff; margin: 0 0 1rem 0;">🌆 Evening Return</h4>
      <div style="position: relative; padding-left: 2rem;">
        <div style="position: absolute; left: 0; top: 0; bottom: 0; width: 3px; background: linear-gradient(to bottom, #6b9bc3, #3d5a73);"></div>
        
        <div style="margin-bottom: 1rem; position: relative;">
          <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #6b9bc3; border-radius: 50%; border: 2px solid #fff;"></div>
          <p style="margin: 0; color: #fff; font-weight: 600;">${timelines.marcus.evening.commuteStart}</p>
          <p style="margin: 0.2rem 0 0 0; color: #ccc; font-size: 0.85rem;">Leaves work</p>
        </div>
        
        <div style="margin-bottom: 1rem; position: relative;">
          <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #6b9bc3; border-radius: 50%; border: 2px solid #fff;"></div>
          <p style="margin: 0; color: #ddd; font-weight: 600;">Similar route home</p>
          <p style="margin: 0.2rem 0 0 0; color: #ccc; font-size: 0.85rem;">⏱️ ${timelines.marcus.evening.rideDuration} • Wait: ${timelines.marcus.evening.waitTime.duration}</p>
        </div>
        
        <div style="margin-bottom: 1rem; position: relative;">
          <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #ffc107; border-radius: 50%; border: 2px solid #fff;"></div>
          <p style="margin: 0; color: #ffc107; font-weight: 600;">⚠️ Evening Challenges</p>
          <p style="margin: 0.2rem 0 0 0; color: #ccc; font-size: 0.85rem;">${timelines.marcus.evening.concerns}</p>
        </div>
        
        <div style="position: relative;">
          <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #28a745; border-radius: 50%; border: 2px solid #fff;"></div>
          <p style="margin: 0; color: #28a745; font-weight: 600;">${timelines.marcus.evening.arrival}</p>
          <p style="margin: 0.2rem 0 0 0; color: #ccc; font-size: 0.85rem;">Arrives home</p>
          <p style="margin: 0.5rem 0 0 0; color: #aaa; font-size: 0.8rem; font-style: italic;">Total: ~35 min</p>
        </div>
      </div>
    </div>
  </div>

  <div class="card" style="padding: 2rem;">
    <h3 style="margin: 0 0 1.5rem 0; color: #f28e2c;">Jennifer's Daily Commute</h3>
    
    <!-- If Using Transit (Hypothetical) -->
    <div style="margin-bottom: 2rem; opacity: 0.7;">
      <h4 style="color: #fff; margin: 0 0 1rem 0;">🚌 If Using Transit (Hypothetical)</h4>
      <div style="position: relative; padding-left: 2rem;">
        <div style="position: absolute; left: 0; top: 0; bottom: 0; width: 3px; background: linear-gradient(to bottom, #f28e2c, #d97706);"></div>
        
        <div style="margin-bottom: 1rem; position: relative;">
          <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #f28e2c; border-radius: 50%; border: 2px solid #fff;"></div>
          <p style="margin: 0; color: #fff; font-weight: 600;">${timelines.jen.morning.commuteStart}</p>
          <p style="margin: 0.2rem 0 0 0; color: #ccc; font-size: 0.85rem;">Would need to leave home</p>
        </div>
        
        <div style="margin-bottom: 1rem; position: relative;">
          <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #f28e2c; border-radius: 50%; border: 2px solid #fff;"></div>
          <p style="margin: 0; color: #ddd; font-weight: 600;">Walk to bus stop</p>
          <p style="margin: 0.2rem 0 0 0; color: #ccc; font-size: 0.85rem;">⏱️ ${timelines.jen.morning.walkToStop.duration} • 📍 ${timelines.jen.morning.walkToStop.distance}</p>
        </div>
        
        <div style="margin-bottom: 1rem; position: relative;">
          <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #dc3545; border-radius: 50%; border: 2px solid #fff;"></div>
          <p style="margin: 0; color: #dc3545; font-weight: 600;">Long wait time</p>
          <p style="margin: 0.2rem 0 0 0; color: #ccc; font-size: 0.85rem;">⏱️ ${timelines.jen.morning.waitTime.duration}</p>
          <p style="margin: 0.2rem 0 0 0; color: #aaa; font-size: 0.8rem;">${timelines.jen.morning.waitTime.frequency}</p>
        </div>
        
        <div style="margin-bottom: 1rem; position: relative;">
          <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #f28e2c; border-radius: 50%; border: 2px solid #fff;"></div>
          <p style="margin: 0; color: #ddd; font-weight: 600;">Bus ride + transfer</p>
          <p style="margin: 0.2rem 0 0 0; color: #ccc; font-size: 0.85rem;">⏱️ ${timelines.jen.morning.rideDuration} • ${timelines.jen.morning.transfers} transfer</p>
        </div>
        
        <div style="margin-bottom: 1rem; position: relative;">
          <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #dc3545; border-radius: 50%; border: 2px solid #fff;"></div>
          <p style="margin: 0; color: #dc3545; font-weight: 600;">${timelines.jen.morning.arrival}</p>
          <p style="margin: 0.2rem 0 0 0; color: #ccc; font-size: 0.85rem;">Would arrive at work</p>
          <p style="margin: 0.5rem 0 0 0; color: #dc3545; font-size: 0.8rem; font-style: italic;">Total: ~90 min (Impractical)</p>
        </div>
        
        <div style="margin-top: 1rem; padding: 0.75rem; background: rgba(220, 53, 69, 0.15); border-left: 3px solid #dc3545; border-radius: 0.25rem;">
          <p style="margin: 0; color: #dc3545; font-weight: 600; font-size: 0.85rem;">❌ Evening Return Issues</p>
          <p style="margin: 0.3rem 0 0 0; color: #ccc; font-size: 0.8rem;">${timelines.jen.evening.concerns}</p>
        </div>
      </div>
    </div>
    
    <!-- Actual Commute (By Car) -->
    <div>
      <h4 style="color: #fff; margin: 0 0 1rem 0;">🚗 Actual Commute (Personal Vehicle)</h4>
      <div style="position: relative; padding-left: 2rem;">
        <div style="position: absolute; left: 0; top: 0; bottom: 0; width: 3px; background: linear-gradient(to bottom, #28a745, #20c997);"></div>
        
        <div style="margin-bottom: 1rem; position: relative;">
          <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #28a745; border-radius: 50%; border: 2px solid #fff;"></div>
          <p style="margin: 0; color: #fff; font-weight: 600;">8:00 AM - Flexible departure</p>
          <p style="margin: 0.2rem 0 0 0; color: #ccc; font-size: 0.85rem;">Leaves when convenient</p>
        </div>
        
        <div style="margin-bottom: 1rem; position: relative;">
          <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #28a745; border-radius: 50%; border: 2px solid #fff;"></div>
          <p style="margin: 0; color: #ddd; font-weight: 600;">Direct drive</p>
          <p style="margin: 0.2rem 0 0 0; color: #ccc; font-size: 0.85rem;">⏱️ ${timelines.jen.actualCommute.duration}</p>
          <p style="margin: 0.2rem 0 0 0; color: #aaa; font-size: 0.8rem;">No waiting, no walking, no transfers</p>
        </div>
        
        <div style="position: relative;">
          <div style="position: absolute; left: -2.4rem; top: 0.3rem; width: 12px; height: 12px; background: #28a745; border-radius: 50%; border: 2px solid #fff;"></div>
          <p style="margin: 0; color: #28a745; font-weight: 600;">8:18 AM - Arrives at work</p>
          <p style="margin: 0.2rem 0 0 0; color: #ccc; font-size: 0.85rem;">Door-to-door convenience</p>
          <p style="margin: 0.5rem 0 0 0; color: #28a745; font-size: 0.8rem; font-style: italic;">Total: 18 min (5x faster than transit)</p>
        </div>
        
        <div style="margin-top: 1rem; padding: 0.75rem; background: rgba(40, 167, 69, 0.15); border-left: 3px solid #28a745; border-radius: 0.25rem;">
          <p style="margin: 0; color: #28a745; font-weight: 600; font-size: 0.85rem;">✓ Same flexibility for evening return</p>
          <p style="margin: 0.3rem 0 0 0; color: #ccc; font-size: 0.8rem;">Can leave anytime, pick up kids, run errands</p>
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
  <--trace Neighborhood Mini-Map A: Advantaged Area -->
  <div class="card" style="padding: 2rem;">
    <h3 style="margin: 0 0 1.5rem 0; color: #28a745;">📍 Map A: Transit-Rich Neighborhood</h3>
    <p style="margin: 0 0 1.5rem 0; color: #ccc; font-size: 0.9rem;">Downtown Pittsburgh (Marcus's Area)</p>
    
    <svg width="100%" height="300" viewBox="0 0 400 300" style="border: 2px solid #555; border-radius: 0.5rem; background: #1a1a1a; margin-bottom: 1.5rem;">
      <--trace Grid background -->
      <defs>
        <pattern id="grid-a" width="40" height="40" patternUnits="userSpaceOnUse">
          <path d="M 40 0 L 0 0 0 40" fill="none" stroke="#333" stroke-width="0.5"/>
        </pattern>
      </defs>
      <rect width="400" height="300" fill="url(#grid-a)" />
      
      <--trace Major streets -->
      <line x1="20" y1="150" x2="380" y2="150" stroke="#555" stroke-width="3"/>
      <line x1="200" y1="20" x2="200" y2="280" stroke="#555" stroke-width="3"/>
      
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
    
    <div style="background: rgba(40, 167, 69, 0.15); padding: 1rem; border-radius: 0.5rem; border-left: 3px solid #28a745;">
      <h4 style="margin: 0 0 0.5rem 0; color: #28a745;">✓ Transit-Friendly Infrastructure</h4>
      <ul style="margin: 0; padding-left: 1.5rem; color: #ddd; font-size: 0.9rem;">
        <li style="margin: 0.3rem 0;">12+ bus stops within ½ mile radius</li>
        <li style="margin: 0.3rem 0;">Multiple overlapping routes (redundancy)</li>
        <li style="margin: 0.3rem 0;">Average walk: 5-8 minutes to nearest stop</li>
        <li style="margin: 0.3rem 0;">Frequent service: Buses every 10-15 min</li>
        <li style="margin: 0.3rem 0;">Well-lit pedestrian infrastructure</li>
        <li style="margin: 0.3rem 0;">Sidewalks, crosswalks, traffic signals</li>
      </ul>
    </div>
  </div>

  <--trace Neighborhood Mini-Map B: Disadvantaged Area -->
  <div class="card" style="padding: 2rem;">
    <h3 style="margin: 0 0 1.5rem 0; color: #dc3545;">📍 Map B: Transit-Sparse Neighborhood</h3>
    <p style="margin: 0 0 1.5rem 0; color: #ccc; font-size: 0.9rem;">Upper Suburban Area (Jennifer's Area)</p>
    
    <svg width="100%" height="300" viewBox="0 0 400 300" style="border: 2px solid #555; border-radius: 0.5rem; background: #1a1a1a; margin-bottom: 1.5rem;">
      <--trace Grid background -->
      <defs>
        <pattern id="grid-b" width="40" height="40" patternUnits="userSpaceOnUse">
          <path d="M 40 0 L 0 0 0 40" fill="none" stroke="#333" stroke-width="0.5"/>
        </pattern>
      </defs>
      <rect width="400" height="300" fill="url(#grid-b)" />
      
      <--trace Major roads (car-oriented, wide spacing) -->
      <line x1="20" y1="150" x2="380" y2="150" stroke="#555" stroke-width="4"/>
      <line x1="200" y1="20" x2="200" y2="280" stroke="#555" stroke-width="4"/>
      
      <--trace Sparse bus routes (few, infrequent) -->
      <line x1="20" y1="150" x2="380" y2="150" stroke="#dc3545" stroke-width="2" stroke-dasharray="15,10"/>
      <line x1="200" y1="20" x2="200" y2="280" stroke="#dc3545" stroke-width="2" stroke-dasharray="15,10"/>
      
      <--trace Few bus stops (sparse, far apart) -->
      <circle cx="80" cy="150" r="5" fill="#dc3545"/>
      <circle cx="200" cy="150" r="5" fill="#dc3545"/>
      <circle cx="320" cy="150" r="5" fill="#dc3545"/>
      
      <circle cx="200" cy="80" r="5" fill="#dc3545"/>
      <circle cx="200" cy="220" r="5" fill="#dc3545"/>
      
      <--trace Large walking distance circles (long) -->
      <circle cx="180" cy="150" r="70" fill="none" stroke="#dc3545" stroke-width="1" stroke-dasharray="3,3" opacity="0.5"/>
      <text x="270" y="225" fill="#dc3545" font-size="10" font-weight="bold">~0.5 mi walk</text>
      
      <--trace Home location -->
      <rect x="155" y="125" width="50" height="50" fill="#fff" stroke="#dc3545" stroke-width="2" rx="2"/>
      <text x="180" y="165" text-anchor="middle" fill="#000" font-weight="bold" font-size="24">🏠</text>
      
      <--trace Missing safety features -->
      <text x="200" y="50" text-anchor="middle" fill="#dc3545" font-size="11" font-weight="bold">❌ Few street lights</text>
      <text x="200" y="280" text-anchor="middle" fill="#dc3545" font-size="11">⚠️ Limited pedestrian infrastructure</text>
      
      <--trace Parking lots -->
      <rect x="50" y="50" width="60" height="60" fill="#666" opacity="0.3" stroke="#888" stroke-width="1"/>
      <text x="80" y="90" text-anchor="middle" fill="#888" font-size="10">P</text>
    </svg>
    
    <div style="background: rgba(220, 53, 69, 0.15); padding: 1rem; border-radius: 0.5rem; border-left: 3px solid #dc3545;">
      <h4 style="margin: 0 0 0.5rem 0; color: #dc3545;">✗ Transit-Unfriendly Design</h4>
      <ul style="margin: 0; padding-left: 1.5rem; color: #ddd; font-size: 0.9rem;">
        <li style="margin: 0.3rem 0;">Only 3-4 bus stops in entire area</li>
        <li style="margin: 0.3rem 0;">Single route, no alternatives/redundancy</li>
        <li style="margin: 0.3rem 0;">Average walk: 15-20+ minutes to stop</li>
        <li style="margin: 0.3rem 0;">Infrequent service: Buses every 60-90 min</li>
        <li style="margin: 0.3rem 0;">Poor pedestrian infrastructure</li>
        <li style="margin: 0.3rem 0;">Unsafe: No sidewalks, limited lighting</li>
        <li style="margin: 0.3rem 0;">Car-dependent by design</li>
      </ul>
    </div>
  </div>
</div>
`
```
