# Hasher circuit

Hasher circuit computes the Pedersen hash value of given inputs.

## Inputs

Both `nullifier` and `secret` values are generated when a user deposits a token into a voting contract.

| Pesudocode name | zk-SNARK input type | Description |
| ----            | ----                | ----        |
| `nullifier`     | Public              | A random `𝑘` value such that `𝑘 ∈ 𝔹248`.|
| `secret`        | Public              | A random `𝑟` value generated `𝑟 ∈ 𝔹248`.|

## Outpus

The outputs of Hasher circuit are computed outputs of hash function `𝘏1` such that `𝘏1:𝔹 → ℤp`. 

Let `𝘏1` is Pedersen hash function which is imported frbbom `circomlib` library [here](https://github.com/iden3/circomlib/blob/master/circuits/pedersen.circom).

| Pesudocode name | zk-SNARK input type | Description                        |
| ----            | ----                | ----                               |
| `commitment`    | Public              | A value `𝐶` such that `𝐶 = 𝘏1(𝑘∥𝑟)`. | 
| `nullifierHash` | Public              | A value `ℎ` output of `ℎ = 𝘏1(𝑘)`. |

