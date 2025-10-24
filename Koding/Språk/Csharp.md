#programmeringsspråk 

# Eksamen
Ha en solution for alle deloppgaver, men dele i egne 
```csharp
// deloppgave a
{
	// kode
}
```

# Strukturer
Break/Continue
- The `continue` statement breaks one iteration (in the loop).
- The `break` statement breaks the loop.
## Conditions
- Less than: a < b
- Less than or equal to: a <= b
- Greater than: a > b
- Greater than or equal to: a >= b
- Equal to a == b
- Not Equal to: a != b

The logical Boolean operators perform logical operations with [bool](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/bool) operands. The operators include the unary logical negation (`!`), binary logical AND (`&`), OR (`|`), and exclusive OR (`^`), and the binary conditional logical AND (`&&`) and OR (`||`).
## While-loops
```csharp
while (condition) 
{
  // code block to be executed
}
```
## Do/while-loop
```csharp
do 
{
  // code block to be executed
}
while (condition);
```



## For-loops
```csharp
for (statement 1; statement 2; statement 3) 
{
  // code block to be executed
}
```
// **Statement 1** is executed (one time) before the execution of the code block.
// **Statement 2** defines the condition for executing the code block.
// **Statement 3** is executed (every time) after the code block has been executed.

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
//The `continue` statement breaks one iteration (in the loop), if a specified condition occurs, and continues with the next iteration in the loop.


## If Else
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


## Switch / Case
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
**break**: used to "jump out" of a `switch` statement.
Ved å fjerne innholdet i en case (også break) vil tilstanden utføre innholdet i neste case.

**Updated examples for C# 9**
[c# - Multiple cases in switch statement - Stack Overflow](https://stackoverflow.com/questions/68578/multiple-cases-in-switch-statement)
```csharp
switch(myValue)
{
    case <= 0:
        Console.WriteLine("Less than or equal to 0");
        break;
    case > 0 and <= 10:
        Console.WriteLine("More than 0 but less than or equal to 10");
        break;
    default:
        Console.WriteLine("More than 10");
        break;
}
```
_or_
```csharp
var message = myValue switch
{
    <= 0 => "Less than or equal to 0",
    > 0 and <= 10 => "More than 0 but less than or equal to 10",
    _ => "More than 10"
};
Console.WriteLine(message);
```

## Exceptions, Try Catch
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
}
```

# Reference Types

Reference types are objects that exist in external memory space. The reference types in C# are as follows:
- `object`
- `string`
- `dynamic`
# Operatorer
> [!info]- Bilde
![[Csharp-1.png]]
![[Csharp-2.png]]
Negering = !

# Datatyper
![[Csharp-3.png]]

| Data Type | Size                  | Description                                                                       |
| --------- | --------------------- | --------------------------------------------------------------------------------- |
| `int`     | 4 bytes               | Stores whole numbers from -2,147,483,648 to 2,147,483,647                         |
| `long`    | 8 bytes               | Stores whole numbers from -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |
| `float`   | 4 bytes               | Stores fractional numbers. Sufficient for storing 6 to 7 decimal digits           |
| `double`  | 8 bytes               | Stores fractional numbers. Sufficient for storing 15 decimal digits               |
| `bool`    | 1 bit                 | Stores true or false values                                                       |
| `char`    | 2 bytes               | Stores a single character/letter, surrounded by single quotes                     |
| `string`  | 2 bytes per character | Stores a sequence of characters, surrounded by double quotes                      |

| C# type/keyword | Range                                                   | Size                              |
| --------------- | ------------------------------------------------------- | --------------------------------- |
| `sbyte`         | -128 to 127                                             | Signed 8-bit integer              |
| `byte`          | 0 to 255                                                | Unsigned 8-bit integer            |
| `short`         | -32,768 to 32,767                                       | Signed 16-bit integer             |
| `ushort`        | 0 to 65,535                                             | Unsigned 16-bit integer           |
| `int`           | -2,147,483,648 to 2,147,483,647                         | Signed 32-bit integer             |
| `uint`          | 0 to 4,294,967,295                                      | Unsigned 32-bit integer           |
| `long`          | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 | Signed 64-bit integer             |
| `ulong`         | 0 to 18,446,744,073,709,551,615                         | Unsigned 64-bit integer           |
| `nint`          | Depends on platform (computed at runtime)               | Signed 32-bit or 64-bit integer   |
| `nuint`         | Depends on platform (computed at runtime)               | Unsigned 32-bit or 64-bit integer |
|                 |                                                         |                                   |


| Type     | Description                                                  | Range                                                             | Suffix |
| -------- | ------------------------------------------------------------ | ----------------------------------------------------------------- | ------ |
| byte     | 8-bit unsigned integer                                       | 0 to 255                                                          |        |
| sbyte    | 8-bit signed integer                                         | -128 to 127                                                       |        |
| short    | 16-bit signed integer                                        | -32,768 to 32,767                                                 |        |
| ushort   | 16-bit unsigned integer                                      | 0 to 65,535                                                       |        |
| int      | 32-bit signed integer                                        | -2,147,483,648  <br>to  <br>2,147,483,647                         |        |
| uint     | 32-bit unsigned integer                                      | 0 to 4,294,967,295                                                | u      |
| long     | 64-bit signed integer                                        | -9,223,372,036,854,775,808  <br>to  <br>9,223,372,036,854,775,807 | l      |
| ulong    | 64-bit unsigned integer                                      | 0 to 18,446,744,073,709,551,615                                   | ul     |
| float    | 32-bit Single-precision floating point type                  | -3.402823e38 to 3.402823e38                                       | f      |
| double   | 64-bit double-precision floating point type                  | -1.79769313486232e308 to 1.79769313486232e308                     | d      |
| decimal  | 128-bit decimal type for financial and monetary calculations | (+ or -)1.0 x 10e-28  <br>to  <br>7.9 x 10e28                     | m      |
| char     | 16-bit single Unicode character                              | Any valid character, e.g. a,*, \x0058 (hex), or\u0058 (Unicode)   |        |
| bool     | 8-bit logical true/false value                               | True or False                                                     |        |
| object   | Base type of all other types.                                |                                                                   |        |
| string   | A sequence of Unicode characters                             |                                                                   |        |
| DateTime | Represents date and time                                     | 0:00:00am 1/1/01  <br>to  <br>11:59:59pm 12/31/9999               |        |


```C#
bool isOpen = true;
byte age = 45;
sbyte temperature = 58;
char grade = 'a';
decimal numberOfAtoms = 1493867940.23m;
double weightOfHippos = 243906.12;
float heightOfGiraffe = 908.32f;
int seaLevel = -24;
uint year = 2023u;
nint pagesInBook = 412;
unint milesToNewYork = 2597;
long circumferenceOfEarth = 25000l;
ulong depthOfOcean = 28000ul;
short tableHeight = 4;
ushort treeBranches = 33;
```


> [!Bilde]- ASCII-tabell
> ![[Csharp-4.png]]
> Get the ASCII Value of Characters in a String Using Typecasting in C#
>Typecasting is achieved by using a casting operator. Specifically, we use the (int) casting operator to convert a character (of type char) to its corresponding ASCII value, which is represented as an integer (of type int).
>``(int)char``



## String
### String interpolation / Formatted strings
[$ - string interpolation - format string output - C# reference | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/tokens/interpolated)
```csharp
int i = 42; // Your variable
// Using string interpolation
Console.WriteLine($"{i}. siffer:");
```
```C#
Console.WriteLine($"({Ar} + {Aj}j) * ({Br} + {Bj}j) = {C}");
```
[Kan også brukes utenom Console.Write](https://www.programiz.com/csharp-programming/library/string/format)
```C#
string strFormat = String.Format("Hello {0}", name);
String.Format(String format, Object...args);
```

```C#
var name = "Mark";
var date = DateTime.Now;

