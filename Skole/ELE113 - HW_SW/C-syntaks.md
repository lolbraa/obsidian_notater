# Overordnet
C kan kompilleres i C++, så C++ er en versjon av C som er mer komplett.
## Kompilering 
Creating a machine executable usually involves three steps 
- Preprocessing – processes commands that begin with # (known as directives). Can add things to a program and make modifications 
- Compiling – translates code into machine language, producing object code (files) 
- Linking – links user code with any other code (library functions, other user code, etc.) to produce an executable 


## Direktiver
feks `#include <stdio.h>`

- Include the information in stdio.h in the compilation process 
- Header files such as this contain some information about some part(s) of one or more library functions


## Kommentarer
- Multi-line comments 
`/* This is a valid comment */` 

- Single line comments (introduced in C99 standard) 
- Begin with // and extend to the end of the line 
`// This is a valid comment` 


# Variabler
Every variable must have a type (defines an intended use) 
## Datatyper
C data types include: 
- char – a single byte capable of holding a single character 
	- 1 byte
- int – an integer, typically reflecting the natural size of integers on the target processor 
	- 2 eller 4 bytes? Avhengig av kompilator
- float – single precision floating point 
	- 4 bytes
- double – double precision floating point 
	- 8 bytes

Modifiers to the basic data types usually include unsigned, long, short 
- unsigned int would refer to an integer to be treated by the compiler as an unsigned quantity 
- long = dobbel byte lengde?
- short = kortere byte lengde

Individual compilers may support additional data types defined for the compiler/user 
- These are usually derived from the basic data types and are supported for program readability

Har ikke bool-variabeltypen. Bruker heller `unsigned char`.

Kan lage egne datatyper
```c
#define word unsigned int
#define byte unsigned char
```

## Deklarasjon
En variabel må deklareres FØR den designeres/gis verdi.
```C
directives 
declarations 
int main(void) 
{ 
  declarations 
  statements 
} 
```

```C
#include <stdio.h> 
int i; 
int main(void) 
{ 
  // declaration and 
  // initial assignment 
  int j=0; 
  i=j; 
} 
```


## Pointers
- Pointers are declared by using the * in front of the variable identifier.
- Example:
```C
int *ip; //declares a pointer to an integer
float *fp = NULL; //pointer to a float
```
- NULL pointer points to a place in memory that cannot be accessed.
- Useful for checking error conditions
- The & operator is used to specify the address-of-x:
```C
int x = 5; 
int *ip; 
ip = &x; //the pointer *ip points to the address where x = 5 is stored
```

Eksempel fra F13
```C
//function prototype
void get_rtc_time(byte *second, byte *minute, byte *hour, byte *week_day, byte *day, byte *month, byte *year);

//function definition
void get_rtc_time(byte *second, byte *minute, byte *hour, byte *week_day, byte *day, byte *month, byte *year)
{
	*second =
	*minute =
	*hour =
	*week_day =
	*day =
	*month =
	*year =
}

//function call
unsigned char second, minute, hour, week_day, day, month, year; // definerer variablene som skal brukes
get_rtc_time(&second,&minute,&hour,&week_day,&day,&month,&year); // bruker adressene til variablene så funksjonen kan skrive dit
```


## Arrays
- Arrays are a collection of items (i.e. ints, floats, chars) whose memory is allocated in a contiguous block of memory.
- Arrays and pointers have a special relationship. 
- This is because arrays use pointers to reference memory locations. 
- Therefore, most of the times, pointer and array references can be used interchangeably.
- A simple array of 5 ints would look like:
```C
int ia[5];
```
- We reference  areas of memory inside the array by the [] operator:
```C
printf("%d ", ia[3]);
```
- C demands that the array size is known at compile time!

### Arrays og Pointers
- An array name is just a pointer to the beginning of the allocated memory space
- Example:
```C
int ia[6] = {0, 1, 2, 3, 4, 5}; 
int *ip; 
ip = ia;            /* equivalent to ip = &ia[0]; */
ip[3] = 32;         /* equivalent to ia[3] = 32; */
ip++;               /* ip now points to ia[1] */
printf("%d ", *ip); /* prints 1 to the screen */
ip[3] = 52;         /* equivalent to ia[4] = 52 */
```




# Operatorer
## Arithmetic Operators
![[C-2025.01.29 09.18.48.jpg|550]]

## Compound Operators
C supports compound operators for both manipulating a value and assigning the result to a variable 
For example, i=i+2; can be written as i+=2; 
Other compound operators include 
```C
-= 
*= 
/= 
%= 
```
For example, i=i/j; can be written as i/=j; 
Increment operators (++ or --) are also supported 
```C
i++; 
++i; 
i--; 
–--i; 
```

![[C-2025.01.29 09.23.18.jpg|550]]


