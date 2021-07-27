# Large number calculator (longcalc)
This calculator is include and created for the SA-MP server (Pawn language).
Also, in each cell of the variable, it stores a digit of the number itself.
It performs operations with string variables: addition, subtraction, multiplication and division.

## Setting
#define CAL_MAX 20 - changing this parameter will change the maximum number of digits for large numbers.  
You can change it from 15 to 20.

# Functions of include

## cal_con
**cal_con(cal_cisin[]) - checking the number for correctness**
  
parameters:  
cal_cisin[] (input) - string containing a number (recommended size - 32 char)  
  
returned integer values:  
0 - the number is incorrect  
1 - the number is correct  

## cal_cmp
**cal_cmp(cal_cisin1[], cal_cisin2[]) - compare of two numbers**

parameters:  
cal_cisin1[] (input) - string containing a first number in compare (recommended size - 32 char)  
cal_cisin2[] (input) - string containing a second number in compare (recommended size - 32 char)  
  
returned integer values:  
0 - the numbers are equal  
1 - fisrt number > second number  
2 - fisrt number < second number

## cal_pf
**cal_pf(cal_cisin1[], cal_cisout2[]) - translate simple string value to formated string value**

parameters:  
cal_cisin1[] (input) - string containing a simple string value (recommended size - 32 char)  
cal_cisout2[] (output) - string containing a formated string value (recommended size - 40 char)  
  
returned integer values:  
0 - incorrect input string value  
1 - function has completed successful  

## cal_pp
**cal_pp(cal_cisin1[], cal_cisout2[]) - translate formated string value to simple string value**

parameters:  
cal_cisin1[] (input) - string containing a formated string value (recommended size - 40 char)  
cal_cisout2[] (output) - string containing a simple string value (recommended size - 32 char)  
  
returned integer values:  
0 - incorrect input string value  
1 - function has completed successful  

## cal_add
**cal_add(cal_cisin1[], cal_cisin2[], cal_cisout3[], cal_cmode) - the operation of addition of numbers**

parameters:  
cal_cisin1[] (input) - string containing a first summand (recommended size - 32 char)  
cal_cisin2[] (input) - string containing a second summand (recommended size - 32 char)  
cal_cisin3[] (output) - string containing a summ (recommended size - 40 char)  
cal_cmode (input) - 0 - simple output string value, 1 - formated output string value  
  
returned integer values:  
0 - overflow during addition  
1 - function has completed successful  
2 - incorrect first summand  
3 - incorrect second summand  

## cal_sub
**cal_sub(cal_cisin1[], cal_cisin2[], cal_cisout3[], cal_cmode) - the operation of substraction of numbers**

parameters:  
cal_cisin1[] (input) - string containing a minuend (recommended size - 32 char)  
cal_cisin2[] (input) - string containing a subtrahend (recommended size - 32 char)  
cal_cisin3[] (output) - string containing a difference (recommended size - 40 char)  
cal_cmode (input) - 0 - simple output string value, 1 - formated output string value  
  
returned integer values:  
0 - overflow during substraction  
1 - function has completed successful  
2 - incorrect minuend  
3 - incorrect subtrahend

## cal_mul
**cal_mul(cal_cisin1[], cal_cisin2[], cal_cisout3[], cal_cmode) - the operation of multiplication of numbers**
 
parameters:  
cal_cisin1[] (input) - string containing a first multiplier (recommended size - 32 char)  
cal_cisin2[] (input) - string containing a second multiplier (recommended size - 32 char)  
cal_cisin3[] (output) - string containing a multiplication (recommended size - 40 char)  
cal_cmode (input) - 0 - simple output string value, 1 - formated output string value  
   
returned integer values:  
0 - overflow during multiplication  
1 - function has completed successful  
2 - incorrect first multiplier  
3 - incorrect second multiplier


## cal_div
**cal_div(cal_cisin1[], cal_cisin2[], cal_cisout3[], cal_cmode) - the operation of division of numbers**

parameters:  
cal_cisin1[] (input) - string containing a dividend (recommended size - 32 char)  
cal_cisin2[] (input) - string containing a divisor (recommended size - 32 char)  
cal_cisin3[] (output) - string containing a quotient (recommended size - 40 char)  
cal_cmode (input) - 0 - simple output string value, 1 - formated output string value  
   
returned integer values:  
0 - error of overflow  
1 - function has completed successful  
2 - incorrect dividend  
3 - incorrect divisor  
4 - error of division by zero

# How to work with it

**In order to convert a number (variable or constant) to a large number, you need to use the format (or valstr) function.  
For example, we will use string variable *largenumber* as large number and integer variable *number* as the number to convert.**
```Pawn
format(largenumber, sizeof(largenumber), "%i", number);
```  
**or (but with this option, your number should be in the range from -1'410'065'407 to 1'410'065'407)**  
```Pawn
valstr(largenumber, number);
```
**The call_pp and call_pf functions are needed to add or remove apostrophes to numbers.  
Thus, if you write a function cal_pf("1000000", *largenumberapo*), the variable *largenumberapo* will contain "1'000'000".**  
  
Now we need to create a pair of large numbers to add up, and then show the player at the entrance:
```Pawn
public OnPlayerConnect(playerid)
{
    new lnumf[40];
    
    new lnum1[32];
    new lnum2[32];
    
    format(lnum1, sizeof(lnum1), "%i", 1234567891);
    format(lnum2, sizeof(lnum2), "%i", 8765432109);
    
    cal_add(lnum1, lnum2, lnumf, 1);
    
    SendClientMessage(playerid, -1, lnumf);
    
    return 1;
}
```
The player will see the message "10'000'000'000".  
  
**You CAN'T use large numbers with apostrophes in operation functions!!!**