// Composite formatting:
Console.WriteLine("Hello, {0}! Today is {1}, it's {2:HH:mm} now.", name, date.DayOfWeek, date);
// String interpolation:
Console.WriteLine($"Hello, {name}! Today is {date.DayOfWeek}, it's {date:HH:mm} now.");
// Both calls produce the same output that is similar to:
// Hello, Mark! Today is Wednesday, it's 19:40 now.
```

```C#
Console.WriteLine($"|{"Left",-7}|{"Right",7}|");

const int FieldWidthRightAligned = 20;
Console.WriteLine($"{Math.PI,FieldWidthRightAligned} - default formatting of the pi number");
Console.WriteLine($"{Math.PI,FieldWidthRightAligned:F3} - display only three decimal digits of the pi number");
// Output is:
// |Left   |  Right|
//     3.14159265358979 - default formatting of the pi number
//                3.142 - display only three decimal digits of the pi number
```

```C#
string message = $"The usage policy for {safetyScore} is {
    safetyScore switch
    {
        > 90 => "Unlimited usage",
        > 80 => "General usage, with daily safety check",
        > 70 => "Issues must be addressed within 1 week",
        > 50 => "Issues must be addressed within 1 day",
        _ => "Issues must be addressed before continued use",
    }
    }";
```

See [String formatting in C#](http://blog.stevex.net/string-formatting-in-csharp/) for some example uses of String.Format
Actually a better example of [formatting int](https://learn.microsoft.com/en-us/dotnet/standard/base-types/custom-numeric-format-strings#the-0-custom-specifier)
```csharp
String.Format("{0:00000}", 15);          // "00015"
```
or use [String Interpolation](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/tokens/interpolated):
```csharp
$"{15:00000}";                           // "00015"
```

### String som array


## Integers (heltall)
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

## Convert to Float
```C#
float.Parse("stringy");
```
```csharp
int val1 = 1;
float val2 = (float)val1;
```
```csharp
int i = 8;
float f = Convert.ToSingle(i);
```

## Random
```C#
Random r = new Random();
int tall = r.Next(<min>, <maks>); // min =< tall < maks (ekskludert maks)
Console.WriteLine(tall);

float tall = (float)r.NextDouble(); // mellom 0 og 1
r.Next(10,50)/10.0 // mellom 1,0 og 4,9

int[] tall = new int[10];
tall[0] = r.Next(10,100);
```

```C#
Random r = new Random();
float tall = (float)r.NextDouble();
Console.WriteLine($"{tall:F5}");
```

I klasser burde definere random 
```C#
public static random r = new Random();
```

## Array / Tabell
```C#
int [] tab = new int[10];
tab[3] = 11; tab[3] = tab[3] + 1;
Console.WriteLine("Verdi i posisjon 4: " + tab[3].ToString());
```
// En initialisert array av **int** eller **double** vil inneholde kun 0.

```C#
// seks elementer - tegn
char[] tegnTab = { 'B', 'e', 'r', 'g', 'e', 'n' };
// ti elementer - heltall
int[] tallTab = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
// tre elementer - tekst
string[] tekstTab = { "Bergen", "Oslo", "Trondheim" };
```

### Tabell av objekter
```C#
Rektangel [] rtab = new Rektangel[10]; // null-verdi for referanser er 'null'

for (int i = 0; i < 10; i++)
{
	rtab[i] = new Rektangel(i,i);
}
```


## Liste
Kan i mange sammenhenger brukes i stedet for tabell.
Ingen øvre grense. Legger til med Add.
Henter verdier på samme måte som Arrays.
```C#
List<int> tall = new List<int>(); 

