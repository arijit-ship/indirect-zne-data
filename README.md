# Indirect-ZNE DATA

The indirect-control paradigm offers a scalable approach to quantum computation by restricting external operations to a small subset of qubits, whereas the entire system evolves under its intrinsic manybody Hamiltonian. This framework reduces hardware complexity and limits the noise introduced through control channels. Recently, Anan et al. proposed an implementation of the variational quantum eigensolver (VQE) within this indirect-control architecture. However, the impact and integration of quantum error mitigation techniques in such a setting remain largely unexplored. In particular, zero-noise extrapolation (ZNE), a widely used error mitigation strategy, has not yet been systematically adapted to indirect-control VQE. A key requirement of ZNE is the controlled amplification of noise, which is commonly achieved through circuit-level techniques such as unitary folding. In the indirect-control framework, however, quantum operations are largely governed by continuous time-evolution under the system Hamiltonian, making the construction of physically realizable inverse operations non-trivial. In this study, we investigate the feasibility of implementing ZNE within the indirect-control VQE framework. We address the challenges associated with noise amplification in the presence of time-evolution operators and, with a minimal relaxation of the indirect-control constraint, propose a ZNE-based error-mitigation strategy that exploits the symmetry of the one-dimensional XY spin chain.

# Source Code Repository

Simulation source code can be found here:

[GitHub indirect-zne](https://github.com/arijit-ship/indirect-zne/tree/dev/src)

# _VQE.json File

| **Section**  | **Key**                             | **Type**          | **Description**                                                                                     |
|--------------|--------------------------------------|--------------------|-------------------------------------------------------------------------------------------------------|
| **Meta**     | `id`                                  | String             | Unique UUID identifying the run. Also embedded in the output file name.                              |
|              | `datetime`                            | String             | Timestamp (`YYYYMMDD_HHMMSS`) marking when the run started.                                          |
|              | `datetime_finished`                   | String             | Timestamp (`YYYYMMDD_HHMMSS`) marking when the run finished.                                         |
|              | `run_index`                           | Integer            | Index of this run, used when the same configuration is repeated multiple times.                      |
|              | `python_version`                      | String             | Python interpreter version and build info used to execute the run.                                   |
|              | `os`                                  | String             | Operating system on which the run was executed.                                                      |
|              | `hostname`                            | String             | Name of the machine that executed the run.                                                           |
|              | `cpu_logical_cores`                   | Integer            | Number of logical CPU cores available on the host machine.                                           |
|              | `ram_total_gb`                        | Float              | Total system RAM (in GB) available on the host machine.                                              |
| **Config**   | `run`                                 | String             | Algorithm executed. Options: `'vqe'`, `'redundant'`, `'zne'`.                                        |
|              | `history`                             | Boolean            | If `true`, indicates the full optimization history was recorded (e.g., in HDF5).                     |
|              | `nqubits`                             | Integer            | Number of qubits in the quantum system.                                                              |
|              | `state`                               | String             | State representation used. Options: `'dmatrix'` (density matrix) or `'statevector'`.                 |
|              | `output.file_name_prefix`             | String             | Prefix used for naming output files.                                                                 |
|              | `output.draw.status`                  | Boolean            | If `true`, enables figure drawing.                                                                    |
|              | `output.draw.fig_dpi`                 | Integer            | Resolution (DPI) of output figures.                                                                   |
|              | `output.draw.type`                    | String             | File format of output figures (e.g., `"png"`).                                                       |
|              | `observable.def`                      | String             | Target Hamiltonian type. Options: `'custom'`, `'ising'`, `'heisenberg'`.                              |
|              | `observable.coefficients.cn`          | List of Floats     | Interaction-term coefficients of the target Hamiltonian.                                             |
|              | `observable.coefficients.bn`          | List of Floats     | Coupling-term coefficients of the target Hamiltonian.                                                |
|              | `observable.coefficients.r`           | Float              | Scaling coefficient of the target Hamiltonian.                                                       |
|              | `ansatz.layer`                        | Integer            | Number of layers in the ansatz circuit.                                                              |
|              | `ansatz.gateset`                      | Integer            | Identifier of the gate set used in the ansatz.                                                       |
|              | `ansatz.ugate.type`                   | String             | Type of the ansatz/U-gate. Options: `'custom'`, `'xy-iss'`, `'ising'`, `'heisenberg'`.                |
|              | `ansatz.ugate.coefficients.cn`        | List of Floats     | Interaction-term coefficients of the U gate.                                                          |
|              | `ansatz.ugate.coefficients.bn`        | List of Floats     | Coupling-term coefficients of the U gate.                                                             |
|              | `ansatz.ugate.coefficients.r`         | Float              | Scaling coefficient of the U gate.                                                                    |
|              | `ansatz.ugate.time.min`               | Float              | Minimum evolution time for the U gate.                                                               |
|              | `ansatz.ugate.time.max`               | Float              | Maximum evolution time for the U gate.                                                               |
|              | `vqe.iteration`                       | Integer            | Number of VQE iterations/restarts.                                                                    |
|              | `vqe.optimization.status`             | Boolean            | If `true`, enables classical optimization.                                                            |
|              | `vqe.optimization.algorithm`          | String             | Classical optimization algorithm used (e.g., `"SLSQP"`).                                              |
|              | `vqe.optimization.constraint`         | Boolean            | If `true`, enables constrained optimization.                                                          |
|              | `vqe.optimization.opt_options`        | Object             | Solver-specific options (e.g., `maxiter`, `disp`, `ftol`) passed to the optimizer.                    |
|              | `init_param.value`                    | String             | Method used to initialize ansatz parameters (e.g., `"random"`).                                      |
|              | `noise_profile.status`                | Boolean            | If `true`, noise is applied to the simulation.                                                        |
|              | `noise_profile.type`                  | String             | Type of noise model applied (e.g., `"time-depol"`).                                                  |
|              | `noise_profile.noise_prob`            | List of Floats     | Noise probabilities used by the noise model.                                                          |
|              | `noise_profile.noise_on_init_param`   | Object             | Settings controlling whether noise is applied to initial parameters (`status`, `value`).              |
|              | `redundant.identity_factors`          | List of Lists      | Identity-scaling factors used to generate redundant circuits.                                        |
|              | `zne.method`                          | String             | Zero-noise-extrapolation method used (e.g., `"richardson"`).                                          |
|              | `zne.degree`                          | Integer            | Polynomial degree used for the extrapolation fit.                                                    |
|              | `zne.sampling`                        | String             | Sampling strategy for extrapolation points (e.g., `'default'`, `'default-N'`, `'random-N'`).          |
|              | `zne.data_points`                     | List of Lists / Null | Data points used for extrapolation, or `null` if not applicable to this run.                       |
| **Output**   | `exact_sol`                           | Float              | Exact (analytic/diagonalized) ground-state energy of the target Hamiltonian.                          |
|              | `initial_cost_history`                | List of Floats     | Cost-function value(s) at the initial (pre-optimization) parameters.                                 |
|              | `optimized_minimum_cost`              | List of Floats     | Minimum cost-function value(s) found after optimization.                                             |
|              | `optimized_parameters`                | List of Floats     | Optimized ansatz parameter values at the minimum cost.                                               |
|              | `fun`                                 | Float              | Final cost-function value returned by the optimizer (matches `optimized_minimum_cost`).               |
|              | `success`                             | Boolean            | Whether the optimizer reported successful convergence.                                               |
|              | `message`                             | String             | Termination message returned by the optimizer.                                                       |
|              | `nit`                                 | Integer            | Number of iterations performed by the optimizer.                                                     |
|              | `nfev`                                | Integer            | Number of cost-function evaluations performed by the optimizer.                                      |
|              | `jac`                                 | List of Floats     | Final gradient (Jacobian) of the cost function at the optimized parameters.                          |
|              | `hess_inv`                            | Object / Null      | Inverse Hessian approximation returned by the optimizer, if available.                               |
