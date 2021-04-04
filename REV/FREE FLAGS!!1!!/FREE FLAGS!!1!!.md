# FREE FLAGS!!1!!

## Description

Clam was browsing armstrongctf.com when suddenly a popup appeared saying "GET YOUR FREE FLAGS HERE!!!" along with [a download](./free_flags). Can you fill out the survey for free flags?

Find it on the shell server at /problems/2021/free_flags or over netcat at nc shell.actf.co 21703.

Author: aplet123

### Hint

Check out decompilers like GHIDRA.

## Approach

I did indeed check out [GHIDRA](https://ghidra-sre.org/) as the hint said and now I'm glad to say I finally how some semblance of how to use it ~~that's probably a lie guys~~

I loaded the [file](./free_flags) into GHIDRA and clicked on the main function under Symbol Tree which is located on the left side of the layout. (if someone actually reads this and requests it, I'll make a video walkthrough assuming I stil remember how to solve this).

This showed the code on the right side of the screen:

```cpp
undefined4 main(void)

{
  int iVar1;
  size_t sVar2;
  long in_FS_OFFSET;
  undefined4 local_128;
  int local_124;
  int local_120;
  int local_11c;
  char local_118 [264];
  long local_10;
  
  local_10 = *(long *)(in_FS_OFFSET + 0x28);
  puts(
      "Congratulations! You are the 1000th CTFer!!! Fill out this short survey to get FREE FLAGS!!!"
      );
  puts("What number am I thinking of???");
  __isoc99_scanf("%d",&local_11c);
  if (local_11c == 0x7a69) {
    puts("What two numbers am I thinking of???");
    __isoc99_scanf("%d %d",&local_120,&local_124);
    if ((local_120 + local_124 == 0x476) && (local_120 * local_124 == 0x49f59)) {
      puts("What animal am I thinking of???");
      __isoc99_scanf(" %256s",local_118);
      sVar2 = strcspn(local_118,"\n");
      local_118[sVar2] = '\0';
      iVar1 = strcmp(local_118,"banana");
      if (iVar1 == 0) {
        puts("Wow!!! Now I can sell your information to the Russian government!!!");
        puts("Oh yeah, here\'s the FREE FLAG:");
        print_flag();
        local_128 = 0;
      }
      else {
        puts("Wrong >:((((");
        local_128 = 1;
      }
    }
    else {
      puts("Wrong >:((((");
      local_128 = 1;
    }
  }
  else {
    puts("Wrong >:((((");
    local_128 = 1;
  }
  if (*(long *)(in_FS_OFFSET + 0x28) == local_10) {
    return local_128;
  }
                    /* WARNING: Subroutine does not return */
  __stack_chk_fail();
}
```

This part requires some careful analysis:

```cpp
puts("What number am I thinking of???");
__isoc99_scanf("%d",&local_11c);
if (local_11c == 0x7a69) {
    puts("What two numbers am I thinking of???");
    __isoc99_scanf("%d %d",&local_120,&local_124);
    if ((local_120 + local_124 == 0x476) && (local_120 * local_124 == 0x49f59)) {
      puts("What animal am I thinking of???");
      __isoc99_scanf(" %256s",local_118);
      sVar2 = strcspn(local_118,"\n");
      local_118[sVar2] = '\0';
      iVar1 = strcmp(local_118,"banana");
```

### Analysis

```cpp
puts("What number am I thinking of???");
__isoc99_scanf("%d",&local_11c);
if (local_11c == 0x7a69)
```

This outputs "What number am I thinking of???" then takes the user input and stores it into the memory space of `&local_11c` (wherever that is). It then checks if the number stored in `local_11c` is equal to `0x7a69`. The `0x` prefix is a prefix meaning hex number so I converted it to a numberic value using [this site](https://www.thecalculatorsite.com/math/hex-to-decimal.php). This says the expected value is `31337`.

```cpp
puts("What two numbers am I thinking of???");
__isoc99_scanf("%d %d",&local_120,&local_124);
if ((local_120 + local_124 == 0x476) && (local_120 * local_124 == 0x49f59))
```

Alright this time it asks for two numbers and these two numbers need to add up to `0x476` as well as multiply to form `0x49f59`. I once again used [this site](https://www.thecalculatorsite.com/math/hex-to-decimal.php) which told me the sum it wanted was `1142` and the product it wanted was `302937`. ~~This reminds me of a game we used to play in math class called sum and product from when we practiced solving quadratic equations.~~ The two values of `x` in the equation are the two values

$$
x^2 + 1142x = 302937
\\
x^2 + 1142x - 302937 = 0
\\
(x - 419)(x - 723) = 0
\\
x_1 = 419
\\
x_2 = 723
$$

Alternatively just use a [factorization website](https://www.alpertron.com.ar/ECM.HTM) to solve it. The math was not that important.

```cpp
puts("What animal am I thinking of???");
__isoc99_scanf(" %256s",local_118);
sVar2 = strcspn(local_118,"\n");
local_118[sVar2] = '\0';
iVar1 = strcmp(local_118,"banana");
```

Alright no more numbers!!! This just wants an animal called "banana". I don't see why bananas can't be animals.

## Final Connection and Getting Flag

I connected to the webshell and inputted everything I found earlier:

```bash
$ nc shell.actf.co 21703
Congratulations! You are the 1000th CTFer!!! Fill out this short survey to get FREE FLAGS!!!
What number am I thinking of???
31337
What two numbers am I thinking of???
723 419
What animal am I thinking of???
banana
Wow!!! Now I can sell your information to the Russian government!!!
Oh yeah, here's the FREE FLAG:
actf{what_do_you_mean_bananas_arent_animals}
```

## Flag

actf{what_do_you_mean_bananas_arent_animals}
