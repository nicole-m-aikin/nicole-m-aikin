# Hi, I'm Nicole Aikin 👋

I'm a geoscientist and applied ML practitioner working at the intersection of **mineral systems, geochemistry, geochronology, remote sensing, and scientific computing**.

My background spans **U-Th-Pb geochronology, metamorphic petrology, environmental consulting, mineral exploration data, and applied machine learning**. I build reproducible workflows that turn messy, spatially structured Earth data into defensible geological interpretations and exploration decisions.

What interests me most is the layer between **geoscience, data, and action**:

* Is a model learning real geology or historical exploration bias?
* Are labels and features scientifically independent?
* How sensitive is a target to thresholds, assumptions, or sparse data?
* What additional observation would most reduce uncertainty?
* Does a geological signal remain compelling once economic and operational constraints are included?

I tend to approach ML as **one line of evidence inside a geological decision framework**, not as a substitute for domain reasoning.

## Featured Projects

### Au + REE Placer Assessment Pipeline

A config-driven, 10-module mineral exploration workflow for evaluating **co-placer rare earth element and gold potential in northeastern Washington**.

The pipeline integrates:

* NURE stream-sediment geochemistry
* USGS MRDS mineral occurrences
* aeromagnetics
* lithology and spatial geology
* LiDAR-derived terrain information
* mine-waste geochemistry
* REE and Au-pathfinder geochemistry
* acid-base accounting
* techno-economic assumptions

The analysis is structured around a **source → pathway → trap → preservation** mineral-systems framework.

Key components include:

* Random Forest prospectivity classification
* anti-leakage label design using independent MRDS proximity
* 5-fold stratified cross-validation
* ROC-AUC of **0.891**
* 2,000-sample Monte Carlo uncertainty analysis
* P10 / P50 / P90 endowment estimates
* break-even NdPr pricing
* NPV screening
* tornado-style sensitivity analysis
* multi-criterion target ranking
* environmental risk screening
* pytest unit tests and GitHub Actions CI

The goal is not just to identify anomalous ground, but to connect:

**geological evidence → model probability → uncertainty → economics → field prioritization**

[View repository](https://github.com/nicole-m-aikin/au-ree-placer-pipeline)

---

### Critical Minerals ASTER

A remote-sensing pipeline evaluating whether **ASTER thermal infrared alteration signals** correspond with known critical-mineral occurrences across **45 USGS Earth MRI sites**.

The workflow compares satellite-derived spectral anomalies against more than **30,000 USGS MRDS records** and explicitly tests where the method succeeds, fails, or becomes biased.

Key features include:

* automated ASTER processing across multiple sites
* alteration-index calculation and normalization
* spatial validation against mineral occurrences
* statistical significance testing
* Wilson score confidence intervals
* threshold-perturbation sensitivity
* discovery-bias controls
* deposit-type performance comparison
* YAML-driven site configuration
* DuckDB outputs
* automated tests and reproducible batch workflows

One of the main findings is that ASTER TIR behaves more like a **deposit-type-sensitive screening tool** than a universal mineral detector, with stronger performance in some skarn, carbonate-hosted, and arid porphyry systems than in sediment-hosted, placer, or heavily vegetated settings.

The broader question behind the project is simple:

**Is the remote-sensing signal detecting geology, or merely where people historically explored?**

[View repository](https://github.com/nicole-m-aikin/critical-minerals-aster)

---

### RockClock

A graduate research pipeline for identifying chemically distinct mineral-growth domains from large electron microprobe datasets.

RockClock converts high-dimensional geochemical maps into pixel-scale feature vectors, applies dimensionality reduction and unsupervised clustering, and maps those results back into spatially coherent mineral domains.

Methods include:

* PCA
* K-means clustering
* Gaussian Mixture Models
* automated domain classification
* spatial reconstruction of mineral chemistry

The pipeline was developed for **U-Th-Pb geochronology and metamorphic petrology**, where subtle chemical zoning can preserve distinct episodes of mineral growth, deformation, metamorphism, melt interaction, or fluid activity.

Across more than **100,000 analytical points**, the workflow achieved approximately **98% classification accuracy** relative to expert-defined domains.

RockClock is currently private because it is tied to collaborative research.

---

### ML Geo Pixel Poppers

An earlier supervised-learning project using multi-element chemical maps to classify mineral phases.

The workflow included:

* manual training labels
* feature engineering
* PCA
* Random Forest classification
* hyperparameter tuning
* spatial reconstruction of predicted mineral classes

The project achieved roughly **96%+ accuracy for garnet** and about **80% for biotite**, with the performance difference reflecting real compositional overlap and geological complexity rather than simply a modeling limitation.

This project was one of my first demonstrations that domain knowledge can matter as much as model complexity in scientific ML.

[View repository](https://github.com/nicole-m-aikin/ML-Geo-Pixel-Poppers)

## Scientific Background

My graduate research focused on **U-Th-Pb geochronology, metamorphic petrology, geochemistry, and tectonics**.

I worked with mineral-scale analytical datasets to reconstruct geological histories from chemical zoning, age populations, metamorphic reactions, deformation fabrics, and melt-related processes.

Before graduate school, I spent two years in environmental and remediation consulting, where I managed technical work across multiple concurrent projects and served as a primary liaison with agencies including the EPA, California DTSC, RWQCB, and BAAQMD.

That combination of analytical science, software, and stakeholder-facing work is what now drives my interest in **applied geoscience for mineral exploration, critical minerals, remote sensing, and industrial AI**.

## How I Work

I care about:

* scientifically meaningful labels
* leakage prevention
* uncertainty quantification
* reproducibility
* interpretable models
* physically defensible feature engineering
* spatial context
* explicit assumptions
* honest failure modes
* decision relevance

I am especially interested in problems involving:

**legacy geoscience data · mineral systems · critical minerals · remote sensing · exploration targeting · geochemistry · geochronology · scientific ML · uncertainty · technical deployment**

## Tools

**Languages & Data**

Python · pandas · NumPy · SciPy · scikit-learn · DuckDB · SQL

**Geospatial**

GeoPandas · Rasterio · Shapely · GDAL · ArcGIS / GIS workflows · remote sensing

**ML & Statistics**

Random Forest · PCA · K-means · Gaussian Mixture Models · cross-validation · Monte Carlo simulation · sensitivity analysis · uncertainty quantification

**Software Practices**

pytest · GitHub Actions · configuration-driven pipelines · modular scientific software · reproducible workflows

## Currently Exploring

I'm particularly interested in work where **geoscience, applied ML, and technical translation overlap**, including:

* mineral exploration and critical-minerals technology
* geospatial and remote-sensing platforms
* scientific AI for physical systems
* exploration decision support
* multimodal Earth-data integration
* technical deployment and customer-facing scientific roles
* uncertainty-aware targeting and resource screening

## Contact

[LinkedIn](https://www.linkedin.com/in/nicole-m-aikin/)
[GitHub](https://github.com/nicole-m-aikin)


