# Usage

## Simple anonymous voting

Let's take a simple vote as an example.

### Configurations

The following are the minimum settings needed to deploy the contract and use zkC.R.E.A.M.

```yml
cream:
  merkleTrees: 4
  recipients: [
    "0x65A5B0f4eD2170Abe0158865E04C4FF24827c529",
    "0x9cc9C78eDA7c7940f968eF9D8A90653C47CD2a5e",
    "0xb97796F8497bb84C63e650E9527Be587F18c09f8"
  ]
  zeroValue: "2558267815324835836571784235309882327407732303445109280607932348234378166811"

maci:
  initialVoiceCreditBalance: 100
  signUpDurationInSeconds: 3600 # 1 hour
  votingDurationInSeconds: 3600 # 1 hour
  coordinatorPrivKey: "2222222222263902553431241761119057960280734584214105336279476766401963593688"
  tallyBatchsize: 4
  messageBatchSize: 4
  quadVoteTallyBatchSize: 4
  voteOptionsMaxLeafIndex: 3

  merkleTrees:
    stateTreeDepth: 4
    messageTreeDepth: 4
    voteOptionTreeDepth: 2

  chain:
	privateKeysPath: './'
```

| Property       | Description                                                                                                                  |
|----------------|------------------------------------------------------------------------------------------------------------------------------|
| `merkleTree`   | Specify the size of the merkle tree for managing the history of deposits. The size of the tree is `2**N`.                    |
| `denomination` | The total amount of tokens needed for the `deposit()` function call.                                                          |
| `recipients`   | An array of ethereum addresses to be candidates for the ballot.                                                              |
| `zeroValue`    | Zero value which defined at `Cream.sol`. It is pre-calculated as `uint256(keccak256(abi.encodePacked('cream'))) % FIELD_SIZE`. |

### Deposit

The implementation of deposits is described in detail in the [#Deposit](./05-contract_api.html#deposit) section of the Contract API.

### Withdraw

The implementation of withdrawal is described in detail in the [#Withdraw](./05-contract_api.html#withdraw) section of the Contract API.
