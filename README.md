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
* label
* jump
* jtrue
* jfalse
* print
* exit

### Registers

* R1
* R2
* R3
* R4
* CP
* SP

### Values

* Value may be an constant (integer) preceded by `%`
* Value may be another register

## Usage

```bash
./spasm examples/countdown.spasm
```

