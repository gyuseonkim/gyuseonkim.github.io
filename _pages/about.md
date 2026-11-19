---
layout: about
title: about
permalink: /
subtitle: Research Engineer at RealtimeVisual Co., Ltd. | Reinforcement Learning for Aerospace Systems

profile:
  align: right
  image: gyu-seon-kim-profile.jpg
  image_circular: false
  more_info: >
    <p>RealtimeVisual Co., Ltd.</p>
    <p>Seoul, Republic of Korea</p>

selected_papers: false
social: true

research_keyword_groups:
  - title: Methods & Technologies
    style: methods
    keywords:
      - Reinforcement Learning
      - Multi-Agent RL
      - Quantum Machine Learning
      - Sim-to-Real
  - title: Application Areas
    style: applications
    keywords:
      - Aircraft & UAV Control
      - Urban Air Mobility
      - Satellite Autonomy
      - LEO Satellite Networks

announcements:
  enabled: false
  scrollable: true
  limit: 5

latest_posts:
  enabled: false
  scrollable: true
  limit: 3
---

<style>
  .about-keyword-groups {
    display: flow-root;
    margin: 1rem 0 1.5rem;
  }

  .about-keyword-group + .about-keyword-group {
    margin-top: 0.9rem;
  }

  .about-keyword-group > h3 {
    margin: 0 0 0.5rem;
    color: var(--global-text-color);
    font-size: 0.85rem;
    font-weight: 600;
    line-height: 1.4;
  }

  .about-keyword-group--methods {
    --keyword-text: #6b35a5;
    --keyword-bg: #f5effb;
    --keyword-border: #dfd0ef;
  }

  .about-keyword-group--applications {
    --keyword-text: #0f6262;
    --keyword-bg: #edf8f6;
    --keyword-border: #c5e7e1;
  }

  html[data-theme="dark"] .about-keyword-group--methods {
    --keyword-text: #ddc4ff;
    --keyword-bg: #31263f;
    --keyword-border: #5b4470;
  }

  html[data-theme="dark"] .about-keyword-group--applications {
    --keyword-text: #a4e4dd;
    --keyword-bg: #193634;
    --keyword-border: #315e59;
  }

  .about-keywords {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
    padding: 0;
    margin: 0;
    list-style: none;
  }

  .about-keywords > li {
    max-width: 100%;
    padding: 0.35rem 0.75rem;
    margin: 0;
    color: var(--keyword-text);
    font-size: 0.8rem;
    font-weight: 500;
    line-height: 1.4;
    background-color: var(--keyword-bg);
    border: 1px solid var(--keyword-border);
    border-radius: 999px;
  }
</style>

I am a research engineer specializing in **Reinforcement Learning**, **Quantum Machine Learning**, and **Autonomous Aerospace Systems**. My research focuses on developing advanced reinforcement learning for **Fighter Aircraft**, **Unmanned Aerial Vehicles (UAVs)**, **Urban Air Mobility (UAM)**, and **Satellite Systems**.

I am currently an **Aerospace AI Research Engineer** at **RealtimeVisual Co., Ltd.** in Seoul, Republic of Korea. My research centers on reinforcement-learning-based control algorithms for fighter aircraft and other aerospace vehicles, with a particular focus on **Sim-to-Real Transfer** to facilitate the reliable deployment of learned control policies on real-world flight platforms.

<div class="about-keyword-groups" aria-label="Research keywords">
  {% for group in page.research_keyword_groups %}
    <section class="about-keyword-group about-keyword-group--{{ group.style }}" aria-labelledby="keywords-{{ group.style }}">
      <h3 id="keywords-{{ group.style }}">{{ group.title | escape }}</h3>
      <ul class="about-keywords" role="list">
        {% for keyword in group.keywords %}
          <li>{{ keyword | escape }}</li>
        {% endfor %}
      </ul>
    </section>
  {% endfor %}
</div>

My research interests include:

- Reinforcement learning, multi-agent reinforcement learning, and quantum machine learning
- Physical AI for reinforcement-learning-based flight control
- Guidance, navigation, and control (GNC) for aerospace systems
- AI-based intelligent flight control for aircraft and UAVs
- Autonomous coordination and swarm control of UAM and UAV Fleets
- Autonomous satellite systems and low Earth orbit (LEO) satellite networks

<!-- - #Sim-to-real transfer and real-world deployment of reinforcement-learning-based flight control policies -->

<section class="about-background" aria-labelledby="background-heading">
  <h2 id="background-heading">Academic Background</h2>
  <div class="about-background__grid">
    <article class="about-background__card">
      <div class="about-background__logo">
        <img src="{{ '/assets/img/university-of-houston-interlock.png' | relative_url }}" alt="University of Houston interlocking UH logo">
      </div>
      <p class="about-background__eyebrow">Research Experience</p>
      <h3><strong>University of Houston</strong>, Houston, TX, USA</h3>
      <p class="about-background__detail"><strong>Visiting Scholar</strong>, <strong>Department of Electrical and Computer Engineering</strong></p>
    </article>

    <article class="about-background__card">
      <div class="about-background__logo about-background__logo--cv about-background__logo--korea">
        <img src="{{ '/assets/img/korea-university-emblem.png' | relative_url }}" alt="Korea University emblem">
      </div>
      <p class="about-background__eyebrow">Doctoral Degree</p>
      <h3><strong>Korea University</strong>, Seoul, Republic of Korea</h3>
      <p class="about-background__detail"><strong>Ph.D. in Electrical and Computer Engineering</strong></p>
    </article>

    <article class="about-background__card">
      <div class="about-background__logo about-background__logo--cv about-background__logo--inha">
        <img src="{{ '/assets/img/inha-university-emblem.svg' | relative_url }}" alt="Inha University emblem">
      </div>
      <p class="about-background__eyebrow">Bachelor's Degree</p>
      <h3><strong>Inha University</strong>, Incheon, Republic of Korea</h3>
      <p class="about-background__detail"><strong>B.S. in Aerospace Engineering</strong></p>
    </article>

  </div>
</section>

<section class="about-background" aria-labelledby="industry-background-heading">
  <h2 id="industry-background-heading">Industry Background</h2>
  <div class="about-background__grid about-background__grid--single">
    <article class="about-background__card about-background__card--industry">
      <div class="about-background__logo about-background__logo--company">
        <img src="{{ '/assets/img/realtimevisual-logo.png' | relative_url }}" alt="RealtimeVisual company logo">
      </div>
      <div class="about-background__copy">
        <p class="about-background__eyebrow">Current Position</p>
        <h3><strong>RealtimeVisual Co., Ltd.</strong></h3>
        <p class="about-background__detail"><em><strong>Aerospace AI Research Engineer (Military Service Exception)</strong></em></p>
        <p class="about-background__detail about-background__detail--description">
          Research on reinforcement learning-based flight control for fighter aircraft and other aerial vehicles, with a focus on sim-to-real policy transfer to physical flight platforms.
        </p>
      </div>
    </article>
  </div>
</section>
