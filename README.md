# PhysPred
Data and experimental artifacts for Stage-Wise Physics-Guided Latency Prediction for Resource-Partitioned Hardware-Aware Neural Architecture Search.

# TCAD-2026-0638 Supplementary Artifact

This artifact accompanies **Stage-Wise Physics-Guided Latency Prediction for Resource-Partitioned Hardware-Aware Neural Architecture Search**. It contains the machine-readable evidence used by the revised manuscript and response letter. No result should be inferred from a file name alone; the `protocol.json`, summary tables, and this index define the intended semantics.

## 1. Benchmark core and exact architecture pool

- `data/benchmark_core/arch_pool.json`: the 1,500 OFA-MBv3 architecture pool and stable architecture identifiers used to form the 1,200/300 architecture-disjoint split.
- `data/benchmark_core/dataset_gpu_hybrid.pkl`: original RTX 3090 multi-batch/multi-quota latency dataset.
- `data/benchmark_core/dataset_cpu_amd.pkl` and `dataset_cpu_intel.pkl`: original AMD 4800H and Intel 125H latency datasets.
- `data/benchmark_core/res_cpu_quota_*.json`: original CPU quota measurement exports.
- `data/local/operating_cells/` and `data/derived/*holdout_per_cell.csv`: audited per-cell MAPE and ranking results used in Fig. 2 and the robustness discussion.

## 2. Main predictor, baselines, and ablations

- `data/server/revision_results/fixed_cv_gpu/`: grouped five-fold RTX 3090 results, fold metrics, and run metadata.
- `data/local/original_cpu_baselines/`: preserved CPU baseline scripts, datasets, summaries, and SHA-256 provenance records.
- `data/server/scripts/baseline_results_gpu/`: original GPU baseline summaries and per-cell outputs.
- `data/server/revision_results/resnet_ablation_v2/` and `resnet_cv/`: OFA-ResNet50 architecture-disjoint evaluation and cumulative A/B/C/D ablation.
- `data/server/revision_results/jet_ablation_v1/`: fixed Jet-Nemotron-2B workload experiments, capacity-boundary record, grouped-split metrics, predictions, and quota-anchor diagnostics.
- `data/derived/jet_quota_holdout.csv`: compact quantitative quota-holdout diagnostic used in the revised manuscript and response; this is a fixed-workload diagnostic, not an OFA-MBv3 architecture-extrapolation result.
- `data/derived/nested_ablation.csv` and `data/server/scripts/ablation_summary.csv`: compact values used by the manuscript ablation table and regeneration script.

## 3. HELP, supervised MLP, and label-efficiency curves

- `data/server/revision_results/official_help_vs_physpred_fullcurve/`: official HELP adaptation protocol, five-repeat metrics, per-task metrics, and predictions.
- `data/local/official_help_vs_physpred_fullcurve/`: local mirror of the audited HELP/PhysPred curve.
- `data/local/supervised_mlp_efficiency_curve/`: matched outer split, nested support sizes, and five-repeat supervised architecture-MLP results.
- `data/derived/official_help_physpred_supervised_curve.csv`: the compact three-method curve used in Fig. 3(c).

## 4. Cross-hardware calibration

- `data/server/revision_results/transfer_amd_to_intel/` and `transfer_intel_to_amd/`: protocols, raw repetitions, and summary statistics for zero-/few-shot CPU transfer.
- `data/derived/cross_hardware_calibration.csv`: compact figure input.

## 5. Direct hardware-counter validation

- `data/local/direct_feature_counter_validation_gpu/`: GPU feature-to-counter units and protocol.
- `data/local/feature_counter_validation/`: audited GPU/Intel/AMD feature and counter joins.
- `data/local/intel24_physical_feature_validation/`: Intel fixed-cell and quota-delta units, correlations, and summaries.
- `data/local/amd_4800h/`: AMD clean latency, counter index, and representative-architecture manifest.
- `data/derived/feature_counter_relationships.csv` and `counter_quota_changes.csv`: exact compact inputs for Fig. 4.

The artifact includes the exported measurements and audit metadata used in the paper. Large vendor-specific profiler databases (for example, complete VTune, NSYS, NCU, or AMDuProf session directories) are not duplicated; the included unit tables, logs/index records, and protocols preserve the values and measurement semantics used in the analysis.

## 6. Complete HW-NAS, automatic quota, and slowdown-factor baselines

- `data/server/revision_results/gnn_accuracy_pool/`: trained accuracy-predictor checkpoint and OOD predictions.
- `data/server/revision_results/imagenet_pareto_actual/`: measured ImageNet-1K candidate accuracies, candidate records, and complete fixed-quota decisions.
- `data/server/revision_results/hwnas_pareto_gnn/`: Pareto fronts, selected candidates, prediction tables, and summary statistics.
- `data/server/revision_results/sla_autoquota_gnn/`: disjoint calibration/evaluation decisions, residual safety factors, and automatic-quota summaries.
- `data/server/revision_results/reviewer_exact_slowdown_all_baselines/`: the reviewer-proposed quota-only slowdown baseline, batch-specific extension, label costs, Q95 factors, prediction metrics, and architecture--quota decisions.
- `data/derived/accuracy_predictor_validation.csv`, `automatic_quota_hwnas_n20.csv`, and `slowdown_curve.csv`: compact manuscript inputs.

## 7. Regeneration and audit scripts

- `scripts/generate_paper_figures.py`: regenerates every manuscript figure from the tabular artifacts; vector PDF is the authoritative output and PNG is a preview.
- `scripts/run_supervised_mlp_efficiency.py`: matched-split supervised architecture-MLP efficiency experiment.
- `scripts/legacy_core/`: preserved original predictor, baseline, ablation, and Top-K evaluation scripts corresponding to the original benchmark files.
- `requirements_original.txt`: original experiment environment requirements.
- `MANIFEST_SHA256.csv`: relative path, byte size, and SHA-256 digest for every artifact file.

## 8. Figure numbering

The generated file `fig4_scope_transfer_efficiency.pdf` appears as **Fig. 3** in the revised manuscript; `fig6_counter_validation.pdf` appears as **Fig. 4**. Their source canvases use the same 7.12-inch width and the same Matplotlib typography. Both are inserted at `0.92\textwidth`, so their figure text is rendered at the same scale in the paper.

## Reproduction notes

1. Run scripts from the artifact root so relative paths resolve under `data/`.
2. The plotting script requires Python, NumPy, pandas, and Matplotlib.
3. Model-training scripts additionally require the versions recorded by the original requirements and protocol files.
4. Re-running hardware profiling requires the named physical devices and vendor tools; the supplied processed outputs are sufficient to reproduce the manuscript tables and figures without re-profiling.

## Readable supplementary experimental details

`supplementary/supplementary.pdf` provides the six-page experimental supplement. Its editable source is `supplementary/supplementary.tex`; the original IEEEtran class, full-precision numeric inputs, four generated LaTeX tables, and a standard-library-only table-regeneration script are included in the same directory. It restores the original profiling detail, all operating-cell and Top-K values, the six-budget sample-efficiency comparison, quota-stratified results, and complete regression-backbone metrics. The manuscript itself is unchanged by this addition.
