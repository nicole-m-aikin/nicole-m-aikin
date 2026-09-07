## Hi, I'm Nicole Aikin 👋

I'm a geoscientist and applied ML practitioner working at the intersection of mineral systems, geochemistry, geochronology, remote sensing, and scientific computing.

My background spans U-Th-Pb geochronology, metamorphic petrology, environmental consulting, mineral exploration data, and applied machine learning. I build reproducible workflows that turn messy, spatially structured Earth data into defensible geological interpretations and exploration decisions.

What interests me most is the layer between geoscience, data, and action:

- Is a model learning real geology or historical exploration bias?
- Are labels and features scientifically independent?
- How sensitive is a target to thresholds, assumptions, or sparse data?
- What additional observation would most reduce uncertainty?
- Does a geological signal remain compelling once economic and operational constraints are included?

I tend to approach ML as one line of evidence inside a geological decision framework, not a substitute for domain reasoning.

## Featured Projects

### Au + REE Placer Assessment Pipeline

*In plain terms: I took decades of public government data on rocks, streams, and old mine sites and built a tool that ranks the most promising places to look for gold and rare earth elements in northeastern Washington, then checks whether mining any of them would actually pay off.*

A config-driven, 10-module mineral exploration workflow for evaluating co-placer rare earth element and gold potential in northeastern Washington.

The pipeline integrates:

- NURE stream-sediment geochemistry
- USGS MRDS mineral occurrences
- aeromagnetics
- lithology and spatial geology
- LiDAR-derived terrain information
- mine-waste geochemistry
- REE and Au-pathfinder geochemistry
- acid-base accounting
- techno-economic assumptions

The analysis is structured around a source, pathway, trap, preservation mineral-systems framework.

Key components include:

- Random Forest prospectivity classification
- anti-leakage label design using independent MRDS proximity
- 5-fold stratified cross-validation
- ROC-AUC of 0.891
- 2,000-sample Monte Carlo uncertainty analysis
- P10 / P50 / P90 endowment estimates
- break-even NdPr pricing
- NPV screening
- tornado-style sensitivity analysis
- multi-criterion target ranking
- environmental risk screening
- pytest unit tests and GitHub Actions CI

The goal is not to identify anomalous ground alone, but to connect geological evidence to model probability, uncertainty, economics, and field prioritization in a single traceable chain.

