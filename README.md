# Visualizing Graphs with PyTorch Geometric (PyG): A Practical Guide

## Overview
This repository accompanies the article **"Visualizing Graphs with PyTorch Geometric (PyG): A Practical Guide"** by Mohammad Heydari. It provides practical examples for creating and visualizing graphs using PyTorch Geometric (PyG) and Pyvis.

Graph data visualization is essential for analyzing relationships in data, and PyG offers robust tools to manage and understand complex graphs efficiently.

---

## Repository Contents

### Files:
- **`simple_graph.py`:** Demonstrates how to create and visualize a small graph.
- **`large_graph.py`:** Showcases the generation and visualization of large-scale graphs.
- **`requirements.txt`:** Contains the Python dependencies needed for the project.

---

## Features
- **Graph Representation:** Define graphs with nodes, edges, and features to represent complex structures.
- **Interactive Visualization:** Use Pyvis for creating interactive graph visualizations.
- **Scalability:** Support for creating and visualizing large-scale graphs.
- **Customization:** Customize graphs with labels, colors, and sizes for better insights.

---

## Getting Started

### Prerequisites
- Python 3.8 or higher
- Pip installed on your machine

### Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/pytorch-graph-visualization.git
   cd pytorch-graph-visualization
   ```

2. Install the dependencies:
   ```bash
   pip install -r requirements.txt
   ```

---

## Running the Examples

### Visualizing a Simple Graph
1. Run the `simple_graph.py` script:
   
   ```bash
   python simple_graph.py
   ```
3. The visualization will be saved as `graph.html` and can be opened in your browser.

### Visualizing a Large Graph
1. Run the `large_graph.py` script:
   
   ```bash
   python large_graph.py
   ```
3. The visualization will be saved as `large_graph.html` and can be opened in your browser.

---

## Example Code

### Simple Graph (`simple_graph.py`)
```python
import torch
from torch_geometric.data import Data
from pyvis.network import Network

# Define edges (connections between nodes)
edge_index = torch.tensor([[0, 1, 1, 2], [1, 0, 2, 1]], dtype=torch.long)

# Node features
x = torch.tensor([[1], [2], [3]], dtype=torch.float)

# Create the graph
data = Data(x=x, edge_index=edge_index)

# Visualize the graph
def visualize_graph(data, filename="graph.html"):
    net = Network(notebook=False)

    # Add nodes
    for i in range(data.x.size(0)):
        net.add_node(i, label=f"Node {i}")

    # Add edges
    edges = data.edge_index.t().tolist()
    for edge in edges:
        net.add_edge(edge[0], edge[1])

    # Save and display the graph
    net.show(filename)

visualize_graph(data)
```

### Large Graph (`large_graph.py`)
```python
import torch
from torch_geometric.data import Data
from pyvis.network import Network
import random

# Create a large graph
num_nodes = 1000  # Number of nodes
num_edges = 5000  # Number of edges

# Create nodes and edges
x = torch.rand((num_nodes, 1))
edge_index = torch.randint(0, num_nodes, (2, num_edges))

data = Data(x=x, edge_index=edge_index)

# Visualize the graph
def visualize_graph(data, filename="large_graph.html"):
    net = Network(notebook=False, height="800px", width="1000px", directed=False)

    # Add nodes
    for i in range(data.x.size(0)):
        net.add_node(i, label=f"Node {i}", size=10, color=f"#{random.randint(0, 0xFFFFFF):06x}")

    # Add edges
    for edge in data.edge_index.t().tolist():
        net.add_edge(edge[0], edge[1])

    # Save and display the graph
    net.show(filename)

visualize_graph(data)
```

## Visualization
![Graph](https://github.com/MohammadHeydari/PyTorch-Graph-Visualization/blob/main/download.png)

---
