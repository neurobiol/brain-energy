# Brain Energy

**Authors:** Yashine H. Goolam Hossen, Lea Gassab, T. J. A. Craddock  
**Department of Biology, University of Waterloo**

This project asks how recorded brain activity changes after a visual flash, how activity in one brain region helps predict activity in another, and whether compact mathematical models can describe those patterns.

The website includes the A0 research poster, an explanation of every poster section, and links to the related project pages. The poster PDF is in [`public/poster/brain-energy-v8-poster.pdf`](public/poster/brain-energy-poster.pdf).

## Read the poster

[Open or download the poster PDF](poster.pdf)

## What we did

We analyzed real recordings from the Allen Institute’s Visual Coding Neuropixels dataset. Neuropixels probes record the brief electrical spikes produced by many neurons. The analysis selected three mouse recording sessions and studied responses to brief black or white visual flashes.

The recordings covered the lateral geniculate nucleus (**LGd**, a visual relay area), primary visual cortex (**VISp**, also called V1), and lateral visual cortex (**VISl**). Two sessions had usable flash-period data in all three regions. In the third, the selected V1 recordings did not overlap the flash period, so that session was used only for its two available regions. Missing V1 data were treated as unavailable, not as zero activity.

Each session contributed 150 flashes. In total, the analysis included 450 flashes and 131,080 recorded spike times. Models were trained on earlier whole trials, tuned on separate trials, and evaluated on held-out later trials. This helps test how well a model predicts data it did not fit.

## What each poster section means

### 1. The question and study design

The poster compares classical models with a quantum-like mathematical description inspired by work from Scholes and colleagues. “Quantum-like” here means that the model borrows mathematical tools such as complex amplitudes and density matrices. It does **not** mean that the experiment measured quantum coherence or quantum behavior in the brain.

The goal is to see whether this representation predicts recorded neural activity well, and how its model size and estimated costs compare with classical alternatives.

### 2. Predicting neural activity

The forecasting task asks: given recent recorded activity, how accurately can a model predict the next neural spike counts? A lower root-mean-square error (**RMSE**) means predictions are closer to the observed counts on average.

At the 100 ms forecast, the quantum-like density model had an RMSE of **0.399 spikes per bin**. Its classical complex-amplitude twin had exactly the same score, as the two formulations encode the same predictor in this analysis. Classical VAR scored **0.393**, and a stimulus-time baseline scored **0.386**. These classical baselines predicted slightly better.

The compact complex predictor used fewer fitted coefficients than the selected VAR model. This is a possible compactness-versus-accuracy tradeoff. It is not a uniquely quantum advantage, because the classical twin has the same predictions and compact dynamics.

### 3. Decoding the flash after it ended

The decoder was given neural activity from about 100 to 350 ms after the flash ended. It tried to identify whether the earlier flash was black or white. On the two sessions with complete regional coverage, the classical linear-count decoder reached **98.3% accuracy** on held-out trials. The classical latent-linear decoder reached **93.3%**, while the quantum-like density readout and its classical quadratic twin both reached **90.0%**.

This shows that information about flash polarity remained readable from activity in that time window. It does not establish working memory: ordinary visual response, rebound, or other post-stimulus activity could also carry the information. A controlled delay task is needed to test memory directly.

### 4. Directed predictability between regions

The analysis tested whether the recent activity of one recorded region improved predictions of another region after accounting for the other measured regions, recent running speed, and average flash responses. It found four exploratory region-to-region links that passed the stated shuffle and multiple-testing checks.

These links show conditional predictive timing relationships in this dataset. They do not prove that one region caused activity in another, that there is a direct synaptic connection, or that information physically travels along the inferred direction. Hidden inputs and other unmeasured factors could explain some relationships. The pattern also differed across animals.

### 5. Energy and model efficiency

The energy values use a historical ATP-based calculation based on the number of included units and their spikes. This is a **proxy estimate**, not a measurement of ATP use, oxygen consumption, or electrical power in these mice. The same cost assumptions were applied across the model comparisons.

Under this proxy, the quantum-like decoder did not have a higher information-per-cost score than the raw classical linear-count decoder. Its classical quadratic twin matched it. Selecting fewer recorded units for an analysis also does not mean that neurons were switched off or that the living brain saved energy.

### 6. Main conclusion and limits

The main result is that post-flash neural activity contains decodable information about flash polarity, and that measured activity between regions has some conditional predictive relationships. Classical models matched or outperformed the quantum-like models in predictive accuracy. The results support testing compact collective descriptions, while requiring a classical equivalent as a fair control.

This is a preliminary analysis of three mouse sessions, with only two complete three-region sessions for the primary forecasting and decoding comparison. It does not demonstrate quantum coherence, causal routing, working memory, or biological energy savings. Larger independent datasets, a controlled memory task, and direct metabolic measurements would be needed to test those claims.

## Related project pages

- [Research welcome page](https://github.com/neurobiol/welcome/tree/main)
- [Unlearn project example](https://github.com/neurobiol/unlearn)

## Run the website locally

Requirements: Node.js 20 or newer and npm.

```bash
npm install
npm run dev
```

Create a production build with `npm run build`. To preview it locally, run `npm run preview`.

## Publish with GitHub Pages

1. Create a new public repository for this project and push these files to its `main` branch.
2. In the repository settings, open **Pages** and set the source to **GitHub Actions**.
3. The included workflow builds the Vue app and publishes the `dist/` folder after pushes to `main`.

The Vite config reads the repository name from GitHub Actions so the app works from the Pages subpath. For local builds, it uses `/`.

## QR code space

The poster has a reserved QR-code area. Generate a QR code for the published GitHub Pages URL and add it to the poster source before printing if you want the printed poster to link directly to the app.

## Poster source and scientific data

The included PDF is the finalized poster. The detailed numerical methods, reproducibility files, and source recording excerpts belong in the separate V8 research archive; this small website repository is designed to remain easy to clone and publish.