// Bruk:
tall.Add(2); // posisjon 0
tall.Add(3); // posisjon 1
tall.Add(8); // posisjon 2
tall.Insert(0,1000)
int x = tall[2] + 5; // x = 8 + 5
tall.RemoveAt(2); // fjerner 3


List<double> tall = new List<double>() {1,2,3,4,5};
```
[C# List (with Examples)](https://www.programiz.com/csharp-programming/list)

`languages.Insert(2, "JavaScript")` inserts `"JavaScript"` at the 2nd index position

We can delete one or more items from `List<T>` using **2** methods:
- `Remove()` - removes the first occurrence of an element from the given list
- `RemoveAt()` - removes the elements at the specified position in the list

#### Iterate list
```C#
for (int i = 0; i < albums.Count; i++)
	Console.WriteLine(albums[i]);

foreach(uint t in liste) {
	Console.WriteLine(t);
}
```

#### Sort list
[How to sort a list in C# | List.Sort() Method Set -1 - GeeksforGeeks](https://www.geeksforgeeks.org/how-to-sort-list-in-c-sharp-set-1/)
[C# sort List - sorting list elements in C# language](https://zetcode.com/csharp/sortlist/)
The method has four overloads:
```C#
- Sort(Comparison<T>) - Sorts the elements in the entire List<T> using the specified Comparison<T>.
- Sort(Int32, Int32, IComparer<T>) - Sorts the elements in a range of elements in List<T> using the specified comparer.
- Sort() - Sorts the elements in the entire List<T> using the default comparer.
- Sort(IComparer<T>) - Sorts the elements in the entire List<T> using the specified comparer.
```

Default:
```C#
List<int> nums = [2, 1, 8, 0, 4, 3, 5, 7, 9];

nums.Sort();
Console.WriteLine(string.Join(",", nums));

nums.Reverse();
Console.WriteLine(string.Join(",", nums));
```

List sort by string length
```C#
List<string> words = ["falcon", "order", "war",
    "sky", "ocean", "blue", "cloud", "boy", "by", "raven",
    "station", "batallion"];

words.Sort((a, b) => a.Length.CompareTo(b.Length));
Console.WriteLine(string.Join(",", words));

words.Sort((a, b) => b.Length.CompareTo(a.Length));
Console.WriteLine(string.Join(",", words));
```

### Liste av objekter
```C#
List<Rektangel> rList = new List<Rektangel>();

for (int i = 0; i < 5; i++)
{
	rList.Add(new Rektangel(i,i));
}
```


## Dictionary
### Create a Dictionary
To create a dictionary in C#, we need to use the `System.Collections.Generic` namespace. Here is how we can create a dictionary in C#.
- `dictionaryName` - name of the dictionary
- `dataType1` - datatype of keys
- `dataType2` - datatype of values
```C#
Dictionary<dataType1, dataType2> dictionaryName = new Dictionary<dataType1, dataType2>();
```
```C#
Dictionary<string, string> songs = new Dictionary<string, string>() {
	   { "Queen", "Break Free" },
	   { "Free", "All right now" } }
```

### Operasjoner
```C#
// access the value having key "Name"
Console.WriteLine(student["Name"]);

// add items to dictionary
student.Add("Name", "Susan");
student.Add("Faculty", "History");

// change the value of "Model" key to "Maruti"
car["Model"] = "Maruti";


// remove value with key "Role"
employee.Remove("Role");

// iterate through the car dictionary 
foreach (KeyValuePair<string, string> items in car)
{
	Console.WriteLine("{0} : {1}", items.Key, items.Value);
}
```
**Note:** If you want to remove all the elements of the dictionary, use the `Clear()` method.

# Funksjoner og metoder
Funksjoner gjør gjerne en spesifikk oppgave (5-7 linjer?)
Metode er en funksjon i en klasse.
Behøver navn, retur-datatype, argument-datatype og funksjonskroppen.
> I klasse "Program" må man ha "static" foran.
```C#
// En metode (i Program) defineres ved å skrive:
static void metodenavn(int Tall)
{
	// metodekropp
	return Resultat
}
// En slik metode kan brukes (dette omtales som metodekall) i klassen ved å skrive: 
metodenavn();

// Er man i en annen klasse må man spesifisere klassen
Program.metodenavn(999);
```

> Man bruker "static" når man er i program-klassen? Det er noe med klasser, og hvordan det skal kalles. klasse.funksjon (Console.WriteLine) eller variabel.funksjon (s.Length).
## Metoder med argumenter og *uten returverdi
```C#
void funksjonsnavn(dt_1 fa_1, …, dt_n fa_n)
{
	// funksjonskropp 
}
```
- Forkortelse dt står for datatype og fa står for ’formell argument’.
- Vi ser at en funksjon kan ha flere argumenter og at hver argument har en datatype.
- Formelle argumenter kan brukes i funksjonskroppen som vanlige variabler.

## Metoder med argumenter og *med* returverdi
```C#
dt_rt metodenavn(dt_1 fa_1, …, dt_n fa_n)
{
	// metodekropp
	return utr;
}
```
- Forkortelse dt står for datatype og fa står for formell argument.
- Forkortelse dt_rt står for ’datatypen til metodens returverdi’.
- Navn utr i linjen med return står for et uttrykk (variabel, litteral, sammensatt operasjon, …) som evalueres til en verdi av datatypen dt_rt.

## «Default» argumenter
- En metodes argumenter (for verdioverføring) kan ha «default»-verdier. Disse brukes i tilfelle brukeren kaller metoden uten å oppgi (alle) metodeargumenter.
- ”Default”-verdier kan oppgis i metodedefinisjonen:
```C#
void foo(int x = 0, int y = 0) { … }
```


## Referanser
- En referanse kan oppfattes som et nytt navn for et (allerede eksisterende) minneområde.
- Det nye navnet kan brukes på samme måte som variabelnavn (sjekke eller endre verdien).
- Dette konseptet kan brukes i C# ved argument-overføring:
	- vil kan ha mer enn ett navn for et minneområde.
	- de forskjellige navn kan ha forskjellige rekkevidder (et som brukes i funksjonen) og et som brukes i koden som kaller funksjonen.
- Nøkkelordet ref (eller out) brukes - når metoden implementeres (metodedefinisjon) og når metoden brukes (metodekall).

Metode som bruker verdioverføring:
```C#
static int add1(int x, int y)
{
	return x + y;
}
```
Metode som bruker referanseoverføring
```C#
static int add2(ref int x, ref int y)
{
	return x + y;
}
```
- Metoder har samme effekt (returnerer summen av argumenter), men på to forskjellige måter. 
- `ref` sender minneaddressen (64 bits) som argument.
- Skisser minneområdet for å observere forskjeller. Bruk følgende main:
```C#
static void Main(string[] args)
{
	int a1 = 5;
	int a2 = 10;
	int z = add1(a1, a2); // int x = a1; int y = a2; z = 15;
	int q = add2(ref a1, ref a2); // x <-> a1 = 5; y <-> a2 = 10;
}
```

### Metode som bruker referanse-return: static void (ref)
Man kan ha en funskjon som ikke returnerer med `return`, men referanse-refererer:
Kan returnere flere variabler.
```C#
int res = 0; // må deklarere mottaker-variabelen hvis man bruker `ref`
add3(ref a, ref b, ref res); // sender a og b, mottar res

