---
layout: page
permalink: /publications/domestic-conferences/
title: Domestic Conferences
description: Domestic conference publications.
nav: false
---

{% include bib_search.liquid %}

<style>
  .publications .author > em {
    font-weight: 700;
  }
</style>

<div class="publications">

<h2>Presented and Published</h2>

{% bibliography --query @inproceedings[category=domestic_conference] %}

</div>
