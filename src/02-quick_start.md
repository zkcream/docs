# Quick start

This page is basically ported from [README.md](https://github.com/couger-inc/cream).

[![Actions Status](https://github.com/couger-inc/cream/workflows/cream%20contract%20test/badge.svg)](https://github.com/couger-inc/cream/actions)

## Requirement

* `node` >=v11.x <=v12.x

## Setup

### Config file
Check out the [config/test.yml](https://github.com/couger-inc/cream/blob/master/config/test.yml) file for how to configure the settings:

```yml
cream:
  merkleTrees: 4
  denomination: 1000000000000000000
  recipients: [
    "0x65A5B0f4eD2170Abe0158865E04C4FF24827c529",
    "0x9cc9C78eDA7c7940f968eF9D8A90653C47CD2a5e",
    "0xb97796F8497bb84C63e650E9527Be587F18c09f8"
  ]
  zeroValue: "2558267815324835836571784235309882327407732303445109280607932348234378166811"
```

### Circuit
Make sure you set the same value of merkleTrees depth on both [config/test.yml](https://github.com/couger-inc/cream/blob/master/packages/config/test.yml) and [circuits/circom.circom](https://github.com/couger-inc/cream/blob/master/packages/circuits/circom/vote.circom).

After you finish setting the configuration, you can run:

```bash

$ npm run bootstrap && \
$ npm run build
$ ganache-cli // or cd contracts && npm run ganache

# In up another terminal
$ cd contracts && npm run migrate
```

## Test

```bash
# after finished setting:
$ npm run test
```

If you get an error after `npm run test` (probably on node version `<=10.x`), such as `Error: Cannot find module 'worker_threads'`, please run the following command.

```bash
$ export NODE_OPTIONS=--experimental-worker
```
