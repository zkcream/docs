# Contract API

You can always get the latest version of the zkC.R.E.A.M. contract source code [here](https://github.com/couger-inc/cream/blob/master/contracts/contracts/Cream.sol).

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

## User: Deposit

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
import { createDepost, toHex } from 'libcream'

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

## User: Sign Up MACI

```solidity
function signUpMaci(
  PubKey calldata pubKey,
  uint256[8] memory _proof,
  bytes32 _root,
  butes32 _nullifierHash
)
```

### Argument details

| Argument      | Description                                                                                                                                  |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| `pubKey` | user public key for MACI.|
| `_proof` | A zk-SNARK proof.|
| `_root`| The value of the root hash of the Merkle Tree.|
| `_nullifierHash` | The value of `X` of `BabyJubJub` (see [here](https://eips.ethereum.org/EIPS/eip-2494)) from the return value of `nullifier` = `𝑘` passed to `pedersenHash()`.|

## User: Publish Message

This method call MACI contract directly.

Please also see very usuful CLI tool [documentation](https://appliedzkp.github.io/maci/cli.html#user-publish-message) if you prefer to use command line interface. Or you can use [zkcream-cli](https://github.com/zkcream/zkcream-cli)

## Coordinator: Generate proof

This method call MACI contract directly.

Please also see very usuful CLI tool [documentation](https://appliedzkp.github.io/maci/cli.html#coordinator-generate-proofs) if you prefer to use command line interface. Or you can use [zkcream-cli](https://github.com/zkcream/zkcream-cli)

## Coordinator: Publish Tally Hash

```solidity
function publishTallyHash(
    string calldata _tallyHash
)
```

## Anyone: Verify tally

This method call MACI contract directly.

Please also see very usuful CLI tool [documentation](https://appliedzkp.github.io/maci/cli.html#anyone-verify-tally) if you prefer to use command line interface.

## Coordinator: Withdraw

```solidity
function withdraw (
    uint256 _index
)
```

### Argument details

| Argument      | Description                                                                                                                                  |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| `index` | Index of recipient |

### Usage

```javascript
// Get a published tallyHash and recipients from zkCream contract
const hash = await zkCreamInstance.tallyHash()
const recipients = await zkCreamInstance.getRecipients()

const r_tally = await get('ipfs/' + hash)
const resultsArr = r_tally.data.results.tally

for (let i = 0; i < recipients.length; i++) {
    const count = resultsArr[i]
    for (let j = 0; j < count; j++) {
        const tx = await zkCreamInstance.withdraw(i)
        if (tx) {
            await tx.wait()
        }
    }
}

// check if recipients received a token
const r2 = await get(
    'zkcream/' + zkCreamAddress + '/' + election.recipients[0]
)
expect(r2.data[0]).toEqual(1)
```
