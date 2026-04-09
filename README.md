# CSLAP Synthetic Data Generator & Datasets

This repository contains the synthetic data generation pipeline and the generated datasets required to evaluate the Correlated Storage Location Assignment Problem (CSLAP) under operational constraints.

These environments mathematically enforce physical capacity limits ($\zeta_s$) and workload time limits ($T_s$) directly onto heterogeneous picking stations, preventing operations research algorithms from deriving mathematically "optimal" groupings that would inherently overflow local conveyor buffers in a real warehouse.

## Contents
1. **`CSLAP_synthetic_data_generator.py`**: A python script that dynamically constructs warehouse networks ranging from 50 to thousands of SKUs. The generator ensures structural realism by deploying a Common Itemset correlation logic while ensuring structural matrix feasibility across all synthetic zones.
2. **`synthetic_datasets/`**: Directory containing pre-generated `.csv` environments at specific item scaling benchmarks (50, 500, 1000, 2000 SKUs).

## Executing the Generator
The script uses standard `numpy` and `pandas` libraries. To regenerate datasets or build custom-sized warehouse configurations, execute:

```bash
python CSLAP_synthetic_data_generator.py --sizes 50 500 1000 2000 --theta 0.7
```

## Dataset Formats
The output consists of three CSV files per scale:
* `syn_[size]sku_orders.csv`: The itemized receipt of generated orders containing random product pairings bound by a $\theta=0.7$ affinity threshold.
* `syn_[size]sku_products.csv`: Baseline data per stock-keeping unit (SKU), mapping products to logical groupings.
* `syn_[size]sku_stations.csv`: Operational boundaries of discrete warehouse nodes, stipulating $\zeta_s$ physical capacity, and $T_s$ daily workload processing limits.
