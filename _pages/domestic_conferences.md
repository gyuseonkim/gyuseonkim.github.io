---
layout: page
permalink: /publications/domestic-conferences/
title: Domestic Conferences
description: Domestic conference publications.
nav: false
---

{% include bib_search.liquid %}

{% capture publication_count %}{% bibliography_count --query @*[category=domestic_conference] %}{% endcapture %}
{% assign publication_counter_start = publication_count | plus: 1 %}

<style>
  .publications .author > em {
    font-weight: 700;
  }

  .numbered-publications {
    counter-reset: publication-number {{ publication_counter_start }};
  }

  .numbered-publications ol.bibliography > li {
    position: relative;
    padding-left: 2.75rem;
    counter-increment: publication-number -1;
  }

  .numbered-publications ol.bibliography > li::before {
    position: absolute;
    top: 0;
    left: 0;
    width: 2rem;
    content: counter(publication-number) ".";
    font-weight: 600;
    text-align: right;
  }

  .numbered-publications ol.bibliography > li[data-publication-number]::before {
    content: attr(data-publication-number) ".";
  }
</style>

<div class="publications numbered-publications">

<h2>Presented and Published</h2>

{% bibliography --query @inproceedings[category=domestic_conference] %}

</div>

<script>
  document.querySelectorAll(".numbered-publications ol.bibliography > li").forEach((entry, index, entries) => {
    entry.dataset.publicationNumber = entries.length - index;
  });
</script>