## Bit-operations
![[C-2025.01.29 09.56.03.jpg|550]]

## Masks
A mask is a variable that decides which bit(s) in a byte, nibble, word (etc.) that can be read or modified.
- Example: “00101101” would mark bits 0, 2, 3 and 6 in the mask variable.
- The mask and the target give a result for simple bit manipulation.
![[C-2025.01.29 09.56.55.jpg|550]]

## Set og get bit fra en binary string
![[C-syntaks-2025.05.26 09.01.43.png|550]]
![[C-syntaks-2025.05.26 09.31.28.png|550]]

# Statements
Statement – a command to be executed 
- Terminated with a semicolon 
- return 0; is an example of a statement 

C has relatively few statements 
In addition to the return and expression/assignment statements, most C statements can be grouped into one of three categories:
- **Selection statements** – the `if and switch` statements allow a program to select a particular execution path 
- **Iteration statements** – the `while, do, and for` statements support iteration (looping) 
- **Jump statements** – the `break, continue, and goto` statements cause an unconditional jump to some other location in the program (return falls into this category as well) 


## Logical expression
Logical expressions are used in selection statements to determine an operation to be performed 
Test operators (relational, equality, and logical) are commonly used in formulating logical expressions 
![[C-2025.01.29 09.26.59.jpg]]


## if-statement
The if statement allows for 
selection of program flow 
alternatives
- Allows for multiple statement execution 
- Includes else if and else clauses 
- Can be nested
 
```C
if (expression) { 
  statements; 
} 
else if (expression) { 
  statements; 
} 
else { 
  statements; 
} 
```

The if statement allows for performing an action based on a condition
A C conditional operator allows for producing a value depending on the value of a condition
- General form:  `expr1 ? expr2 : expr3` 
- Operation: 
	- if expr1 is true then return expr2, else expr3 
- Example: 
```C
int i=1, j=2, k; 
k = i > j ? i : j; // k=2 
k = ( i >= 0 ? i : 0) + j; // k=3 
```
- One common use, instead of: 
```C
if (i>j) 
  return i; 
else 
  return j; 
```
- write the following: 
```C
return i > j ? i : j; 
```


## switch-statement
The switch statement is useful in comparing an expression against a series of values (preferable to cascaded if 
statements) 
Må ha en `break`
```C
switch (expression) { 
 case constant-expression : statements 
 … 
 case constant-expression : statements 
 default : statements 
} 
```

- Controlling expression – the switch keyword must be followed by an integer expression (a character is also allowed) 
- Case label – each case begins with a label of the form case constant-expression : 
- The constant expression cannot contain variables or function calls 
- Statements – one or more statements follow the label (no braces are required). The last statement is usually break 
- A default case is usually the last case, but is not required 


## while-statement
- The while statement provides the most basic looping functionality in C
- General form: 
```C
while (expression) statement 
```
- Example 
```C
while (i<n) // controlling expression 
i*=2; // loop body 
```
- Infinite loops can be created using syntax similar to
```C
while (1) { statements } 
```
- Completely interrupt driven embedded systems will often have a main function similar to this, particularly if there is no 
operating system and no multitasking 



