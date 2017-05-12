![](assets/images/regex.gif)

# Regular Expressions
Searching for patterns

### Resources
* [Rubular](http://rubular.com/)
* [A good video](https://youtu.be/EkluES9Rvak) + [corresponding app](http://leaverou.github.io/regexplained/)

### Notes
* `/` everything between slashes `/`
* case sensitive by default
* Metacharacters have a meaning. If you need to match a metacharacter, you have to `\` escape them in most cases
	* `[`, `{`, `(`, `)`, `\`, `^`, `$`, `.`, `|`, `?`, `*`, `+`
* Engine is greedy, will always match as much as possible by default
* parentheses capture groups

### Examples
Validate a hex

	/^#([a-f\d]{3}){1,2}$/i

A 6+ letter password with at least: one number, one letter and one symbol
	
	/^(?=.*\d)(?=.*[a-z])(?=.*[\W_]).{6,}$/i

Any number that's NOT divisible by 50

	/\b(?!\d+[50]0)\d+\b/

Anything that doesn't contain "foo"

	/^(?!.*foo).+$/

## Quick Reference

	[abc]		// A single character of: a, b, or c
	[^abc]		// Any single character except: a, b, or c
	[a-z]		// Any single character in the range a-z
	[a-zA-Z]	// Any single character in the range a-z or A-Z
	^		// Start of line
	$		// End of line
	\A		// Start of string
	\z		// End of string
	.		// Any single character
	\s		// Any whitespace character
	\S		// Any non-whitespace character
	\d		// Any digit
	\D		// Any non-digit
	\w		// Any word character (letter, number, underscore)
	\W		// Any non-word character
	\b		// Any word boundary
	(...)		// Capture everything enclosed
	(a|b)		// a or b
	a?		// Zero or one of a
	a*		// Zero or more of a
	a+		// One or more of a
	a{3}		// Exactly 3 of a
	a{3,}		// 3 or more of a
	a{3,6}		// Between 3 and 6 of a