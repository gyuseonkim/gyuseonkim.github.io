---
layout: page
permalink: /publications/international-journals/
title: International Journals
description: Peer-reviewed international journal publications.
nav: false
---

{% include bib_search.liquid %}

{% capture publication_count %}{% bibliography_count --query @*[category=international_journal] %}{% endcapture %}
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

<h2>Under Review</h2>

{% bibliography --group_by none --query @unpublished[category=international_journal&&note~=Under.Review] %}

<h2>Under Revision</h2>

{% bibliography --group_by none --query @unpublished[category=international_journal&&note~=Under.Revision] %}

<h2>Published</h2>

{% bibliography --group_by none --query @article[category=international_journal&&note~=Early.Access] %}

{% bibliography --query @article[category=international_journal&&note!~Early.Access] %}

</div>

<script>
  document.querySelectorAll(".numbered-publications .periodical").forEach((periodical) => {
    periodical.childNodes.forEach((node) => {
      if (node.nodeType === Node.TEXT_NODE) {
        node.textContent = node.textContent.replace(/\s+,/g, ",");
      }
    });

    const reviewStatus = periodical.textContent.trim().match(/^(.+?)\s+(\(Under (?:Review|Revision)\))$/);

    if (reviewStatus) {
      const journal = document.createElement("em");
      journal.textContent = reviewStatus[1];
      periodical.replaceChildren(journal, document.createTextNode(` ${reviewStatus[2]}`));
    }
  });

  document
    .querySelectorAll('.numbered-publications .author > [data-content="Gyu Seon Kim is a co-first author."]')
    .forEach((annotation) => {
      const selfAuthor = annotation.parentElement.querySelector(":scope > em");

      if (selfAuthor && !annotation.parentElement.querySelector(":scope > .co-first-label")) {
        const label = document.createElement("span");
        label.className = "co-first-label";
        label.textContent = " (co-first)";
        selfAuthor.insertAdjacentElement("afterend", label);
      }

      annotation.remove();
    });

  document.querySelectorAll(".numbered-publications ol.bibliography > li").forEach((entry, index, entries) => {
    entry.dataset.publicationNumber = entries.length - index;
  });
</script>
