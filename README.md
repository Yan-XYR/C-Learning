Program Structure:  

The "main" function and one or more other functions may be in a file. There are no procedures, a function may be used like a procedure with the function return value, if any, just ignored. Files are compiled with the C compiler that can produce an executable file.
一个文件中必有一个main主函数和若干其他函数。编译器成功编译后生成可执行文件。

Some typical file structures: 常见形式

int main()                            /* This could be a complete program
*/
{
  sequence_of_statements
  return 0;
}

#include <stdio.h>
#include ...     more header files from which definitions are needed
global and/or external declarations and/or type definitions
int main()                     /* main function and other functions  */
{                              /* in same file                       */
  local_declarations
  sequence_of_statements
  return 0;
}

void function_1( int i, double x, more_parameters )
                      /* function definitions can NOT be nested */
                      /* flat name space, make all function names unique */
{
  local_declarations
  sequence_of_statements
  /* no return needed at end of function when return tyoe is 'void' */
}

some_type function_2( void )
{
  local_declarations
  sequence_of_statements
  return something-of-some_type;
}                              /* as many functions as desired       */

#include <stdio.h>          
/* a main function that can get command line arguments */
global and/or external declarations

void main(int argc, char *argv[])
    /* argc, the number of command line items                   */
    /* argv, command line items including calling name as [0]   */
{
  local_declarations
  sequence_of_statements
}

Executable statements: 可执行声明

Statements end with a semicolon or brace. A compound statement may be made from a sequence of statements by enclosing them in braces.

