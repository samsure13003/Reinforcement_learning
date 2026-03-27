# Reinforcement_learning
# 🎯 Ads CTR Optimisation — Reinforcement Learning

![Python](https://img.shields.io/badge/Python-3.x-blue?style=flat&logo=python)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?style=flat&logo=jupyter)
![Algorithm](https://img.shields.io/badge/Algorithm-UCB%20%7C%20Thompson%20Sampling-green?style=flat)
![Dataset](https://img.shields.io/badge/Dataset-10%2C000%20Rounds%20%C3%97%2010%20Ads-lightgrey?style=flat)
![License](https://img.shields.io/badge/License-MIT-yellow?style=flat)

> Which ad should we show to maximize clicks? This project answers that question using two classic **Reinforcement Learning** algorithms — **Upper Confidence Bound (UCB)** and **Thompson Sampling** — on a simulated ad click-through rate (CTR) dataset.

---

## 📌 Problem Statement

A company runs **10 different advertisements**. Each time a user visits the platform, one ad is shown and we record whether the user clicked it (reward = 1) or ignored it (reward = 0). The challenge is:

> **Without knowing which ad performs best upfront, which ad should be shown at each round to maximise total clicks over time?**

This is the classic **Multi-Armed Bandit** problem — a core scenario in Reinforcement Learning where we must balance **exploration** (trying new ads) and **exploitation** (showing the best known ad).

---

## 📁 Project Structure

```
ads-ctr-optimisation/
│
├── Ads_CTR_Optimisation.csv        # Dataset: 10,000 rounds × 10 ads (0/1 rewards)
├── upper_confidence_bound.ipynb    # UCB algorithm implementation
├── thompson_sampling.ipynb         # Thompson Sampling implementation
└── README.md
```

---

## 📊 Dataset

| Property | Detail |
|---|---|
| File | `Ads_CTR_Optimisation.csv` |
| Rows | 10,000 (simulated user rounds) |
| Columns | 10 (Ad 1 through Ad 10) |
| Values | Binary — `1` (clicked) or `0` (not clicked) |

Each row represents one user visit. The value in each column tells us whether that user *would have* clicked that ad if it had been shown. In reality, only one ad is shown per round — the algorithms decide which one.

**Ground truth clicks (if all rounds were used):**

| Ad | Total Clicks |
|---|---|
| Ad 1 | 1703 |
| Ad 2 | 1295 |
| Ad 3 | 728 |
| Ad 4 | 1196 |
| **Ad 5** | **2695 ✅ Best** |
| Ad 6 | 126 |
| Ad 7 | 1112 |
| Ad 8 | 2091 |
| Ad 9 | 952 |
| Ad 10 | 489 |

**Ad 5 is the best-performing ad** — a good algorithm should converge to showing it most frequently.

---

## 🤖 Algorithms Implemented

### 1. Upper Confidence Bound (UCB)

UCB is a deterministic algorithm that maintains an **upper confidence bound** on the estimated reward for each ad. It selects the ad with the highest upper bound, which naturally balances exploration and exploitation.

**How it works:**
- At each round `i`, for each ad `j`, compute:

$$UCB_j = \bar{x}_j + \sqrt{\frac{3}{2} \cdot \frac{\ln(i)}{N_j}}$$

- Where `x̄ⱼ` is the average reward so far, and `Nⱼ` is the number of times ad `j` was selected.
- The ad with the highest UCB is shown.

**Key properties:**
- Fully deterministic (no randomness)
- Provably converges to the optimal arm
- Runs over all **10,000 rounds**

---

### 2. Thompson Sampling

Thompson Sampling is a **probabilistic / Bayesian** algorithm. It maintains a Beta distribution for each ad based on observed clicks and non-clicks, then samples from these distributions to pick an ad.

**How it works:**
- For each ad `i`, maintain counts of successes (`rewards_1`) and failures (`rewards_0`)
- At each round, sample a random value from each ad's Beta distribution:

$$\theta_i \sim \text{Beta}(\text{rewards\_1}_i + 1,\ \text{rewards\_0}_i + 1)$$

- Show the ad with the highest sampled value.

**Key properties:**
- Probabilistic and Bayesian in nature
- Tends to converge faster than UCB in practice
- Run here for **500 rounds** (faster convergence demonstration)

---

## 🔬 Comparison

| Feature | UCB | Thompson Sampling |
|---|---|---|
| Type | Deterministic | Probabilistic (Bayesian) |
| Exploration strategy | Confidence intervals | Posterior sampling |
| Rounds used | 10,000 | 500 |
| Convergence speed | Slower | Faster in practice |
| Randomness | None | Yes (Beta distribution) |
| Best for | Stable environments | Noisy / online settings |

Both algorithms aim to identify **Ad 5** as the optimal choice without knowing the ground truth in advance.

---

## ▶️ How to Run

### Prerequisites

```bash
pip install numpy pandas matplotlib
```

### Steps

1. Clone this repository:
   ```bash
   git clone https://github.com/your-username/ads-ctr-optimisation.git
   cd ads-ctr-optimisation
   ```

2. Launch Jupyter Notebook:
   ```bash
   jupyter notebook
   ```

3. Open and run either notebook:
   - `upper_confidence_bound.ipynb`
   - `thompson_sampling.ipynb`

> Make sure `Ads_CTR_Optimisation.csv` is in the same directory as the notebooks.

---

## 📈 Results

Both algorithms converge to showing **Ad 5** the most, confirming it as the optimal ad. The histogram output from each notebook visualises how many times each ad was selected throughout the experiment.

- **UCB** distributes selections more evenly early on before converging.
- **Thompson Sampling** converges more aggressively toward the best ad.

---

## 🧠 Concepts Covered

- Multi-Armed Bandit Problem
- Exploration vs. Exploitation Trade-off
- Upper Confidence Bound (UCB1)
- Bayesian Inference & Beta Distribution
- Thompson Sampling
- Click-Through Rate (CTR) Optimisation

---

## 🛠️ Tech Stack

- **Python 3.x**
- **NumPy** — numerical operations
- **Pandas** — dataset loading
- **Matplotlib** — visualisation
- **Jupyter Notebook** — interactive experimentation

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---

## 🙋‍♂️ Author

Made with ❤️ as part of a Reinforcement Learning study project.  
Feel free to ⭐ the repo if you found it useful!
