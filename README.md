# Spasm

My implementation of `spasm` for the [TrueAbility Linux Showdown Part 1](https://trueability.com/assembler-challenge-round-one)

## Specification

`spasm [operation] [target] [value]`

### Operations

* mov
* add
* sub
* mul
* eq
* gt
* lt

### Registers

* R1
* R2
* R3
* R4
* CP

### Values

* Value may be an constant (integer) preceded by `%`
* Value may be another register

## Usage

```bash
./spasm mov R1 %4
```

