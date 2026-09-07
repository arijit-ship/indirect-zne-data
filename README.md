# Indirect-ZNE DATA

The indirect-control paradigm offers a scalable approach to quantum computation by restricting external operations to a small subset of qubits, whereas the entire system evolves under its intrinsic manybody Hamiltonian. This framework reduces hardware complexity and limits the noise introduced through control channels. Recently, Anan et al. proposed an implementation of the variational quantum eigensolver (VQE) within this indirect-control architecture. However, the impact and integration of quantum error mitigation techniques in such a setting remain largely unexplored. In particular, zero-noise extrapolation (ZNE), a widely used error mitigation strategy, has not yet been systematically adapted to indirect-control VQE. A key requirement of ZNE is the controlled amplification of noise, which is commonly achieved through circuit-level techniques such as unitary folding. In the indirect-control framework, however, quantum operations are largely governed by continuous time-evolution under the system Hamiltonian, making the construction of physically realizable inverse operations non-trivial. In this study, we investigate the feasibility of implementing ZNE within the indirect-control VQE framework. We address the challenges associated with noise amplification in the presence of time-evolution operators and, with a minimal relaxation of the indirect-control constraint, propose a ZNE-based error-mitigation strategy that exploits the symmetry of the one-dimensional XY spin chain.

# Source Code Repository

Simulation source code can be found here:

