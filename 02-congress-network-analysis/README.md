# Congressional Twitter Network Analysis

Graph theory and social network analysis applied to the Congressional Twitter Network — a directed, weighted graph of 475 U.S. Congress members where each edge encodes the estimated probability that one member's tweet will be retweeted by another. Custom graph algorithms are implemented from scratch in Problem 2; NetworkX is used for full-scale analysis in Problem 3.

---

## Dataset

- **Source:** [Congressional Twitter Network](https://github.com/bill10/congress-twitter)
- **Nodes:** 475 U.S. Congress members (House + Senate) with Twitter accounts
- **Edges:** 13,289 directed, weighted edges
- **Edge weights:** Estimated retweeting probability (influence strength) between member pairs
- **Secondary dataset:** Facebook social network (4,039 nodes, 88,234 edges) — used as the test graph for all Problem 2 algorithm implementations

---

## Key Findings

- **Leadership dominates centrality rankings:** Members appearing in multiple top-10 centrality lists tend to be high-profile figures — party leadership, senators with large national followings, and members who bridge partisan divides. This aligns with pre-analysis expectations that institutional influence on Twitter mirrors institutional influence in Congress.

- **Closeness, eigenvector, and PageRank centrality agree substantially:** These three measures show significant overlap in their top-10 lists because all three reward global network position. A member with short average paths to all others is also likely connected to other well-connected members, producing correlated rankings.

- **Clustering coefficient is the most distinct measure:** High clustering coefficient identifies members embedded in tight-knit local groups (party or committee clusters), not necessarily those with global reach. Its top-10 list overlaps minimally with the other four centrality measures.

- **Approximate power-law degree distribution:** The log-log degree distribution shows a roughly linear trend with a negative slope (gamma ~ -2 to -3), consistent with scale-free-like behavior driven by preferential attachment dynamics. Deviations in the tail are expected given the network's small, fixed membership of 475 nodes.

- **Small-world structure confirmed:** Short average path lengths combined with high local clustering are consistent with the small-world property. The strong institutional structure of Congress (shared committees, party affiliation, joint legislation) creates dense local clusters while maintaining short paths across the full network.

---

## Custom Graph Functions (Problem 2)

All functions below were implemented from scratch without using NetworkX equivalents. Tested on the Facebook social network dataset.

| Function | Description |
|---|---|
| `count_node(edges)` | Count unique nodes from an edge list |
| `vertex_degree(edges, vertex)` | Degree of a specific vertex |
| `adjacency_matrix(edges)` | Build adjacency matrix as NumPy array |
| `degree_distribution(edges)` | Degree distribution as a frequency list |
| `degree_probability(dist, degree)` | P(degree >= k) for a given k |
| `eccentricity(vertex, edges)` | Max shortest path length from a vertex |
| `diameter(edges)` | Maximum eccentricity over all nodes |
| `radius(edges)` | Minimum eccentricity over all nodes |
| `clustering_coefficient(vertex, edges)` | Local clustering coefficient |
| `betweenness_centrality(vertex, edges)` | Fraction of shortest paths through vertex |
| `closeness_centrality(vertex, edges)` | Reciprocal of avg shortest path length |
| `eigenvector_centrality(adj_matrix, max_iter)` | Power iteration with L2 normalization |

---

## Tech Stack

- Python 3
- NumPy
- NetworkX
- Matplotlib
- JupyterLab

---

## How to Run

```bash
# 1. Clone the repo
git clone https://github.com/<your-username>/data-mining-projects.git
cd data-mining-projects/02-congress-network-analysis

# 2. Install dependencies
pip install -r requirements.txt

# 3. Launch the notebook
jupyter lab notebook.ipynb
```

The notebook reads all data from the `data/` directory and saves figures to `figures/`. Both directories are included in the repo.

---

## Project Structure

```
02-congress-network-analysis/
├── notebook.ipynb              # Main analysis notebook
├── requirements.txt
├── data/
│   ├── congress_network_data.json   # Node list and metadata
│   ├── congress.edgelist            # Weighted directed edge list
│   └── facebook_combined.txt        # Facebook graph (test dataset)
└── figures/
    ├── graph_visualization.png
    └── degree_distribution.png
```
