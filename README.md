![](https://raw.githubusercontent.com/jjcxdev/xscript/5d3dffe4ebf038f60c1616854c9baa5cf37ddfb4/xs.svg)

# XScript
XScript is a superset of JavaScript that emphasizes precise and explicit type management. In XScript, every numerical expression must be explicitly defined as either a string, enclosed in double quotes "", or as a number, prefixed with #. Failure to do so will result in a “Number type not defined” error, highlighting the language’s commitment to explicit type declaration. This document provides a comprehensive guide to the syntax, principles, and usage of XScript, with a focus on its unique approach to handling numeric types.

## Contents

1. Introduction
2. Syntax and Features
3. Addressing JavaScript’s Logical Quirks
4. Variable Declarations
5. Numeric Operations and Conversion Rules
6. Function Definitions
7. Invalid Conversion Attempts
8. Objects, Arrays, and Extended Syntax for Arrays
9. Control Structures
10. Error Handling and Special Considerations
11. Examples

## 1. Introduction
JavaScript, a mainstay in web development, is known for its versatility and ubiquity. However, its dynamic typing system can sometimes lead to type-related issues. TypeScript addressed these with a type-safe environment but at the cost of verbosity. XScript emerges to balance type safety with JavaScript’s simplicity, mandating explicit definition for every numeric literal. This clarity in type declaration enhances code predictability and conciseness, making XScript an effective tool for reducing type-related errors while maintaining JavaScript’s essence.

## 2. Syntax and Features
XScript redefines JavaScript's approach to type handling with clear rules:
- **Explicit Numeric Declaration**: All numeric literals must be declared as a string (`"123"`) or as a numeric value with `#` (e.g., `#123`). 
- **String and Number Handling**: Strings can contain mixed characters, but numbers declared with `#` must be purely numeric (integers or floats).
- **Variable-based Conversion**: Direct conversion of strings to numbers using `#` (like `#"123"`) is not allowed. Instead, conversion must be done through variables.
- **Error Prevention**: XScript provides clear error messages for type mismatches and incorrect declarations.
- **Explicit String Conversion Syntax in XScript**: In XScript, `""` is used as a prefix to explicitly convert a variable's value into a string. This is particularly important when you want to ensure the variable is treated as a string, especially in operations that depend on the data type, such as concatenation.

### Example of Explicit String Conversion
###### XScript
```javascript
// XScript example for explicit string conversion
let numericValue = #123; // A numeric value
let stringifiedNumber = "" + numericValue; // Explicitly converts the numeric value 123 to a string "123"

// Demonstrating its use in string concatenation
let concatenationResult = stringifiedNumber + " is a string"; // "123 is a string"

// In this case, without the "" prefix, the operation could lead to a type error or unintended results.
```
This example illustrates the conversion of a numeric value to a string by prefixing it with `""`. This explicit conversion is crucial for string concatenations and operations where the string representation of a number is necessary.
- **Simplified Equality Comparison**: In XScript, the `==` operator is designed to behave like JavaScript's `===` operator, performing strict type and value comparison. This means that XScript inherently does not perform type coercion in equality checks, rendering the `===` operator unnecessary. In XScript, using `==` ensures both operands are of the same type and then compares their values.

### Example of Simplified Equality Comparison
###### XScript
```javascript
// In XScript, '==' performs strict comparison, similar to '===' in JavaScript.
let numericValue = #123;
let stringValue = "123";
let areEqual = numericValue == stringValue; // False, as one is a number and the other is a string.

// This strict comparison makes the '===' operator redundant in XScript.
```

## 3. Addressing JavaScript’s Logical Quirks
XScript counters JavaScript’s type coercion quirks by enforcing explicit type handling, ensuring more predictable and error-resistant code. The quirks and XScript's handling of them are detailed in this section.

### Zero and String Zero Comparison:

```javascript
// JavaScript
// In JavaScript, comparing a numeric zero with a string '0' returns true due to type coercion.
let isEqualJS = 0 == "0"; // returns true

// TypeScript
// TypeScript also enforces type safety, so a comparison like this would be flagged during compilation.
let numericZeroTS: number = 0;
let stringZeroTS: string = "0";
let isEqualTS = numericZeroTS == stringZeroTS; // TypeScript error: Type 'number' is not comparable to type 'string'.

// XScript
// In XScript, the '==' operator is designed to behave like JavaScript's '==='.
let numericZero = #0; // Numeric zero
let stringZero = "0"; // String zero
let isEqualXScript = numericZero == stringZero; // False, as XScript's '==' does not perform type coercion
```
	
### Zero and Empty Array Comparison:

```javascript
// JavaScript
// In JavaScript, comparing zero with an empty array returns true.
let isEqualToArrayJS = 0 == []; // returns true

// TypeScript
// TypeScript will identify this as an error due to strict type checking.
let emptyArrayTS: any[] = [];
let isEqualToArrayTS: boolean = 0 == emptyArrayTS; // TypeScript error: Type 'number' is not comparable to type 'any[]'.

// XScript
// In XScript, an empty array and a number are considered different types.
let emptyArray = []; // An empty array
let numericZeroXScript = #0; // Numeric zero in XScript

// Comparing a numeric value with an array results in an error in XScript.
let isEqualToArrayXScript = numericZeroXScript == emptyArray; // Results in an error

// The error arises because XScript strictly enforces type safety and does not perform implicit type conversions between arrays and numbers.
```
	
### Number and String Addition:

```javascript
// JavaScript
// In JavaScript, adding a number and a string results in string concatenation.
let additionJS = 2 + "2"; // Results in "22" due to implicit type coercion.

// TypeScript
// TypeScript allows this operation, resulting in string concatenation.
let numTS: number = 2;
let strTS: string = "2";
let additionTS: string = numTS + strTS; // "22"

// XScript
// Attempting to add a number directly to a string results in an error in XScript.
let num = #2;
let str = "2";
let additionXScript = num + str; // Error: Cannot directly add a number and a string
```

### String Multiplication:

```javascript
// JavaScript
// In JavaScript, multiplying two stringified numbers performs implicit conversion to numbers and then multiplies.
let productJS = "2" * "3"; // Results in 6.

// TypeScript
// TypeScript allows string multiplication due to JavaScript's implicit coercion.
let productTS: number = "2" * "3"; // 6

// XScript
// In XScript, direct conversion like `#"2"` is not allowed. Multiplication should be done through variables.
let str1 = "2";
let str2 = "3";
let productXScript = #str1 * #str2; // Valid in XScript: Both strings are converted to numbers before multiplication.
```

### Null and Undefined Comparison:

```javascript
// JavaScript
// In JavaScript, null and undefined are considered equal.
let isEqualJS = null == undefined; // true

// TypeScript
// TypeScript follows JavaScript's behavior for null and undefined comparison.
let isEqualNullUndefinedTS: boolean = null == undefined; // true

// XScript
// In XScript, the behavior of comparing null and undefined remains the same as JavaScript for practicality.
let isEqualXScript = null == undefined; // true
```

### Array and Number Comparison:

```javascript
// JavaScript
// In JavaScript, comparing an array containing a single number to that number returns true due to type coercion.
let isEqualToArrayJS = [10] == 10; // true

// TypeScript
// TypeScript will also treat this as a type mismatch, similar to XScript.
let arrayTS: number[] = [10];
let isEqualToArrayTS: boolean = arrayTS == 10; // TypeScript error: Type 'number[]' is not comparable to type 'number'.

// XScript
// In XScript, strict type comparisons are enforced.
let arrayXScript = [#10];
let numberXScript = #10;
let isEqualToArrayXScript = arrayXScript == numberXScript; // false, as an array and a number are different types.
```

## 4. Variable Declarations
XScript follows JavaScript’s syntax with strict numeric literal rules. Examples of variable declarations in XScript are provided, showcasing the explicit type declaration requirement.

###### XScript
```javascript
let str = "123"; // String
let num = #123;  // Number
let notDefined = 123; // Error: "Number type not defined"
```

## 5. Numeric Operations and Conversion Rules
This section covers explicit numeric operations and rules for converting strings to numbers, emphasizing the use of variables for conversion and the prohibition of direct conversion.

###### XScript
```javascript
let strNum1 = "100";
let strNum2 = "200";
let num1 = #strNum1;  // Converts string to number
let num2 = #strNum2;  // Converts string to number
let sum = num1 + num2; // Correct numeric addition

let directConversion = #"100"; // Error: Direct conversion not allowed
```
### Handling of Number Strings in XScript

XScript allows for the explicit conversion of strings that represent numerical values into actual numbers. This is particularly useful when dealing with data that comes in string format but is essentially numerical (like user input or data from a file).

###### XScript
```javascript
// XScript example for converting a string representation of a number
let strNumber = "123"; // A string representing a number
let convertedNumber = #strNumber; // Explicitly converts the string "123" to the numeric value 123

// This conversion is crucial for performing numeric operations on string inputs.
let sum = convertedNumber + #25; // Performs numeric addition: 123 + 25 = 148
```
In this example, #strNumber converts the string `"123"` into the number `123`, enabling accurate numeric operations.

## 6. Function Definitions
Function definitions in XScript require explicit numeric conversions for parameters. Examples demonstrate how functions are defined and used with XScript's type rules.

### Numeric Addition

```javascript
// JavaScript
// Function to add two numbers, interpreted as strings.
function addNumbersJS(strNum1, strNum2) {
    return parseInt(strNum1) + parseInt(strNum2);
}
let resultJS = addNumbersJS("10", "20"); // Valid: 30
 
// TypeScript
// Function to add two numbers, with string inputs converted to numbers.
function addNumbersTS(num1: string, num2: string): number {
    return parseInt(num1) + parseInt(num2);
}
let resultTS = addNumbersTS("10", "20"); // Valid: 30

// XScript
// Function to add two numbers, with string inputs converted to numbers.
function addNumbers(strNum1, strNum2) {
    return #strNum1 + #strNum2;
}
let result = addNumbers("10", "20"); // Valid: Converts strings to numbers and adds them
```

### String Concatenation

```javascript
// JavaScript
// Function to concatenate two numbers as strings.
function concatenateNumbersJS(num1, num2) {
    return num1.toString() + num2.toString();
}
let concatenatedResultJS = concatenateNumbersJS(10, 20); // "1020"

// TypeScript
// Function to concatenate two numbers as strings.
function concatenateNumbersTS(num1: number, num2: number): string {
    return num1.toString() + num2.toString();
}
let concatenatedResultTS = concatenateNumbersTS(10, 20); // "1020"

// XScript
// Function to concatenate two numbers as strings.
function concatenateNumbers(num1, num2) {
    let ""str1 = num1; // Explicitly converting number to string
    let ""str2 = num2;
    return str1 + str2;
}
let concatenatedResult = concatenateNumbers(#10, #20); // Valid: Concatenates "10" and "20" as strings.
```

### Conditional Function

```javascript
// JavaScript
// Function to check if a number is greater than a threshold.
function isGreaterThanThresholdJS(num, threshold) {
    return num > threshold;
}
let isGreaterJS = isGreaterThanThresholdJS(15, 10); // Valid: Checks if 15 is greater than 10.

// TypeScript
// TypeScript function with type annotations to check if a number is greater than a threshold.
function isGreaterThanThresholdTS(num: number, threshold: number): boolean {
    return num > threshold;
}
let isGreaterTS = isGreaterThanThresholdTS(15, 10); // Valid: Checks if 15 is greater than 10.

// XScript
// Function to check if a number is greater than a threshold.
function isGreaterThanThreshold(strNum, threshold) {
    let num = #strNum; // Convert string to number
    let numThreshold = #threshold;
    return num == numThreshold; // Uses XScript's '==' for strict comparison
}
let isGreater = isGreaterThanThreshold("15", "10"); // False, as '15' is not equal to '10'
```

## 7. Invalid Conversion Attempts
XScript's strict rules for type conversions aim to prevent common errors related to type mismatch. The following examples illustrate scenarios where XScript would throw errors due to invalid conversion attempts:

### Non-Numeric String Conversion
###### XScript
```javascript
// Attempting to convert a non-numeric string to a number.
let invalidNum1 = #"abc"; // Error: Throws an error due to non-numeric characters.
```

### Boolean to Number Conversion
###### XScript
```javascript
// Attempting to convert a boolean value to a number.
let invalidNum2 = #true; // Error: Throws an error as true is not a numeric value.
```

### Array to Number Conversion
###### XScript
```javascript
// Attempting to convert an array directly to a number.
let invalidNum3 = #[1, 2, 3]; // Error: Throws an error as it's an array, not a numeric string.
```

These examples demonstrate the kinds of operations that are not allowed in XScript, emphasizing the importance of adhering to its explicit numeric declaration rules. Understanding these limitations is crucial for developers to effectively use XScript and avoid runtime errors.

## 8. Objects, Arrays, and Extended Syntax for Arrays
XScript adheres to standard JavaScript syntax for objects and arrays, with additional rules for numeric types. This section also introduces the extended prefix syntax for arrays, allowing for concise and efficient type conversions.

###### XScript
```javascript
// Objects and Arrays
let obj = { key: "value" };
let arr = ["10", "20", "30"].map(item => #item); // Convert string to numbers

// Extended Syntax for Arrays
let stringNumbers = ["1", "2", "3"];
let numbers = #[...stringNumbers]; // Converts all elements to numbers
```
## 9. Control Structures
Control structures such as loops and conditionals in XScript follow JavaScript syntax but require explicit numeric literal rules for any numeric values used.

### Numeric Summation of Array Elements

###### XScript
```javascript
let limit = #10;
for (let i = #0; i < limit; i++) {
    console.log(i); // Loop with explicit numeric values
}

let condition = #5;
if (condition > #3) {
    console.log("Condition met."); // Conditional with explicit numeric values
}
```

## 10. Error Handling and Special Considerations
XScript uses JavaScript’s try-catch mechanism for error handling, with additional focus on type-related errors. Special considerations for handling strings and numbers are discussed, emphasizing the importance of explicit type declaration.

##### Numeric Addition vs String Concatenation
###### JavaScript
```javascript
// JavaScript example demonstrating error handling
try {
    let num = parseInt("123");
    let invalid = parseInt("abc"); // This will not throw an error but will result in NaN
} catch (error) {
    console.error("Caught error:", error.message);
}
```
###### XScript
```javascript
// XScript example demonstrating type-related error handling
try {
    let numValue = #50;
    let invalidValue = #"abc"; // Error: String "abc" cannot be converted to number
} catch (error) {
    console.error("Caught error:", error.message); // Handles the type conversion error
}

// Demonstrating explicit string conversion in XScript
let stringValue = "" + numValue; // Explicitly converting number to string
console.log("Number as string:", stringValue);
```
In the XScript example, the `try-catch` block is used to handle errors resulting from incorrect type usage, like attempting to convert a non-numeric string to a number. The JavaScript example is corrected to use standard JavaScript syntax, showcasing typical error handling in JavaScript. This comparison helps to illustrate how XScript enhances error handling, particularly for type-related issues.

## 11. Examples
The examples section illustrates various scenarios in JavaScript, TypeScript, and XScript, highlighting the differences in how each language handles type conversions, operations, and structure handling.

### Numeric Addition vs String Concatenation

```javascript
// JavaScript
let jsNum1 = "10";
let jsNum2 = "20";
let jsNumericAddition = parseInt(jsNum1) + parseInt(jsNum2); // 30
let jsStringConcatenation = jsNum1 + jsNum2; // "1020"

// TypeScript
let tsNum1: string = "10";
let tsNum2: string = "20";
let tsNumericAddition: number = parseInt(tsNum1) + parseInt(tsNum2); // 30
let tsStringConcatenation: string = tsNum1 + tsNum2; // "1020"

// XScript
let xsNum1 = "10";
let xsNum2 = "20";
let xsNumericAddition = #xsNum1 + #xsNum2; // 30
let xsStringConcatenation = xsNum1 + xsNum2; // "1020"
```
### Mixing Numbers and Strings

```javascript
// JavaScript
let jsValue = 5;
let jsText = "5";
let jsMixedAddition = jsValue + parseInt(jsText); // 10
let jsMixedConcatenation = jsValue.toString() + jsText; // "55"

// TypeScript
let tsValue: number = 5;
let tsText: string = "5";
let tsMixedAddition: number = tsValue + parseInt(tsText); // 10
let tsMixedConcatenation: string = tsValue.toString() + tsText; // "55"

// XScript
let xsValue = #5;
let xsText = "5";
let xsMixedAddition = xsValue + #xsText; // 10
let ""xsStrValue = xsValue;
let xsMixedConcatenation = xsStrValue + xsText; // "55"
```
