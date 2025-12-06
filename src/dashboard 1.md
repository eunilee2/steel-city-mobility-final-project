---
theme: light
title: Demographics of Pittsburgh
toc: false
---

# Demographics of Pittsburgh

## Demographic of Pittsburgh showing the details of Race, Age, Income, and Disability

<!-- ========================= -->
<!--   ARC GIS MAP #1 (TOP)    -->
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
    title="Income Vulnerability Across Pittsburgh Neighborhoods"
    src="https://carnegiemellon.maps.arcgis.com/apps/mapviewer/index.html?configurableview=true&webmap=e0c77d237cf24affab8d03c9012a7ece&theme=light&heading=true&legend=true&information=true&scroll=false&center=-79.93790252330189,40.44524173363545&scale=144447.638572">
  </iframe>
</div>

---

<!-- ========================= -->
<!--   TABLEAU VISUALIZATIONS  -->
<!--   SIDE BY SIDE LAYOUT     -->
<!-- ========================= -->

<div style="display: flex; gap: 20px; flex-wrap: wrap; justify-content: space-between;">

  <!-- Disability Chart -->
  <div style="flex: 1; min-width: 350px;">
    <div class='tableauPlaceholder' id='vizDisability' style='position: relative'>
      <noscript><a href='#'>
        <img alt='Pittsburgh Disability Status Breakdown'
             src='https://public.tableau.com/static/images/Pi/PittsburghDisabilityStatusBreakdown/PittsburghDisabilityStatusBreakdown/1.png' />
      </a></noscript>
      <object class='tableauViz' style='display:none;'>
        <param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F'/>
        <param name='embed_code_version' value='3'/>
        <param name='name' value='PittsburghDisabilityStatusBreakdown/PittsburghDisabilityStatusBreakdown'/>
        <param name='tabs' value='no' />
        <param name='toolbar' value='yes' />
      </object>
    </div>
  </div>

  <!-- Age Chart -->
  <div style="flex: 1; min-width: 350px;">
    <div class='tableauPlaceholder' id='vizAge' style='position: relative'>
      <noscript><a href='#'>
        <img alt='Age Breakdown of Pittsburgh Residents'
             src='https://public.tableau.com/static/images/Ag/AgeBreakdownofPittsburghResidents/AgeBreakdownofPittsburghResidents/1.png' />
      </a></noscript>
      <object class='tableauViz' style='display:none;'>
        <param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F'/>
        <param name='embed_code_version' value='3'/>
        <param name='name' value='AgeBreakdownofPittsburghResidents/AgeBreakdownofPittsburghResidents'/>
        <param name='tabs' value='no' />
        <param name='toolbar' value='yes' />
      </object>
    </div>
  </div>

  <!-- Race Chart -->
  <div style="flex: 1; min-width: 350px;">
    <div class='tableauPlaceholder' id='vizRace' style='position: relative'>
      <noscript><a href='#'>
        <img alt='Pittsburgh Population by Race'
             src='https://public.tableau.com/static/images/Pi/PittsburghPopulationbyRace/PittsburghPopulationbyRace/1.png' />
      </a></noscript>
      <object class='tableauViz' style='display:none;'>
        <param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F'/>
        <param name='embed_code_version' value='3'/>
        <param name='name' value='PittsburghPopulationbyRace/PittsburghPopulationbyRace'/>
        <param name='tabs' value='no' />
        <param name='toolbar' value='yes' />
      </object>
    </div>
  </div>

</div>

<!-- ========================= -->
<!--   TABLEAU SCRIPT LOADER   -->
<!-- ========================= -->

<script type='text/javascript'>
  const makeViz = (id) => {
    const div = document.getElementById(id);
    const viz = div.getElementsByTagName('object')[0];
    viz.style.width = '100%';
    viz.style.height = '500px';
    const script = document.createElement('script');
    script.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';
    viz.parentNode.insertBefore(script, viz);
  };

  makeViz('vizDisability');
  makeViz('vizAge');
  makeViz('vizRace');
</script>

---

<div style="width: 100%; margin-bottom: 30px;">
<iframe width="700" height="600" allow="local-network-access; geolocation" title="Mobility Equity Map: Disability, Age, and Race" src="https://carnegiemellon.maps.arcgis.com/apps/mapviewer/index.html?configurableview=true&webmap=9fe674b63681452c87f55d94257ede6d&theme=light&bookmarks=true&heading=true&legend=true&information=true&scroll=false&center=-79.95869383411862,40.44552048874948&scale=144447.638572" ></iframe>
 </div>

