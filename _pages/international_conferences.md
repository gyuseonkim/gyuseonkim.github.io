---
layout: page
permalink: /publications/international-conferences/
title: International Conferences
description: Peer-reviewed international conference publications.
nav: false
---

{% include bib_search.liquid %}

{% capture publication_count %}{% bibliography_count --query @*[category=international_conference] %}{% endcapture %}
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

{% bibliography --query @inproceedings[category=international_conference] %}

</div>

<script>
  const getConferenceBibtexField = (entry, field) => {
    const bibtex = entry.querySelector(".bibtex code")?.textContent;
    if (!bibtex) return "";

    const match = bibtex.match(new RegExp(`^\\s*${field}\\s*=\\s*\\{([^{}]*)\\},?\\s*$`, "mi"));
    return match?.[1]?.trim() ?? "";
  };

  document.querySelectorAll(".numbered-publications ol.bibliography > li").forEach((entry) => {
    const periodical = entry.querySelector(".periodical");
    const proceedings = periodical?.querySelector("em");
    const address = getConferenceBibtexField(entry, "address");
    const month = getConferenceBibtexField(entry, "month");
    const year = getConferenceBibtexField(entry, "year");
    const pages = getConferenceBibtexField(entry, "pages").replaceAll("--", "-");

    if (!periodical || !proceedings || !address || !year) return;

    proceedings.textContent = proceedings.textContent.replace(/^In\s+/i, "").trim();

    const details = [address, [month, year].filter(Boolean).join(" ")];
    if (pages) details.push(`pp. ${pages}`);

    periodical.replaceChildren(document.createTextNode("in "), proceedings, document.createTextNode(`, ${details.join(", ")}.`));
  });

  document.querySelectorAll(".numbered-publications ol.bibliography > li").forEach((entry, index, entries) => {
    entry.dataset.publicationNumber = entries.length - index;
  });
</script>
