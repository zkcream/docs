# libcream

## Types

**`SnarkBigint`**

A big integer type compatible with the `cream-merkle-tree` [library](https://github.com/kazuakiishiguro/cream-merkle-tree). This type was ported from `snarkjs =< 0.1.20` library.

## Interfaces

**`PedersenHash`**

Encupslates an outputs of `pedersenHash()` function.

```typescript
interface PedersenHash {
    babyJubX: SnarkBigInt,
    babyJubY: SnarkBigInt
}
```

**`Deposit`**

Encapsulates some of the information essential to create a Snark proof. It provides an output interface to the `createDeposit()` method.

```typescript
interface Deposit {
    nullifier: SnarkBigInt,
    secret: SnarkBigInt,
    preimage: SnarkBigInt,
    commitment: SnarkBigInt,
    nullifierHash: SnarkBigInt
}
```

## Functions

**`pedersenHash`**

Function to hash the given value and return a value of type along the `PedersenHash` interface.

```typescript
const pedersenHash (
	value: SnarkBigInt
): PedersenHash => {}
```

**`createDeposit`**

Function to return a value of type along the `Deposit` interface from given 2 values, nullifier and secret.

```typescript
const createDeposit (
	nullifier: SnarkBigInt,
	secret: SnarkBigInt
): Deposit => {}
```

**`generateDeposit`**

Generates a type along the Deposit interface from a given string.

```typescript
const generateDeposit (
	note: string
): Deposit => {}
```

**`toHex`**

Returns a string in hexadecimal format from the passed values and optionally specifies the length of the string (default `length = 32`).

```typescript
const toHex (
	n: SnarkBigInt,
	length = 32
	): string => {}
```

**`rbigInt`**

Function to return a random integer of type `SnarkBigInt` for a given number of bytes.

```typescript
const rbigInt = (
    nbytes: number
): SnarkBigInt => {}
```
