# Unsupervised Characterization of LMC Stellar Populations using Gaia DR3

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](YOUR_COLAB_NOTEBOOK_SHAREABLE_LINK_HERE)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

An end-to-end, unsupervised machine learning and dimensionality reduction pipeline designed to isolate and characterize stellar populations within a high-density field of the Large Magellanic Cloud (LMC) utilizing high-fidelity astrometry and photometry from **Gaia Data Release 3 (DR3)**.

---

## 🚀 Project Architecture

Rather than relying on traditional, manual 2D color-magnitude selections which suffer from projection and foreground contamination biases, this project maps stellar members across a **4D mixed physical phase space**:
1. **Thermodynamic Subspace:** Color Index ($BP - RP$) and Apparent Brightness ($G$).
2. **Kinematic Subspace:** Proper Motion vector components ($\mu_{\alpha}^*$, $\mu_{\delta}$).

### Pipeline Steps:
* **Preprocessing & Scaling:** Handled null astrometry and applied Z-score standardization to ensure unbiased, equal weight across different physical dimensions.
* **Hyperparameter Optimization:** Leveraged side-by-side **Within-Cluster Sum of Squares (Elbow Method)** and **Silhouette Analysis** to mathematically confirm an optimal centroid count of $K=3$.
* **Centroid Partitioning:** Executed $K$-Means clustering (`init='k-means++'`) to segment populations.
* **Density-Based Benchmarking:** Utilized **HDBSCAN** to explore continuous, non-parametric spatial structures and filter out highly scattered outliers.
* **Dimensionality Reduction:** Applied **Principal Component Analysis (PCA)** to project the 4D hypervolume onto 2D orthogonal axes, tracking feature variance loadings.
* **Blind Validation:** Performed independent physical verification using trigonometric parallax ($\varpi$) to mathematically confirm extra-galactic distance floors.

---

## 📊 Key Results & Visualizations

The machine learning pipeline successfully isolated three distinct astrophysical populations:

1. **Cluster 0 (LMC Main Sequence):** Dominated by faint, blue, core hydrogen-fusing stars with a highly concentrated, co-moving velocity profile.
2. **Cluster 1 (LMC Red Giant Branch):** Highly luminous, evolved helium-fusing red giants sharing the exact narrow proper-motion core as Cluster 0, confirming shared LMC membership.
3. **Cluster 2 (Milky Way Foreground Contamination):** A high-velocity-dispersion foreground screen consisting of local thin/thick disk and halo stars.

*(Tip: Upload your exported plots to the `figures/` folder in your repo, then link them here!)*

| Color-Magnitude Diagram (CMD) | Latent PCA Space |
|---|---|
| ![`CMD`](figures/color_magnitude_diagram.png) | ![`PCA`](figures/pca_latent_space.png) |

### 🔒 Physical Verification Check
Trigonometric parallax ($\varpi$) was withheld during model training to act as a pure, blind validation metric. As shown in the validation profile, the machine-isolated LMC clusters naturally converge on the true physical LMC distance floor ($\varpi \approx 0.02 \text{ mas}$, or $\sim 50 \text{ kpc}$), confirming the high scientific integrity of the algorithm.

---

## 🛠️ Installation & Execution

To run this pipeline locally or in Colab:

1. Clone this repository:
   ```bash
   git clone [https://github.com/yourusername/LMC-Stellar-Clustering-GaiaDR3.git](https://github.com/yourusername/LMC-Stellar-Clustering-GaiaDR3.git)
