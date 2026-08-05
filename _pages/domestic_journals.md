---
layout: page
permalink: /publications/domestic-journals/
title: Domestic Journals
description: Peer-reviewed domestic journal publications.
nav: false
---

{% include bib_search.liquid %}

<style>
  .publications .author > em {
    font-weight: 700;
  }
</style>

<div class="publications">

<h2>Under Review</h2>

{% bibliography --group_by none --query @unpublished[category=domestic_journal] %}

<h2>Published</h2>

{% bibliography --query @article[category=domestic_journal] %}

</div>
