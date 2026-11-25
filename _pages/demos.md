---
layout: page
permalink: /demos/
title: Demos
description: Interactive visualizations and recorded demonstrations of research prototypes in reinforcement learning for aerospace systems.
nav: true
nav_order: 2.5
---

<style>
  .demo-card {
    position: relative;
    padding: 1.5rem;
    margin-bottom: 2rem;
    overflow: hidden;
    background: var(--global-card-bg-color, var(--global-bg-color));
    border: 1px solid var(--global-divider-color);
    border-radius: 0.75rem;
    box-shadow: 0 0.25rem 0.75rem rgba(0, 0, 0, 0.06);
  }

  .demo-card::before {
    position: absolute;
    top: 0;
    right: 0;
    left: 0;
    height: 3px;
    content: "";
    background: var(--global-theme-color);
  }

  .demo-card__eyebrow {
    margin: 0 0 0.35rem;
    color: var(--global-theme-color);
    font-size: 0.75rem;
    font-weight: 700;
    letter-spacing: 0.04em;
    text-transform: uppercase;
  }

  .demo-card > h2 {
    margin: 0 0 0.75rem;
    font-size: 1.35rem;
    line-height: 1.35;
  }

  .demo-card h3 {
    margin: 1.5rem 0 0.6rem;
    font-size: 1.05rem;
    font-weight: 600;
  }

  .demo-card p {
    line-height: 1.6;
  }

  .demo-card__tags {
    display: flex;
    flex-wrap: wrap;
    gap: 0.4rem;
    padding: 0;
    margin: 0 0 1.25rem;
    list-style: none;
  }

  .demo-card__tags > li {
    padding: 0.2rem 0.65rem;
    margin: 0;
    color: var(--global-text-color-light);
    font-size: 0.75rem;
    font-weight: 500;
    line-height: 1.4;
    border: 1px solid var(--global-divider-color);
    border-radius: 999px;
  }

  .demo-card__viewer {
    position: relative;
    min-height: 480px;
    overflow: hidden;
    background: #080b11;
    border: 1px solid var(--global-divider-color);
    border-radius: 0.5rem;
    aspect-ratio: 16 / 10;
  }

  .demo-card__viewer iframe {
    position: absolute;
    inset: 0;
    width: 100%;
    height: 100%;
    border: 0;
  }

  .demo-card__caption {
    margin: 0.6rem 0 0;
    color: var(--global-text-color-light);
    font-size: 0.85rem;
  }

  .demo-card__actions {
    margin: 0.75rem 0 0;
  }

  .demo-card__table {
    width: 100%;
    margin: 0;
    font-size: 0.9rem;
    border-collapse: collapse;
  }

  .demo-card__table th,
  .demo-card__table td {
    padding: 0.45rem 0.75rem 0.45rem 0;
    text-align: left;
    vertical-align: top;
    border-bottom: 1px solid var(--global-divider-color);
  }

  .demo-card__table th {
    font-weight: 600;
    white-space: nowrap;
  }

  .demo-card__table thead th {
    color: var(--global-text-color-light);
    font-size: 0.75rem;
    letter-spacing: 0.04em;
    text-transform: uppercase;
  }

  .demo-card__table-wrap {
    overflow-x: auto;
  }

  .demo-card__note {
    margin: 1.25rem 0 0;
    color: var(--global-text-color-light);
    font-size: 0.8rem;
    font-style: italic;
  }

  @media (max-width: 640px) {
    .demo-card {
      padding: 1.1rem;
    }

    .demo-card__viewer {
      min-height: 0;
      aspect-ratio: 4 / 5;
    }
  }
</style>

