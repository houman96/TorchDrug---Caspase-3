Generative Modeling of Caspase-3 Inhibitor Candidates Using TorchDrug GCPN and RGCN

This project applies the Graph Convolutional Policy Network (GCPN) and Relational Graph Convolutional Network (RGCN) implementations provided by TorchDrug to generate candidate molecules within the chemical space of reported caspase-3 inhibitors. Supervised learning and reinforcement learning are combined to promote chemically valid structures and optimize selected molecular properties.

The generated compounds are computational candidates and should not be considered confirmed caspase-3 inhibitors without additional activity prediction, molecular modeling, synthesis, and experimental validation.

Overview

* Objective: Generate chemically valid candidate molecules related to reported caspase-3 inhibitors.
* Dataset: Curated compounds with reported caspase-3 activity obtained from BindingDB.
* Models:
    * GCPN: Graph Convolutional Policy Network for property-guided molecular graph generation.
    * RGCN: Relational Graph Convolutional Network used as the message-passing backbone.
* Training objectives:
    * NLL: Negative log-likelihood for supervised pretraining.
    * PPO: Proximal Policy Optimization for reinforcement learning.
* Hardware: NVIDIA GeForce RTX 4070 GPU.
* Training configuration:
    * Epochs: 500
    * Batch size: 16
    * Approximate duration: 3 hours

Methodology

Data Preparation

Compounds with reported caspase-3 activity were obtained from BindingDB and curated before training. The molecular structures were processed into graph representations compatible with TorchDrug.

The presence of a compound in the source dataset does not independently establish its potency, selectivity, or suitability for therapeutic development.

Environment Setup

The project was developed and tested using:

* Python: 3.8.19
* TorchDrug: 0.2.1
* CUDA Toolkit: 11.6.2
* Environment manager: Conda

Create the environment using the supplied environment.yml file:

conda env create -f environment.yml
conda activate aihouman

The machine-specific prefix line should be removed from environment.yml before creating the environment on another system.

Model Architecture

The RGCN backbone contains eight message-passing layers with a hidden dimension of 256. It extracts relational features from molecular graphs, while GCPN generates new molecular structures through sequential graph construction.

Training Procedure

Training consisted of two stages:

1. Supervised learning: Negative log-likelihood was used to learn molecular graph-generation patterns from the curated dataset.
2. Reinforcement learning: Proximal Policy Optimization was used to optimize selected computational properties, including drug-likeness and synthetic accessibility.

The reported run was conducted for 500 epochs with a batch size of 16 on an NVIDIA GeForce RTX 4070 GPU.

Results

The training curves show a general reduction in edge, node, stop, and total losses, together with improvements in their associated accuracy measures.

The trained model generated candidate molecular structures within the chemical space learned from the caspase-3 dataset. However, the training metrics assess model-learning behavior and do not establish caspase-3 inhibition.

The biological activity, target selectivity, synthetic feasibility, safety, and pharmacological properties of the generated molecules require further computational and experimental evaluation.

Limitations

* No experimental caspase-3 inhibition assays were performed.
* The generated structures were not confirmed as active or selective caspase-3 inhibitors.
* Generative-model training metrics do not measure biological activity.
* Further filtering, activity prediction, molecular docking, molecular dynamics, synthesis, and wet-laboratory validation may be required.
* The quality of the generated chemical space depends on the composition and curation of the source dataset.

TorchDrug Integration

This project uses TorchDrug for molecular graph representation, neural-network modeling, and molecular generation. Additional information is available in the TorchDrug molecule-generation tutorial.

Model File Recombination

The trained model was divided into four parts to satisfy file-size limitations. On Linux or macOS, reconstruct the model using:

cat gcpn6.pkl.001 gcpn6.pkl.002 gcpn6.pkl.003 gcpn6.pkl.004 > gcpn6.pkl

To verify that the reconstructed file was created:

ls -lh gcpn6.pkl

The reconstructed gcpn6.pkl file is a serialized model file and should not be unzipped.

References

* TorchDrug molecule-generation tutorial
* BindingDB
* You J, Liu B, Ying Z, Pande V, Leskovec J. Graph Convolutional Policy Network for Goal-Directed Molecular Graph Generation. Advances in Neural Information Processing Systems. 2018;31.

License

This project is licensed under the Apache License 2.0. See the LICENSE file for details.
