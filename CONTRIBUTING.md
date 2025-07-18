# Contributing

When contributing to this repository, please first discuss the change you wish
to make via issue, email, or any other method with the owners of this repository
before making a change.

Please note we have a code of conduct, please follow it in all your interactions
with the project.

# Use A Single Commit For Each Feature Or Bug Fix

To make searching history easier, we ask that you bundle your changes into a
single commit, and that commit should address a single feature or issue.

# Commit Message Rules

The goal of the following rules is to make the output for the follow command
line easier to read:

```git log --pretty=oneline```

as well as making it easier to generate releases, perform interactive
rebasing, and any number of other project related tasks.

Please adhere to the following rules for each commit. This will help make
generating the RELEASE.md file easier, and will help to make your
contributions easier to understand.

 * Separate subject from body with a blank line
 * Limit the subject line to 50 characters
 * Do not end the subject line with a period
 * Use the imperative, present mood in the subject line and body
 * Wrap the body at 72 characters
 * Use the body to explain what and why vs. how


 
## Do
 * Use one of the allowed verbs to start the prolog. See the table below for the set of verbs and their usage.
 * Always leave the second line blank.
 * Line break the commit message (to make the commit message readable without having to scroll horizontally in gitk).

## Do Not
 * Don't end the summary line with a period - it's a title and titles don't end with a period.

## Tips
 * If it seems difficult to summarize what your commit does, it may be because it includes more than one feature or bug
   fix. If that is the case, please consider breaking them up into multiple commits and open a separate issue for each.

## Commit Message Verbs

| Verb     | Usage                                                               |
|----------|---------------------------------------------------------------------|
| feat     | A new feature                                                       |
| refactor | A code change that neither fixes a bug nor adds a feature           |
| fix      | A bug fix                                                           |
| test     | Adding missing tests or correcting existing tests                   |
| build    | Changes that affect the build system or external dependencies       |
| ci       | Changes to our CI configuration and automation around pull requests |
| docs     | Documentation only changes                                          |

# Commit Template

