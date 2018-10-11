# 1. Code guidelines Complement 
## 1.1 Use Javadoc standard comments
Every file should have a copyright statement at the top, followed by package and import statements 
(each block separated by a blank line) and finally the class or interface declaration. In the Javadoc comments, 
describe what the class or interface does.

```java
/*
 * Copyright 2017 The Android Open Source Project
 *
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *      http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */

package com.android.internal.foo;

import android.os.Blah;
import android.view.Yada;

import java.sql.ResultSet;
import java.sql.SQLException;

/**
 * Does X and Y and provides an abstraction for Z.
 */

public class Foo {
    ...
}
```

Every class and nontrivial public method you write must contain a Javadoc comment with at least one sentence describing what the class or method does. This sentence should start with a third person descriptive verb.

Examples:


```java
/** Returns the correctly rounded positive square root of a double value. */
static double sqrt(double a) {
    ...
}
```
or 

```java
/**
 * Constructs a new String by converting the specified array of
 * bytes using the platform's default character encoding.
 */
public String(byte[] bytes) {
    ...
}
```
You do not need to write Javadoc for trivial get and set methods such as setFoo() if all your Javadoc would say is "sets Foo". If the method does something more complex (such as enforcing a constraint or has an important side effect), then you must document it. If it's not obvious what the property "Foo" means, you should document it.