[View repository](https://github.com/nicole-m-aikin/au-ree-placer-pipeline)

### Critical Minerals ASTER

*In plain terms: satellites can sense heat patterns from space that hint at certain kinds of mineral deposits underground. This project tests whether that heat signal actually finds real deposits, or just re-finds the places people already explored decades ago, and it's built with statistical checks specifically designed to catch itself being fooled.*

A remote sensing pipeline testing whether ASTER thermal infrared alteration signals correspond with known critical mineral occurrences, now covering 109 USGS Earth MRI districts across the western US.

The workflow validates satellite-derived spectral anomalies against USGS MRDS deposit records under a statistical framework built to catch its own false positives: a site-specific geometric null in place of an earlier pooled-null version that manufactured significance at sites with unusually large anomaly zones, Benjamini-Hochberg FDR correction across both a binomial test and a threshold-free continuous-score test, DBSCAN spatial declustering of non-independent MRDS records, and a classification-threshold sensitivity sweep.

Key features include:

- automated ASTER processing across 109 sites, 58 of them added in a pre-registered expansion with a written detectability expectation recorded before the imagery was processed
- site-specific geometric null and Benjamini-Hochberg FDR correction across the full test family
- DBSCAN spatial declustering of correlated MRDS records
- classification-threshold sensitivity sweep
- deposit-type performance comparison across skarn, porphyry, epithermal, VMS, and placer systems
- YAML-driven site configuration
- DuckDB outputs and a zero-credential demo mode
- automated tests and reproducible batch workflows via GitHub Actions

Current results: 20 of 109 sites are FDR-significant on the primary binomial test, 31 on the continuous-score test. Thirteen sites hold up under every check, including spatial declustering, and nine of those are arid skarn or carbonate-replacement districts spanning Arizona, New Mexico, Texas, and California, pointing to a Southwest-wide detection pattern rather than one isolated belt. Skarn/carbonate-replacement is the only deposit-system category whose enrichment confidence interval excludes 1.0. A humid-terrain control of six skarn districts in Pennsylvania, New York, and Washington returns zero significant sites, consistent with a vegetation and exposure explanation for where the method fails. An earlier claim that the signal tracked historical discovery-era bias did not survive an unconditioned re-run and has been retracted: no era signal, 0.92x enrichment, p = 0.73.

The question behind the project hasn't changed: is the signal detecting geology, or the places people already looked? The current answer is that TIR functions as a deposit-type selector, not a universal detector, and the failure modes are documented as carefully as the successes.

Zero-credential demo, no EarthData account or rasters required:

```
git clone https://github.com/nicole-m-aikin/critical-minerals-aster.git
cd critical-minerals-aster && pip install -e .
python -m critical_minerals_aster demo
```

[View repository](https://github.com/nicole-m-aikin/critical-minerals-aster)

### RockClock

*In plain terms: monazite crystals record a rock's history the way tree rings record a tree's, but reading those rings by eye means two scientists can look at the same crystal and reach different conclusions. RockClock flags the different chemical "rings" inside a crystal using a documented, repeatable process, then hands the reading to a geologist to confirm rather than treating the computer's output as the final word.*

A pipeline for identifying chemically distinct domains in accessory minerals from electron microprobe (EMPA) chemical maps, developed during graduate research on U-Th-Pb monazite geochronology in a polydeformed migmatite (Grand Canyon).

As of September 2026, RockClock is undergoing a full reproducibility and provenance audit ahead of publication. The project is being reframed from a domain-classification demo into a provenance-first workflow: it proposes candidate chemical regions and phase boundaries without automatically naming minerals or geological events, and every domain, phase, and age assignment routes through geologist review rather than treating a statistical cluster as a finished interpretation.

Reproducibility infrastructure is in place and passing: deterministic notebooks, a pinned environment, automated validation, and continuous integration. End-to-end scientific reproduction against the original dataset is still in progress, pending recovery of the original raw maps, masks, and dated-spot tables. Several method choices, including normalization approach, retained PCA variance, and cluster count, remain open pending controlled comparison against held-out grains. Numbers reported in earlier drafts are being reconciled against this audit rather than restated here.

RockClock is currently private, tied to a manuscript in preparation.

### ML Geo Pixel Poppers

*In plain terms: this project teaches a computer to recognize different minerals inside a rock scan by their chemical signature, the same way you might sort fruit by color and shape, and tests how well that works when two minerals look almost identical up close.*

An earlier supervised-learning project using multi-element chemical maps to classify mineral phases.

The workflow included:

- manual training labels
- feature engineering
- PCA
- Random Forest classification
- hyperparameter tuning
- spatial reconstruction of predicted mineral classes

The project achieved roughly 96%+ accuracy for garnet and about 80% for biotite, with the performance difference reflecting real compositional overlap and geological complexity, not simply a modeling limitation.

This project was one of my first demonstrations that domain knowledge can matter as much as model complexity in scientific ML.

[View repository](https://github.com/nicole-m-aikin/ML-Geo-Pixel-Poppers)

## Scientific Background

My graduate research focused on U-Th-Pb geochronology, metamorphic petrology, geochemistry, and tectonics.

I worked with mineral-scale analytical datasets to reconstruct geological histories from chemical zoning, age populations, metamorphic reactions, deformation fabrics, and melt-related processes.

Before graduate school, I spent two years in environmental and remediation consulting, where I managed technical work across multiple concurrent projects and served as a primary liaison with agencies including the EPA, California DTSC, RWQCB, and BAAQMD.

That combination of analytical science, software, and stakeholder-facing work is what now drives my interest in applied geoscience for mineral exploration, critical minerals, remote sensing, and industrial AI.

## How I Work

I care about:

- scientifically meaningful labels
- leakage prevention
- uncertainty quantification
- reproducibility
- interpretable models
- physically defensible feature engineering
- spatial context
- explicit assumptions
- honest failure modes
- decision relevance

I am especially interested in problems involving: legacy geoscience data, mineral systems, critical minerals, remote sensing, exploration targeting, geochemistry, geochronology, scientific ML, uncertainty, technical deployment.

## Tools

**Languages & Data**
Python, pandas, NumPy, SciPy, scikit-learn, DuckDB, SQL

**Geospatial**
GeoPandas, Rasterio, Shapely, GDAL, ArcGIS / GIS workflows, remote sensing

**ML & Statistics**
Random Forest, PCA, K-means, Gaussian Mixture Models, cross-validation, Monte Carlo simulation, sensitivity analysis, uncertainty quantification

**Software Practices**
pytest, GitHub Actions, configuration-driven pipelines, modular scientific software, reproducible workflows

## Currently Exploring

I'm particularly interested in work where geoscience, applied ML, and technical translation overlap, including:

- mineral exploration and critical-minerals technology
- geospatial and remote-sensing platforms
- scientific AI for physical systems
- exploration decision support
- multimodal Earth-data integration
- technical deployment and customer-facing scientific roles
- uncertainty-aware targeting and resource screening

## Contact

LinkedIn: [linkedin.com/in/nicole-m-aikin](https://www.linkedin.com/in/nicole-m-aikin)
GitHub: [github.com/nicole-m-aikin](https://github.com/nicole-m-aikin)