[GitHub indirect-zne](https://github.com/arijit-ship/indirect-zne/tree/dev/src)

# _VQE.json File

| **Section**    | **Key**                                          | **Type**              | **Description**                                                                 |
|----------------|----------------------------------------------------|------------------------|-----------------------------------------------------------------------------------|
| **Observable** | `config.observable.def`                            | String                 | Target Hamiltonian type. Options: `'custom'`, `'ising'`, `'heisenberg'`.          |
|                | `config.observable.coefficients.cn`                 | List of Floats         | Interaction-term coefficients.                                                    |
|                | `config.observable.coefficients.bn`                 | List of Floats         | Coupling-term coefficients.                                                       |
|                | `config.observable.coefficients.r`                  | Float                  | Scaling coefficient.                                                              |
| **Ansatz**     | `config.ansatz.layer`                               | Integer                | Number of layers in the ansatz circuit.                                          |
|                | `config.ansatz.gateset`                             | Integer                | Identifier of the gate set used.                                                  |
|                | `config.ansatz.ugate.type`                          | String                 | Ansatz/U-gate type. Options: `'custom'`, `'xy-iss'`, `'ising'`, `'heisenberg'`.    |
|                | `config.ansatz.ugate.coefficients.cn/bn/r`          | List of Floats / Float | Interaction, coupling, and scaling coefficients of the U gate.                    |
|                | `config.ansatz.ugate.time.min/max`                  | Float                  | Evolution time range for the U gate.                                             |
| **VQE**        | `config.vqe.iteration`                              | Integer                | Number of VQE iterations/restarts.                                               |
|                | `config.vqe.optimization.status`                    | Boolean                | Whether classical optimization is enabled.                                       |
|                | `config.vqe.optimization.algorithm`                 | String                 | Optimization algorithm used (e.g., `"SLSQP"`).                                    |
|                | `config.vqe.optimization.constraint`                | Boolean                | Whether constrained optimization is enabled.                                     |
|                | `config.vqe.optimization.opt_options`               | Object                 | Solver-specific settings (`maxiter`, `disp`, `ftol`, etc.).                       |
|                | `config.init_param.value`                           | String                 | Ansatz parameter initialization method (e.g., `"random"`).                       |
| **Output**     | `output.exact_sol`                                  | Float                  | Exact ground-state energy of the target Hamiltonian.                             |
|                | `output.initial_cost_history`                       | List of Floats         | Cost value(s) at the initial parameters.                                         |
|                | `output.optimized_minimum_cost`                     | List of Floats         | Minimum cost value(s) found after optimization.                                  |
|                | `output.optimized_parameters`                       | List of Lists (Floats) | Optimized ansatz parameter values per run.                                       |
|                | `output.run_time_sec`                               | Float                  | Total wall-clock run time, in seconds.                                           |
|                | `output.noise_details.identity_factors`             | List of Integers       | Identity-scaling factors applied per gate type.                                  |
|                | `output.noise_details.noise_level`                  | List of Integers       | Noise levels applied per gate type.                                              |
|                | `output.noise_details.gates_num`                    | List of Integers       | Gate counts per gate type used for noise scaling.                                |
|                | `output.noise_details.noise_profile`                | Object                 | Copy of the noise settings actually applied (`status`, `type`, `noise_prob`, ...). |
|                | `output.noise_details.odd_wires`                    | Integer                | Number of wires with an odd noise-application count.                            |
|                | `output.noise_details.raw_gate_count`               | Object                 | Raw gate counts by type (`R`, `CZ`, `U`, `Y`, `total`).                          |
| **Others**     | `meta.id`                                           | String                 | Unique UUID identifying the run; embedded in the output file name.               |
|                | `meta.datetime` / `datetime_finished`               | String                 | Run start/finish timestamps (`YYYYMMDD_HHMMSS`).                                 |
|                | `meta.run_index`                                    | Integer                | Index of this run within a repeated configuration.                              |
|                | `meta.python_version`, `os`, `hostname`             | String                 | Environment/provenance info for the run.                                        |
|                | `meta.cpu_logical_cores`, `ram_total_gb`            | Integer / Float        | Host machine resources at run time.                                             |
|                | `config.run`                                        | String                 | Algorithm executed. Options: `'vqe'`, `'redundant'`, `'zne'`.                     |
|                | `config.history`                                    | Boolean                | Whether full optimization history is stored (e.g., in HDF5).                     |
|                | `config.nqubits`, `state`                           | Integer / String       | Number of qubits and state representation (`'dmatrix'`/`'statevector'`).          |
|                | `config.output.file_name_prefix`, `draw`            | String / Object        | Output file naming prefix and figure-drawing settings.                          |
|                | `config.noise_profile`                              | Object                 | Noise settings requested: `status`, `type`, `noise_prob`, `noise_on_init_param`.  |
|                | `config.redundant.identity_factors`                 | List of Lists          | Identity-scaling factors for redundant circuits.                                 |
|                | `config.zne`                                        | Object                 | ZNE settings: `method`, `degree`, `sampling`, `data_points`.                      |
|                | `others.observable_string`                          | String                 | Human-readable Pauli-string form of the target Hamiltonian.                      |
|                | `others.time_evolution_gate_hamiltonian_string`     | List of Strings        | Human-readable Pauli-string form of the U-gate Hamiltonian.                      |
|                | `others.initial_parameters`                         | List of Floats         | Ansatz parameter values before optimization.                                     |
|                | `others.lie_trotter_details`                        | Object / Null          | Lie-Trotter decomposition details, if applicable.                                |
| **Artifacts**  | `artifacts.cost_callings_total`                     | Integer                | Total number of cost-function evaluations across the whole run.                 |
|                | `artifacts.opt_obj.x`                                | List of Floats         | Optimized parameter vector returned by the optimizer.                           |
|                | `artifacts.opt_obj.fun`                              | Float                  | Final cost-function value at the optimum.                                       |
|                | `artifacts.opt_obj.success`                          | Boolean                | Whether the optimizer reported successful convergence.                          |
|                | `artifacts.opt_obj.message`                          | String                 | Termination message returned by the optimizer.                                  |
|                | `artifacts.opt_obj.nit`                              | Integer                | Number of iterations performed by the optimizer.                                |
|                | `artifacts.opt_obj.nfev`                             | Integer                | Number of cost-function evaluations performed by the optimizer.                 |
|                | `artifacts.opt_obj.jac`                              | List of Floats         | Final gradient (Jacobian) at the optimized parameters.                          |
|                | `artifacts.opt_obj.hess_inv`                         | Object / Null          | Inverse Hessian approximation, if available.                                    |