## Dahboard 2 • Demographics & Mobility Equity Dashboard Report 
---
This report summarizes the key demographic patterns across Pittsburgh and highlights how these populations relate to vulnerability and mobility needs. The goal of this phase was to build a clear picture of *who* lives in Pittsburgh by race, age, and disability status and then use mapping tools to understand *where* these groups are concentrated across the city.

---

## Background  
Pittsburgh’s population is extremely uneven across neighborhoods. Some communities are diverse, dense, and transit-reliant, while others are older, wealthier, or geographically isolated.

The goal of this dashboard is to break down these differences into three core questions:

1. **Who makes up Pittsburgh’s population?**  
   (Race, age, disability)

2. **Where do vulnerable groups live?**  
   (Shown in the ArcGIS Income Vulnerability and Mobility Equity maps)

3. **How do these differences relate to mobility equity?**  
   (Transit access and neighborhood-level mobility support)

This report focuses only on the *demographic* layer of inequality setting up the foundation for understanding mobility access in the next dashboards.

---

# Demographic Insights

## 1. Disability Status  
The disability breakdown chart makes it clear that: although the majority of Pittsburgh residents do *not* have a disability, the group that *does* represents one of the most mobility-dependent populations in the city.

- The chart shows a massive gap between “with a disability” and “without a disability.”  
- Disabled residents are more sensitive to things like sidewalk conditions, bus stop accessibility, and route frequency.  

This is important because disability isn’t just a demographic category, it's a key vulnerability indicator that should influence where transit improvements go.

---

## 2. Age Breakdown  
The age histogram shows a really clear pattern:

- The largest group is **35–64 years old**, reflecting Pittsburgh’s strong working-age population.  
- The second major groups are:
  - **18–34 year olds** (students and early-career workers)
  - **65+ residents** (who often depend heavily on public transit)

The older adult population is especially important for mobility planning. If they live in steep, disconnected areas, or places where bus service has declined, the impact is way more severe than for other age groups.

Understanding where older adults live helps explain why some neighborhoods have higher mobility needs than others.

---

## 3. Race in Pittsburgh  
Race also plays a major role in neighborhood structure:

- White residents make up the largest portion of the population.  
- Black or African American residents form the second largest group.  
- Asian, multiracial, and American Indian populations make up smaller segments.

But what matters more than the counts is the *geography*:

- Black residents are heavily concentrated in neighborhoods like **Homewood, Hill District, Larimer**, and parts of East Liberty.  
- Asian residents cluster in **Squirrel Hill, Oakland, and Shadyside**.  
- White residents dominate most outer neighborhoods and the hills.

This matters because racial geography often lines up with historical transit investment patterns, which directly affects mobility equity today.

---

# Spatial Analysis with ArcGIS Maps

## 4. Income Vulnerability Map  

The Income Vulnerability map shows how economic challenge layers across the city. The greener regions represent high income vulnerability.

Some notable patterns:

- Vulnerable clusters appear in the **Hill District**, **Hazelwood**, **Homewood**, and pockets of the South Hills.  
- Wealthier neighborhoods like **Shadyside, Squirrel Hill, and Point Breeze** appear with significantly lower vulnerability.  
- These differences matter because transit-reliant residents tend to cluster in the same neighborhoods that already lack economic resources.

In other words: the people who rely most on transit often live in the areas where transit access is already the weakest.

---

## 5. Mobility Equity Map (Disability, Age, Race)  

This map overlays multiple demographic factors:

- Disability  
- Older adults  
- Income differences  
- Racial distribution  
- Transit access layers  

### Key takeaways:

- Many East End neighborhoods have overlapping vulnerabilities (age, race, disability, and income).  
- Some neighborhoods with high mobility needs are located in steep areas where walking is physically harder, meaning transit is even more important.  
- Wealthier areas with lower vulnerability often still have strong bus access, while high-vulnerability neighborhoods sometimes face service gaps.

This shows that mobility inequality in Pittsburgh isn’t random, it follows demographic and historical lines.

---

Note: All Tableau charts were generated using demographic datasets obtained from ArcGIS Online layers that were used to create the Maps (https://arcg.is/0Ty0rT and https://arcg.is/fvbTv0).


*Built with Observable, Tableau Public, and ArcGIS (Dec 2025)*  
