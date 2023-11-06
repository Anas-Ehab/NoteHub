# Regular Expressions
* RegEx are enclosed between */ /*
* To specify a set of characters enclose them in *[]*: In example *[ab]* - Matches a or b.
* *[]* followed by a *+* can be used to specify unlimited numbers of matches: *[0-9]+* - Matches 0 & 01 & 11 & 21111221111
* *[]* followed by *{#}* specify a limited number of matches: *[0-9]{5}* - Matches 01111 11111 99999
* *[]* followed by *{#,#}* specify a limited number of matches (From # to #): *[0-9]{5,8}* - Matches 01111 11111 99999 011111 11111111