声明以分号；或者花括号{结束，复合声明可以包含一系列的声明在花括号中。
{ statement_1 ; statement_2 ; statement_3 ; } 

is a statement but usually
{ /* make code readable, one statement per line. */ statement_1; statement_2; statement_3; }
Assignment statements 赋值声明

  x = 10;
  x = x+1;
  ++x;                /* same as x = x+1; */
  x++;                /* same as x = x+1;  sets a false flag to true */
  --x;                /* same as x = x-1; decrements x then uses value*/
  x--;                /* same as x = x-1; uses x then decrements value*/
  x = x+20;
  x += 20;            /* same as x = x+20; add */
  x -= 20;            /* same as x = x-20; subtract */
  x *= 20;            /* same as x = x*20; multiply */
  x /= 20;            /* same as x = x/20; divide */
  x %= 20;            /* same as x = x%20; modulo */
  x <<= 2;            /* same as x = x<<2; shift left */
  x >>= 2;            /* same as x = x>>2; shift right */
  x &= 20;            /* same as x = x&20; bit by bit and*/
  x ^= 20;            /* same as x = x^20; bit by bit exclusive or */
  x |= 20;            /* same as x = x|20; bit by bit or */
  x = (y=3,y++);      /* same as y=3; x=y; y=y+1; */
  x = who ? 3 : y;    /* same as if(who)x=3; else x=y; */
  y = sin(x) ;        /* function call use #include <math.h>  */
  x = mat[i][j] ;     /* subscripting two dimensional array  */

Function call with return ignored:  调用返回会忽略的函数

  go_do_it();         /* actual parameters are optional              */
  exit(0);            /* special function that terminates execution  */
Unconditional branches: 无条件连接

  break;              /* immediate exit from loop or switch          */

  continue;           /* immediate jump to end of loop ( not exit )  */
                      /* also used to exit a switch in a loop        */

  return;             /* immediate exit from function, no value      */
  return exp;         /* exit from function returning value of exp   */

  goto label;         /* unconditional jump                          */

label: statement;     /* label definition                            */

Conditional branching: 有条件连接

  if ( condition ) statement ;  /* basic form of if statement */

  if ( condition ) statement ;
  else statement_2 ;            /* optional  else  clause */

  if ( condition_1 )
     if ( condition_2 ) statement ;
     else statement_2 ;         /* else  belongs to closest previous if */

  if ( expression )           /* condition may be any expression        */
  {                           /* zero value is false, non zero is true  */
     statement_sequence       /* { } may enclose sequence of statements */
  }
  else
  {                           /* it is good to use braces, safer for    */
     statement_sequence       /* updates to code later.                 */
  }

  if-else-if ladder structure (must be space in  'else if')

  if(exp_1)             /*  the first expression that is true, e.g. exp_i */
       statement_1;     /*  causes statement_i to be executed             */
  else if(exp_2)        /*  then jump to end after statement_n            */
       statement_2;
  else if(exp_3)
       statement_3;
  ...
  else
       statement_n;     /*  executed if no exp_i was true, else skipped   */


Switch statement  Switch声明



  switch ( expression )      /* constants must be unique              */
  {
      case constant_1:       /* do nothing for this case              */
         break;
      case constant_2:       /* drop through and do same as constant_3*/
      case constant_3:
         statement_sequence  /* can have but does not need  { }       */
         break;
      case constant_4:
         statement_sequence  /* does this and next */
                             /* statement_sequence also*/
      case constant_5:
         statement_sequence
         break;
      default:               /* default executes if no constant equals*/
         statement_sequence  /* the expression. This is optional      */
 }



Iteration statements 重复（遍历）声明



  for ( initialization ; condition ; increment ) statement ;
                                  /* The flow sequence is :              */
                                  /*    initialization                   */
                                  /*    test condition and exit if false */
                                  /*    statement                        */
                                  /*    increment                        */
                                  /*    loop back to test condition      */

  while ( condition ) statement ; /* keep repeating statement until the */
                                  /* condition is false, zero. This is */
                                  /* classical C thinking, rather than saying*/
                                  /* keep repeating while condition is true*/

  do                              /* another form of the 'while statement'*/
  {                               /* always execute once before testing   */
    statement_sequence
  } while ( condition ) ;         /* test for finished at the end, all    */
                                  /* other loops test first               */

  for(;;) statement;              /* infinite loop, break; can get out    */
                                  /* return and exit() can also get out   */
  while(1) statement;             /* another form of infinite loop        */
                                  /* this version is called an endless    */
                                  /* and must have something else to      */
                                  /* terminate the loop                   */

  in all iteration statements,  break; causes an immediate exit from loop
                                continue; causes an immediate increment



Function definition 函数定义

Function Prototype 样板



  type function_name(type_1 var_1, type_2 var_2,...);
                            /* e.g. double sin(double x);                 */
                            /* char * strcpy(char * s1, const char * s2); */
                            /* causes the compile to do type checking     */
                            /* const says s2 is an 'in' parameter         */
   /* a prefix of  static  makes the function visible only in this file */



Function Definition



  type function_name(int a, float b, const char * ch,...)
  { function_body }

  /* only parameters passed by address can are modified*/
  /* in the calling function, local copy can be modified*/
  char * strcpy( char * s1, const char * s2 ) { statements }

  type function_name(a, b)    /* older form of definition, DO NOT USE ! */
  int a;
  float b;
  { function_body }           /* same as combined parameters above */



example of a function and call passing the address of a scalar



     void func(int *num)
     {
         *num *= *num; /* square num back in its place */
     } ...

     func(&i); /* call, passing address of i, the lvalue of i */



Reserved words 保留名字（不能自定义）

    
Like everything else, must be lower case. (exactly 32 reserved words)
term
Description
auto 
optional local declaration 
break 
used to exit loop and used to exit switch 
case 
choice in a switch 
char 
basic declaration of a type character 
const 
prefix declaration meaning variable can not be changed 
continue 
go to bottom of loop in for, while and do loops 
default 
optional last case of a switch 
do 
executable statement, do-while loop 
double 
basic declaration double precision floating point 
else 
executable statement, part of "if" structure 
enum 
basic declaration of enumeration type 
extern 
prefix declaration meaning variable is defined externally 
float 
basic declaration of floating point 
for 
executable statement, for loop 
goto 
jump within function to a label 
if 
executable statement 
int 
basic declaration of integer 
long 
prefix declaration applying to many types 
register 
prefix declaration meaning keep variable in register 
return 
executable statement with or without a value 
short 
prefix declaration applying to many types 
signed 
prefix declaration applying to some types 
sizeof 
operator applying to variables and types, gives size in bytes 
static 
prefix declaration to make local variable static 
struct 
declaration of a structure, like a record 
switch 
executable statement for cases 
typedef 
creates a new type name for an existing type 
union 
declaration of variables that are in the same memory locations 
unsigned 
prefix declaration applying to some types 
void 
declaration of a typeless variable 
volatile 
prefix declaration meaning the variable can be changed at any time 
while 
executable statement, while loop or do-while loop 


Declarations have the forms 声明格式



  basic_type variable ;

  basic_type variable_1, variable_2=value;  /* only initializes variable_2  */

  prefix_type(s) basic_type modifier_type variable_1, variable_2 ,... ;

  type variable[val][val]...[val]={data,data,...}; /*multidimensional array*/

  struct struct_name {                 /* struct_name is optional */
     type variable_1;                  /* any declaration */
     type variable_2;                  /* all variable names must be unique*/
         ...
     type variable;
  } variable_1, variable_2, ... ;      /* variables are optional */

  struct struct_name {                 /* struct_name is optional */
     type variable_1: length;          /* any declaration : length in bits */
     type variable_1: length;          /* type is int, unsigned or signed */
         ...
     type variable_n: length_n;
  } variable_1, variable_2, ... ;      /* variables are optional, they can */
                                       /* also be arrays and pointers */

  struct struct_name more_variables;   /* struct_name becomes a type */

  union union_name {                   /* union_name is optional */
    type variable_1;                   /* variable_1 overlays variable_2 */
    type variable_2;
        ...
    type variable_n;
  } variable_a, variable_b, ...;       /* variables are optional */

  union union_name variable ;          /* use an existing union definition */

  enum enum_type                       /* enum_name is optional */
  { enumeration_name_1,                /* establishes enumeration literals */
    enumeration_name_2=number,         /* optional number, */
      ...                              /* default is 0, 1, 2, ... */
    enumeration_name_n
  } variable, variable, ...;           /* variables are optional */

  enum enum_type variable;             /* use an existing enum definition */

  enum enum_type variable = enumeration_name;

  typedef existing_type new_type_name ; /* e.g. typedef unsigned int size_t */
      /* use dot notation to select a component of a struct or union */



Basic types 基本数据类型

Type
Description


char 
character type, usually one byte ( a string is array of char ) 


int 
integer type, usually 2 or 4 bytes ( default ) 


float 
floating point type, usually 4 bytes 


double 
floating point type, usually 8 bytes 


void 
no type, typeless 


enum 
enumeration type ( user defines the type name ) 




Type modifiers, prefix for basic types 可用来改变基本数据类型的前缀

Modifiers
Description


signed 
has a sign ( default ) 


unsigned 
no sign bit in variable 


long 
longer version of type (short or long alone means short int or 


short 
shorter version of type long int because int is the default) 


const 
variable can not be stored into 





Storage class, prefix for types  指定数据类型生效范围的前缀

Prefix
Description


auto 
local variable ( default ) 


static 
permanent when function exits, not auto 


volatile 
can change from outside influence 


extern 
variables are defined elsewhere, externally 


register 
assign variable to register 





Modifier type 


  *         makes variable a pointer

     int i = 1000;   /* allocate storage and initialize value to 1000 */
     int *ptr;       /* allocate storage for a pointer, garbage initially */
     ptr = &i;       /* ptr now points to i */
     *ptr = 100;     /* change value of i to 100 */



Samples of variable declarations 变量声明例子



  auto int xyz;            /* int no longer is default */
  unsigned long int pqr;
  extern int global_stuff, remote_function();
  register int quick;
  void just_do_it();   /* called a function prototype  */
  char * ch;           /* a pointer to a character     */
  char * argv[];       /* an array of strings          */
  struct account       /* type definition for structure 'account' */
  {
    char name[20];     /* name is 19 characters and a null */
    float bal;
    unsigned int sex:1; /* sex needs only 1 bit but probably uses a word */
  } person;            /* person is a variable, object in memory         */
  struct account *p;
  p=&person;           /* p is pointer to person */
  (*p).bal=100.00;     /* older usage */
  p->bal=100.00;       /* better usage, means same as above */



Automatic setting of array size based on data



  char msg[]="Set the size to correct length \n";
  char *p="auto length";
  char ary[3]="Element in an array of messages"; /* 3 items, 0,1 and 2 */
  float matrix[][3]={1.,2.,3.,4,.5.,6.};      /* fills in blank with 6 */
  float ***a;  /* (a+10)[0][0][0] is a way to index 3 dimensional array*/



Getting storage



  int *p;
  p=(int *)malloc(50*sizeof(int)); /* or p=(int *)calloc(50*sizeof(int)); */
  free(p);



Expressions




                  octal and hexadecimal
                  01777  0x248fff

                  long decimal, octal and hexadecimal
                  123456789L  017777777L  oxFFFFFFFFL
variable names 
1 to 32 characters including alphabetic, numeric and underscore
  some_name  ELSE  Else  z999 
numbers 
integer and floating point like in FORTRAN
1  12345  .1  1.  1.5E-20 
character 
single character between apostrophes plus special backslash codes
'a'  'Z'  '\n' 
string 
characters between quotes plus special backslash codes a null is automatically placed at end of every string
"Hello"  "good by \n" 

let exp, exp1, exp2, exp3  etc. stand for expressions


expressions are:

  variables
  numbers
  characters
  strings
  unary_operator expression
  expression binary_operator expression
  ( expression )
  variable post_operator    ( ++ and -- )



operator precedence and associativity is


highest
LR 
( ) [ ] -> . x++ x-- 
RL 
! ~ - + ++x --x * & sizeof (type) 
LR 
* / % 
LR 
+ - 
LR 
<< >> 
LR 
< <= > >= 
LR 
== != 
LR 
& 
LR 
^ 
LR 
| 
LR 
&& 
LR 
|| 
RL 
? : 
RL 
= += -= *= /= %= >>= <<= &= ^= |= 
LR 
, 

lowest
LR means associate left to right, RL means associate right to left

This is why  a = b = c = 1;  /* works, a,b and c get set to 1 */
But          int a,b,c = 1;  /* fails, only c gets set to 1   */
             *p++ = -x->y;   /* is ((*p)=(-(x->y)), p++)      */



operator definitions :



  ( )  grouping parenthesis, function call
  [ ]  array indexing, also  [ ][ ]  etc.
  ->   selector, structure pointer  employee->wage = 7.50 ;
  .    select structure element     employee.wage = 7.50 ;
  !    relational not, complement, ! a  yields true or false
  ~    bitwise not, ones complement, ~ a
  ++   increment, pre or post to a variable
  --   decrement, pre or post to a variable
  -    unary minus, - a
  +    unary plus,  + a
  *    indirect, the value of a pointer,  * p is value at pointer p address
  &    the memory address, & b is the memory address of variable b
  sizeof  size in bytes,   sizeof a     or  sizeof (int)
  (type)  a cast, explicit type conversion,  (float) i, (*fun)(a,b), (int*)x
  *    multiply, a * b
  /    divide, a / b
  %    modulo, a % b
  +    add, a + b
  -    subtract, a - b
  <<   shift left,  left operand is shifted left by right operand bits
  >>   shift right, left operand is shifted right by right operand bits
  <    less than, result is true or false,  a %lt; b
  <=   less than or equal, result is true or false,  a <= b
  >    greater than, result is true or false,  a > b
  >=   greater than or equal, result is true or false, a >= b
  ==   equal, result is true or false,  a == b
  !=   not equal, result is true or false,  a != b
  &    bitwise and,  a & b
  ^    bitwise exclusive or,  a ^ b
  |    bitwise or,  a | b
  &&   relational and, result is true or false,  a < b && c >= d
  ||   relational or, result is true or false,  a < b || c >= d
  ?     exp1 ? exp2 : exp3  result is exp2 if exp1 != 0, else result is exp3
  =    store
  +=   add and store
  -=   subtract and store
  *=   multiply and store
  /=   divide and store
  %=   modulo and store
  <<=  shift left and store
  >>=  shift right and store
  &=   bitwise and and store
  ^=   bitwise exclusive or and store
  |=   bitwise or and store
  ,    separator as in   ( y=x,z=++x )

  zero evaluates to false ( a null pointer has a zero value )
  non zero evaluates to true ( !null_pointer is true )
  * is heavily overloaded, so is &

Backslash codes for in character constants and strings


These can be used as characters when enclosed in apostrophies

  \a  alert, audible alarm, bell, ^G
  \b  Backspace, ^H
  \f  Form feed, new page, ^L
  \n  New line, carriage return and line feed, ^M^J
  \o  Octal constant, \oddd, \ddd
  \r  Carriage return, no line feed, ^M
  \t  Horizontal tab, tab, ^I
  \v  Vertical tab, ^K
  \x  Hexadecimal constant,  \xdd    0 <= d <= F
  \0  null, zero value character, ^@
  \"  Quote character
  \'  Apostrophe character
  \\  Backslash character
  \?  Question mark character
  \ddd  Octal character value 0 <= d <= 7



Format commands for printf() scanf() fprintf(), fscanf() sprintf() sscanf()

  %c  a single character, char
  %d  a decimal number, int   %hd is for short  %ld is for long
  %e  a floating point number, float in scientific notation, %E for 1.0E-3
      %le is for double, %Le is for long double
  %f  a floating point number with decimal point   %10.4f  10 wide  .dddd
      %lf is for double, %Lf is for long double
  %g  a floating point number, %f or %e as needed, %G for capital E
      %lg is for double, %Lg is for long double
  %h  an unsigned hexadecimal short integer (scanf only), old usage
  %i  an integer, int  %hi is for short int,  %li is for long int
  %n  pointer to integer to receive number of characters so far, int *i
  %o  an unsigned octal number, unsigned int  %ho and %lo for short and long
  %p  a pointer, void **x
  %s  a string ( must be null terminated ! ), use %s for scanf
  %u  an unsigned decimal integer (printf only), unsigned int  %hu %lu
  %x  a hexadecimal number, %X for capital ABCDEF, unsigned int  %hx %lx
  [...]  string, x[]
  %   none

Text may be around format characters for printf(), The list follows the
single quoted format string.

Output is right justified unless format  %-s or %-10.4f is used.
%+... causes plus sign to be printed.
%*    suppresses assignment, no store, in scanf().
%#    converts value to alternate form.


Field is expanded if not enough room to print.
numeric data into scanf() must be separated by space, tab or newline, not
comma
characters between % in scanf() format must be in input and are ignored


Preprocessor directives:

#include "mine.h" 
search current working directory first 
#include <stdio.h> 
search command line directory then system 
#define TRUE 1 
macro substitution, usually use capitals 
#define min(a,b) (a<b)?(a):(b) 
macro substitution with parameters 
#define abs(a) (a<0)?(-(a)):(a) 
macro substitution 
#define note /* comment */ 
this comment gets inserted every time note appears */
backslash \ at end of a line means continue 
#undef TRUE 
undefines a previously defined macroname 
#error 
stop compiling at this point 
#if expression 
conditional compilation, start if structure 
#elif expression 
else if expression != 0 compile following code 
#else 
else compile following code 
#endif 
end of conditional compiling 
#ifdef macroname 
like #if, compiles if macroname defined 
#ifndef 
like #if, compiles if macroname undefined 
#line number [filename] 
set origin for __LINE__ and __FILE__ 
#pragma 
gives the compiler commands 
