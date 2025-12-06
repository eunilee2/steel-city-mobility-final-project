---
theme: dashboard
title: Demographics & Ridership in Pittsburgh
toc: false
---

# Demographics & Ridership in Pittsburgh

## Demographic of Pittsburgh showing the details of Race, Age, Income, and Vehicle Access

<!-- ========================= -->
<!--   ARC GIS MAP: INCOME     -->
<!-- ========================= -->

<div style="width: 100%; margin-bottom: 30px;">
  <iframe
    width="100%"
    height="600"
    frameborder="0"
    scrolling="no"
    marginheight="0"
    marginwidth="0"
    allow="local-network-access; geolocation"
    title="Income Map"
    src="https://carnegiemellon.maps.arcgis.com/apps/mapviewer/index.html?configurableview=true&webmap=13f177b6a6584fd98e362b506fa7162e&theme=light&bookmarks=true&heading=true&legend=true&information=true&scroll=false&center=-79.85647249987123,40.38671485630146&scale=72223.819286">
  </iframe>
</div>

<!-- ========================= -->
<!--   ARC GIS MAP: RACE       -->
<!-- ========================= -->

<div style="width: 100%; margin-bottom: 30px;">
  <iframe
    width="100%"
    height="600"
    frameborder="0"
    scrolling="no"
    marginheight="0"
    marginwidth="0"
    allow="local-network-access; geolocation"
    title="Race Map"
    src="https://carnegiemellon.maps.arcgis.com/apps/mapviewer/index.html?configurableview=true&webmap=77a67122be424390a6d8205ecfceb192&theme=light&bookmarks=true&heading=true&legend=true&information=true&scroll=false&center=-79.88617192974102,40.45846431816441&scale=72223.819286">
  </iframe>
</div>

<!-- ========================= -->
<!--   ARC GIS MAP: VEHICLE    -->
<!-- ========================= -->

<div style="width: 100%; margin-bottom: 30px;">
  <iframe
    width="100%"
    height="600"
    frameborder="0"
    scrolling="no"
    marginheight="0"
    marginwidth="0"
    allow="local-network-access; geolocation"
    title="Vehicle Map"
    src="https://carnegiemellon.maps.arcgis.com/apps/mapviewer/index.html?configurableview=true&webmap=5ac5fcd0fe2c413393451736973f13fe&theme=light&bookmarks=true&heading=true&legend=true&information=true&scroll=false&center=-80.00896278789035,40.469974633593715&scale=72223.819286">
  </iframe>
</div>

<!-- ========================= -->
<!--   ARC GIS MAP: AGE & DISABILITY    -->
<!-- ========================= -->

<!-- Load the embeddable components script (only needed once per dashboard) -->
<script type="module" src="https://js.arcgis.com/4.34/embeddable-components/"></script>

<div style="width: 100%; margin-bottom: 30px;">
  <arcgis-embedded-map 
    style="height:600px;width:100%;" 
    item-id="9eb3f457e6d0439ca6a7a2c9fa3f9d32" 
    theme="light" 
    bookmarks-enabled 
    heading-enabled 
    legend-enabled 
    information-enabled 
    center="-80.01708173870044,40.43438041560807"
    scale="144447.638572"
    portal-url="https://carnegiemellon.maps.arcgis.com">
  </arcgis-embedded-map>
</div>

---

## **Dashboard 2 • Demographics & Mobility Equity**
---
This dashboard summarizes key demographic and mobility patterns across Pittsburgh and highlights how these populations relate to transit dependency and vulnerability. The goal of this dashboard is to build a clear picture of who lives in Pittsburgh by income, race, age, and disability status and then use mapping tools to simplify in understanding where these groups are concentrated and how their access and use of different modes of mobility (car/bus) differs across neighborhoods.

---

---

## **Income Boundaries by Stop Ridership**

### **High Poverty + High Ridership (Transit-Dependent & Well-Served)**
These areas show strong overlap between **blue poverty-qualified tracts** and dense **stop ridership**:
- Hill District  
- Homewood (especially Homewood South)  
- East Liberty / Larimer corridor  
- North Side (California-Kirkbride, Perry South)  
- South Side Slopes & Knoxville  

These communities appear to **depend heavily on transit**, and service is clearly being used.

### **High Poverty + Low Ridership (Transit-Dependent but Underserved)**
These areas raise concern because need is high but bus activity is noticeably weaker:
- Braddock / North Braddock / Rankin  
- McKees Rocks  
- Duquesne  
- Outer Penn Hills tracts  
- Parts of Lincoln–Lemington  

These tracts may have infrequent routes, poor stop spacing, or limited service hours.  
**Conclusion:** These communities show **significant unmet need**.

---

## **Race Boundaries by Stop Ridership**

