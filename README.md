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

*In plain terms: I took decades of public stream-sediment and mine-site data and built a northeastern Washington screen for gold and rare-earth placers, then checked whether the score survives a data audit, whether it works on other belts, and whether any site would pay at a rare-earth price benchmark.*

A config-driven mineral exploration workflow for co-placer rare earth element and gold potential. The published product is a northeastern Washington lookalike model, served as a live API, and a transfer test. California is a separate walk list: a public pin map for the Sierra, plus belt screens in the repo.

The pipeline integrates:

- NURE stream-sediment geochemistry
- USGS MRDS mineral occurrences
- lithology and catchment geology
- LiDAR-derived terrain on the California walk list
- mine-waste geochemistry
- REE and Au-pathfinder geochemistry
- acid-base accounting
- techno-economic assumptions

Aeromagnetics were scored in an early rank and then excluded as synthetic.

The analysis is structured around a source, pathway, trap, preservation mineral-systems framework.

Key components include:

- Random Forest prospectivity classification with MRDS-proximity labels
- shuffled 5-fold ROC-AUC of 0.891 on the unvalidated extract
- CIM audit: 287 of 1,045 NURE samples kept; validated scores 0.66 shuffled and 0.58 on spatial blocks; sample submitter alone scores 0.57
- transfer test of the frozen Washington model: Idaho 0.50, California 0.52, Montana 0.34, Colorado 0.56, North Carolina Fall Zone 0.50
- 2,000-sample Monte Carlo uncertainty analysis, P10 / P50 / P90 endowment estimates, break-even NdPr pricing, and tornado-style sensitivity analysis
- Bossburg is the only site under the $109/kg NdPr benchmark, and its coordinate is unverified
- environmental screening that flags Big Iron, Silver Bell, and Turk as acid-generating
- pytest and GitHub Actions CI
- live Washington lookalike API: [placer-lookalike.onrender.com/docs](https://placer-lookalike.onrender.com/docs)
- California pin map: [ca-placer-pins](https://nmaikin27.users.earthengine.app/view/ca-placer-pins)

The goal is to connect geological evidence to model probability, uncertainty, and economics, and to report the score that survives validation.

[View repository](https://github.com/nicole-m-aikin/au-ree-placer-pipeline)

### Critical Minerals ASTER

*In plain terms: a satellite measures how rock at the surface emits thermal infrared light. This project tests whether those patterns line up with known critical-mineral deposits, or only with the host rock and the places already mapped. Where a hyperspectral flight exists, a second sensor checks for clay alteration. The statistics are built to catch a false match.*

A remote sensing pipeline testing whether ASTER thermal infrared signals correspond with known critical mineral occurrences, covering 109 USGS Earth MRI districts. The current input is daytime AST_05 surface emissivity. GEMx AVIRIS supplies a SWIR clay check on the districts a flight actually covered.

The workflow validates those signals against USGS MRDS deposit records. The primary null is bedrock-versus-cover, because an earlier radiance-ratio result tracked acquisition temperature. A geometric null is reported beside it. Benjamini-Hochberg FDR correction covers a binomial test and a threshold-free continuous-score test, with DBSCAN spatial declustering of MRDS records and a classification-threshold sensitivity sweep.

Key features include:

- automated ASTER processing across 109 sites, 58 of them added in a pre-registered expansion with a written detectability expectation recorded before the imagery was processed
- bedrock/cover-stratified null, with the geometric null reported alongside, and Benjamini-Hochberg FDR correction across the test family
- DBSCAN spatial declustering of correlated MRDS records
- classification-threshold sensitivity sweep
- deposit-type comparison, including pre-registered nulls for epithermal, Carlin-type, and uranium
- YAML-driven site configuration
- DuckDB outputs and a zero-credential demo mode
- automated tests and GitHub Actions CI

Current thermal results: 19 of 108 sites are FDR-significant on the primary binomial test (23 under the geometric null). Three sites replicate on declustering, night imagery, and a multi-year mean: Courtland-Gleeson, Pioche, and Providence Mountains. Only Providence Mountains also survives a finer lithology null; Courtland-Gleeson and Pioche repeat the carbonate host package. Fourteen of 28 skarn and carbonate-replacement districts are significant, and that category's enrichment interval reaches 1.0 (1.44×, 1.00–1.63). Pre-registered nulls held for epithermal (0/4), Carlin-type (0/6), and uranium (0/9). Humid skarn controls are untestable after vegetation masking. Discovery-era cohorts are enriched by similar amounts (pre-1950 1.39×, post-1950 1.32×).

The SWIR check is a second result, not a replacement. On the 19 FDR sites, 14 are complementary to the thermal zones and none overlap. On the 40-site equal-area census, the SWIR hit rate is 30.4% and the thermal hit rate is 21.2% at the same map area, and the thermal map is nearer at 25 of 40 sites. SWIR coverage is 71 of 109 districts; 38 have none.

The question behind the project hasn't changed: is the signal detecting geology, or the places people already looked? Thermal infrared works as a host-rock screen. SWIR does the clay check where GEMx flew. Together they are a two-sensor screen, not one ore detector.

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

Static reproducibility checks pass on the private research repository. End-to-end scientific reproduction against the original dataset is still in progress, pending recovery of the original raw maps, masks, and dated-spot tables. Several method choices, including normalization approach, retained PCA variance, and cluster count, remain open pending controlled comparison against held-out grains. Numbers reported in earlier drafts are being reconciled against this audit rather than restated here.

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
