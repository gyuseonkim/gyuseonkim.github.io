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
    font-style: normal;
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
  const formatDomesticPublicationTitle = (title) => {
    const titleText = title.textContent.trim();
    if (!titleText.endsWith(")")) return;

    let depth = 0;
    let englishTitleStart = -1;

    for (let index = titleText.length - 1; index >= 0; index -= 1) {
      if (titleText[index] === ")") depth += 1;
      if (titleText[index] === "(") {
        depth -= 1;
        if (depth === 0) {
          englishTitleStart = index;
          break;
        }
      }
    }

    if (englishTitleStart < 1) return;

    const koreanTitle = titleText.slice(0, englishTitleStart).trim();
    const englishTitle = titleText.slice(englishTitleStart + 1, -1).trim();
    if (!koreanTitle || !englishTitle) return;

    const englishTitleLine = document.createElement("span");
    englishTitleLine.textContent = `- ${englishTitle} -`;
    title.replaceChildren(document.createTextNode(koreanTitle), document.createElement("br"), englishTitleLine);
  };

  document.querySelectorAll(".numbered-publications .title").forEach(formatDomesticPublicationTitle);

  document.querySelectorAll(".numbered-publications .periodical").forEach((periodical) => {
    periodical.childNodes.forEach((node) => {
      if (node.nodeType === Node.TEXT_NODE) {
        node.textContent = node.textContent.replace(/\s+,/g, ",");
      }
    });
  });

  document.querySelectorAll(".numbered-publications ol.bibliography > li").forEach((entry, index, entries) => {
    entry.dataset.publicationNumber = entries.length - index;
  });
</script>
