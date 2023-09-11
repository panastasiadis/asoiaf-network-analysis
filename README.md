# An In-Depth Network Analysis of Character Interactions in the 'A Song of Ice and Fire' Book Series

This repository contains an analysis of the "A Song of Ice and Fire" dataset, representing a fictional social network from George R. R. Martin's book series. The analysis covers various aspects of the network.

The dataset "A Song of Ice and Fire" is sourced from http://konect.cc/networks/asoiaf and https://github.com/mathbeveridge/asoiaf.

## Overview

The analysis begins by importing necessary libraries and loading the dataset, which includes character interactions and character information.

## Data Preparation

1. **Data Cleaning**: Unnecessary columns are removed from the dataset.

2. **Indexing**: Integer IDs are added to characters and edges for efficient processing.

3. **Data Export**: Cleaned data is exported as CSV files for future use.

## Network Visualization

A visualization of the social network is created using NetworkX and Matplotlib.

## Stage 1.1: Analyzing the Real Network

### Degree Distribution

- Key character interactions and their degrees are analyzed.

### Connectivity

- The network's connectivity is checked.

### Centralities

- Various centrality measures (degree, weighted degree, betweenness, closeness, eigenvector centrality) are calculated and analyzed to identify influential characters.

### Eccentricity

- The radius and diameter of the network are computed, revealing its tight connectivity.

### Cliques

- Cliques within the network are identified and analyzed.

### Other Metrics

- Metrics such as triangles, minimum node cut, minimum edge cut, clustering coefficients, average clustering, transitivity, and density are calculated to understand network characteristics.

## Stage 1.2: Generating a Synthetic Network

A synthetic network is generated using the Barabasi-Albert model to mimic the characteristics of the real network. This is done to compare key metrics between the real and synthetic networks.

### Data Preparation

- A subgraph is extracted from the real network for initializing the Barabasi-Albert model.

### Network Generation

- A random network is generated using the Barabasi-Albert algorithm.

### Comparison

- Key metrics of the synthetic network are compared to the real network.

## Stage 2: Link Prediction Using Adamic-Adar Index

In this stage, a link prediction algorithm (Adamic-Adar) is implemented on both the synthetic and real networks. The algorithm's performance is evaluated using k-fold cross-validation.

### Import Necessary Libraries

- Libraries like scikit-learn for cross-validation and metrics, NumPy, and statistics are imported.

### Calculate Complement Graphs

- Complement graphs are calculated for both the real and synthetic networks.

### Calculate Adamic-Adar Index Values

- Adamic-Adar index values are computed for both edges and non-edges in the real graph. Metrics such as mean, standard deviation, maximum, and minimum values are examined.

### Visualization

- The distribution of Adamic-Adar values for existing edges and non-existing edges is plotted.

### Identify High Adamic-Adar Index Values

- Character pairs corresponding to non-edges in the graph with Adamic-Adar index values greater than 4.5 are identified and counted. The list of edges satisfying this condition is displayed.

### Explore Character Pairs

- Character pairs corresponding to high Adamic-Adar index values are examined. An example is provided to understand the significance of the Adamic-Adar index in capturing specific relationships between characters.

### Test Algorithm on Real and Synthetic Graphs

- The Adamic-Adar index is calculated for both edges and non-edges in the Barabasi-Albert graph, and the algorithm's performance is tested on both the real and synthetic networks.

### Evaluate with Logistic Regression

- Logistic regression is used for a 5-fold cross-validation evaluation of the link prediction algorithm, calculating accuracy, precision, recall, and displaying confusion matrices.

### Further Tests and Evaluations

- Additional tests are conducted to evaluate the model's performance when trained on one network and tested on another, providing insights into the model's ability to capture graph characteristics and similarities.

The Adamic-Adar index serves as a valuable metric for capturing nuanced relationships within the social network, as demonstrated in the analysis. The evaluation results shed light on the algorithm's performance in predicting connections in both real and synthetic networks, offering insights into the effectiveness of the link prediction approach.

## Stage 3: Simulating Influence Spreading and Identifying K-Seeds

In this stage, we simulate influence spreading on the graph by selecting k-seeds to maximize influence and defining parameters to determine the optimal number of k-seeds and parameter values that achieve 60% network influence.

We will use the Independent Cascade model for this task, which assumes that each node in the network can independently activate its neighboring nodes with a certain probability.

### Import Necessary Libraries

- Libraries like `ndlib.models`, `ModelConfig`, `epidemics`, and `matplotlib.pyplot` are imported to perform influence spreading simulations.

### Subgraph Selection

To achieve the desired influence spreading of 60% in the network, we first create a subgraph that includes important key characters with a weighted degree greater than 150. We use the weighted degree as a criterion for selecting characters. 

By analyzing the weight distribution of the nodes in the subgraph, we determine that adding a value of 0.3 to the weight ratio as the probability of influence along the edges is appropriate.

### Greedy Search for the Best K-Seeds

We implement a greedy search algorithm to find the best k-seeds for influence spreading. The function `get_maximum_influence_across_iterations` calculates the maximum influence achieved across multiple iterations in a given model. The function `get_best_candidate` determines the best candidate node from a set of candidates by evaluating their potential influence.

### Determine Optimal K-Seeds

We determine the optimal k-seeds for the subgraph by incrementally increasing the value of k. In the testing cell, we empirically find that a minimum of k=25 seeds is required to achieve a 60% network influence with the given fixed probability.

### Evaluate Model

We evaluate the model's performance using the selected k-seeds and determine whether we are able to influence 60% of the network through the iterations of the model. Visualization of the diffusion trend is also presented.

## Stage 4: Community Detection

In this stage, our goal is to identify and uncover the communities within the graph that correspond to specific storylines in the book series. This analysis may also help us discover the locations where these plot lines take place.

### Community Detection Algorithm

We utilize the Girvan-Newman community detection algorithm, which iteratively removes edges with high betweenness centrality to identify and separate communities within the network.

### Cluster Identification

We identify and map the produced clusters with different colors and visualize the network with the identified clusters.

### Protagonist Node for Each Community

We identify key protagonist nodes for each community based on their weighted degree within the community. The nodes with the highest weighted degrees are considered as the main characters of each community.

These analyses help us uncover the storylines and character interactions within the "A Song of Ice and Fire" network, shedding light on the connections and plotlines within the series.
