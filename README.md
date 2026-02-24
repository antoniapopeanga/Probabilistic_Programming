# Probabilistic Modeling of Political Networks  
**Final Project – Probabilistic Programming**

## Overview
This project applies **Bayesian probabilistic modeling** and **latent space models** to analyze political interaction networks. Using message and meeting count data, it uncovers hidden social structure, leadership, negotiation roles, and faction alignment under uncertainty.

**Tools:** Python, PyMC, ArviZ, NetworkX, NumPy/SciPy, Matplotlib, Pandas

---

## Exercise 1 – Influence in a Bipartisan Network

**Data:**  
- Nodes = politicians, edges = number of exchanged messages  
- Two known factions (A, B)  
- Count data modeled with a Poisson distribution

**Model:** Latent Distance Model  
\[
\lambda_{ij} = \exp(\beta_0 - \|U_i - U_j\|), \quad
Y_{ij} \sim \text{Poisson}(\lambda_{ij})
\]
- \(U_i \in \mathbb{R}^2\): latent social positions  
- Closer nodes interact more frequently

**Findings:**
- Latent space clearly separates the two factions
- **Faction A:** centralized, hierarchical leadership  
  - Node 23 is most influential (≈84% posterior probability)
- **Faction B:** decentralized, competitive leadership  
  - Nodes 39 and 41 are nearly tied
- Best negotiators (cross-faction bridges) are *not* always the most influential nodes

**Model checks:**  
- Good MCMC convergence (R-hat ≈ 1)  
- Posterior predictive checks show good fit, with minor tail misfit

---

## Exercise 2 – Splitting the Triumvirate

**Data:**  
- Three factions: Caesar, Pompey, Crassus  
- Crassus members have unknown future allegiance  
- Meeting counts show strong overdispersion

**Model:** Joint Latent Space + Classifier  
- Anchored latent space (Caesar at (0,0), Pompey at (2,0))  
- Meetings modeled with a **Negative Binomial** likelihood  
- Logistic classifier predicts faction membership from latent positions

**Findings:**
- Clear separation between Caesar and Pompey in latent space
- 70% accuracy on known Crassus labels
- Probabilistic predictions reflect genuine ambiguity for some nodes
- Simulations show Caesar is slightly more likely to recruit more Crassus members
- Identifies the most undecided politicians (probabilities near 0.5)

---

## Key Takeaways
- Latent space models effectively reveal hidden political structure  
- Bayesian inference enables uncertainty-aware leadership and faction analysis  
- Influence, negotiation, and allegiance are distinct social roles  
- Joint modeling outperforms simple heuristic approaches