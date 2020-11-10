# BatchVote

## Inputs

| Pesudocode name                     | zk-SNARK input type | Description                                                                                                         |
| ----                                | ----                | ----                                                                                                                |
| `root[batch_size]`                  | Public              | A merkle root of the tree.                                                                                          |
| `nullifierHash[batch_size]`         | Public              | A value ℎ output of `ℎ =𝘏1(𝑘)`                                                                                      |
| `nullifier[batch_size]`             | Private             | A private known `𝑘` value at the time of deposit.                                                                   |
| `secret[batch_size]`                | Private             | A private know `𝑟` value at the time of deposit.                                                                    |
| `path_elements[batch_size][levels]` | Private             | A private path elements to prove the existance of the current leaf represented by `𝑂(𝜏, 𝜄)` at the time of deposit. |
| `path_index[batch_size][levels]`    | Private             | A private path index `𝜄` from merkle tree at the time of deposit.                                                   |
| `recipient[batch_size]`             | Public              | A recipient ethereum address.                                                                                       |
| `relayer[batch_size]`               | Public              | A relayer ethereum address. (optional)                                                                              |
| `fee[batch_size]`                   | Public              | A relayer fee. (optional)                                                                                           |

## Outputs

| Pesudocode name | zk-SNARK input type | Description                                                     |
| ----            | ----                | ----                                                            |
| `new_root`      | Public              | An updated merkle root of the tree after the batch transaction. |
