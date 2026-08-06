---
layout: page
permalink: /publications/international-journals/
title: International Journals (SCI)
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

  .publications .co-first-label {
    font-weight: 700;
  }

  .publications .co-first-mark {
    font-size: 0.75em;
    line-height: 0;
    vertical-align: super;
  }

  .publications .co-first-note {
    margin-top: 0.15rem;
    font-size: 0.9rem;
    line-height: 1.4;
  }

  .publications .co-first-entry .more-authors {
    color: inherit;
    cursor: default;
    border-bottom: 0;
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

  const createCoFirstMark = () => {
    const mark = document.createElement("sup");
    mark.className = "co-first-mark";
    mark.textContent = "†";
    return mark;
  };

  document
    .querySelectorAll('.numbered-publications .author > [data-content="Gyu Seon Kim is a co-first author."]')
    .forEach((annotation) => {
      const authorLine = annotation.parentElement;
      const selfAuthor = authorLine.querySelector(":scope > em");
      const firstAuthor = Array.from(authorLine.childNodes).find(
        (node) => node.nodeType === Node.TEXT_NODE && node.textContent.trim(),
      );
      const firstAuthorParts = firstAuthor?.textContent.match(/^(\s*[^,]+)(,.*)$/);

      if (firstAuthorParts && !authorLine.querySelector(":scope > .co-first-mark")) {
        firstAuthor.textContent = firstAuthorParts[1];
        firstAuthor.after(createCoFirstMark(), document.createTextNode(firstAuthorParts[2]));
      }

      if (selfAuthor && !selfAuthor.querySelector(":scope > .co-first-mark")) {
        selfAuthor.append(createCoFirstMark());
      }

      if (selfAuthor && !authorLine.querySelector(":scope > .co-first-label")) {
        const label = document.createElement("span");
        label.className = "co-first-label";
        label.textContent = " (co-first author)";
        selfAuthor.insertAdjacentElement("afterend", label);
      }

      const moreAuthors = authorLine.querySelector(":scope > .more-authors");

      if (moreAuthors && /more authors?$/.test(moreAuthors.textContent.trim())) {
        const hiddenAuthors = moreAuthors
          .getAttribute("onclick")
          ?.match(/more_authors_text\s*=[\s\S]*?\?\s*'([^']+)'\s*:/)?.[1]
          ?.split(", ");

        if (hiddenAuthors?.length) {
          const precedingText = moreAuthors.previousSibling;

          if (hiddenAuthors.length > 1 && precedingText?.nodeType === Node.TEXT_NODE) {
            precedingText.textContent = precedingText.textContent.replace(/,\s+and\s*$/, ", ");
          }

          moreAuthors.textContent =
            hiddenAuthors.length > 1
              ? `${hiddenAuthors.slice(0, -1).join(", ")}, and ${hiddenAuthors.at(-1)}`
              : hiddenAuthors[0];
        } else {
          moreAuthors.click();
        }

        moreAuthors.removeAttribute("onclick");
        moreAuthors.removeAttribute("title");
      }

      const entry = authorLine.closest("li");
      entry?.classList.add("co-first-entry");

      if (!authorLine.nextElementSibling?.classList.contains("co-first-note")) {
        const note = document.createElement("div");
        note.className = "co-first-note";
        note.append(createCoFirstMark(), document.createTextNode(" These authors contributed equally."));
        authorLine.insertAdjacentElement("afterend", note);
      }

      annotation.remove();
    });

  document.querySelectorAll(".numbered-publications ol.bibliography > li").forEach((entry, index, entries) => {
    entry.dataset.publicationNumber = entries.length - index;
  });
</script>
