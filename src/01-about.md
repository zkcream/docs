# About

**[C.R.E.A.M](https://github.com/couger-inc/cream)** stands for **Confidential Reliable Ethereum Anonymous Mixer**. It is a protocol being developed as part of a pilot program to develop a more robust, accessible, secure, anonymous and verifiable voting technology for elections and situations that require voting.

The protocol consists of a smart contract and a zero-knowledge component. C.R.E.A.M smart contract handles the validation of voting status, permissions and proofs on-chain. The zero-knowledge component works off-chain, allowing the user to generate proofs, and if these proofs are valid, the smart contract can update the state.

## System designning

C.R.E.A.M aims to be simple in design, with the basic functions being "deposit" which means reception and "drawer" which means voting. 

To ensure the secrecy of the vote, the voter generates a random value on their device when they make a deposit. Anyone who has a knowledge of this random value can withdraw it, making the source of the token (i.e. the address where the deposit was made) secret.

### Basic feature

Here's what you'll need to do to set it up in a nutshell:

1. Set required deposit amount.
2. Set recipients(candidates) ethereum address.

All other election-specific parameters are automatically passed to the constructor at contract deployment time. You can check the configuration in the source code [here](https://github.com/couger-inc/cream/blob/master/config/test.yml).

