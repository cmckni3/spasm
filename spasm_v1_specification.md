For this challenge, you're going to be using your scripting skills to implement a "Sub-Par Assembler" dubbed: `spasm`

Your task will be to build a program that simulates some of the features of a low-level assembly language.  You may use any language you want, but the program must be named `/usr/local/bin/spasm` and meet the specifications below.  If you finish in the top 50, you will be invited back for Part 2 where we'll make the program a little more complicated... so **make sure to save your script**!

### But... what's an "assembly language"?

Normally assembly language is a very low level set of instructions you use to perform arithmetic or logical operations.  You load data into *registers* on the CPU, send an instruction to perform an *operation* on the data, and then recover the result from one of the registers.  The benefit is that it gives you access directly to the internals of the computer system and allows you to perform calculations without the overhead or restrictions found in higher level languages such as Python or Ruby.  The drawback is that it's also missing a lot of convenient features found in higher level languages (ie, there's usually no concept of a "list" data type so instead you have to manage the location of the beginning and end of an array in memory yourself) and this typically leads to very large and very complex programs.

### What We're Going to Do

This challenge is to implement a simple subset of a fake assembly language.  In order to simulate the *registers* on a CPU we will use files to store our data and only implement a small set of operations.  Our *operations* will be determined by the first argument to the script, with the registers and/or data to process being passed as the remaining command line arguments.

Our *registers* are all going to be files located in `/var/lib/spasm`.  For this phase of the challenge, we are only going to need to work with 5 *registers* (note all filenames in the `/var/lib/spasm` directory are uppercase):

   1. `/var/lib/spasm/R1` - General purpose register #1
   1. `/var/lib/spasm/R2` - General purpose register #2
   1. `/var/lib/spasm/R3` - General purpose register #3
   1. `/var/lib/spasm/R4` - General purpose register #4
   1. `/var/lib/spasm/CP` - Comparison result

Your program should not allow files with any other name to be created in the `/var/lib/spasm/` directory.

*Operations* will be performed by passing an argument to the `/usr/local/bin/spasm` script and providing 2 more arguments to specify the target *register*  and either the name of another *register* or a *constant value* to be used for the operation.

 The format for an *operation* looks like:

```
# /usr/local/bin/spasm [operation] [target] [value]
```

Where:

 * `[operation]` is one of the ops listed below
 * `[target]` is one of the general purpose registers (R1-4)
 * `[value]` can be either a general purpose register (R1-4) or a constant

*Constants* (such as "100") are the actual data that is stored in the *registers* and used for the calculations in the *operations*.  They are denoted by placing a `%` sign in front of them (no spaces).  `spasm` only supports integer operations so there is no need to specify data types for the *constant values*, and only integers will be used during grading.

The first argument after the *operation* will always be a register, but the 2nd (and last) argument may be either the name of another *register* or a *constant value* (such as `%42`).

###  Operations

`spasm`  needs to support one utility operation:

 * `mov [target] [value]` - Places the `[value]` into the register specified by `[target]`

The arithmetic operations `spasm` needs to support for this first round are:

 * `add [target] [value]` - Places the sum of `[target]` and `[value]` into `[target]`
 * `sub [target] [value]` - Places the difference of `[target]` and `[value]` into `[target]`
 * `mul [target] [value]` - Places the product of `[target]` and `[value]` into `[target]`

(Yay!  No division!)  Note that `spasm` will destroy the data stored in the `[target]` after the operation is completed by overwriting it with the newly computed value.

Finally, `spasm` also needs to support doing some basic comparisons.  For these operations, you will need to put the result into the CP register (`/var/lib/spasm/CP`).  A value of `0` indicates `TRUE`, anything else is `FALSE` (Note: be sure that newline characters are not included in CP as `0\n` evaluates to `FALSE`).

 * `eq [target] [value]` - Sets `CP` to be `TRUE` if `[target]` and `[value]` are the same, else `CP` is set to `FALSE`
 * `gt [target] [value]` - Sets `CP` to be `TRUE` if `[target]` is greater than `[value]`, else `CP` is set to `FALSE`
 * `lt [target] [value]` - Sets `CP` to be `TRUE` if `[target]` is less than `[value]`, else `CP` is set to `FALSE`

Here is an example of `spasm` in action:

```
# spasm mov R1 %100          # places "100" into R1
# spasm mov R2 %98           # places "98" into R2
# spasm sub R1 R2            # places "2" into R1
# spasm mul R1 %2            # places "4" into R1
# spasm eq R1 %4             # places "0" into CP
# spasm gt R1 R2             # places "1" (or anything except "0") into CP
```

### Grading

Requirements for successfully completing this challenge are that your `spasm` script must:

1.  Be located at `/usr/local/bin/spasm` as an executable file that does not throw an error when given a valid `spasm` operation.
1. Support the utility operation: `mov`
1. Support the arithmetic operations: `add`, `sub`, and `mul`
1. Support the comparison operations: `eq`,`lt`,`gt`
1. Require that any *constant value* used in an operation be prefixed with a '%'
1. Not allow an invalid register file in `/var/lib/spasm` to be created
1. Exit with a non-zero return value if the user requests an operation that is not supported.

In order to grade your solution, we will be running a bash script that performs a series of `spasm` operations similar to the ones in the example above, and then we will be checking the resulting files in `/var/lib/spasm` for the correct values.  Be sure you use the correct filenames (including uppercase for the register filename!) for your registers.  We will be using the full path to the script of `/usr/local/bin/spasm` in our grading process.  You do not need to worry about producing any output to STDOUT/STDERR for any operation, and you don't need to worry about doing any data type checking on *constant values* input to ensure that it's an integer.

And that's about it.

Go get it done so you can tell your friends about that one time back in the day when you wrote an assembler....

And be sure to save your script!
