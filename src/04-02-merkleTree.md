# Merkle Tree circuit

## Inputs

Let `𝑂(𝜏, 𝜄)` be the path of the merkle tree `𝜏` represented by the root hash `𝑅` with the index `𝜄`.

| Pesudocode name         | zk-SNARK input type | Description                              |
| ----                    | ----                | ----                                     |
| `leaf`                  | Public              | An output of Pedersen hash function `𝐶` such that `𝐶 = 𝘏1(𝑘∥𝑟)`|
| `path_elements[levels]` | Public              | A path elements to prove the existance of the current leaf represented by`𝑂(𝜏, 𝜄)`.|
| `path_index[levels]`    | Public              | A path index `𝜄` from merkle tree. |

## Outputs

| Pesudocode name | zk-SNARK input type | Description |
| ----            | ----                | ----        |
| `root`          | Public              | A value of current merkle root `𝑅`.|
