# Operatorer
[Python Operators](https://www.w3schools.com/python/python_operators.asp)
[Python Programming/Basic Math - Wikibooks, open books for an open world](https://en.wikibooks.org/wiki/Python_Programming/Basic_Math)

| Syntax         | Math                                                                                                                                                     | Operation Name                                                                                                                                                                                                           |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `a+b`          | a + b ![{\displaystyle a+b\,}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ad12cac1b9cc0f0d5333307f5f416d4d9fe74073)                         | [addition](https://en.wikipedia.org/wiki/Addition "w:Addition")                                                                                                                                                          |
| `a-b`          | a − b ![{\displaystyle a-b\,}](https://wikimedia.org/api/rest_v1/media/math/render/svg/85f7dd23b20a82224d94faadd0024340a77d5f69)                         | [subtraction](https://en.wikipedia.org/wiki/Subtraction "w:Subtraction")                                                                                                                                                 |
| `a*b`          | a × b ![{\displaystyle a\times b\,}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b20565f3d445c9e431c5211467d0f4dcb250c29b)                   | [multiplication](https://en.wikipedia.org/wiki/Multiplication "w:Multiplication")                                                                                                                                        |
| `a/b`          | a ÷ b ![{\displaystyle a\div b\,}](https://wikimedia.org/api/rest_v1/media/math/render/svg/79d75238e836848d80b790150c47908b29b7a7c3)                     | [division](https://en.wikipedia.org/wiki/Division_\(mathematics\) "w:Division (mathematics)") (see note below)                                                                                                           |
| `a//b`         | ⌊ a ÷ b ⌋ ![{\displaystyle \lfloor a\div b\,\rfloor }](https://wikimedia.org/api/rest_v1/media/math/render/svg/cf88e5797ea67c28ac0b71b818bf4df99242cd90) | [floor](https://en.wikipedia.org/wiki/Floor_function "w:Floor function") [division](https://en.wikipedia.org/wiki/Division_\(mathematics\) "w:Division (mathematics)") (e.g. 5//2=2) - Available in Python 2.2 and later |
| `a%b`          | a   mod   b ![{\displaystyle a~{\bmod {~}}b\,}](https://wikimedia.org/api/rest_v1/media/math/render/svg/88dfd7e1421543c4b7b155fdf0f31285536f1855)        | [modulo](https://en.wikipedia.org/wiki/Modulo_operation "w:Modulo operation")                                                                                                                                            |
| `-a`           | − a ![{\displaystyle -a\,}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0fc8a42b82321c485fa4ab3bf0a4bfff9406bf64)                            | [negative value](https://en.wikipedia.org/wiki/Negative_number "w:Negative number")                                                                                                                                      |
| `abs(a)`       | \| a \| ![{\displaystyle \|a\|\,}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9b769e3c31b2dafbe243dc419c40f57d321c2794)                     | [absolute value](https://en.wikipedia.org/wiki/Absolute_value "w:Absolute value")                                                                                                                                        |
| `a**b`         | a b ![{\displaystyle a^{b}\,}](https://wikimedia.org/api/rest_v1/media/math/render/svg/45725181a4104849e748178f68059996675b5db7)                         | [exponent](https://en.wikipedia.org/wiki/exponentiation "w:exponentiation")                                                                                                                                              |
| `math.sqrt(a)` | a ![{\displaystyle {\sqrt {a}}\,}](https://wikimedia.org/api/rest_v1/media/math/render/svg/355ad575c71e630c5a84bca720aaf0cbec887b1f)                     | [square root](https://en.wikipedia.org/wiki/Square_root "w:Square root")                                                                                                                                                 |

## Python Assignment Operators

Assignment operators are used to assign values to variables:

| Operator | Example       | Same As             | Try it |
| -------- | ------------- | ------------------- | ------ |
| =        | x = 5         | x = 5               |        |
| +=       | x += 3        | x = x + 3           |        |
| -=       | x -= 3        | x = x - 3           |        |
| *=       | x *= 3        | x = x * 3           |        |
| /=       | x /= 3        | x = x / 3           |        |
| %=       | x %= 3        | x = x % 3           |        |
| //=      | x //= 3       | x = x // 3          |        |
| **=      | x **= 3       | x = x ** 3          |        |
| &=       | x &= 3        | x = x & 3           |        |
| \|=      | x \|= 3       | x = x \| 3          |        |
| ^=       | x ^= 3        | x = x ^ 3           |        |
| >>=      | x >>= 3       | x = x >> 3          |        |
| <<=      | x <<= 3       | x = x << 3          |        |
| :=       | print(x := 3) | x = 3  <br>print(x) |        |
|          |               |                     |        |
|          |               |                     |        |


## Python Comparison Operators

Comparison operators are used to compare two values:

| Operator | Name                     | Example | Try it |
| -------- | ------------------------ | ------- | ------ |
| ==       | Equal                    | x == y  |        |
| !=       | Not equal                | x != y  |        |
| >        | Greater than             | x > y   |        |
| <        | Less than                | x < y   |        |
| >=       | Greater than or equal to | x >= y  |        |
| <=       | Less than or equal to    | x <= y  |        |

## Python Logical Operators

Logical operators are used to combine conditional statements:

| Operator | Description                                             | Example               | Try it |
| -------- | ------------------------------------------------------- | --------------------- | ------ |
| and      | Returns True if both statements are true                | x < 5 and  x < 10     |        |
| or       | Returns True if one of the statements is true           | x < 5 or x < 4        |        |
| not      | Reverse the result, returns False if the result is true | not(x < 5 and x < 10) |        |


## Python Bitwise Operators

Bitwise operators are used to compare (binary) numbers:

| Operator | Name                 | Description                                                                                             | Example | Try it |
| -------- | -------------------- | ------------------------------------------------------------------------------------------------------- | ------- | ------ |
| &        | AND                  | Sets each bit to 1 if both bits are 1                                                                   | x & y   |        |
| \|       | OR                   | Sets each bit to 1 if one of two bits is 1                                                              | x \| y  |        |
| ^        | XOR                  | Sets each bit to 1 if only one of two bits is 1                                                         | x ^ y   |        |
| ~        | NOT                  | Inverts all the bits                                                                                    | ~x      |        |
| <<       | Zero fill left shift | Shift left by pushing zeros in from the right and let the leftmost bits fall off                        | x << 2  |        |
| >>       | Signed right shift   | Shift right by pushing copies of the leftmost bit in from the left, and let the rightmost bits fall off | x >> 2  |        |

## Python Membership Operators

Membership operators are used to test if a sequence is presented in an object:

| Operator | Description                                                                      | Example    | Try it |
| -------- | -------------------------------------------------------------------------------- | ---------- | ------ |
| in       | Returns True if a sequence with the specified value is present in the object     | x in y     |        |
| not in   | Returns True if a sequence with the specified value is not present in the object | x not in y |        |