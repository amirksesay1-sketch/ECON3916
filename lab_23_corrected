FedSpeak Analysis — NLP on FOMC Minutes
Objective: Applied natural language processing to two decades of Federal Reserve meeting minutes to quantify shifts in monetary policy sentiment, identify distinct communication regimes, and measure how the Fed's language responded to major macroeconomic shocks.
Methodology

Loaded FOMC meeting minutes corpus via HuggingFace datasets and engineered a preprocessing pipeline: lowercasing, non-alphabetic character removal, NLTK tokenization, stop word filtering, and WordNet lemmatization
Constructed a TF-IDF document-term matrix with unigram and bigram features, applying frequency thresholds (min_df, max_df) to suppress both rare noise terms and ubiquitous background vocabulary
Scored each document using a Loughran-McDonald financial sentiment lexicon, computing net sentiment (positive minus negative word share) and an uncertainty ratio — both normalized by document length to ensure comparability across meetings of varying length
Plotted sentiment and uncertainty time series with 12-month rolling averages and annotated key policy events: Lehman Brothers collapse, the 2013 taper tantrum, COVID-19 emergency easing, and the 2022 tightening cycle
Applied TruncatedSVD for dimensionality reduction on the sparse TF-IDF matrix, then fit K-Means (K=3) to identify latent language regimes; validated with silhouette scoring and 2D PCA scatter plots
Segmented the corpus at March 2020 and compared pre- vs post-COVID sentiment distributions using overlaid KDE plots and box plots

Key Findings

Three distinct language regimes emerged from clustering, broadly corresponding to the pre-crisis expansion era, the unconventional policy period (2008–2015, dominated by vocabulary around balance sheet expansion and forward guidance), and the post-COVID tightening cycle (2021–present, characterized by inflation and supply-side terminology) — demonstrating that shifts in Fed language are structurally detectable without any date labels
Post-COVID minutes are measurably more negative and more uncertain than the pre-2020 baseline, reflecting the Fed navigating simultaneous and historically unusual challenges: pandemic-driven contraction, fiscal stimulus overhang, supply chain disruption, and the sharpest rate tightening cycle since Volcker
Sentiment troughs align with identifiable crisis moments — the most negative documents cluster around the 2008–2009 financial crisis and the March–April 2020 COVID shock — validating that the LM lexicon captures genuine economic distress rather than statistical noise
Uncertainty scores are structurally elevated post-2020, consistent with a period in which the Fed's own forward guidance repeatedly required revision, and in which the neutral rate, inflation persistence, and labor market slack were all simultaneously contested empirical questions
