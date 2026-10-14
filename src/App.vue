<script setup lang="ts">
import { ref } from 'vue'
import { posterUrl } from './paths'

const active = ref('overview')
const sections = [
  { id: 'overview', label: 'At a glance' },
  { id: 'experiment', label: 'The recordings' },
  { id: 'forecast', label: 'Prediction' },
  { id: 'decoding', label: 'Flash decoding' },
  { id: 'directed', label: 'Region links' },
  { id: 'energy', label: 'Energy estimates' },
  { id: 'limits', label: 'What it means' },
]

function setActive(id: string) {
  active.value = id
}
</script>

<template>
  <div class="site-shell">
    <header class="topbar">
      <a class="brand" href="#top" aria-label="Brain Energy home">
        <span class="brand-mark"><span></span><span></span><span></span></span>
        <span>Brain Energy <i>/ V8</i></span>
      </a>
      <nav class="top-links" aria-label="Main navigation">
        <a href="#poster">Poster</a>
        <a href="#guide">Guide</a>
        <a href="https://github.com/neurobiol/welcome/tree/main" target="_blank" rel="noreferrer">Research home ↗</a>
      </nav>
      <a class="github-pill" href="https://github.com/neurobiol/unlearn" target="_blank" rel="noreferrer">
        <span class="github-dot"></span> Project example
      </a>
    </header>

    <main id="top">
      <section class="hero">
        <div class="hero-copy">
          <p class="eyebrow"><span class="eyebrow-line"></span> REAL NEURAL RECORDINGS · EXPLORATORY ANALYSIS</p>
          <h1>What can neural<br /><em>activity tell us?</em></h1>
          <p class="hero-deck">A guide to our poster, comparing classical and quantum-like mathematical models on real visual-system recordings.</p>
          <div class="author-line">
            <div class="author-dots"><span>Y</span><span>L</span><span>C</span></div>
            <div><strong>Yashine H. Goolam Hossen, Lea Gassab, T. J. A. Craddock</strong><small>Department of Biology · University of Waterloo</small></div>
          </div>
          <div class="hero-actions">
            <a class="btn-main" href="#guide">Explore the findings <span>↓</span></a>
            <a class="btn-text" href="#poster">View the poster <span>↗</span></a>
          </div>
        </div>
        <div class="hero-art" aria-label="Illustration of neural activity across connected brain regions">
          <div class="orbit orbit-one"></div><div class="orbit orbit-two"></div><div class="orbit orbit-three"></div>
          <div class="region region-lgd"><span class="region-label">LGd</span><b></b></div>
          <div class="region region-visp"><span class="region-label">VISp</span><b></b></div>
          <div class="region region-visl"><span class="region-label">VISl</span><b></b></div>
          <svg class="neural-lines" viewBox="0 0 600 560" role="presentation">
            <path d="M150 286 C235 220, 278 185, 365 197"/><path d="M169 307 C255 340, 340 365, 430 320"/>
            <path d="M365 211 C399 251, 416 272, 431 305"/><path d="M148 271 C227 148, 355 133, 432 304" class="line-faint"/>
            <circle cx="150" cy="286" r="4"/><circle cx="365" cy="197" r="4"/><circle cx="430" cy="320" r="4"/>
          </svg>
          <div class="spark spark-a">✳</div><div class="spark spark-b">✳</div><div class="art-note">A simplified map<br />of recorded regions</div>
          <div class="art-stamp">V8<br /><small>DATA STUDY</small></div>
        </div>
        <div class="hero-bottom"><span>01 — RESEARCH OVERVIEW</span><span>SCROLL TO EXPLORE <b>↓</b></span></div>
      </section>

      <section class="metrics-strip" aria-label="Study summary">
        <div><strong>3</strong><span>mouse recording<br />sessions</span></div>
        <div><strong>450</strong><span>visual flash<br />trials</span></div>
        <div><strong>131k</strong><span>recorded spike<br />times</span></div>
        <div class="metric-note"><span class="tiny-star">✳</span><p>Data from the Allen Institute’s Visual Coding Neuropixels recordings.</p></div>
      </section>

      <section id="guide" class="guide-section">
        <aside class="side-index">
          <p class="eyebrow">IN THIS GUIDE</p>
          <a v-for="(item, index) in sections" :key="item.id" :href="`#${item.id}`" :class="{ selected: active === item.id }" @click="setActive(item.id)">
            <span>0{{ index + 1 }}</span>{{ item.label }}
          </a>
          <div class="index-note"><span>↳</span> Start with the big picture, then explore each result.</div>
        </aside>

        <div class="guide-content">
          <section id="overview" class="content-block intro-block" @mouseenter="setActive('overview')">
            <p class="eyebrow"><span class="section-number">01</span> THE BIG PICTURE</p>
            <h2>One dataset.<br /><em>Two ways to describe it.</em></h2>
            <p class="body-lead">We asked whether compact, quantum-like mathematics can help describe patterns in brain activity. Then we compared it with classical models using recordings from mice watching brief black or white flashes.</p>
            <div class="callout"><span class="callout-icon">i</span><p><strong>What “quantum-like” means here</strong><br />The model uses mathematical forms also found in quantum theory. The recordings do not show that neurons were quantum coherent, and the analysis does not test for quantum effects in the brain.</p></div>
          </section>

          <section id="experiment" class="content-block" @mouseenter="setActive('experiment')">
            <p class="eyebrow"><span class="section-number">02</span> THE RECORDINGS</p>
            <h2>Following a flash<br />through the visual system.</h2>
            <p class="body-copy">Neuropixels probes record brief electrical spikes from neurons. We studied three areas: LGd, a visual relay area; VISp, also called primary visual cortex (V1); and VISl, lateral visual cortex.</p>
            <div class="flow-card">
              <div class="flow-step"><span class="step-icon flash-icon">✳</span><b>Black or white<br />flash</b><small>about 250 ms</small></div>
              <div class="flow-arrow">→</div>
              <div class="flow-step"><span class="step-icon pulse-icon">⌁</span><b>Neural spike<br />recordings</b><small>20 ms bins</small></div>
              <div class="flow-arrow">→</div>
              <div class="flow-step"><span class="step-icon model-icon">◉</span><b>Held-out<br />predictions</b><small>later trials</small></div>
            </div>
            <p class="caption">Two sessions had all three regions available during flashes. The third lacked V1 data in that time window, so those V1 links were marked unavailable.</p>
          </section>

          <section id="forecast" class="content-block" @mouseenter="setActive('forecast')">
            <p class="eyebrow"><span class="section-number">03</span> FORECASTING</p>
            <h2>Classical models<br />predicted a little better.</h2>
            <p class="body-copy">We gave each model recent activity and asked it to predict spike counts 100 milliseconds later. Smaller error means a closer prediction.</p>
            <div class="score-card">
              <div class="score-head"><span>100 ms forecast error (RMSE)</span><small>Lower is better</small></div>
              <div class="bar-row"><span>Quantum-like density</span><div class="bar-track"><i style="width:80%"></i></div><b>0.399</b></div>
              <div class="bar-row"><span>Classical complex twin</span><div class="bar-track"><i style="width:80%"></i></div><b>0.399</b></div>
              <div class="bar-row best"><span>Classical VAR</span><div class="bar-track"><i style="width:78%"></i></div><b>0.393</b></div>
              <div class="bar-row best"><span>Stimulus-time baseline</span><div class="bar-track"><i style="width:76%"></i></div><b>0.386</b></div>
              <div class="score-foot">A lower RMSE means the model's predicted spike counts were closer to the held-out recordings.</div>
            </div>
            <p class="caption">The quantum-like model and its classical twin have identical predictions by construction. The compact model also used fewer fitted coefficients than VAR, a tradeoff in model size and accuracy rather than a quantum advantage.</p>
          </section>

          <section id="decoding" class="content-block" @mouseenter="setActive('decoding')">
            <p class="eyebrow"><span class="section-number">04</span> AFTER THE FLASH</p>
            <h2>The earlier flash<br />was still readable.</h2>
            <p class="body-copy">We used activity after the flash to ask whether it had been black or white. The classical linear-count decoder was correct on 98.3% of held-out trials in the two complete sessions.</p>
            <div class="decode-card">
              <div class="decode-number">98<span>.3%</span></div>
              <div class="decode-details"><b>Classical linear-count decoder</b><small>held-out flash-polarity accuracy</small><div class="decode-track"><i></i></div><small>Chance level for two balanced choices: 50%</small></div>
              <div class="decode-flashes"><span class="black-flash"></span><span class="white-flash"></span><small>BLACK / WHITE</small></div>
            </div>
            <p class="caption">The readout used activity about 100–350 ms after the flash ended. This shows that information was available in the recorded activity; it does not prove the animals held the flash in working memory.</p>
          </section>

          <section id="directed" class="content-block" @mouseenter="setActive('directed')">
            <p class="eyebrow"><span class="section-number">05</span> BETWEEN REGIONS</p>
            <h2>Some activity<br />helped predict other activity.</h2>
            <p class="body-copy">After accounting for average flash responses, other recorded regions, and running speed, four directed links improved held-out prediction in shuffle checks.</p>
            <div class="links-card">
              <div class="link-row"><span>VISp</span><i>→</i><b>LGd</b><small>Session 1</small></div>
              <div class="link-row"><span>VISl</span><i>→</i><b>VISp</b><small>Session 2</small></div>
              <div class="link-row"><span>LGd</span><i>→</i><b>VISl</b><small>Session 3*</small></div>
              <div class="link-row"><span>VISl</span><i>→</i><b>LGd</b><small>Session 3*</small></div>
              <p>*The third session had two regions available, so its estimates are not directly equivalent to three-region results.</p>
            </div>
            <p class="caption">These are conditional predictive relationships, not proof of cause, direct synapses, or a route taken by information. The pattern differed across animals.</p>
          </section>

          <section id="energy" class="content-block" @mouseenter="setActive('energy')">
            <p class="eyebrow"><span class="section-number">06</span> ENERGY ESTIMATES</p>
            <h2>A useful proxy,<br />not a metabolic measurement.</h2>
            <p class="body-copy">We carried forward an ATP-based estimate from the earlier project version. It combines the number of recorded units and spikes with assumed costs from published conventions.</p>
            <div class="energy-card"><div class="energy-symbol">ATP<br /><small>proxy</small></div><div><b>Same estimated activity cost across model comparisons</b><p>The quantum-like decoder did not score higher in information per estimated cost than the raw classical decoder. Its classical twin matched it.</p></div><span class="energy-tag">ESTIMATE</span></div>
            <p class="caption">ATP was not measured in these animals. Choosing fewer units in a model does not turn neurons off or show that the living brain saves energy.</p>
          </section>

          <section id="limits" class="content-block takeaway-block" @mouseenter="setActive('limits')">
            <p class="eyebrow"><span class="section-number">07</span> THE TAKEAWAY</p>
            <h2>What we learned<br /><em>and what comes next.</em></h2>
            <div class="takeaway-grid">
              <div><span class="takeaway-icon">✓</span><b>Supported by this analysis</b><p>Post-flash recordings carried decodable information about flash polarity. Some regional activity improved prediction of other regions.</p></div>
              <div><span class="takeaway-icon muted">↗</span><b>Still to be tested</b><p>Quantum coherence, working memory, causal routing, and biological energy savings require different measurements and larger studies.</p></div>
            </div>
            <p class="closing-line">A compact model can be useful. Its classical equivalent must be part of the comparison.</p>
          </section>
        </div>
      </section>

      <section id="poster" class="poster-section">
        <div class="poster-copy"><p class="eyebrow">THE FULL RESEARCH POSTER</p><h2>See the complete<br /><em>V8 poster.</em></h2><p>Open the A0 poster PDF to explore the figures, methods, and full summary in one place.</p><a class="btn-main" :href="posterUrl" target="_blank" rel="noreferrer">Open poster PDF <span>↗</span></a><small>PDF · A0 portrait · 3.1 MB</small></div>
        <a class="poster-preview" :href="posterUrl" target="_blank" rel="noreferrer" aria-label="Open poster PDF">
          <div class="poster-paper"><div class="poster-mini-head"><span>Brain Energy · V8</span><i>RESEARCH POSTER</i></div><h3>Real neural activity,<br /><em>new mathematical views.</em></h3><p>Yashine · Lea · Craddock</p><div class="mini-figure"><span></span><span></span><span></span><span></span></div><div class="mini-columns"><i></i><i></i><i></i></div><div class="mini-qr">QR<br />CODE</div></div>
          <span class="preview-label">A0 PORTRAIT <b>↗</b></span>
        </a>
      </section>

      <section class="next-links">
        <div><p class="eyebrow">EXPLORE MORE</p><h2>Part of a wider<br /><em>research journey.</em></h2></div>
        <a href="https://github.com/neurobiol/welcome/tree/main" target="_blank" rel="noreferrer"><span class="link-index">01</span><b>Research welcome page</b><small>More projects and research notes</small><i>↗</i></a>
        <a href="https://github.com/neurobiol/unlearn" target="_blank" rel="noreferrer"><span class="link-index">02</span><b>Unlearn project</b><small>An example of the project-site format</small><i>↗</i></a>
      </section>
    </main>

    <footer><a class="brand" href="#top"><span class="brand-mark"><span></span><span></span><span></span></span><span>Brain Energy <i>/ V8</i></span></a><p>Department of Biology · University of Waterloo</p><span>EXPLORATORY RESEARCH · 2026</span></footer>
  </div>
</template>
