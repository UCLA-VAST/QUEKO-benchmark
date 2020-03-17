# QUEKO - Quantum Mapping Examples with Known Optimal

This is the benchmark circuits used in this [paper](https://arxiv.org/abs/2002.09783).
```
@misc{tan2020optimality,
    title={Optimality Study of Existing Quantum Computing Layout Synthesis Tools},
    author={Bochen Tan and Jason Cong},
    year={2020},
    eprint={2002.09783},
    archivePrefix={arXiv},
    primaryClass={quant-ph}
}
```

The device layouts can be found in `CONNECTION.py`, where `INDEX_CONNECTION_LIST` stores all the edges in the corresponding device layouts as tuples of qubit indices.

Generally, the set-up parameters of every QUEKO benchmark can be read off from its name:
- Device graph (`16QBT` is Rigetti Aspen-4, `20QBT` is IBM Tokyo, `53QBT` is IBM Rochester, `54QBT` is Google Sycamore)
- Optimal depth (`**CYC` means the optimal solution has `**` cycles)
- Gate density vector (`TFL` is [Toffoli gate](https://en.wikipedia.org/wiki/Toffoli_gate), `QSE` is quantum supremacy experiment[1])
- The serial number of its meta file (from `0` to `9`)

`BNTF` are **b**enchmarks that are **n**ear-**t**erm **f**easible (depth 5, 10, ..., 45). There are two sets of benchmarks: 1) Aspen-4 as device and TFL gate density, 2) Sycamore as device and QSE gate density.

`BSS` are **b**enchmarks for **s**calability **s**tudy (depth 100, 200, ..., 900). All four devices are tested.

`BIGD` are **b**enchmarks for **i**mpact of **g**ate **d**ensity on depth ratio. For all the `BIGD` benchmarks, the device is IBM Tokyo, the depth is 45. Their name also indicates the gate density vector (`_.0S1_.5S2` means the gate density vector components d1=0 and d2=0.5).

The benchmarks are `qasm` files easily derived from meta files. All the meta files are in `meta` folder. They are `csv` files of which each row is a cycle of gates. In every row of a meta file, there are multiple entries: a single integer means a single-qubit gate on the qubit with this index, an integer tuple means a two-qubit gate on the two qubits with those indices. Since we are only focusing on legalizing all the two-qubit gates under the device layout constraints, we only care about the qubits they use, not specifically what gates they are. For example, whether a two-qubit gate is a CZ gate or a CX gate makes no difference.

Accompanying each meta file, there is also a `solution` file. It contains the optimal mapping of the corresponding meta file. If the first line of solution files is `5`, then the optimal mapping for `q[0]` in the benchmark is physical qubit with index `5`. The second line stands for the optimal mapping of `q[1]`...

[1]: Arute, F., Arya, K., Babbush, R. _et al_. Quantum supremacy using a programmable superconducting processor. _Nature_ __574__, 505–510 (2019). [https://doi.org/10.1038/s41586-019-1666-5](https://doi.org/10.1038/s41586-019-1666-5)
