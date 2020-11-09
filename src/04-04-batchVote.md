# BatchVote

## Inputs

| Pesudocode name                     | zk-SNARK input type | Description |
| ----                                | ----                | ----        |
| `root[batch_size]`                  | Public              |             |
| `nullifierHash[batch_size]`         | Public              |             |
| `nullifier[batch_size]`             | Private             |             |
| `secret[batch_size]`                | Private             |             |
| `path_elements[batch_size][levels]` | Private             |             |
| `path_index[batch_size][levels]`    | Private             |             |
| `recipient[batch_size]`             | Public              |             |
| `relayer[batch_size]`               | Public              |             |
| `fee[batch_size]`                   | Public              |             |

## Outputs

| Pesudocode name | zk-SNARK input type | Description |
| ----            | ----                | ----        |
| `new_root`      | Public              |             |
