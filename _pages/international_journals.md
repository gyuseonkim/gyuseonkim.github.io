---
layout: page
permalink: /publications/international-journals/
title: International Journals
description: Peer-reviewed international journal publications.
nav: false
---

{% include bib_search.liquid %}

<style>
  .publications .author > em {
    font-weight: 700;
  }
</style>

<div class="publications">

<h2>Under Review and Revision</h2>

{% bibliography --group_by none --query @unpublished[category=international_journal] %}

<h2>Published and Early Access</h2>

{% bibliography --query @article[category=international_journal] %}

</div>
