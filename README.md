# Vehicle Routing Problem — Random Instance Generator & Gurobi Solver

A Jupyter notebook that generates configurable random VRP instances and solves them with Gurobi.

---

## Features

- **Instance generation** across a wide parameter space
- **Two Gurobi formulations**: MTZ subtour elimination and lazy-cut callback
- **Multi-depot** support with per-depot vehicle pools
- **Visualisation** of instances and solution routes
- **Batch sweep** to compare configurations
- **Export** to CSV / NumPy / JSON

---

## Parameter Space

| Parameter | Range / Options |
|---|---|
| Customers | 200 – 3,000 |
| Depots | 1 – 50 |
| Distance | Euclidean symmetric or asymmetric |
| Customer placement | Uniform, Clustered, Mixed |
| Capacity tightness | Loose, Medium, Tight, Near-infeasible |
| Demand distribution | Uniform, Normal, Exponential, Gamma |

---

## Requirements

### Python packages

```bash
pip install numpy scipy matplotlib pandas networkx
```

### Gurobi

`gurobipy` is the Python client for Gurobi. The version must match your Gurobi server exactly.

```bash
pip install gurobipy==<your_server_version>
```

To find your server version:

```bash
# SSH into the server and run:
gurobi_cl --version
```

---

## Licence Setup

If you are connecting to a **Gurobi Compute Server**, create a `gurobi.lic` file:

```
COMPUTESERVER=<ip_address>
PASSWORD=<password>
```

Then point Gurobi to it before importing:

```python
import os
os.environ["GRB_LICENSE_FILE"] = "/path/to/gurobi.lic"
import gurobipy as gp
```

Or set it at the shell level before launching Jupyter:

```bash
export GRB_LICENSE_FILE=/path/to/gurobi.lic
jupyter notebook
```

---

## Usage

1. Clone the repo and install dependencies
2. Set up your `gurobi.lic` file
3. Open `vrp_gurobi.ipynb`
4. Edit the parameters in **Cell 1** (Configuration)
5. Run all cells

---

## Notebook Structure

| Cell | Description |
|---|---|
| 0 | Imports & dependency check |
| 1 | Configuration — edit parameters here |
| 2 | Instance generator |
| 3 | Instance visualisation |
| 4 | Gurobi MTZ formulation |
| 5 | Gurobi callback formulation |
| 6 | Solution report |
| 7 | Route plot |
| 8 | Batch parameter sweep |
| 9 | Export instance to CSV / NPY / JSON |

---

## Notes

- For instances with more than 500 customers the notebook automatically switches to the callback formulation, which scales better than MTZ.
- Near-infeasible capacity settings may produce no feasible solution depending on fleet size.
- The `gurobipy` PyPI package is a client only — it does not include a solver. A valid Gurobi licence or Compute Server is required.
