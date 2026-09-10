# Indirect-ZNE DATA

The indirect-control paradigm offers a scalable approach to quantum computation by restricting external operations to a small subset of qubits, whereas the entire system evolves under its intrinsic manybody Hamiltonian. This framework reduces hardware complexity and limits the noise introduced through control channels. Recently, Anan et al. proposed an implementation of the variational quantum eigensolver (VQE) within this indirect-control architecture. However, the impact and integration of quantum error mitigation techniques in such a setting remain largely unexplored. In particular, zero-noise extrapolation (ZNE), a widely used error mitigation strategy, has not yet been systematically adapted to indirect-control VQE. A key requirement of ZNE is the controlled amplification of noise, which is commonly achieved through circuit-level techniques such as unitary folding. In the indirect-control framework, however, quantum operations are largely governed by continuous time-evolution under the system Hamiltonian, making the construction of physically realizable inverse operations non-trivial. In this study, we investigate the feasibility of implementing ZNE within the indirect-control VQE framework. We address the challenges associated with noise amplification in the presence of time-evolution operators and, with a minimal relaxation of the indirect-control constraint, propose a ZNE-based error-mitigation strategy that exploits the symmetry of the one-dimensional XY spin chain.

# Source Code Repository

Simulation source code can be found here (Note that the code requires some setup before it can be executed:):

[GitHub indirect-zne (dev branch)](https://github.com/arijit-ship/indirect-zne/tree/dev/src)


# Figures

| Figure | Link |
| --- | --- |
| ![trotter1](experiments/recent/REVIEW-SIMULATIONS/reports/6Q-trotter/COMPARISION_TROTTER_VS_NO_TROTTER_6-QUBIT_VARY_GAMMA.png) | [Jupyter Notebook](experiments/recent/REVIEW-SIMULATIONS/6Q-trotter.ipynb), [JSON Data][experiments/recent/REVIEW-SIMULATIONS/data/6Q-trotter]|
|![trotter2](experiments/recent/REVIEW-SIMULATIONS/reports/6Q-trotter/COMPARISION_TROTTER_VS_NO_TROTTER_6-QUBIT_SCALE_FACTOR.png)| [Jupyter Notebook](experiments/recent/REVIEW-SIMULATIONS/6Q-trotter.ipynb), [JSON Data][experiments/recent/REVIEW-SIMULATIONS/data/6Q-trotter]|
|![univariate-7Q](experiments/recent/REVIEW-SIMULATIONS/reports/7Q-various-tmax/RESULT-SINGLE-RIC-ZNE-VS-ORDER-IEEE_SINGLE_COL.png)|[Jupyter Notebook](experiments/recent/REVIEW-SIMULATIONS/7Q-various-tmax.ipynb), [JSON Data](experiments/recent/REVIEW-SIMULATIONS/data/7Q-various-tmax/7Q_tmax_sweep_ising_depol_tmax20_20260725_110811)|
|![7Q-var-scaling](experiments/recent/REVIEW-SIMULATIONS/reports/7Q-various-tmax/cost_beta_ric3.png)|[Jupyter Notebook](experiments/recent/REVIEW-SIMULATIONS/7Q-various-tmax.ipynb), [JSON Data](experiments/recent/REVIEW-SIMULATIONS/data/7Q-various-tmax/7Q_tmax_sweep_ising_depol_tmax20_20260725_110811)|
|![7Q-various-tmax](experiments/recent/REVIEW-SIMULATIONS/reports/7Q-various-tmax/VARIOUS-TMAX-IEEE.png)|[Jupyter Notebook](experiments/recent/REVIEW-SIMULATIONS/7Q-various-tmax.ipynb), [JSON Data](experiments/recent/REVIEW-SIMULATIONS/data/7Q-various-tmax)|
|![7Q-various-gamma](experiments/recent/REVIEW-SIMULATIONS/reports/7Q-various-gamma/RESULT-ZNE-VS-DELP-IEEE_SINGLE_COL.png)|[Jupyter Notebook](experiments/recent/REVIEW-SIMULATIONS/7Q-various-gamma.ipynb), [JSON Data](experiments/recent/REVIEW-SIMULATIONS/data/7Q-various-gamma)|
|![8Q-mulvariate-zne](experiments/recent/REVIEW-SIMULATIONS/reports/8Q-ising-depol/multivar_zne_8q_time-depol.png)|[Jupyter Notebook](experiments/recent/REVIEW-SIMULATIONS/8Q-ising-depol.ipynb), [JSON Data](experiments/recent/REVIEW-SIMULATIONS/data/8Q-ising-depol)|
|![8Q-sampling-overhead](experiments/recent/REVIEW-SIMULATIONS/reports/8Q-ising-depol/zne_overhead_8q_time-depol.png)|[Jupyter Notebook](experiments/recent/REVIEW-SIMULATIONS/8Q-ising-depol.ipynb), [JSON Data](experiments/recent/REVIEW-SIMULATIONS/data/8Q-ising-depol)|
|![8Q-depth](experiments/recent/REVIEW-SIMULATIONS/reports/8Q-ising-depol/depth_perlayer_8q_time-depol.png)|[Jupyter Notebook](experiments/recent/REVIEW-SIMULATIONS/8Q-ising-depol.ipynb), [JSON Data](experiments/recent/REVIEW-SIMULATIONS/data/8Q-ising-depol)|
|![8Q-gate-count](experiments/recent/REVIEW-SIMULATIONS/reports/8Q-ising-depol/gatecounts_perlayer_8q_time-depol.png)|[Jupyter Notebook](experiments/recent/REVIEW-SIMULATIONS/8Q-ising-depol.ipynb), [JSON Data](experiments/recent/REVIEW-SIMULATIONS/data/8Q-ising-depol)|
|![8Q-runtime](experiments/recent/REVIEW-SIMULATIONS/reports/8Q-ising-depol/runtime_8q_time-depol.png)|[Jupyter Notebook](experiments/recent/REVIEW-SIMULATIONS/8Q-ising-depol.ipynb), [JSON Data](experiments/recent/REVIEW-SIMULATIONS/data/8Q-ising-depol)|