## YARA Rules (https://yara.readthedocs.io/en/stable/writingrules.html#:~:text=Text%20strings%20are%20enclosed%20in,not%20allowed%20in%20hex%20strings.)

### Introduction
* Yara rules are set of rules that are used to identify a file based on its contents
* It's created by Victor Alvarez of VirusTotal

### Structure & Syntax
The structure of YARA rules:

![image](https://github.com/Anas-Ehab/NotesHub/assets/55194408/8cc0cbba-5eb0-425e-910a-6ae6c148f25b)

#### Rule Indetifier
* First we identify the rule name (Rule Identifier) which can be any alphanumeric character and the underscore character, but the first character cannot be a digit.
* Rule identifiers are case sensitive and cannot exceed 128 characters.
* The following are preserved keywords that can't be used as rule identifiers
  
  all	and	any	ascii at base64 base64wide condition contains endswith entrypoint false filesize
  for	fullword global import	icontains	iendswith	iequals	in include int16 int16be int32	int32be int8
  int8be istartswith	matches	meta	nocase none	not	of or	private	rule startswith	strings them true
  uint16 uint16be	uint32 uint32be	uint8	uint8be wide xor defined

#### Meta Section
* The meta is an optional section which is added to provide a description for the YARA rule or other additonal information but it doesnt affect the functionality of the rule
* The meta sections is identified with the keyword *meta:* and contains identifier/value pairs i.e. *description: "Yara Rule to detect .exe"*

#### Strings Section
* The strings definition section can be omitted if the rule doesn't rely on any string, but the condition section is always required.
* Each string has an identifier consisting of a $ character followed by a sequence of alphanumeric characters and underscores.
* Strings can be defined in text or hexadecimal form.
* Text strings are enclosed in double quotes ($StringVariable = "String")
* Hex strings are enclosed by curly brackets, and they are composed by a sequence of hexadecimal numbers that can appear contiguously or separated by spaces ($HexVariable = {1A 2B})

##### Strings Types
* There are three types of strings in YARA: hexadecimal strings, text strings and regular expressions.

###### Hexadecimal Strings
* Hexadecimal strings allow four special constructions that make them more flexible: wild-cards, not operators, jumps, and alternatives.
* Wild-cards are just placeholders that you can put into the string indicating that some bytes are unknown and they should match anything.
* The placeholder character is the question mark (?).
* The wild-cards are nibble-wise (4 bits), which means that you can define just one nibble of the byte and leave the other unknown.
* Example: *$hex_string = { E2 34 ?? C8 A? FB }*

* Starting with version 4.3.0, you may specify that a byte is not a specific value using the not operator (*~*).
* The not operator can also be used with nibble-wise wild-cards, so the second string, in the following example, will only match if the second nibble is not zero.
* Example: *$hex_string = { F4 23 ~00 62 B4 } $hex_string2 = { F4 23 ~?0 62 B4 }*

* Jumps are a pair of numbers enclosed in square brackets and separated by a hyphen.
* Example: *$hex_string = { F4 23 [4-6] 62 B4 }*
* In the case of the example, any arbitrary sequence from 4 to 6 bytes can occupy the position of the jump.
* Example for valid hex strings according to the provided example:
  * F4 23 *01 02 03 04* 62 B4
  * F4 23 *00 00 00 00 00* 62 B4
  * F4 23 *15 82 A3 04 45 22* 62 B4

* Any jump *[X-Y]* must meet the condition *0 <= X <= Y*.
* In previous versions of YARA both X and Y must be lower than 256, but starting with YARA 2.0 there is no limit for X and Y.
* Valid jump examples:
  * FE 39 45 [0-8] 89 00
  * FE 39 45 [23-45] 89 00
  * FE 39 45 [1000-2000] 89 00
 
* Invalid jump examples:
  * FE 39 45 [10-7] 89 00
 
* If the lower and higher bounds are equal you can write a single number enclosed in brackets:
  * *FE 39 45 [6] 89 00* which is equivalent to:
  * FE 39 45 [6-6] 89 00
  * FE 39 45 ?? ?? ?? ?? ?? ?? 89 00

* Starting with YARA 2.0 you can also use unbounded jumps:
  * FE 39 45 [10-] 89 00 (10 - infinite)
  * FE 39 45 [-] 89 00 (infinite - infinite)

* A syntax which resembles a regular expression can be used to provide different alternatives for a given fragment of your hex string
* Example:
  * $hex_string = { F4 23 ( 62 B4 | 56 ) 45 } (F4 23 62 B4 45 or F4 23 56 45)

* There are no limits to the amount of alternative sequences you can provide, and neither to their lengths.
* Strings containing wild-cards are allowed as part of alternative sequences.
* Example:
  * $hex_string = { F4 23 ( 62 B4 | 56 | 45 ?? 67 ) 45 }

###### Text Strings
* In its simplest case, text strings are provided as an ASCII-encoded, case-sensitive string. However, text strings can be accompanied by some useful modifiers that alter the way in which the string will be interpreted.
* Those modifiers are appended at the end of the string definition separated by spaces.

* Escape Sequeneces (Needs clarification):
  * \"	Double quote
  * \\	Backslash
  * \r	Carriage return
  * \t	Horizontal tab
  * \n	New line
  * \xdd	Any byte in hexadecimal notation

* Text strings in YARA are case-sensitive by default, to make a string case insensitive, the modifier *nocase* is used.
  * Example: $text_string = "foobar" nocase (Will match Foobar, FOOBAR, and fOoBaR)
  * It can be used in conjunction with any modifier, except *base64*, *base64wide*, and *xor*.

* The wide modifier can be used to search for strings encoded with two bytes per character.
  * Example: $wide_string = "Borland" wide (Will match B\x00o\x00r\x00l\x00a\x00n\x00d\x00)
  * Keep in mind that this modifier just interleaves the ASCII codes of the characters in the string with zeroes, it does not support truly UTF-16 strings containing non-English characters.
  * To search for strings in both ASCII and wide form, you can use the ascii modifier in conjunction with wide , no matter the order in which they appear ($wide_and_ascii_string = "Borland" wide ascii)
  * The ascii modifier can appear alone, without an accompanying wide modifier, but it's not necessary to write it because in absence of wide the string is assumed to be ASCII by default.
  * 



#### Condition Section
* The condition section is where the logic of the rule resides.
* This section must contain a boolean expression telling under which circumstances a file or process satisfies the rule or not. ($StringVariable or $HexVariable)
* Previously defined strings by using their identifiers are used as a boolean variable


#### Comments
* Comments can be added using *//* for single line comments and using */* */* for multi-line comments

#### Extra
* In all versions of YARA before 4.1.0 text strings accepted any kind of unicode characters, regardless of their encoding. Those characters were interpreted by YARA as raw bytes, and therefore the final string was actually determined by the encoding format used by your text editor. This never meant to be a feature, the original intention always was that YARA strings should be ASCII-only and YARA 4.1.0 started to raise warnings about non-ASCII characters in strings. This limitation does not apply to strings in the metadata section or comments. See more details [here](https://github.com/VirusTotal/yara/wiki/Unicode-characters-in-YARA)
* 
