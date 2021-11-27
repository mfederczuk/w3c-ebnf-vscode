<!--
  Copyright (c) 2021 Michael Federczuk
  SPDX-License-Identifier: CC-BY-SA-4.0
-->

# Development Guidelines #

These guidelines need to be followed when contributing code or other file changes.

These guides and rules **do not** apply to binary files, except when explicitly stated.  
Exceptions may apply to some of these rules, see the [`.editorconfig`](.editorconfig) file for more information.

## General ##

* **Encoding & Character Set**  
  All files must be encoded using **UTF-8** and use **Unicode** as the character set.  
  The only **ASCII** control characters that are allowed in files are the horizontal tab and the line break character.  
  In source code, identifiers should never contain non-**ASCII** characters and string literals should only consist of
  printable **ASCII** characters if possible. (make use of escape sequences)

* **Use Unix-like line endings** (`LF`)

* **Max line length is 120 characters**

* **No trailing whitespace**

* **Files must have exactly one trailing newline character**

* **File Naming**  
  Broad rules for how to name files & directories of different classifications/categories.

  * community files: `CONST_CASE`
  * handwritten documentation: `PascalCase`
  * executable scripts/binaries: `kebab-case` (and no extension)
  * source code (depending on the language): `snake_case`, `PascalCase` or `camelCase`
  * resources / assets / (non-executable) binaries: `snake_case`

  Filenames should also only consist of **ASCII** characters and non-binary files that do not start with a dot should
  always have an extension.

## Coding ##

* **On the subject of tabs & spaces**

  [_"Nobody talks about the real reason to use Tabs over Spaces"_ - reddit.com/r/javascript](https://redd.it/c8drjo)

  Since this topic is largely based on the programming/development language that is being used, there are some
  exceptions to the these specific rules.

  * **Indent with tabs & align with spaces**

    ```c
    // wrong
    enum·color·{
    →	RED→	=·0xFF0000,
    →	GREEN→	=·0x00FF00,
    →	BLUE→	=·0x0000FF
    };
    ```

    ```c
    // wrong
    enum·color·{
    ····RED···=·0xFF0000,
    ····GREEN·=·0x00FF00,
    ····BLUE··=·0x0000FF
    };
    ```

    ```c
    // right
    enum·color·{
    →	RED···=·0xFF0000,
    →	GREEN·=·0x00FF00,
    →	BLUE··=·0x0000FF
    };
    ```

  * **Tab Width**

    When calculating the length of a line, a tab counts for 4 characters.

    Locally, the tab width may be changed to any value needed, if it helps with visual clarity.  
    The [`.editorconfig`](.editorconfig) file contains the `indent_size` attribute, set to `4`.  
    If it is necessary for you to change this value to a different one, you are free to do so, just please don't commit
    and push this change.

  * **Tabs must only appear at the beginning of lines**

* **Prefer guard clauses & avoid `else`**

  ```c
  // wrong
  void func(int x) {
  	if(x == 0) {
  		foo();
  	} else {
  		bar();
  	}
  }
  ```

  ```c
  // right
  void func(int x) {
  	if(x == 0) {
  		foo();
  		return;
  	}

  	bar();
  }
  ```

* **Don't rely on "truthy"/"falsy" values**

  ```js
  // wrong
  const str = "";
  if(str) { // hard to understand; what does this actually mean?
  }
  ```

  ```js
  // right
  const str = "";
  if(typeof(str) === "string" && str.length > 0) { // easy to understand; no ambiguity what this check is supposed to do
  }
  ```

## Git ##

* **Don't track generated files**  
  Generated files like binaries or reference documentation should not be checked into version control - there are some
  rare exceptions to this rule.

* **Branching System**  
  The branching system used in this repository is based off of **[t3m v1.0.0-rc01]**, which is just partially followed
  and it won't be fully enforced.

* **One commit should contain one logical change**  
  One commit should only be a single logical change, like fixing a bug or changing formatting.  
  This means that changes may also span several files.  
  Changes to documentation, based on the changed code (e.g.: API references, changelog files, …), can also be
  incorporated into the commit.

* **Prefer more smaller commits over fewer bigger commits**  
  This point goes hand-in-hand with the previous one; when it is possible and logically acceptable, split a big commit
  that contains an entire feature into multiple smaller commits.

* **Don't Squash**  
  It doesn't matter if a branch has 100 or more commits, as long as each one of those commits is one logical change,
  ***do not squash them down to a single commit***.

* **Never commit broken code**  
  Never commit code with wrong syntax, compilation errors, static semantic errors or missing assets/resources.  
  Every commit should be a functional build.

* **Commit Message guidelines**
  * The subject line should be capitalized (like in a sentence)
  * Use the imperative mood & present tense in the subject line
  * The subject line should consist of maximum 50 characters
  * The subject line should not end with a period
  * The subject line should be a short summary of the changes
  * Separate the subject line from the message body with an empty line
  * Wrap the message body after 72 characters
  * The message body should primarily be used to explain *what* changed and *why* this change was necessary instead of
    *how* the change was implemented
  * The entire message should not be just a reference to an issue that got fixed

* **Merge Commit Messages**

  When merging into the master/main branch...

  * the message of non-release commits should be: _"Merge in [feature/change/fix]"_
  * the message of release commits should be: _"Release v[version name]"_

[t3m v1.0.0-rc01]: https://github.com/mfederczuk/t3m/tree/v1.0.0-rc01
