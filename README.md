![](https://raw.githubusercontent.com/jjcxdev/xscript/5d3dffe4ebf038f60c1616854c9baa5cf37ddfb4/xs.svg)

# XScript
XScript is a superset of JavaScript that emphasizes precise and explicit type management. In XScript, every numerical expression must be explicitly defined as either a string, enclosed in double quotes "", or as a number, prefixed with #. Failure to do so will result in a “Number type not defined” error, highlighting the language’s commitment to explicit type declaration. This document provides a comprehensive guide to the syntax, principles, and usage of XScript, with a focus on its unique approach to handling numeric types.

## Contents

1.	Introduction
2.	Resolving Logical Quirks in XScript
3.	Variable Declarations
4.	Numeric Operations
5.	Handling Non-Numeric Strings
6.	String to Number Conversion Rules
7.	Function Definitions
8.	Objects and Arrays
9.	Control Structures
10.	Error Handling
11.	Special Considerations
12.	Examples

## 1. Introduction

JavaScript, a mainstay in web development, is known for its versatility and ubiquity. However, its dynamic typing system can sometimes lead to type-related issues. TypeScript addressed these with a type-safe environment but at the cost of verbosity. XScript emerges to balance type safety with JavaScript’s simplicity, mandating explicit definition for every numeric literal. This clarity in type declaration enhances code predictability and conciseness, making XScript an effective tool for reducing type-related errors while maintaining JavaScript’s essence.

## 2. Addressing JavaScript’s Logical Quirks

XScript counters JavaScript’s type coercion quirks by enforcing explicit type handling, ensuring more predictable and error-resistant code.

1.	Zero and String Zero Comparison:
	•	JavaScript: `0 == "0"` returns true.
	•	XScript: Should be `#0 == "0"` in XScript. This is the correct explicit numeric declaration.
	
2.	Zero and Empty Array Comparison:
	•	JavaScript: `0 == []` returns true.
	•	XScript: The correct comparison in XScript would be `#0 == []`. However, this will result in an error in XScript due to type mismatch.
	
3.	Number and String Addition:
	•	JavaScript: `2 + "2"` results in `"22"`.
	•	XScript: Results in an error. In XScript, `#2` and `"2"` cannot be directly concatenated. They must be converted through variables before any operation.

4.	String Multiplication:
	•	JavaScript: `"2" * "3"` gives `6`.
	•	XScript: In XScript, direct conversion like `#"2"` is not allowed. Therefore, the multiplication of two strings should be done through variables. For example:
```javascript
let str1 = "2";
let str2 = "3";
let product = #str1 * #str2;  // This is valid in XScript.
```

5.	Null and Undefined Comparison:
	•	JavaScript: `null == undefined` is true.
	•	XScript: This comparison would not typically result in an error in XScript, as it doesn’t involve numeric literals.

6.	Array and Number Comparison:
	•	JavaScript: `[10] == 10` is true.
	•	XScript: In XScript, this should be `[#10] == #10`. However, this comparison would be false because an array and a number are different types, and XScript enforces strict type comparisons..

## 3. Variable Declarations

XScript follows JavaScript’s syntax with strict numeric literal rules.

```javascript
let a = "123"; // String
let b = #123;  // Number
let c = 123;   // Error: "Number type not defined"
```

## 4. Numeric Operations

Explicit numeric declaration is required for arithmetic operations.

```javascript
let sum = #a + #b; // Converts 'a' and 'b' to numbers
let total = a + b; // Error without explicit numeric declaration
```

## 5. Function Definitions

Functions in XScript require explicit numeric conversions.

```javascript
function multiply(x, y) {
    return #x * #y;
}
multiply("10", "20");  // Valid
multiply(10, 20);      // Error without explicit numeric declaration
```

## 6. Objects and Arrays

XScript adheres to standard JavaScript syntax with numeric type rules.

```javascript
let obj = { key: "value" };
let arr = ["10", "20", "30"].map(item => #item); // Convert strings to numbers
```

## 7. Control Structures

XScript uses familiar JavaScript syntax with strict numeric literal rules.

```javascript
if (#x > #10) { ... } // Explicit numeric declaration
```

## 8. Error Handling

XScript utilizes JavaScript’s try-catch mechanism with additional type-related errors.

```javascript
try {
    // Code with potential type errors
} catch (error) {
    // Handle specific type errors
}
```

9. Special Considerations

In XScript, both the # prefix for numbers and "" for strings are crucial for explicit type handling.

```javascript
let numString = "123";  // Declared as a string
let num = #numString;   // Correctly converts string to number using variable

console.log(num);       // Displays the number 123
console.log(numString); // Displays the string "123"

let incorrectNum = 123; // Error: "Number type not defined" without `#`
console.log(#incorrectNum); // Also an error, direct conversion is not allowed
```

The importance of explicit type declaration in XScript is emphasized here. Numeric literals must be prefixed with # when they are meant to be numbers, and strings must be enclosed in double quotes "". Direct conversion of literals from one type to another using these prefixes is not allowed; instead, conversion must be carried out through variables, as demonstrated in the examples.

## 10. Examples

Numeric Addition vs String Concatenation

JavaScript
```javascript
let a = "10";
let b = "20";
let numericAddition = parseInt(a) + parseInt(b); // 30
let stringConcatenation = a + b; // "1020"
```
TypeScript
```javascript
let a: string = "10";
let b: string = "20";
let numericAddition: number = parseInt(a) + parseInt(b); // 30
let stringConcatenation: string = a + b; // "1020"
```
XScript
```javascript
let a = "10";
let b = "20";
let numericAddition = #a + #b; // 30, using # for numeric operation
let stringConcatenation = a + b; // "1020", already in string context
```

Mixing Numbers and Strings in Operations

JavaScript
```javascript
let value = 5;
let text = "5";
let mixedAddition = value + parseInt(text); // 10
let mixedConcatenation = value.toString() + text; // "55"
```
TypeScript
```javascript
let value: number = 5;
let text: string = "5";
let mixedAddition: number = value + parseInt(text); // 10
let mixedConcatenation: string = value.toString() + text; // "55"
```
XScript
```javascript
let value = #5;
let text = "5";
let mixedAddition = value + #text; // 10, adding as numbers
let ""strValue = value;
let mixedConcatenation = strValue + text; // "55", concatenating as strings
```
Function Parameter Handling

JavaScript
```javascript
function addValues(val1, val2) {
    return parseInt(val1) + parseInt(val2); // Adds as numbers
}
function concatenateValues(val1, val2) {
    return val1.toString() + val2.toString(); // Concatenates as strings
}
```
TypeScript
```javascript
function addValues(val1: string, val2: string): number {
    return parseInt(val1) + parseInt(val2); // Adds as numbers
}
function concatenateValues(val1: string, val2: string): string {
    return val1 + val2; // Concatenates as strings
}
```
XScript
```javascript
function processValues(val1, val2) {
    return #val1 + #val2; // Adds as numbers, converting from strings
}
function concatenateValues(val1, val2) {
    return val1 + val2; // Concatenates as strings, no need for "" prefix if already strings
}
```