Every method you write, public or otherwise, would benefit from Javadoc. Public methods are part of an API and therefore require Javadoc. Android does not currently enforce a specific style for writing Javadoc comments, but you should follow the instructions [How to Write Doc Comments for the Javadoc Tool](https://www.oracle.com/technetwork/java/javase/documentation/index-137868.html).

## 1.2 Use TODO comments

Use TODO comments for code that is temporary, a short-term solution, or good-enough but not perfect. 
TODOs should include the string TODO in all caps, followed by a colon:

```
// TODO: Remove this code after the UrlTable2 has been checked in.
```
and 
```
// TODO: Change this to use a flag instead of a constant.
```
If your TODO is of the form "At a future date do something" make sure that you either include a very specific date ("Fix by November 2005") or a very specific event ("Remove this code after all production mixers understand protocol V7.").

## 1.3 Naming
### 1.3.1 Rules common to all identifiers
Identifiers use only ASCII letters and digits, and, in a small number of cases noted below, underscores. Thus each valid identifier name is matched by the regular expression \w+ .

In Google Style, special prefixes or suffixes are not used. For example, these names are not Google Style: name_, mName, s_name and kName.

### 1.3.2 Rules by identifier type
#### 1.3.2.1 Package names
Package names are all lowercase, with consecutive words simply concatenated together (no underscores). For example, com.example.deepspace, not com.example.deepSpace or com.example.deep_space.

#### 1.3.2.2 Class names
Class names are written in UpperCamelCase.

Class names are typically nouns or noun phrases. For example, Character or ImmutableList. Interface names may also be nouns or noun phrases (for example, List), but may sometimes be adjectives or adjective phrases instead (for example, Readable).

There are no specific rules or even well-established conventions for naming annotation types.

Test classes are named starting with the name of the class they are testing, and ending with Test. For example, HashTest or HashIntegrationTest.

#### 1.3.2.3 Method names
Method names are written in lowerCamelCase.

Method names are typically verbs or verb phrases. For example, sendMessage or stop.

Underscores may appear in JUnit test method names to separate logical components of the name, with each component written in lowerCamelCase. One typical pattern is <methodUnderTest>_<state>, for example pop_emptyStack. There is no One Correct Way to name test methods.

#### 1.3.2.4 Constant names
Constant names use CONSTANT_CASE: all uppercase letters, with each word separated from the next by a single underscore. But what is a constant, exactly?

Constants are static final fields whose contents are deeply immutable and whose methods have no detectable side effects. This includes primitives, Strings, immutable types, and immutable collections of immutable types. If any of the instance's observable state can change, it is not a constant. Merely intending to never mutate the object is not enough. Examples:

```java
// Constants
static final int NUMBER = 5;
static final ImmutableList<String> NAMES = ImmutableList.of("Ed", "Ann");
static final ImmutableMap<String, Integer> AGES = ImmutableMap.of("Ed", 35, "Ann", 32);
static final Joiner COMMA_JOINER = Joiner.on(','); // because Joiner is immutable
static final SomeMutableType[] EMPTY_ARRAY = {};
enum SomeEnum { ENUM_CONSTANT }

// Not constants
static String nonFinal = "non-final";
final String nonStatic = "non-static";
static final Set<String> mutableCollection = new HashSet<String>();
static final ImmutableSet<SomeMutableType> mutableElements = ImmutableSet.of(mutable);
static final ImmutableMap<String, SomeMutableType> mutableValues =
    ImmutableMap.of("Ed", mutableInstance, "Ann", mutableInstance2);
static final Logger logger = Logger.getLogger(MyClass.getName());
static final String[] nonEmptyArray = {"these", "can", "change"};
```
These names are typically nouns or noun phrases.

#### 1.3.2.5 Non-constant field names
Non-constant field names (static or otherwise) are written in lowerCamelCase.

These names are typically nouns or noun phrases. For example, computedValues or index.

#### 1.3.2.6 Parameter names
Parameter names are written in lowerCamelCase.

One-character parameter names in public methods should be avoided.

#### 1.3.2.7 Local variable names
Local variable names are written in lowerCamelCase.

Even when final and immutable, local variables are not considered to be constants, and should not be styled as constants.

#### 1.3.2.8 Type variable names
Each type variable is named in one of two styles:

* A single capital letter, optionally followed by a single numeral (such as E, T, X, T2)
* A name in the form used for classes (see Section 5.2.2, Class names), followed by the capital letter T (examples: RequestT, FooBarT).

## 1.4 Whitespace
### 1.4.1 Vertical Whitespace
A single blank line always appears:

1. Between consecutive members or initializers of a class: fields, constructors, methods, nested classes, static initializers, and instance initializers.
* Exception: A blank line between two consecutive fields (having no other code between them) is optional. Such blank lines are used as needed to create logical groupings of fields.
* Exception: Blank lines between enum constants are covered in Section 4.8.1.
As required by other sections of this document (such as Section 3, Source file structure, and Section 3.3, Import statements).
2. A single blank line may also appear anywhere it improves readability, for example between statements to organize the code into logical subsections. A blank line before the first member or initializer, or after the last member or initializer of the class, is neither encouraged nor discouraged.

Multiple consecutive blank lines are permitted, but never required (or encouraged).

### 1.4.2 Horizontal whitespace
Beyond where required by the language or other style rules, and apart from literals, comments and Javadoc, a single ASCII space also appears in the following places __only__.

1. Separating any reserved word, such as if, for or catch, from an open parenthesis (() that follows it on that line
2. Separating any reserved word, such as else or catch, from a closing curly brace (}) that precedes it on that line
3. Before any open curly brace ({), with two exceptions:
* @SomeAnnotation({a, b}) (no space is used)
* String[][] x = {{"foo"}}; (no space is required between {{, by item 8 below)
4. On both sides of any binary or ternary operator. This also applies to the following "operator-like" symbols:
* the ampersand in a conjunctive type bound: <T extends Foo & Bar>
* the pipe for a catch block that handles multiple exceptions: catch (FooException | BarException e)
* the colon (:) in an enhanced for ("foreach") statement
* the arrow in a lambda expression: (String str) -> str.length()
but not
* the two colons (::) of a method reference, which is written like Object::toString
* the dot separator (.), which is written like object.toString()
5. After ,:; or the closing parenthesis ()) of a cast
6. On both sides of the double slash (//) that begins an end-of-line comment. Here, multiple spaces are allowed, but not required.
7. Between the type and variable of a declaration: List<String> list
8. Optional just inside both braces of an array initializer
* new int[] {5, 6} and new int[] { 5, 6 } are both valid
9. Between a type annotation and [] or ....
This rule is never interpreted as requiring or forbidding additional space at the start or end of a line; it addresses only interior space.

