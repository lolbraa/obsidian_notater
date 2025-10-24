#programmeringsspråk

[Cheatsheet](https://devhints.io/bash)
[Become a bash scripting pro (youtube)](https://www.youtube.com/watch?v=4ygaA_y1wvQ) med tilhørende [cheatsheet](https://learnxinyminutes.com/docs/bash/)

# Innebygde variabler
```
echo "Last program's return value: $?"
echo "Script's PID: $$"
echo "Number of arguments passed to script: $#"
echo "All arguments passed to script: $@"
echo "Script's arguments separated into different variables: $1 $2..."
```
# If Else
```bash
if [[ -z "$string" ]]; then
  echo "String is empty"
elif [[ -n "$string" ]]; then
  echo "String is not empty"
else
  echo "This never happens"
fi
```

# Subshell

# Variabelmanipulasjon
## Strings
```bash
# Lengde på variabel: 
${#variabel}

# Hvis variabelen ikke har fått en verdi ennå, default til en verdi: 
${variabel:-"standardverdi"}

# Hvis variabelen ikke har fått en verdi ennå, defualt OG SETT til en verdi:
${variabel:="standardverdi"}

#String substitution in variables:
echo "${variable/Some/A}" # => A string
# This will substitute the first occurrence of "Some" with "A".

echo "${variable:0:n}" # => Some st
# This will return only the first n characters of the value

echo "${variable: -5}" # => tring
# This will return the last 5 characters (note the space before -5).
# The space before minus is mandatory here.

# String length:
echo "${#variable}" # => 11

# Indirect expansion:
other_variable="variable"
echo ${!other_variable} # => Some string
# This will expand the value of `other_variable`.

# Brace Expansion {...}
# used to generate arbitrary strings:
echo {1..10} # => 1 2 3 4 5 6 7 8 9 10
echo {a..z} # => a b c d e f g h i j k l m n o p q r s t u v w x y z
# This will output the range from the start value to the end value.
```

## Arrays
```
# Declare an array with 6 elements:
array=(one two three four five six)

# Print the first element:
echo "${array[0]}" # => "one"

# Print all elements:
echo "${array[@]}" # => "one two three four five six"

# Print the number of elements:
echo "${#array[@]}" # => "6"

# Print the number of characters in third element
echo "${#array[2]}" # => "5"

# Print 2 elements starting from fourth:
echo "${array[@]:3:2}" # => "four five"

# Print all elements each of them on new line.
for item in "${array[@]}"; do
    echo "$item"
**done**
```