# Regular Expression
```python
import re

exampleRegEx = re.compile(r'\d\d\d-\d\d\d')
# For multiple suffixes: 
	re.compile(r'Bat(man|mobile|copter|bat)')

mo = exampleRegEx.search(<text>)
mo.groupt(<int>)
```

## Repetition in RegEx patterns
	• batRegEx = re.compile(r'Bat(wo)?man')
	# capture 0 or 1 'wo'
	
	• batRegEx = recompile(r'Bat(wo)*man')
	# capture >= 0 'wo'
	
	• batRegEx = recompile(r'Bat(wo)+man')
	# capture >= 1'wo'
	
	• batRegEx = recompile(r'Bat(wo){x}man')
	# capture exactly x 'wo'
	
	• batRegEx = recompile(r'Bat(wo){x, y}man')
	# capture exactly x-y 'wo'
Greedy/Non-Greedy specified by ? after {}, whereby {}? results in a non-greedy match


![](regex.png)

## Making your own character classes
vowelRegex = re.compile(r'[aeiouAEIOU]')

vowelRegex = re.compile(r'[aeiouAEIOU]{2}')
	# Two in a row vowels 
	
consonantsRegex = re.compile(r'[^aeiouAEIOU]')
	# Opposite character class
	
	• No need to escape characters inside square brackets when creating own character classes


## Caret/Dollar, Dot/Star characters

beginswithHelloRegEx = re.compile(r'^Hello')

endswithHelloRegEx = re.compile(r'world!$')

allDigitsRegEx = re.compile(r'^\d+&')

atRegEx = re.compile(r'.at') 
	# any prefix

Non-Greedy
nameRegEx = re.compile(r'First Name: (.*) Last name: (.*)') 
	# extract = 'First Name: Al Last Name: Sweigart'
	# Found : Al, Sweigart
	
Greedy
nameRegEx = re.compile(r'First Name: (.*?) Last name: (.*?)') 
	# extract = 'First Name: Al Last Name: Sweigart'
	# Found : Al, Sweigart

Up to new line character
dotstar = re.compile(r'.*')

Including new line character
dotstar = re.compile(r'.*', re.DOTALL)

Case insensitive matching
vowelRegex = re.compile(r'[aeiou]', re.I)

## Find and Replace

```python
namesRegex = re.compile(r'Agent \w+')
namesRegex.sub(<sub>, <string>)

```

## Verbose mode

Verbose Mode

Allows to enter spaces and comments in the compile
```python
re.compile(r'''
(\d\d\d-) |         # area code (without parens, with dash)
(\(\d\d\d\) )      # -or- area code with parens and no dash
\d\d\d                # first 3 digits
-                          # second dash
\d\d\d\d           # last 4 digits
''', re.I | re.DOTALL | re.VERBOSE)
```
