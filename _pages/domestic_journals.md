---
layout: page
permalink: /publications/domestic-journals/
title: Domestic Journals (KCI)
description: Peer-reviewed domestic journal publications.
nav: false
---

{% include bib_search.liquid %}

{% capture publication_count %}{% bibliography_count --query @*[category=domestic_journal] %}{% endcapture %}
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

<h2>Published</h2>

{% bibliography --query @article[category=domestic_journal] %}

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

  const getDomesticJournalBibtexField = (entry, field) => {
    const bibtex = entry.querySelector(".bibtex code")?.textContent;
    if (!bibtex) return "";

    const match = bibtex.match(new RegExp(`^\\s*${field}\\s*=\\s*\\{([^{}]*)\\},?\\s*$`, "mi"));
    return match?.[1]?.trim() ?? "";
  };

  document.querySelectorAll(".numbered-publications .title").forEach(formatDomesticPublicationTitle);

  document.querySelectorAll(".numbered-publications ol.bibliography > li").forEach((entry) => {
    const periodical = entry.querySelector(".periodical");
    const journal = periodical?.querySelector("em");
    const volume = getDomesticJournalBibtexField(entry, "volume");
    const number = getDomesticJournalBibtexField(entry, "number");
    const pages = getDomesticJournalBibtexField(entry, "pages").replaceAll("--", "-");
    const month = getDomesticJournalBibtexField(entry, "month");
    const year = getDomesticJournalBibtexField(entry, "year");

    if (!periodical || !journal || !year) return;

    const details = [];
    if (volume) details.push(`vol. ${volume}`);
    if (number) details.push(`no. ${number}`);
    if (pages) details.push(`pp. ${pages}`);
    details.push([month, year].filter(Boolean).join(" "));

    periodical.replaceChildren(journal, document.createTextNode(`, ${details.join(", ")}`));
  });

  document.querySelectorAll(".numbered-publications ol.bibliography > li").forEach((entry, index, entries) => {
    entry.dataset.publicationNumber = entries.length - index;
  });

  const orderPublicationButtons = (links) => {
    const buttons = [...links.children];
    const abstractButton = buttons.find(
      (button) => button.classList.contains("abstract") && button.textContent.trim() === "Abs",
    );
    const bibButton = buttons.find((button) => button.classList.contains("bibtex"));
    const awardButton = buttons.find((button) => button.classList.contains("award"));
    const linkButtons = buttons.filter((button) => button.matches("a"));
    const doiButton = linkButtons.find((link) => link.textContent.trim() === "DOI");
    const htmlButton = linkButtons.find((link) => link.textContent.trim() === "HTML");
    const publicationButton = doiButton ?? htmlButton;

    if (abstractButton) abstractButton.textContent = "Abstract";
    if (publicationButton) publicationButton.textContent = "DOI";
    if (doiButton && htmlButton) htmlButton.remove();

    links.prepend(...[abstractButton, publicationButton, bibButton].filter(Boolean));
    if (awardButton) links.append(awardButton);
  };

  document.querySelectorAll(".numbered-publications .links").forEach(orderPublicationButtons);
</script>
