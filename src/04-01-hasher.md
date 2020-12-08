# Hasher circuit

The hasher circuit computes the Pedersen hash value of the given inputs.

## Inputs

Both `nullifier` and `secret` values are generated when a user deposits a token into a voting contract.

| Pseudocode name | zk-SNARK input type | Description |
| ----            | ----                | ----        |
| `nullifier`     | Public              | A random `𝑘` value such that `𝑘 ∈ 𝔹248`.|
| `secret`        | Public              | A random `𝑟` value generated such that `𝑟 ∈ 𝔹248`.|

## Outputs

The outputs of the Hasher circuit are computed outputs of hash function `𝘏1` such that `𝘏1:𝔹 → ℤp`. 

Let `𝘏1` be the Pedersen hash function which is imported from `circomlib` library [here](https://github.com/iden3/circomlib/blob/master/circuits/pedersen.circom).

| Pesudocode name | zk-SNARK input type | Description                        |
| ----            | ----                | ----                               |
| `commitment`    | Public              | A value `𝐶` such that `𝐶 = 𝘏1(𝑘∥𝑟)`. | 
| `nullifierHash` | Public              | A value `ℎ` output of `ℎ = 𝘏1(𝑘)`. |

