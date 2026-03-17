# SNA_project

⸻
Social Network Analysis of Political Interaction on Reddit

This project investigates the structure, dynamics, and polarization of political discussions on Reddit using tools from Network Science.

The analysis combines data collection, network construction, and multi-level metrics (global, mesoscopic, and temporal), with a particular focus on echo chambers and ideological segregation.

⸻


Note on Crawling Time Windows

The notebook Crawling_network.ipynb includes example time windows, which may appear arbitrary.

In reality, the crawling process was systematically repeated across multiple time windows, as defined and discussed in the accompanying report.

This choice ensures:
	•	reproducibility of the pipeline
	•	flexibility in experimenting with different temporal slices
	•	consistency with a dynamic network analysis framework

⸻

Pipeline Overview

1. Data Collection

Data is collected from Reddit using the PRAW API.

Two types of data are extracted:
	•	Home communities → used to infer users’ ideological alignment
	•	Arena interactions → used to capture cross-community behavior

Each comment includes:
	•	author
	•	subreddit
	•	timestamp (created_utc, day)
	•	thread structure (link_id, parent_id)
	•	score and metadata

⸻

2. User Labeling

Users are assigned a home_label based on their activity in political subreddits.

This produces a mapping:

user → ideological group

This step is fundamental for:
	•	polarization analysis
	•	assortativity computation
	•	validation of community structure

⸻

3. Data Integration

All datasets are merged into:

combined_dynamic.csv

This dataset includes:
	•	temporal information
	•	interaction structure (reply chains)
	•	ideological labels

It represents the core dataset for network construction.

⸻

4. Network Construction

Graphs are built at two levels:

Static Network
	•	Used for global structural analysis

Dynamic Networks (Daily)
	•	One graph per day (.gexf)
	•	Enables temporal analysis of network evolution

Edges represent interactions between users (e.g., replies).

⸻

5. Network Analysis

The project computes key network metrics:

Global Metrics
	•	Density
	•	Clustering coefficient
	•	Average path length
	•	Diameter

Centrality
	•	Degree centrality
	•	Betweenness centrality

Assortativity
	•	By ideology (home_label)
	•	By degree

⸻

6. Model Comparison

The real network is compared with two theoretical models:
	•	Erdős–Rényi (ER) → random graph baseline
	•	Barabási–Albert (BA) → scale-free model

This allows us to assess whether the observed network structure is:
	•	random
	•	scale-free
	•	small-world

⸻

7. Community and Polarization Analysis

Instead of detecting communities, the project validates ideological groups as communities.

Metrics used:
	•	Modularity
	•	Measures how strongly groups are separated globally
	•	Conductance
	•	Measures how well each group is internally connected vs externally linked

These metrics are key to identifying echo chambers.

⸻

8. Temporal Analysis

Using daily graphs, the project tracks:
	•	Evolution of modularity over time
	•	Changes in conductance
	•	Dynamics of ideological segregation

This enables a dynamic view of polarization.

⸻

Research Questions
	•	Do ideological groups form well-separated communities?
	•	How does polarization evolve over time?
	•	Are interactions mostly within-group or cross-group?

⸻
 Technologies Used
	•	Python
	•	NetworkX
	•	Pandas
	•	NumPy
	•	Matplotlib
	•	PRAW (Reddit API)

⸻
 How to Run
	1.	Set your Reddit API credentials:

os.environ["REDDIT_CLIENT_ID"] = "your_id"
os.environ["REDDIT_CLIENT_SECRET"] = "your_secret"

	2.	Run notebooks in order:

	•	Crawling_network.ipynb
	•	network_analysis.ipynb
    •	daily_graphs.ipynb

	3.	Outputs will be generated automatically (CSV + GEXF files)

⸻

Outputs
	•	network_report.csv
→ Global network metrics and comparison with ER/BA models
	•	home_label_metrics_daily.csv
→ Temporal evolution of modularity and conductance
	•	daily_graphs/*.gexf
→ Daily network snapshots

⸻

Final Remarks

This project follows a data-driven network science approach to analyze online political interaction.

By combining:
	•	structural analysis
	•	temporal dynamics
	•	theoretical benchmarks


⸻

Author

Giuliano Gelsomino
Data Science / Social Network Analysis Project

