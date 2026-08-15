# Edge-Aware-GAT (Edge-Aware Graph Attention Networks for Biomolecular Dynamics)
Edge-aware Graph Attention Networks (GATs) as analytical microscopes for molecular dynamics simulations. Implements Edge-Conditioned, Edge-Injected, and Edge-Gated message passing to predict structural evolution and extract interpretable residue communication networks.

This repository contains the Google Colab notebooks and data processing pipeline associated with the manuscript:
"Edge-Aware Graph Attention Networks for Interpreting Biophysical Mechanisms from Molecular Dynamics Simulations"
Mohd Ahsan, Chinmai Pindi, and Giulia Palermo.

Overview:
This repository provides a complete, interpretable AI framework to extract mechanistic insights from Molecular Dynamics (MD) simulations. It implements a suite of edge-aware Graph Attention Networks (GATs) designed to isolate the algebraic role of edge features.

The provided code base uses HIV-1 Protease as the primary application. HIV-1 protease provides a comprehensive demonstration of the entire pipeline—from graph construction to region-level analysis—allowing users to map mutation-induced remodeling between the wild-type (WT) and a drug-resistant non-active-site mutant (NAM).

Data & Pre-trained Models (Figshare):
To maximize accessibility and allow users to run the analysis immediately, all pre-processed graph datasets and fully trained models are hosted on Figshare:

🔗 DOI: 10.6084/m9.figshare.33264075

The figshare repository includes:

Processed PyTorch Graphs: Complete graph datasets for all three replicas of WT and NAM HIV-1 protease (e.g., trajectory_graphs_phi_psi_rmsf_WT_rep1.pt).

Trained Model Weights: Pre-trained weights for all architectures (Methods A, B, and C), across all replicas and systems.

Note: Users can bypass the data processing and training steps entirely by downloading these files and executing the Analysis notebook directly.

Google Colab Notebooks:
The workflow is divided into five modular Google Colab notebooks. Note that throughout the codebase, the three edge-aware architectures are referred to as Methods A (GAT-EC), B (GAT-EI), and C (GAT-EG).

1. Data Preprocessing
📄 data_GNNAC_EDGEAWARE.ipynb

Purpose: Converts raw MD trajectories into PyTorch Geometric (PyG) graph objects containing node features (coordinates, backbone dihedrals, RMSF) and edge features (distance metrics).

Requirement: Input MD trajectories must be strictly aligned on the Cα atoms prior to running this notebook to remove global translation and rotation.

2. Model Training:
These notebooks execute the one-step coordinate prediction training loop for the three distinct edge-aware architectures.

📄 train_WT_methodA(GAT-EC).ipynb

Architecture: Edge-Conditioned GAT (GAT-EC). Edge features contribute exclusively to the attention coefficients.

📄 train_WT_methodB(GAT-EI).ipynb

Architecture: Edge-Injected GAT (GAT-EI). Edge features are added directly to the transmitted message.

📄 train_WT_methodC(GAT-EG).ipynb

Architecture: Edge-Gated GAT (GAT-EG). Edge features generate a nonlinear gate that regulates information transfer.

3. Mechanistic Analysis:
📄 Analysis_EDGEAWARE.ipynb

Purpose: The complete analytical pipeline for interpreting the trained models.

Capabilities: Evaluates model faithfulness and extracts the learned attention into residue-level communication networks. Computes graph-theory descriptors (Node Weight for communication throughput, Strength for intensity, and Betweenness for relay) across all replicas for both WT and NAM, including the region-level structural aggregation.

Usage Instructions:

Align your MD trajectory on Cα atoms.

Run data_GNNAC_EDGEAWARE.ipynb to generate the .pt graph datasets.

Execute the three train_WT_method... notebooks to train the GAT-EC, GAT-EI, and GAT-EG models on your generated graphs.

Run Analysis_EDGEAWARE.ipynb to extract the communication descriptors and compare systems.
