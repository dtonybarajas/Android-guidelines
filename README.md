# Use Javadoc standard comments
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

# Limit line length

Each line of text in your code should be at most 100 characters long. While much discussion has surrounded this rule, the decision remains that 100 characters is the maximum with the following exceptions:

* If a comment line contains an example command or a literal URL longer than 100 characters, that line may be longer than 100 characters for ease of cut and paste.
* Import lines can go over the limit because humans rarely see them (this also simplifies tool writing).


# Use TODO comments

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

