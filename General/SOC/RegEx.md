# Regular Expressions
* RegEx are enclosed between */ /*
  
* To specify a set of characters enclose them in *[]*: In example *[ab]* - Matches a or b.
* *[]* followed by a *+* can be used to specify unlimited numbers of matches: *[0-9]+* - Any character from 0 to 9 that's of lenght 1 or more.
* *[]* followed by *{#}* specify a limited number of matches: *[0-9]{5}* - Any characters from 0 to 9 that are of a length that's exactly 5.
* *[]* followed by *{#,#}* specify a limited number of matches (From # to #): *[0-9]{5,8}* - Any characters from 0 to 9 that are of a length that's between 5 and 8.
* *[]* followed by *{#,}* specify a limited number of matches (From # to unlimited): *[0-9]{5,8}* - Matches 01111 11111 99999 011111 11111111

## Meta characters
* *\d* - matches any digit character equivalent to *[0-9]*
* *\w* - matches any word character equivalent to *[a-zA-Z0-9_'s]*
* *\s* - matches any whitespace character (spaces/tabs)
* *\t* - matches tab characters.
* Can be followed by *{}* to specify number of matches. (i.e. *\d{3}* - 3 digit characters)

## Special Characters
* *+* - One or more.
* *\* - The escape character.
* *[]* - Character set.
* *[^]* - Negate Symbol in a character set.
* *?* - 0-or-1 quantifier (Any optional character Applied to the character before it.)
* *.* - Match any character (Except the newline character)
* *\** - Zero or more quantifier (Similar to *+*)
* Special characters can be combined (i.e. .+ will match anything)
* *^* - Start symbol (Different than when placed inside the [])
* *$* - End symbol.
