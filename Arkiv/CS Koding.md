# Markdown
[Github Cheatsheet](https://github.com/tiimgreen/github-cheat-sheet/blob/master/README.md)

# Bash
[Cheatsheet](https://devhints.io/bash)

### If Else
```bash
if [[ -z "$string" ]]; then
  echo "String is empty"
elif [[ -n "$string" ]]; then
  echo "String is not empty"
else
  echo "This never happens"
fi
```

---
# C\#
## Snippets

### String interpolation / Formatted strings
```csharp
int i = 42; // Your variable
// Using string interpolation
Console.WriteLine($"{i}. siffer:");
```
[Kan også brukes utenom Console.Write](https://www.programiz.com/csharp-programming/library/string/format)
```
string strFormat = String.Format("Hello {0}", name);
String.Format(String format, Object...args);
```

### Exit GUI
```
Environment.Exit(0)
```

## Løkker
### While-loops
```csharp
while (condition) 
{
  // code block to be executed
}
```


### Do/while-loop
```csharp
do 
{
  // code block to be executed
}
while (condition);
```

*Break/Continue*
>The `continue` statement breaks one iteration (in the loop).
>The `break` statement breaks the loop.

### For-loops
```csharp
for (statement 1; statement 2; statement 3) 
{
  // code block to be executed
}
```
> **Statement 1** is executed (one time) before the execution of the code block.
> **Statement 2** defines the condition for executing the code block.
> **Statement 3** is executed (every time) after the code block has been executed.

*Eksempel*
```csharp
for (int i = 0; i < 5; i++) 
{
  Console.WriteLine(i);
}
```

*Loop through array*
```csharp
foreach (type variableName in arrayName) 
{
  // code block to be executed
}
```

*Break/Continue*
>The `continue` statement breaks one iteration (in the loop), if a specified condition occurs, and continues with the next iteration in the loop.


### If Else
```csharp
if (condition1)
{
  // block of code to be executed if condition1 is True
} 
else if (condition2) 
{
  // block of code to be executed if the condition1 is false and condition2 is True
} 
else
{
  // block of code to be executed if the condition1 is false and condition2 is False
}
```

Shorthand
```csharp
variable = (condition) ? expressionTrue :  expressionFalse;
```


### Switch / Case
Kan være vanskelig  å bruke for områder.
```csharp
int day = 4;
switch (day) 
{
  case 6:
    Console.WriteLine("Today is Saturday.");
    break;
  case 7:
    Console.WriteLine("Today is Sunday.");
    break;
  default:
    Console.WriteLine("Looking forward to the Weekend.");
    break;
}
```
> **break**: used to "jump out" of a `switch` statement.

> Ved å fjerne innholdet i en case (også break) vil tilstanden utføre innholdet i neste case.

### Exceptions, Try Catch
```csharp
try
{
  int[] myNumbers = {1, 2, 3};
  Console.WriteLine(myNumbers[10]);
}
catch (Exception e)
{
  Console.WriteLine(e.Message);
  Console.WriteLine("Something went wrong.");
}
finally
{
  Console.WriteLine("The 'try catch' is finished.");
}```

## Array / Tabell
```
int [] tab = new int[10];
tab[3] = 11; tab[3] = tab[3] + 1;
Console.WriteLine("Verdi i posisjon 4: " + tab[3].ToString());
```
> En initialisert array av **int** eller **double** vil inneholde kun 0.

```
// seks elementer - tegn
char[] tegnTab = { 'B', 'e', 'r', 'g', 'e', 'n' };
// ti elementer - heltall
int[] tallTab = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
// tre elementer - tekst
string[] tekstTab = { "Bergen", "Oslo", "Trondheim" };
```
## Tall
### Operatorer
![[Pasted image 20240201110020.png]]
![[Pasted image 20240201110048.png]]

Negering = !
### int / int
Heltallsdivisjon (to INT del på hverandre) vil returnere antall hele tall av divisor som går inn i dividenten.

### Convert to int

#### Eksplisitt konvertering (casting)
Konverterer uten hensyn til hva som er bak komma.
````C#
int varINTEGER = (int)varDOUBLE;
````

#### Math.Convert
Avrunder riktig - men hvis i midten avrunder den ned for partall og opp for oddetall.
````C#
int varInteger = (int)Math.Round(varDouble);
````

#### Convert.ToInt
```C#
int tall = Convert.ToInt16(Console.ReadLine());
```


---
# Arduino
## Serial
```Arduino
void setup() {
  Serial.begin(9600);
}
```


