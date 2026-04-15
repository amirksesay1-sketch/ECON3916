

Clustering World Economies with K-Means & PCA
Objective: Applied unsupervised machine learning to classify ~160 national economies by multidimensional development profile, revealing that algorithmic clustering on diverse socioeconomic indicators substantially — but imperfectly — recovers the World Bank's expert-driven income classifications.
Methodology

Sourced 10 World Development Indicators via the wbgapi API spanning income, health, education, inequality, environment, connectivity, trade, labor markets, and urbanization
Applied StandardScaler prior to clustering to normalize feature scales, preventing high-variance indicators like GDP per capita from dominating Euclidean distance calculations
Fit K-Means (K=4, k-means++ initialization) to align with the World Bank's four canonical income tiers; projected results to 2D via PCA for visual interpretation
Evaluated cluster quality across K=2–10 using the elbow method (WCSS/inertia) and mean silhouette score to assess within-cluster cohesion and between-cluster separation
Cross-tabulated algorithmic cluster assignments against official World Bank income group labels to quantify alignment and surface meaningful divergences
Extended the full pipeline to 20,640 California census tracts (California Housing dataset), clustering by housing stock, demographics, and geography to recover regionally interpretable economic segments

Key Findings

K=4 is economically justified: While silhouette scores peak at K=2–3, K=4 produces the most interpretable structure, with clusters mapping to recognizable development tiers — high-income industrialized economies, upper-middle emerging markets, lower-middle developing nations, and low-income fragile states
High and Low income groups cluster cleanly; the middle is messier: Wealthy and very poor nations are most consistently separated, while Lower-Middle and Upper-Middle income countries show meaningful overlap — reflecting that the World Bank's GNI thresholds are somewhat arbitrary boundaries on a continuous development spectrum
Mismatches are analytically informative: Countries that the algorithm places in a different cluster than their World Bank tier often exhibit structural anomalies — unusually high inequality, commodity dependence, or atypical health outcomes — flagging them as candidates for deeper policy analysis
California Housing replicates the pattern: K=4 segments California census tracts into four economically coherent groups — affluent coastal suburbs, Bay Area middle-class urban tracts, LA Metro dense neighborhoods, and inland/rural lower-income communities — demonstrating that the pipeline generalizes across scales from nations to neighborhoods
