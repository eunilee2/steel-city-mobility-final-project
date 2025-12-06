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

## Dashboard Report  
This dashboard summarizes key demographic patterns across Pittsburgh and overlays bus ridership and vehicle access metrics:

- **Income:** Highlights economic vulnerability across neighborhoods.  
- **Race:** Shows the racial composition of Pittsburgh neighborhoods.  
- **Vehicle Access:** Indicates car availability, helping to assess mobility dependence on public transit.

### Key Takeaways:
- Neighborhoods with higher income vulnerability often overlap with high bus ridership.  
- East End neighborhoods show overlapping vulnerabilities in age, race, and income.  
- Vehicle access disparities correlate with transit dependency, guiding mobility planning.  

*Built with Observable and ArcGIS Online (Dec 2025)*
