---
layout: page
permalink: /publications/
title: publications
description: 
years_journal: [2024_j, 2023_j, 2022_j, 2021_j, 2020_j, 2019_j, 2018_j, 2017_j,2015_j, 2013_j]
years_conference: [2024_c, 2023_c, 2022_c, 2021_c, 2020_c, 2019_c, 2018_c, 2017_c, 2015_c, 2013_c]
years_workshop: [2025_w, 2019_w]
nav: true
nav_order: 1
---
<div class="publications">
 ------------------------------------------

  <h3>Journal Papers</h3>
  {%- for y in page.years_journal %}
    <!-- <h3 class="year">{{y}}</h3> -->
    {% bibliography -f papers -q @*[year={{y}}] and @*[entrytype=article]* -m 5 %}
  {%- endfor %}

 ------------------------------------------

  <h3>Conference Papers</h3>
  {%- for y in page.years_conference %}
    <!-- <h3 class="year">{{y}}</h3> -->
    {% bibliography -f papers -q @*[year={{y}}] and @*[entrytype=article]* -m 5 %}
  {%- endfor %}

 ------------------------------------------


  <h3>Workshop Papers</h3>
  {%- for y in page.years_workshop %}
    <!-- <h3 class="year">{{y}}</h3> -->
    {% bibliography -f papers -q @*[year={{y}}] and @*[entrytype=article]* -m 5 %}
  {%- endfor %}

</div>
