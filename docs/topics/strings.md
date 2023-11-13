[//]: # (title: Strings)

Strings in Kotlin are represented by the type [`String`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-string/).
Generally, a string value is a sequence of characters in double quotes (`"`):

```kotlin
val str = "abcd 123"
```

Elements of a string are characters that you can access via the indexing operation: `s[i]`.
You can iterate over these characters with a `for` loop:

```kotlin
fun main() {
    val str = "abcd"
    //sampleStart
    for (c in str) {
    println(c)
}
//sampleEnd
}
```
{kotlin-runnable="true" kotlin-min-compiler-version="1.3"}

Strings are immutable. Once you initialize a string, you can't change its value or assign a new value to it.
All operations that transform strings return their results in a new `String` object, leaving the original string unchanged:

```kotlin
fun main() {
//sampleStart
    val str = "abcd"
   
    // create and print a new String object
    println(str.uppercase())
    // ABCD
   
    // the original string remains the same
    println(str) 
    // abcd
//sampleEnd
}
```
{kotlin-runnable="true" kotlin-min-compiler-version="1.3"}

To concatenate strings, use the `+` operator. This also works for concatenating strings with values of other types, as long
as the first element in the expression is a string:

```kotlin
fun main() {
//sampleStart
    val s = "abc" + 1
    println(s + "def")
    // abc1def    
//sampleEnd
}
```
{kotlin-runnable="true" kotlin-min-compiler-version="1.3"}

> In most cases using [string templates](#string-templates) or [multiline strings](#multiline-strings) is preferable to string concatenation.
> 
{type="note"}

## String literals

Kotlin has two types of string literals:

* [Escaped strings](#escaped-strings)
* [Multiline strings](#multiline-strings)

### Escaped strings

_Escaped strings_ can contain escaped characters.  
Here's an example of an escaped string:

```kotlin
val s = "Hello, world!\n"
```

Escaping is done in the conventional way, with a backslash (`\`).  
See [Characters](characters.md) page for the list of supported escape sequences.

### Multiline strings

_Multiline strings_ can contain newlines and arbitrary text. It is delimited by a triple quote (`"""`), contains no escaping and can contain newlines and any other characters:

```kotlin
val text = """
    for (c in "foo")
        print(c)
"""
```

To remove leading whitespace from multiline strings, use the [`trimMargin()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/trim-margin.html) function:

```kotlin
val text = """
    |Tell me and I forget.
    |Teach me and I remember.
    |Involve me and I learn.
    |(Benjamin Franklin)
    """.trimMargin()
```

By default, a pipe symbol `|` is used as margin prefix, but you can choose another character and pass it as a parameter, like `trimMargin(">")`.

## String templates

String literals may contain _template expressions_ – pieces of code that are evaluated and whose results are concatenated into the string.
A template expression starts with a dollar sign (`$`) and consists of either a name:

```kotlin
fun main() {
//sampleStart
    val i = 10
    println("i = $i") 
    // i = 10
//sampleEnd
}
```
{kotlin-runnable="true" kotlin-min-compiler-version="1.3"}

or an expression in curly braces:

```kotlin
fun main() {
//sampleStart
    val s = "abc"
    println("$s.length is ${s.length}") 
    // abc.length is 3
//sampleEnd
}
```
{kotlin-runnable="true" kotlin-min-compiler-version="1.3"}

You can use templates both in multiline and escaped strings.
To insert the dollar sign `$`  in a multiline string (which doesn't support backslash escaping) before any symbol,
which is allowed as a beginning of an [identifier](https://kotlinlang.org/docs/reference/grammar.html#identifiers),
use the following syntax:

```kotlin
val price = """
${'$'}_9.99
"""
```
## String formatting
To deal with complex formatting requirements, use the `String.format()` function.  It uses a format string that defines 
how the given arguments look like. The format string contains placeholders (`%`)  and
[format specifiers](https://docs.oracle.com/javase/8/docs/api/java/util/Formatter.html). In the output, 
the arguments replace the placeholders and show the format that the specifiers define:

```kotlin
fun main() {
    //sampleStart
    // format to add zeroes and make a length of seven
    val integerNumber = String.format("%07d", 31416)
    println(integerNumber)
    // 0031416

    // format with four decimals and sign
    val floatNumber = String.format("%+.4f", 3.141592)
    println(floatNumber)
    // +3.1416

    // format with upper case for two placeholders
    val string = String.format("%S %S", "hello", "world")
    println(string)
    // HELLO WORLD
    //sampleEnd
}

```
{kotlin-runnable="true" kotlin-min-compiler-version="1.3"}

This function provides similar functionality to string templates. In comparison, the `String.format()` function is 
more versatile because you have many options for formatting, and it happens during runtime. In contrast, this function is 
also more error-prone because it is easy to mismatch the number or position of the arguments with their corresponding placeholders.