When working on code, please use the following template for your commits:

    <type>[optional scope]: <description> [#issue]
    
    [optional body]
    
    [optional footer(s)]


 * type - the verb (see above)
 * optional scope - the main module in the code affected by the change
 * description - a single sentence describing the change
 * issue - the issue number
 * optional body - a fuller description of the change using the imperative, present tense
 * optional footer - any breaking changes

### Example Commit Messages

#### Adding a new feature

    feat: add the new reader protocol [#2375]
    
    Add support for interacting with the Variant reader.

#### Fixing a bug

If the commit doesn't contain a breaking change, then that part can be left off.

    fix(reader): change how the id is generated [#2376]
    
    Replace the existing id generating with one that guarantees unique
    values for all items in the library.
    
    BREAKING CHANGE:
    Existing ids on clients are no longer valid

#### Refactoring

    refactor(reader): replace the reader feed gererator for directories [#2377]
    
    Replace the old class with the newer Java standard for record types.


# Coding Conventions And Formatting

## Java

The Java code for the project is formatted using the
[Google Java Formatter](https://github.com/google/google-java-format)
tool. Code is automatically formatted for you when you commit locally.

To manually format the code, use the following command line:

```
$ mvn git-code-format:format-code
```

## Typescript

The frontend code uses [Prettier](https://prettier.io/) for code formatting,
and the build process will fail code that does not meet this standard.

Most editors and IDEs support formatting Typescript code. Please check the
documentation for the one you use for how to apply the convention when coding.

### Code Formatting

To ensure your code confirms to coding conventions, run the following command
in the **comixed-webui** module:

```
$ yarn format
```

This will reformat all Typescript-related code.

### Lint Checks

To ensure your Angular code meets project requirements, please run the lint
checks in the **comixed-webui** module:

```
$ cd comixed-webui
$ yarn lint
```

There should be no errors reported.

## Prerequisites

The application depends on the following pieces:
 * [Java Development Kit](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html): Minimum of JDK 12.
 * [NodeJS](https://nodejs.org/en/download/): Minimum of v10.15.3.
 * [Maven](https://maven.apache.org/download.cgi): Maven v3.

## Setting Up Your Build Environment

Once you've installed the requirements, you need to setup your environment:

1. Install [yarn](https://yarnpkg.com/) following [their instructions](https://yarnpkg.com/getting-started/install).

## Running The Build

To build the application, execute the following from the project's root directory:

```mvn clean package -Pci```

If the build is successful, then you will have a file in the
**comixed-app/target** directory named something like **comixed-app-\*.jar**.
This is the final application artifact and what you will now be able to run.

If, however, you saw any errors, you'll need to go back and verify that
you've properly setup your environment.


## Including External Metadata Adaptors

ComiXed supports loading external metadata adaptors at startup. These 
adaptors are distributed as JAR files and can be placed into the ```lib```
directory before starting the application.

To do this in development, where we don't have such a directory, the best
practice is to do the following:

1. Create a directory next to your comixed git repostory named ```extlib```.
1. In IntelliJ:
   * right click on **comixed-app**
   * select **Open Module Settings**
   * select **comixed-app**
   * select **Dependencies**
   * click the + sign
   * select **1. JARs or Directories...**
   * navigate to the external JAR file.

When you start your server, it will load any JAR file in the specified directory.

# Running The Application

To start the application from the project root, launch it from the command
line with:

```$ java -jar comixed-app/target/comixed-app-*.jar```

**NOTE:** As this is still an actively developed project, there's always a
chance that your local database has become corrupted. If you experience problems
with starting the application, a good first step would be to delete your local
database and try running the application again.

The database can be found:

Operating System|Location
---|---
**Windows** | C:\users\[your username]\.comixed
**Linux** | /home/[your username]/.comixed
**MacOS** | /users/[your username].comixed

## Interacting With The Application

To connect to the web application, point a browser to *http://localhost:7171/*.

You can then log into the application with one of two default accounts:

1. **Administrator** username=comixedadmin@localhost password=comixedadmin
1. **Reader** username=comixedreader@localhost password=comixedreader

## Developing The Front End

If you are working on changes to the frontend, you can launch an instance
of the Angular server separately from the backend.
 
You can launch the backend by moving to the **comixed-app** module and
launching it using the commandline:

```
mvn spring-boot:run -DskipTests
```
Then, in the **comixed-webui** subdirectory, launch it using the commandline:

```
$ yarn start
```

You can now connect to the web application from your browser using
*http://localhost:4200/*. And, as your make changes to the Angular code, this
frontend will update automatically.

# Unit Tests

To help keep the code as thoroughly tested and understandable as possible, all
features and bug fixes must come with some set of unit tests to demonstrate
and validate them. Contributions should never reduce the unit test coverage for
the project.

Please also be sure that the contribution does not break any existing unit
tests. So be sure to run the full suite of unit tests for the entire project
before submitting your pull request.

# Translations

Translating the application in a new language, or updating an existing
translation, is a relatively easy method of contributing to the project.
However, there are some elements to understand.

## File Locations

The language files are found in the directory:

```comixed-webgui/src/assets/i18n/```

A different subdirectory exists for each language supported, using the [ISO
2 letter abbreviation](https://www.sitepoint.com/iso-2-letter-language-codes/)
for each; i.e., American English is in a directory named **en**, French is
in the directory **fr**, etc.

## Adding A New Language

To add a new language, create a subdirectory using the appropriate 2-letter
code. Then, copy the files from the **en** directory (which is the reference
translation) into this new directory.

## Translating Entries

Language files use [JSON](https://www.json.org/) to story name/value pairs.
The majority of entries are simple sentences and can be directly translated.

However there are other kinds of entries and their translations are
slightly different.

### Entries With Variable Text

Some entries will contain a word that is enclosed in curly braces ({}). In
those entries, that word and the braces are replaced with some other value
the application wants to display.

For example:
```json
"tab-title": "Reading List: {name}",
```

If "{name}" is equal to "Age Of Apocalypse", then this entry translates to:

    Reading List: Age Of Apocalypse

### Entries With Plurality

Some entries show a slightly different text based on a numeric value from the
application. They always contain the keyword **plural** in the text between
the curly braces. They are used to display a different text if, in the target
language, nouns are modified based on plurality. For example, in English, if
the noun is anything other singular (1), then it has an "s" appended to it.

For example:

```json
"characters": "Character: {name} ({count, plural, =1{One Comic} other{# Comics}})",
```

If "character" is "Batman" and "count" is equal to 1, then this entry
translates to:

    Character: Batman (One Comic)

However, if "count" is equal to any other number, such as 75, then this entry
translates to:

    Character: Batman (75 Comics)

If the target language does not modify nouns based on plurality, entries like
this can be simplified to something like:

```json
"characters": "Character: {name} ({count, plural, other{# Comics}})",
```


### Entries With Selections

Some entries show one of a set of available values based on some value from
the application. They always contain the keyword **select** in the text
between the curly braces, followed by a set of application values and the
language translation within an inner set of curly braces, like this:

For example:

```json
"archive-type": "{type, select, CBZ{Zip File (CBZ)} CBR{RAR File (CBR)} CB7{7Zip File (CB7)} other{Unknown}}",
```

Here the translation looks at the value of "type" and shows the text or it
when it equals either "CBZ", "CBR", or "CB7". The text in those curly braces
needs to be translated in the target language as well, unless otherwise noted.

So, for example, if "type" is equal to "CBZ", then this entry translates to:

    Zip File (CBZ)

However, if it is equal to "CB7", then this entry translates to:

    7Zip File (CB7)

# Pull Requests

Ensure your branch builds without errors or warnings locally. Any PR that does
not pass the automated build process will be automatically declined.
