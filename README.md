# Spasm

My implementation of `spasm` for the [TrueAbility Linux Showdown 8](https://trueability.com/assembler-challenge)

## Requirements

* [Ruby 1.9.3+](https://www.ruby-lang.org/en)

## Specification

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

* Value may be a constant (integer) preceded by `%`
* Value may be another register

## Usage

```bash
./spasm examples/countdown.spasm
```