res = add3(ref a, ref b, ref res); // DETTE FUNGERER IKKE

static void add3(ref int x, ref int y, ref int svar)
{
	svar = x + y;
}
```
### Metode som bruker referanse-return: static void (out)
Man kan ha en funskjon som ikke returnerer med `return`, men referanse-refererer:
Kan returnere flere variabler.
```C#
int res; // trenger ikke deklgiarere mottaker-variabelen en verdihvis man bruker out
add3(ref a, ref b, out res); // sender a og b, mottar res

res = add3(ref a, ref b, out res); // DETTE FUNGERER IKKE

static void add3(ref int x, ref int y, out int svar)
{
	svar = x + y;
}
```
### Hvorfor bruke referanseoverføring?
- Ingen duplisering av verdier (slik som ved verdioverføring).
	- Minnebesparende og (for ikke primitive datatyper som vi skal studere senere) mye raskere.
- Minneområder til argumentene blir endret i metode – det innebærer at vi kan (med visse begrensninger) bruke referanseoverføring i stedet (eller i tillegg til) for returverdier.

![[Csharp-5.png]]![[Csharp-6.png]]![[Csharp-7.png]]



# Klasser 
Ny klasse i Visual Studio:
- Solution Explorer, høyreklikk på programnavn og velg Add→ New Item. Deretter velger du filtypen: class og skriver filnavn.

## Terminologi
- Datamedlem/attributer/datafelt (field, attributes)
- Tilgangsmodifikatorer (access modifiers)
	- Public - tilgjengelig for alle
	- Private - tilgjengelig innad i klasen
	- Internal
	- Protected
- Static - Uavhengig av et objekt, nesten "global" verdi? 
- Funksjonsmedlem (method)
- Konstruktør (constructor)
- Tilgangsmedlem (property)


I C# blir objekter håndtert annerledes enn variabler ved bruk av `=`.
For referansedatatyper, tilordning «a = b» (eller lignende) betyr at a blir «et nytt navn» for «det objektet som b refererer til» (og ikke en kopi av «objektet som b refererer til» – slik som tilordning fungerte for verdi-datatyper) 
- (a får ikke en kopi av dataene som b refererer til, det er kun b-sin adresse som blir kopiert)

## Tilgangsmedlemmer
Generelt: vi bør kunne **kontrollere tilgang** (hva som kan passeres av verdier) til datamedlemmer i en klasse
- Denne utfordringen kan vi løse ved å deklarere datamedlemmer som private og lage (offentlige) funksjonsmedlemmer (en per datamedlem) som kan brukes til å oppdatere/endre datamedlemmer (med koden som kontrollere for ulovlige verdier). Merk at dersom medlemmene er private må du muligens også ha (offentlige) funksjonsmedlemmer som brukes til å lese verdier
- En vanlig måte å håndtere denne utfordringen er ved å benytte seg av «tilgangsmedlem»-konseptet (forklares i kommende lysbilder)

Det er vanlig å deklarere datamedlemmer som private («innkapsling av data») - som igjen betyr at viikke kan bruke dem direkte fra andre moduler (fra for eksempel Main() i klassen Program)Da kan vi definere vi tilgangsmedlemmer (get og/eller set) for hver datamedlem x som vi ønsker åbruke i «klientklasser» (klassen Program i prosjektet vi jobber med):
```C#
public datatypen X
{
	get { return x; }
	set { x = value; }
}
```
Konvensjon: bruk samme navn for tilgangsmedlemmer som for datamedlemmer, men første bokstav i et medlemsnavn skal være stort dersom det er et tilgangsmedlem og liten dersom det er et (privat) datamedlem

For eksempel:
```C#
private double lengde;

public double Lengde
{
	get { return lengde; }
	set
	{
		if (value > 0) lengde = value;
		else lengde = 0;
	}
}

```

### Lambda-notasjon

```C#
namespace N11_O1;

public enum Drivstofftype { Hydrogen, Elektrisk, Gass}
public class Skip
{

    // Datamedlemmer 
    private string navn;
    private Drivstofftype drivstoff;
    private double vekt;
    private Posisjon posisjon;

