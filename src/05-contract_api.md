# Contract API

You can always get the latest version of the C.R.E.A.M. contract source code [here](https://github.com/couger-inc/cream/blob/master/contracts/contracts/Cream.sol).

## Constructor

When you deploy the contract, you need to pass the following elements as arguments.

```solidity
constructor(
    IVerifier _verifier,
    SignUpToken _signUpToken,
    uint256 _denomination,
    uint32 _merkleTreeHeight,
    address[] memory _recipients
)
```

### Argument details

| Argument            | Description                                                                                                                                                                                                                                              |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `_verifier`         | `Verifier` contract address. This contract can be updated later with the `updateVerifer(address)` method.                                                                                                                                                       |
| `_signUpToken`      | `SignUpToken` contract address of the token to be used for voting.                                                                                                                                                                                       |
| `_denomination`     | The total amount of tokens needed for the `deposit()` function call.                                                                                                                                                                                      |
| `_merkleTreeHeight` | Specify the size of the merkle tree for managing the history of deposits. The size of the tree is `2**N`.                                                                                                                                                |
| `_recipients`       | An array of ethereum addresses to be candidates for the ballot. These arrays are passed as an argument to the method `setRecipients()` when the contract is deployed, and cannot be changed after. |

## Deposit

The call to the deposit function is a very simple process of passing a locally generated value, in this case `_commitment`, but you should not forget to send the value of `_denomination` and have a token from the `_signUpToken` token contract.

```solidity
function deposit (
    bytes32 _commitment
)
```

### Argument details

| Argument      | Description                                                                                                                                  |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| `_commitment` | The value of a client-generated commitment. The function `pedersenHash(nullifier, secret)` is used to generate the value of this commitment. |

### Usage

```javascript
const instance = await Cream.deployed()
const tokenContract = await SignUpToken.deployed()

// setApprovalforall for token transfer
await tokenContract.giveToken(voter)
await tokenContract.setApprovalForAll(instance.address, true, { from: voter })

// deposit
const deposit = createDeposit(rbigInt(31), rbigInt(31))
const tx = await instance.deposit(toHex(deposit.commitment), { from: voter })
truffleAssert.eventEmitted(tx, 'Deposit')
```

## Withdraw

```solidity
function withdraw (
    bytes calldata _proof,
    bytes32 _root,
    bytes32 _nullifierHash,
    address payable _recipient,
    address payable _relayer,
    uint256 _fee
)
```

### Argument details

| Argument      | Description                                                                                                                                  |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| `_proof` | A zk-SNARK proof.|
| `_root`| The value of the root hash of the Merkle Tree.|
| `_nullifierHash` | The value of `X` of `BabyJubJub` (see [here](https://eips.ethereum.org/EIPS/eip-2494)) from the return value of `nullifier` = `𝑘` passed to `pedersenHash()`.|
| `_recipient` | Candidate's Ethereum address. Passing an address other than the one specified in the constructor call will cause the transaction to be reverted. |
| `_relayer` | Relayer address.|
| `_fee` | Relayer fee.|

### Usage

```javascript
// Deposit
const deposit = createDeposit(rbigInt(31), rbigInt(31))
tree.insert(deposit.commitment)
await instance.deposit(toHex(deposit.commitment), { from: voter })

// Update tree
const root = tree.root
const merkleProof = tree.getPathUpdate(0)

// Create an input
const input = {
  root,
  nullifierHash: pedersenHash(deposit.nullifier.leInt2Buff(31)).babyJubX,
  relayer: relayer,
  recipient,
  fee,
  nullifier: deposit.nullifier,
  secret: deposit.secret,
  path_elements: merkleProof[0],
  path_index: merkleProof[1]
}

let isSpent = await instance.isSpent(toHex(input.nullifierHash))
assert.isFalse(isSpent)

const {
  proof,
} = await genProofAndPublicSignals(
  input,
  'prod/vote.circom',
  'build/vote.zkey',
  'circuits/vote.wasm'
)

const args = [
  toHex(input.root),
  toHex(input.nullifierHash),
  toHex(input.recipient, 20),
  toHex(input.relayer, 20),
  toHex(input.fee)
]

const proofForSolidityInput = toSolidityInput(proof)

// Create withdraw tx
const tx = await instance.withdraw(proofForSolidityInput, ...args, { from: relayer })

truffleAssert.eventEmitted(tx, 'Withdrawal')
```