## do-while-statement
- The do statement is closely related to the while statement (essentially a while statement whose expression is evaluated 
after each execution of the loop body 
- The loop body will execute at least once 
- General form: 
```C
do statement while (expression); 
```
- Example 
```C
i=10; 
do { 
printf(“T minus %d and counting\n”, i--); 
} 
while (i>0) ;
```


## for-statement
- The for statement is probably the most widely used (and flexible) of all the C looping statements
- Most useful when there is some “counting” variable associated with a loop 
- General form: 
```C
for (expr1 ; expr2 ; expr3) statement; 
```
- expr1 is usually an initial assignment statement, expr2 is a test condition for loop termination, and expr3 is an increment (or decrement) statement affecting a variable in expr1 
- Example 
```C
for ( i=10 ; i>0 ; i-- ) { 
printf(“T minus %d and counting\n”, i); 
} 
```


## break- og continue-statements
- The break statement has already been used in the switch statement, but it can also be used to jump out of (i.e. break
execution of) a while, do, or for loop 
- The continue is similar to the break but it does not terminate the loop. Rather, control is transferred to the end of the loop. 
- Example: 
```C
n=0, sum=0; 
while (n<10) { 
 scanf(“%d”, &i); 
 if (i==0) continue; 
  sum += i; 
  n++; 
 // continue jumps to here 
} 
```



# Functions
Functions – like procedures (or subroutines or methods) in other programming languages 
- A series of statements grouped together and given a name 
- May or may not return a value 
- Grouped into two categories 
	- Those written by the programmer (user functions) 
	- Those provided as a part of the C implementation (library function)



- Each function consists of a name, a return type, and a possible parameter list. 
- This abstract definition of a function is known as it's interface.
- Examples:
```C
char *strdup(char *s); 
int add_two_ints(int x, int y); 
void useless(void);
```
- This is function prototypes – typically declared in header (.h) files
- The body of a function is where the functionality is defined:
```C
int add_two_ints(int x, int y){
return x+y;
}
```
- A function can also return values by using reference parameters.
- Pointers!






# \#define og macros
 \#define statement can be used 
to give the bits individual names
- This makes the code easier to read
- Example:
```C
#define LEDG_1 0x1 
#define LEDG_2 0x2 
#define LEDG_3 0x4 
… 
// only LEDG_1, LEDG_2 on 
PIO_REG = LEDG_1 | LEDG_2; 
// also LEDG_1, LEDG_2 on 
PIO_REG |= LEDG_1 | LEDG_2; 
// LEDG_1 | LEDG_2 off
PIO_REG &= ~( LEDG_1 | LEDG_2); 
```


- Macros are ’defines’ with more complex functions:
- Set (1) one bit: 
```C
#define bit_set(value,bit) ( ( value ) | (1 << bit ) ) 
Bit_set(8,1) ; // Results will be 0x10 
```
- Clear (0) one bit: 
```C
#define bit_clear(value,bit)((value)& ~(1 << bit)) 
bit_clear(5,0); // Results will be 0x4 
```
- Negation (NOT) one bit: 
```C
#define bit_toggle(value,bit)((value)^(1 << bit ) ) 
bit_toggle(10,3) ; // Results will be 0x2 
```
- Test one bit: 
```C
#define bit_test(value,bit) ( ( value) & (1 << bit ) ) 
if ( bit_test(5,0) ); // Results, True, bit(0) = 1
```

# I/O programming

- The function printf() writes to standard output.
- This is typically terminal windows
- Prototype: printf(“format string”, arg1, arg2, …);
- Example:
```
int old = 34; 
printf(“I am %d”,old);
```
- Conversion control character
- %d, %i - Int
- %f - float
- %c - char
- %s - string
- The function scanf() takes the input from the standard input
- Usually keyboard
- Prototype: `Scanf(“format string”, arg1, arg2, …);` 
- Example:
```
int age; 
scanf(“%d”, &age);
```



# Lese og sette bits på bus
```C
#include <stdio.h>
#include <io.h>
#include <system.h>

// returns 1 if addressed bit is set, 0 if bit is not set
// argument 1: adr is adress of 32 bit word
// argument 2: bit_pos is bit position to be tested
unsigned char get_bit(unsigned int adr, unsigned char bit_pos);

// sets adderessed bit to 0 or 1
// argument 1: adr is adress of 32 bit word
// argument 2: bit_pos is bit position to be tested
// argument 3: value is bit to be written
void set_bit(unsigned int adr, unsigned char offset, unsigned char value);


/*
Adressmap:
PIO_IN: PIO_IN_BASE (SW[15..0])
PIO_OUT: PIO_OUT_BASE (LEDR[15..0])
PIO_BID: PIO_BID_BASE (EX_IO[1..0])
*/

int main()
{
    unsigned int temp1, temp2;

    // Sette EX_IO til skriving
    //SKRIVING:
    IOWR_32DIRECT(PIO_BID_BASE + 4, 0, 3);
    //LESING:
    IOWR_32DIRECT(PIO_BID_BASE + 4, 0, 0);


    while (1)
    {
        // Oppgave 1, kontrollere EX_IO med SW
		for (int i = 0; i <= 1; i++) {
			temp = get_bit(PIO_IN_BASE, i);
			set_bit(PIO_BID_BASE, i, temp);
		}

        // Oppgave 2 
		temp1 = get_bit(PIO_BID_BASE, 0);
		temp2 = get_bit(PIO_BID_BASE, 1);
        printf("LESER: %d%d\n", temp1, temp2);


        // Oppgave 3, software-klokke
        for (int i = 0; i <= 1; i++) {
			set_bit(PIO_BID_BASE, 0, i);
		}
    }
    return 0;
}


// get_bit - hente ut en bit
unsigned char get_bit(unsigned int adr, unsigned char offset)
{
    unsigned int temp = IORD_32DIRECT(adr, 0);
    temp >>= offset;
    temp &= 1;
    return (unsigned char)temp;
}


// set_bit
void set_bit(unsigned int adr, unsigned char offset, unsigned char value)
{
    unsigned int temp = IORD_32DIRECT(adr, 0);
    unsigned int maske = 1 << offset;

    if (value == 1) {
        temp |= maske;
    } else {
        temp &= ~maske;
    }

    IOWR_32DIRECT(adr, 0, temp);
}

```
