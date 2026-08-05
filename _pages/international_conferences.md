---
layout: page
permalink: /publications/international-conferences/
title: International Conferences
description: Peer-reviewed international conference publications.
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

{% bibliography --query @inproceedings[category=international_conference] %}

</div>
