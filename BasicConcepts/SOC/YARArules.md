## YARA Rules

#### Introduction
* Yara rules are set of rules that are used to identify a file based on its contents
* It's created by Victor Alvarez of VirusTotal

#### Structure & Syntax
The structure of YARA rules:

![image](https://github.com/Anas-Ehab/NotesHub/assets/55194408/8cc0cbba-5eb0-425e-910a-6ae6c148f25b)

* First we identify the rule name (Rule Identifier) which can be any alphanumeric character and the underscore character, but the first character cannot be a digit.
* Rule identifiers are case sensitive and cannot exceed 128 characters.
* The following are preserved keywords that can't be used as rule identifiers
  
  all	and	any	ascii at base64 base64wide condition contains endswith entrypoint false filesize
  for	fullword global import	icontains	iendswith	iequals	in include int16 int16be int32	int32be int8
  int8be istartswith	matches	meta	nocase none	not	of or	private	rule startswith	strings them true
  uint16 uint16be	uint32 uint32be	uint8	uint8be wide xor defined

* The meta is an optional section which is added to provide a description for the YARA rule or other additonal information but it doesnt affect the functionality of the rule
* The meta sections is identified with the keyword *meta:* and contains identifier/value pairs i.e. *description: "Yara Rule to detect .exe"*
* The strings definition section can be omitted if the rule doesn't rely on any string, but the condition section is always required.