    // Tilgangsmedlemmer
    public string Mavn { get => navn; set => navn = value; }
    internal Drivstofftype Drivstoff { get => drivstoff; set => drivstoff = value; }
    public double Vekt
    {
        get { return vekt; }
        set
        {
            if (value < 0) vekt = 0;
            else vekt = value;
        }
    }
...
```


## Konstruktør
- En konstruktør i en klasse er et spesielt medlem som blir utført når et objekt blir opprettet
	- i programkoden oppgir du konstruktørnavn (og eventuelle arumenter) når objektet blir oprettet (setning 
- med new)
- En konstruktør har (alltid) det samme navn som klassen den hører til har
- En konstruktør har ikke retur verdi (ikke engang void)
- En konstruktør kan ha null eller flere argumenter
- En konstruktør er (nesten) alltid «public» (med mindre vi bruker en spesiell «design pattern»)

```C#
// i klassen Rektangel
public Rektangel()
{
	lengde = 0;
	bredde = 0;
}
// i klassen program
Rektangel r1 = new Rektangel();

```

### Konstruktør med og uten argumenter
```C#
// Datamedlemmer 
private double x, y;

// Tilgangsmedlemmer
public double X
{
	get { return x; }
	set { x = value; }
}

public double Y
{
	get { return y; }
	set { y = value; }
}

// Konstruktører
public Punkt2D()
{
	this.X = 0;
	this.Y = 0;
}

public Punkt2D(double X, double Y)
{
	this.X = X;
	this.Y = Y;
}
```

### Static konstruktør

```C#
// Datamedlemmer
public static double maksX, maksY;

// Statisk konstruktør
static Punkt2D()
{
	maksX = 100;
	maksY = 100;
}
```


### Nullkonstruktør bruker "full" konstruktør
this() passerer parametre til annen konstruktør under.
```C#
public Klubb() : this("null", 0, DraktFarger.UKJENT) {}

public Klubb(string KlubbNavn, int AntallMedlemmer, DraktFarger DraktFarge)
{
	this.KlubbNavn = KlubbNavn;
	this.AntallMedlemmer = AntallMedlemmer;
	this.DraktFarge = DraktFarge;
}
```

### Subklasse-konstruktører baserer seg på parent
base() passerer parametre til parents-konstruktør.
```C#
public FotballKlubb(string n, int am, Drakt df, int d) : base(n, am, df)
{
	Divisjon = d;
	Spillere = new List<string>();  
}

public FotballKlubb() : base()
{
	divisjon = 0;
	Spillere = new List<string>();
}
```

## Funksjonsmedlemmer
```C#
// I klasse:
public double Areal()
{
	return Bredde * Lengde;
}

// Bruk:
double a2 = r2.Areal();
```
- «punktumnotasjon» (i for eksempel double a1 = r1.Areal();) skal vi omtale som **«funksjonsmedlemmet Areal er kvalifisert med objektet r1»** 
- du kan også bruke funksjonsmedlemmet Areal inne i klassen Rektangel (for eksempel i andre funksjonsmedlemmer), men da skal den (vanligvis) ikke kvalifiseres med et objektnavn


## Statiske medlemmer
Statiske medlemmer er spesielle data- og funksjonsmedlemmer:
- Statiske datamedlemmer: 
	- hører ikke til et bestemt objekt slik som datamedlemmer gjør
	- kan brukes til å lagre verdier som (ikke nødvendigvis er konstanter og som) er «felles» for alle objekter av klassen (ordet klasse kan oppfattes som «mengde» (av objekter)
	- «Vanlig» bruk: verdier som er felles for alle objekter (mer at det ikke er det samme som «konstanter»)
	- Eksempel: Rente-verdi for objekter av datatypen Konto (antar da at alle kontoer bruker samme rente)
- Statiske funksjonsmedlemmer:
	- kvalifiseres ikke med et objekt slik som «vanlige» funksjonsmedlemmer gjør, men med klassenavn eksempel: Consol.Write()) 
	- er funksjoner som har med hele klassen å gjøre – de skal (vanligvis) ikke oppdatere «et enkelt objekts»-datamedlemmer
	- de kan motta objekter som argumenter
	- Statiske medlemmer omtales ofte som «klassemedlemmer» - siden de ikke «kvalifiseres» med et 
bestemt objekt






## Arv
En klasse kan arve (programkode) fra en annen klasse og i tillegg kan den ha sitt eget programkode som spesialiserer klassen (i forhold til klassen som den arver i fra).

```C#
// Superklasse
public class Måler
{
	// Generell-måler
}
// Temperaturmaaler er en subklasse av Måler
public class Temperaturmåler : Måler
{
	// Trykkmåler-kode
}
// Teller er også en subklasse av Måler
public class Teller : Måler
{
	// Trykkmåler-kode
}
```

### Tilgangsmodifikator: protected
- Fungerer som private, men kan brukes av subklasser

### Override og Virtual
En subklasse kan omdefinere superklassen sin oppførsel – vi bruke nøkkelordet `override` for å indikere at vi endrer metodeoppførsel
For at vi skal kunne omdefinere metoder i subklasser må metoden være markert med virtual i superklassen
Tilbakeblikk på sammenligningsoperator:  
- vi kan nå ordne (to) varsel som vi har fått da vi har implementert sammenligningsoperator i våre klasser (Rektangel og KomplekstTall):  Equals og GetHashCode skal omdefineres (`override`).

### Klassen `object`
Er i toppen av arvehierarki (alle klasser/delegater/...) er direkte/indirekte subklasser av «`object`»)
Klassen `object` definerer noen funksjonsmedlemmer som kan være nyttige: 
- equals (som vi kan omdefinere dersom vi ønsker å omdefinere sammenligning), 
- getType, 
- ToString (som ofte vil være omdefinert i nye klasser ved å bruke «override»)

### Nøkkelordet `base`
Nøkkelordet kan brukes til å bruke superklasse sine medlemmer i en subklasse-sin programkode
- Nøkkelordet står for superklasse som er oppgitt i subklassen sin implementasjon (etter kolon)
Du kan bruke den også til å utføre superklasse sin konstruktør
- «`: base(…)`»oppgis mellom konstruktør-deklarsjon og blokken som implementerer konstruktøren (slik som vi har brukt «`: this(…)`» i forbindelse med konstruktørimplementasjon)

### Nøkkelordet `sealed`
Nøkkelordet kan brukes til å:
- Forby arv av en klasse (ved å markere en klasse som `sealed`)
- Forby videre `override` ved å markere en (`override`)metode som `sealed`
- Du kan ikke markere metoder merket med `virtual` med `sealed`


### Arv og referanser
Superklassereferanser kan referere til subklasseobjekter. Dette kan være svært nyttig for oss når vi programmerer
Igjen: i C#, en (sub)klasse kan arve fra kun en (super)klasse
- Vi kan ha flere «lag» med arv (Z arver fra Y som arver fra X som ...) – arv er «transitiv»
- Terminologi: X vil også (ofte) omtales som superklassen til Z selv om Z arver fra Y
Tilgangsmodifikator (public/private/...) til en medlem i en klasse vil avgjøre om du kan bruke medlemmet i en eventuell subklasse

Arv i GUI programmer
Alle form-klasser i våre GUI prosjekter arver fra en klasse som heter Form
Klassen inneholder en del medlemmer som vi skal etter hvert finne nyttig


### Polymorfisme
Merk at dersom subklasse omdefinerer en metode (Foo(…)) fra superklassen sin og dersom vi har en superklasse referanse obj vil setningen obj.Foo(…) ha forskjellig effekt avhengig av om obj refererer til et objekt av superklasse-datatype eller et objekt av subklasse datatype
Under programutføring kan begge situasjoner oppstå (selvsagt ikke på en gang ☺)
Slik situasjon (der en og samme kodelinje kan bety forskjellige ting – avhengig av datatypen til objektet som det refereres til) kalles polymorfisme

### Nøkkelord is og as
Vi kan bruke nøkkelordet is til å teste om datatypen til objektet som en referanse refererer til er en gitt datatype. Operatoren returnerer en boolsk verdi. Eksempel:
```C#
object o = new Random();
// Kode som kan endre det o refererer til
// ...
if (o is Random)
{ 
	// ... 
};
```
Vi kan også bruke nøkkelordet `as` til å få en referanse til et objekt (som kan være resultat ev et uttrykkevaluering). Operatoren tar et uttrykk og en (referanse)datatypenavn som argumenter og returnerer en referanse til det objektet som uttrykket ble evaluert til (eller null dersom resultatet ikke var kompatibel med argument-datatypen).
```C#
Random r = o as Random; // r blir satt til objektet som o refererer til, eller null dersom det som o refererer til ikke er kompatibel med Random
```


> [!NOTE]- UML, Unified Modelling Language
> ![[Csharp-2025.08.27 09.44.07.webp]]
> 
> ![[Csharp-2025.08.27 09.49.30.webp]]



## Interface
Ofte, vi ønsker å spesifisere hva programvarekomponenter bør gjøre (i stedet å spesifisere nøyaktig «hva de er»)
Dersom «noe» kan brukes som en hammer og vi trenger hammer-funksjonalitet bryr vi oss ikke om nøyaktig utforming av 
Interface-språkkonstruksjon svarer til dette i programmeringsverden – vi bruker den til å spesifisere hva en komponent bør gjøre (i stedet for å spesifisere en nøyaktig beskrivelse)
- Komponenter i C# implementeres som klasser eller struct (den sistnevnte med en viss forsiktighet) 
I C#, en interface spesifiserer metoder (eller tilgangsmedlemmer) som en klasse (eller struct) må implementere for å «oppfylle kontrakten» (om å implementere interface)
~~En interface inneholder ikke programkode – kun deklarasjoner~~
- Dette stemmer ikke i nyere versjoner av C#
Interface konseptet  er tett knyttet til komponent-orientert-programmering (metodologi) – der programvarekomponenter beskrives (og implementeres) ut i fra nytten/rollen de har/spiller i programsystemet



```C#
interface IKjøretøy
{
	string Registreringsnummer { get; set; }
	void Kjør(double fart);
}

class Automobil : IKjøretøy
{
	string regnr;
	