<article class="demo-card" id="rl-uav-strike" aria-labelledby="rl-uav-strike-title">
  <p class="demo-card__eyebrow">Demo 1 &middot; Interactive 3D Replay &middot; Simulation</p>
  <h2 id="rl-uav-strike-title">Reinforcement Learning-Based Strike Mission of a Military UAV under Integrated Air-Defense Threats</h2>
  <ul class="demo-card__tags" aria-label="Keywords">
    <li>Reinforcement Learning</li>
    <li>Military UAV</li>
    <li>Precision Strike</li>
    <li>Threat-Aware Navigation</li>
    <li>Low-Altitude Flight</li>
  </ul>
  <div class="demo-card__viewer">
    <iframe
      src="{{ '/assets/demos/sortie-replay/' | relative_url }}"
      title="Interactive 3D replay of a reinforcement learning-based UAV strike mission"
      loading="lazy"
      allow="fullscreen"
      allowfullscreen
    ></iframe>
  </div>
  <p class="demo-card__caption">
    <strong>Figure 1.</strong> Interactive replay of a single evaluation episode (Scenario 9003). The flight path is colored by the instantaneous probability of
    detection, P(det), from cyan (low) to red (high), and the timeline strip marks the mission phases. Drag to rotate the view, press Ctrl and scroll to zoom,
    and switch to <em>Cockpit</em> for a first-person view.
  </p>
  <p class="demo-card__actions">
    <a href="{{ '/assets/demos/sortie-replay/' | relative_url }}" class="btn btn-sm z-depth-0" role="button" target="_blank" rel="noopener noreferrer">Open Full Screen</a>
  </p>
  <h3>Overview</h3>
  <p>
    This demonstration replays an evaluation episode of a reinforcement learning (RL) policy that autonomously flies a military unmanned aerial vehicle (UAV) from a
    launch point to a designated ground target. The mission takes place over procedurally generated terrain defended by an integrated air-defense network of
    surveillance radars, a surface-to-air missile (SAM) site, and electronic jammers, together with tall vertical obstacles. The trained actor network commands the
    UAV throughout the sortie, balancing progress toward the target against the adversary's probability of detection and radar track quality. The mission proceeds
    through ingress, midcourse, and terminal phases and concludes with a terminal dive onto the target.
  </p>
  <h3>Scenario Configuration</h3>
  <div class="demo-card__table-wrap">
    <table class="demo-card__table">
      <tbody>
        <tr>
          <th scope="row">Terrain</th>
          <td>8 km &times; 8 km procedurally generated digital elevation model (110 &times; 110 grid; elevation &minus;30 to 390 m)</td>
        </tr>
        <tr>
          <th scope="row">Air-defense threats</th>
          <td>5 surveillance radars (coverage radius 2.8&ndash;3.0 km), 1 SAM site (engagement radius 0.66 km), 2 electronic jammers (0.77&ndash;1.38 km)</td>
        </tr>
        <tr>
          <th scope="row">Obstacles</th>
          <td>4 vertical obstacles, 145&ndash;219 m in height</td>
        </tr>
        <tr>
          <th scope="row">Mission</th>
          <td>Launch-to-target strike along a 9-waypoint reference route (8.4 km straight-line distance)</td>
        </tr>
        <tr>
          <th scope="row">Monitored states</th>
          <td>Airspeed, altitude above ground level (AGL), attitude, P(det), radar track quality, and mission phase</td>
        </tr>
      </tbody>
    </table>
  </div>
  <h3>Episode Results</h3>
  <div class="demo-card__table-wrap">
    <table class="demo-card__table">
      <tbody>
        <tr>
          <th scope="row">Mission outcome</th>
          <td>Success</td>
        </tr>
        <tr>
          <th scope="row">Flight time / distance</th>
          <td>415 s / 9.35 km (1.12&times; the straight-line distance)</td>
        </tr>
        <tr>
          <th scope="row">Airspeed</th>
          <td>22.5 m/s on average (18.1&ndash;34.8 m/s)</td>
        </tr>
        <tr>
          <th scope="row">Altitude</th>
          <td>90 m AGL on average</td>
        </tr>
        <tr>
          <th scope="row">Radar exposure</th>
          <td>100% of the trajectory lies within the nominal coverage of at least one radar</td>
        </tr>
        <tr>
          <th scope="row">Probability of detection</th>
          <td>Mean 0.09, peak 0.87; P(det) &gt; 0.5 in only 1.7% of time steps</td>
        </tr>
        <tr>
          <th scope="row">SAM avoidance</th>
          <td>Closest approach 787 m, outside the 660 m engagement radius</td>
        </tr>
        <tr>
          <th scope="row">Terminal accuracy</th>
          <td>3.8 m horizontal miss distance</td>
        </tr>
      </tbody>
    </table>
  </div>
  <h3>Mission Phases</h3>
  <div class="demo-card__table-wrap">
    <table class="demo-card__table">
      <thead>
        <tr>
          <th scope="col">Phase</th>
          <th scope="col">Time window</th>
          <th scope="col">Mean AGL</th>
          <th scope="col">Mean P(det)</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th scope="row">Ingress</th>
          <td>0&ndash;43 s</td>
          <td>69 m</td>
          <td>0.02</td>
        </tr>
        <tr>
          <th scope="row">Midcourse</th>
          <td>44&ndash;362 s</td>
          <td>96 m</td>
          <td>0.10</td>
        </tr>
        <tr>
          <th scope="row">Terminal</th>
          <td>363&ndash;389 s</td>
          <td>76 m</td>
          <td>0.01</td>
        </tr>
        <tr>
          <th scope="row">Dive</th>
          <td>390&ndash;415 s</td>
          <td>72 m (descending to 10 m)</td>
          <td>0.15</td>
        </tr>
      </tbody>
    </table>
  </div>
  <p class="demo-card__note">The terrain, threat layout, and mission are synthetic and procedurally generated for simulation purposes.</p>
</article>
