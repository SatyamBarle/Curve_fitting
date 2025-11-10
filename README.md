# Curve_fitting
# Problem Statement
You are given a dataset xy_data.csv containing 1500 points that lie on a parametric curve defined as:
<img width="690" height="320" alt="image" src="https://github.com/user-attachments/assets/a58b1da6-75c0-4fd7-9d17-9d7f8ef6d7af" />
# Objective
Minimize the L₁ loss function defined as:
<img width="441" height="54" alt="image" src="https://github.com/user-attachments/assets/69849c3f-4578-41db-8619-0aa7eafdde74" />
This is done using numerical optimization in Python (SciPy) — first with a local optimizer (L-BFGS-B) and then confirmed globally with Differential Evolution (DE).
# Step-by-Step Approach
Step 1 — Data Preparation:
Loaded xy_data.csv using Pandas.
Created parameter 𝑡=linspace(6,60,1500)
Extracted x_data, y_data as NumPy arrays.

Step 2 — Model Function:
Defined a Python function:
def model(params, t):
    theta_deg, M, X = params
    theta = np.deg2rad(theta_deg)
    exp_term = np.exp(M * np.abs(t))
    x_pred = t*np.cos(theta) - exp_term*np.sin(0.3*t)*np.sin(theta) + X
    y_pred = 42 + t*np.sin(theta) + exp_term*np.sin(0.3*t)*np.cos(theta)
    return x_pred, y_pred
Note: np.cos() and np.sin() use radians, so theta must be converted from degrees to radians.

Step 3 — Loss Function
def l1_loss(params):
    x_pred, y_pred = model(params, t)
    return np.sum(np.abs(x_data - x_pred) + np.abs(y_data - y_pred))
    
Step 4 — Optimization
1.Local Search (L-BFGS-B)
  Used bounded optimization with multiple random seeds.
  Explored different starting points within the valid ranges.
  Found stable convergence to the same minimum region.
2. Global Search (Differential Evolution)
  Used population-based stochastic global search.
  Verified that both methods converge to the same optimal parameters.
  Confirms that the found minimum is global.
 #Final Results
 theta = 28.118423074179, M = 0.021388956654, X = 54.901722855097, L1 = 37865.093837691806
 <img width="873" height="692" alt="image" src="https://github.com/user-attachments/assets/b031167f-cd51-4663-85c2-d44914eacb46" />
 