	public string Registreringsnummer
	{
		get { return regnr; }
		set { regnr = value; } 
	}
	
	public void Kjør(double fart)
	{
		// Kode som implementerer Kjør
	}
}
```
Notasjon (at en klasse skal implementere en interfaceer det samme som for arv, men: 
- vi oppgir interface-navn (i stedet for supperklassenavn)
- vi kan oppgi mer enn én interface (med komma mellom interface-navn) som klassen skal implementere
Alle medlemmer oppgitt i interface som klassen implementerer må være offentlige (og ikke statiske) 

Referanser av en «interface-type» kan brukes i programmet – de kan referere til objekter (av klasser som implementerer interface)
Slike referanser kan brukes til å utføre de metodene som er definert i den aktuelle interface-en, men på et konkret objekt (av en klasse som implementerer interface) som referansen refererer til
Vi kan ikke opprette objekter av interface-type


Bruk av interface hjelper oss ikke til å unngå å skrive samme kode flere ganger
Til gjengjeld vil hovedprogrammet ikke bry seg om hvordan en klasse er implementert – så lenge interface er oppfylt vil komponenten kunne brukes!
- Dette gir oss mulighet til å bytte deler av programkode ved behov uten å måtte skrive om resten av programmet


## Override Metoder
### ToString
```C#
public override string ToString()
{
	return string.Format("{0} - {1} - kapasitet: {2} passasjerer", modell, ID, antallPassasjerer);
}
```
eller
```C#
public override string ToString() {
	return $"c-({this.PosisjonX},{this.PosisjonY})";
}
```

### Operatorer
```C#
public static override bool Equals(object? obj)
{
	if (obj is Punkt2D other)
		return this.X == other.X && this.Y == other.Y;
	return false;
}
```

```C#
public static bool operator ==(Punkt2D Punkt1, Punkt2D Punkt2)

{

if ((Punkt1.X == Punkt2.X) & (Punkt1.Y == Punkt2.Y)) return true;

else return false;

}
public static bool operator !=(Punkt2D Punkt1, Punkt2D Punkt2)

{

if ((Punkt1.X == Punkt2.X) & (Punkt1.Y == Punkt2.Y)) return false;

else return true;

}
```

```C#
public static bool operator >=(StudieEmne a, StudieEmne b)
{
	//return a.emneKode >= b.emneKode;  // Endret til studiepoeng siden det er feil i oppgaveteksten.
	return a.studiepoeng >= b.studiepoeng;
}

public static bool operator <=(StudieEmne a, StudieEmne b)
{
	return a.emneKode <= b.emneKode;
}
```



# Nye datatyper: Enum og Struktur/Struct
## Enum
Programmeringsspråkkonstruksjonen enum kan også brukes til å definere en ny datatype. Datatypeverdier må listes opp.
Eksempel deklarasjon:
```C#
enum Ukedag { mandag, … , søndag }
```
Vi kan bruke enum til å øke lesbarheten av koden dersom vi trenger en variabel som kan ha noen få forskjellige verdier: 
- «ukedag» kan programmeres som heltall: vi kan bruke en variabel som kan ha verdier mellom 1 og 7 men programmet vil være mer lesbar dersom vi bruker enum Ukedag i stedet  
Brukes «omtrent» som vanlige datatyper:
```C#
Ukedag x = Ukedag.tirsdag; // x = tirsdag
```

Blir til underliggende integers, som man kan endre med casting.
Merknad: det er ikke vanlig å bruke eller endre underliggende verdier (men det kan være passende i noen situasjoner).

Merknad 1:
- Datatyper definert ved å bruke enum faller under «verdidatatyper» (og ikke «referansetyper»).
- Det er viktig å være klar over dette når en bruker tilordningsoperatoren.
Merknad 2: 
- Siden resulterende datatype er kompilert (default) til heltall (og siden vi kan bruke heltall med switch) kan vi bruke enum -datatype-variabler/verdier i switch konstruksjoner

## Struct
Strukturer (struct) kan vi også bruke til å definere sammensatte datatyper
Strukturer defineres på samme måte som klasser (men vi bruker nøkkelordet struct i stedet for class
- Strukturer kan ha datamedlemmer, metoder, tilgangsmedlemmer, konstruktører (og operatorer)
Eksempel:
```C#
struct Rektangel
{  
	public double Bredde;
	public double Lengde;
	public Rektangel(double initB, double initL) 
		{ Bredde = initB; Lengde = initL; }
	public double Areal() { return Bredde * Lengde; }
}
```

Strukturer ligner på klasser men:
- Vi kan ikke bruke arv (studeres senere i forbindelse med klasser) når vi jobber med strukturer
- Vi kan ikke implementere standardkonstruktør (datamedlemmer nullstilles automatisk)
- Alle konstruktører må initialisere alle datamedlemmer (gir kompileringsfeil dersom ikke oppfylt)
- Vi kan ikke implementere destruktør («finalizer») når vi jobber med strukturer
- Viktig: strukturer er verdi-datatyper
	- Tilordning fungerer på samme måte som for (for eksempel) heltall-variabler/verdier
	- Setningen Rektangel `r = new Rektangel(2,3);` vil ha forskjellig betydning (med tanke på det som skjer i minne) avhengig om vi har definert datatypen Rektangel som en klasse eller som en struktur. Det samme gjelder også setningen `Rektangel r;` og setningen `Rektangel r = new Rektangel();`
- Avansert (for øyeblikket): datamedlemmer i en klasse kan initialiseres i klassedeklarasjon – det samme 
kan du IKKE gjøre med datamedlemmer i en struktur (gir kompileringsfeil)


### Verdidatatype vs. Referansedatatype
Referansedatatype har to minneområder
- O-område med faktiske variabelverdi, ofte sammensatt.
- R-område med inneholder kun henvisning/referanse til variabelen sitt O-område.

Dersom vi utfører variabeltilordning, for eksempel (dersom y er av datatypen Random) setningen: 
`Random x = y;` vil kopiere innhold av y sitt «R»-område inn i minneområdet til x sitt «R»-område 
- Siden «R»-område til y inneholder kun adressen til y sitt «O»-område medfører dette at **x sitt «O» område er det samme som y sitt «O»-område.** 
- Altså: x blir et nytt navn (omtalt ofte som en ny referanse) til y sitt «O»-område

Verdidatatyper:
- «Numeric types» (int, char, … )
- bool
- Alle konstruerte struct-datatyper
- Alle konstruerte enum-datatyper
Referansedatatyper:
- string
- alle tabeller/lister
- klasse-datatyper
- delegat-datatyper
Merknad: datatypen string er spesiell: den er «immutable»: all verdiendring vil lage en ny streng som variabelen henviser til.

#### Struct vs. Klasse
Fordel med å bruke referansedatatyper (klasse) er at vi unngår å kopiere objekt-data. 
- Kopiering kan være svært ineffektiv dersom vi jobber med store objekter
	- Det er lettere å kopiere en adresse enn å kopiere et stort objekt
- Kopiering kan være svært ineffektiv dersom vi jobber med mange objekter
	- Detter forutsetter at et objekt er mer krevende å kopiere enn en adresse

#### Referansedatatyper – praktiske konsekvenser
Alle tilordninger skaper bare et nytt navn for eksisterende minneområder (tenker på «O»-områder) – deretter kan vi manipuler et minneområde (variabelverdien) ved å bruke to (eller flere) forskjellige navn

Ved argumentoverføring i funksjoner: argumenter av referansedatatyper trenger ikke nøkkelordet ref - disse vil uansett bli overført som referanser (det gjør dem til inn/ut-variabler – effekten av det du gjør på argumenter vil vedvare etter at funksjon er ferdigutført)
- For tabeller: dersom en tabell mottas som argument og endres i funksjonen vil endringene vedvare etter at funksjonen er utført
- For fil-skriving/lesing: formell og aktuell argument for en variabel av datatypen StreamWriter (som har åpnet en fil) vil skrive til en og samme fil
- Igjen: merk igjen at string (i utgangspunktet en referanse-datatype) som er «immutable» oppfører seg annerledes ved endring av verdien (dette gjelder også argumentoverføring)

Avansert (for øyeblikket): nøkkelordet kan ref brukes med variabler av referansetyper – men da 
for å kunne endre hva aktuell-argument-referanse referer til.








---


# Filbehandling
Vi kan bruke objekter av følgende datatyper:
- StreamReader – lesing fra filer // StreamWriter – skriving til filer
- Du bør ha using System.IO; i programkoden din dersom du bruker disse i programkoden din

## Skriving
```C#
// Et passende filbehandlings objekt må deklareres:
StreamWriter sw;
// Et passende fil må oprettes (alternativ åpnes):
sw = File.CreateText("Minfil.txt");
// (Objekt)variabelen sw kan brukes omtrent på samme måte som Console klassen når vi sender data til skjerm (Write eller WriteLine):
sw.Write(melding);
// NB! All data (inkludert tall) du sender vil bli lagret som tekst - En åpnet fil bør lukkes etter bruk:
sw.Close();
```

## Lesing
Tilsvarende steg som for «skriving til fil»
```C#
//Et passende filbehandlings objekt må deklareres:
StreamReader sr;
//Et passende fil må åpnes:
sr = File.OpenText("Minfil.txt");
// Objektvariabelen sr kan brukes omtrent på samme måte som Consoleklassen når vi leser data fra brukeren (ReadLine):
string data = sr.ReadLine();
// Merknad: mange andre metoder som kan brukes til fil-lesing finnes og kan brukes.
// Eksempel 1: sr.ReadToEnd();
// Eksempel 2: File.ReadAllLines(…);
// En åpnet fil bør lukkes etter et vi er ferdig med å lese:
sr.Close();
```

Vi kan teste om vi er kommet til filslutt før vi velger å lese videre:
```C#
StreamReader sr = File.OpenText("Personer.txt");
bool ferdig = sr.EndOfStream;
string navn;
while (!ferdig)
{
navn = sr.ReadLine();
Console.WriteLine(navn);
ferdig = sr.EndOfStream;
}
// Merk at lesekoden forutsetter en bestemt filstruktur – hva vil skje dersom filen har «ikke kompatibel» filstruktur?
```

 Filplassering (mappe) bør som oftest oppgis når vi åpner en fil:
```C#
StreamReader sr;
sr = File.OpenText("D:\\Arbeid\\info.txt");
eller
sr = File.OpenText(@"D:\Arbeid\info.txt");
```

# SerialPort
Et objekt av datatypen SerialPort må opprettes (med passende argumenter).
- Krever:
```C#
using System.IO.Ports;
```
- En passende bibliotek-pakke må installeres i prosjekt for VS2022.
	- Bruk Tools→«NuGet Package Manager» til å finne «System.IO.Ports» - Porten må åpnes (bruk try-catch til å håndtere eventuelle problemer).
- Oversikt over aktive porter kan fås ved å bruke
```C#
string [] allePorter = SerialPort.GetPortNames();
```
```C#
SerialPort sp = new SerialPort("COM3", 9600);
sp.Open(); if (sp.IsOpen) {
	// Lesing / skriving
} 
sp.Close();
```
Kode som leser / skriver (logikken må tilpasses problemstillingen):
```C#
if (sp.IsOpen)
{
	int antallByteSomKanLesesNaa = sp.BytesToRead;
	// Lesing
	// obs!lesing kan stoppe programmet inntil data er lest
	// logikken til programmet må tilpasses
	char etTegn = Convert.ToChar(sp.ReadChar());
	string enLinje = sp.ReadLine();
	// mange andre – ReadExisting() kan være meget nyttig
	// Skriving
	sp.Write("1234");
	sp.WriteLine("Bergen");
}
```

# Timer
Komponent av datatypen Timer (finnes i «Toolbox» der vi finner andre komponenter) kan brukes til å få GUI program til å utføre periodisk operasjon. Aktuelle Properties:
- Enabled – må settes til true når Timer skal brukes
- Interval – bestemmer hvor ofte operasjon skal utføres
- Name – navnet til Timer (objekt)variabelen i prosjektet
- Aktuelle hendelser og metoder:
- Tick – hendelse som oppstår når (Interval-definert) tid er gått
- private void t_Tick(object sender, EventArgs e) { … } – metode som utføres når hendelsen Tick har oppstått (når navnet til Timer-objekt-variabel er t)

# Stoppeklokke, måle excecution time
Ikke nøyaktig, men indikasjon
Programkode som kan brukes til å måle sorteringstiden (krever using System.Diagnostics;):
```C#
Stopwatch watch = new Stopwatch();
watch.Start();
// sorteringskode
watch.Stop();
long elapsedMs = watch.ElapsedMilliseconds;
```

# Snippets
## Exit GUI
Sist brukt av lærer: `Application.Exit();`

```C#
Environment.Exit(0);
```

## Alle tall delelig med 9
```C#
for (int i = 1; i <= 100; i++)
{
    if (i % 9 == 0)
    {
        Console.WriteLine(i);

    }
}
```