### **Predominantly Black Neighborhoods With Lower Bus Ridership**
Based on the map, several predominantly Black neighborhoods (shown in yellow) appear to have **less bus ridership** than might be expected given their demographic density and centrality:
- Lincoln–Lemington / Belmar  
- Homewood North  
- Some outer-edge neighborhoods near Penn Hills  

This may suggest:
- No strong direct relationship between racial composition and ridership  
- Or potentially that buses are less convenient, frequent, or accessible in these communities  

However, **this pattern cannot be interpreted definitively without proper statistical analysis**, controlling for factors like:
- Route frequency  
- Stop density  
- Walking accessibility  
- Vehicle availability  
- Population density  

**Conclusion:**  
Ridership appears lower in several predominantly Black areas, but this does *not* confirm a causal pattern. More detailed quantitative analysis would be required.

---

## **Vehicle Availability by Stop Ridership**

### **Low Vehicle Access + Strong Bus Use (Transit is Functioning Well)**
Light-pink tracts (low car availability) match with high ridership:
- Hill District  
- South Oakland  
- East Liberty  
- North Side spine  
- South Side / Slopes  

These areas demonstrate **successful transit alignment** between need and service.

### **Low Vehicle Access + Weak Bus Use (Potential Service Gaps)**
- McKees Rocks  
- Braddock / Rankin  
- Penn Hills outer edges  
- Lincoln–Lemington  

These areas have fewer cars but show **low ridership**, likely due to:
- Sparse routes  
- Long distances to stops  
- Lower service frequency  

**Conclusion:**  
These neighborhoods may be **systematically left at a disadvantage**, as transit need outweighs actual transit access.

---

## **Age & Disability by Stop Ridership**

### **Older or Higher-Disability Communities With Low Ridership**
Purple tracts show older populations or higher disability rates. Areas with concerningly low ridership include:
- Baldwin Township  
- West Mifflin  
- Plum / Penn Hills outskirts  
- Southern suburbs (Pleasant Hills, parts of Brentwood)

These places may have:
- Poor pedestrian infrastructure  
- Long distances between stops  
- Limited service span  

This suggests **mobility barriers** for older adults and disabled populations.

### **Younger Communities With High Ridership**
The green tracts near the core:
- Oakland  
- South Side  
- East Liberty  
- North Side  

These younger, denser areas naturally produce high ridership and have strong service.

**Conclusion:**  
Age- and disability-vulnerable tracts often fall **outside the well-served service core**, meaning many older adults and disabled individuals may have **reduced access to public transit**.

---
## **Overall Patterns Across All Four Layers**

1. **Urban Core Neighborhoods (Downtown, Oakland, East Liberty, South Side, Central North Side)**  
   - High ridership  
   - High density  
   - Consistent service  

2. **Lower-income core neighborhoods (Hill District, Homewood South, Larimer)**  
   - Strong transit dependency  
   - High ridership where service exists  

3. **Outer marginalized communities (Lincoln–Lemington, Braddock, McKees Rocks, Duquesne, outer Penn Hills)**  
   - High need  
   - Low ridership  
   - Likely constrained by weaker service or access barriers  

4. **Older and disabled populations in suburban tracts**  
   - Low ridership  
   - Fewer transit options  
   - Limited walkability  

---

## **Are marginalized communities being “left in the dark”?**

Based on the overlays, several communities show **high need but low ridership**, which may indicate accessibility issues:

- Lincoln–Lemington / Belmar  
- Braddock / Rankin  
- McKees Rocks  
- Duquesne  
- Outer Penn Hills  

However:
- This pattern **does not confirm intentional inequity**  
- And **cannot identify direct causation**  
- A more complete statistical analysis is needed to understand how service levels, socioeconomic status, and ridership interact  

**Conclusion:**  
These maps suggest likely **transit access gaps**, especially in marginalized and low-income communities, but numerical modeling would be required for definitive conclusions.

---

*Built with Observable and ArcGIS Online (Dec 2025)*

*Data Sources Used*
- *https://carnegiemellon.maps.arcgis.com/home/item.html?id=bf1b6035469849a7ac580818cbfa3502*
- *https://carnegiemellon.maps.arcgis.com/home/item.html?id=f1e95b8a159149b586c7cd864ad362b5*
- *https://carnegiemellon.maps.arcgis.com/home/item.html?id=d227d6a4ee3e4d2d87eb9843ee14dd87*
- *https://carnegiemellon.maps.arcgis.com/home/item.html?id=9a9e43ec1603446880c50d4ed1df2207*
- *https://carnegiemellon.maps.arcgis.com/home/item.html?id=23ab8028f1784de4b0810104cd5d1c8f*
- *https://carnegiemellon.maps.arcgis.com/home/item.html?id=573b883f8fd1487991a3136759b00d9c*

