Command Line Options

For this round spasm will only accept a single command line argument which is the name of the file it should read in order to load the program. The spasm interpreter will read a list of instructions to perform from this file in the format of:

[operation] [target] [value]

It does not need to support comments or blank/empty lines, and there will only be one instruction per line in the files used for grading.
New Register

This version of spasm must now support a 6th register in /var/lib/spasm called SP. The purpose of the SP register is to hold the value of the line number of the instruction that will be executed next. Upon startup of spasm, this register should be set to 0 and incremented by 1 upon successful completion of each instruction after it has been executed.

Note that SP is the only register that should be set to 0 upon spasm starting. All other valid registers should retain their values from previous runs.
New Operations

We're also going to add in some new operations to this round in order to allow spasm to handle some branching logic and make it a little more sophisticated. Here's a list of the new stuff that spasm will need to support:

    label [value] - declares a label to be used for jumping... no operation on the registers should be executed and spasm should move to the next instruction
    jump [value] - causes spasm to load the specified label into the SP register and execute it as as the next instruction
    jtrue [value] - causes spasm to load the specified label into the SP register and execute it as the next operation only if the value of CP is TRUE (ie, 0)
    jfalse [value] - causes spasm to load the specified label into the SP register and execute it as the next operation only if the value of CP is FALSE (ie, anything execpt 0)
    print [register] - causes spasm to print the value in the register and a newline character (\n) to STDOUT
    exit [value] - causes spasm to exit and return a code of value to the operating system (note: this value will always be an integer and it does not need the % prefix)

Grading

Your solution will be graded by running several spasm programs and examining the output and the contents of the registers after execution. You should focus on implementing the exit operation first as it will be used to determine that your solution is executing correctly.

Some example scripts that you can use to check your solution have been provided in /root/files/examples/

The 'qbert.spasm' program should always exit with a value of '14' and never with a value of '0' and is an example of how the jump operation and label feature should work.

The countdown.spasm program contains example of a simple loop and should print out a countdown from 100 to 30 before exiting with a value of '16'.

Good luck! Remember, you're free to use any tools or language you want to solve the scenario.
