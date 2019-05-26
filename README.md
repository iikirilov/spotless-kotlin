# spotless-kotlin

A template Kotlin (Java) project configured with Gradle and Spotless plugin for Klean Kotlin Kode.

The template comes with a ktlint, logging, gitignore, gradle and junit preconfigured. See [here](README.md#Steps-used-to-create-this-template) for more information.

The template was designed and tested in Intellij Idea, but should be useable in other IDEs.

# How to use

1. In the parent directory you want your in project run:
    1. `git clone https://github.com/iikirilov/spotless-kotlin <you_project_name>`
    2. `cd <you_project_name>`
    3. `./init.sh`
2. Open your newly created project in you IDE of choice.
3. Create your [modules](README.md#Modules). [Optional]
4. Set-up [logging](README.md#Modules).
5. Write some kotlin.
6. Run `./gradlew spotlessApply` to klean up you kode.
7. Commit, push and repeat from 5.
    
# Modules

Modular code is awesome!! It makes it easier to build, maintain and re-use code. The root directory is already a module. You do not need to create modules if you feel your project does not need them, instead you can put your `src` folder directly in the project root.

### Module structure:

```bash
└── <module_name>
    └── src
        ├── main
        │   ├── kotlin
        │   └── resources
        └── test
            ├── kotlin
            └── resources
```

### Adding a module:

Add a new line to `settings.gradle` in the format `include '<module_name>'`. Then create the folder structure in the project root as decribed in [module structure](README.md#Module-structure).

#### Adding a nested module:

```
include '<parent_module>:<child_module>'
include `<parent_module>:<child_module_1>`
```

Then create the `parnet_module` folder in the project root and then the folder structure described in [module structure](README.md#Module-structure) in the `parnet_module` folder.

The following is an example `settings.gradle` file. The file includes the root project name.

```
rootProject.name = 'spotless-kotlin'

include 'module1'
include 'module2:module2a'
include 'module2:module2b'
```

# Logging

Logging is set up using [kotlin-logging](https://github.com/MicroUtils/kotlin-logging) and [logback](https://github.com/qos-ch/logback).

Declare a logger wherever you need it like this: `val logger = KotlinLogging.logger {}`

Logback configuration should be located in `src/main/resources/logback.xml`. 
Logback configuration for tests should be located in `src/test/resources/logback-test.xml`. 
The following is a minimal configuration of a logback config file.

```
<?xml version="1.0" encoding="UTF-8"?>
<configuration>

    <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
        </encoder>
    </appender>

    <root level="INFO">
        <appender-ref ref="STDOUT" />
    </root>
</configuration>
```

# Steps used to create this template
1. Created a new Gradle project in Intellij checking the Kotlin (Java) checkbox 
in the "Additional Libraries and Frameworks" section
2. Set up git - in the project directory
    1. `git init`
    2. `git remote add origin https://github.com/iikirilov/spotless-kotlin.git`
3. Modify `build.gradle`
    1. Removed the `version` label
    2. Adding [spotless gradle plugin](https://github.com/diffplug/spotless/tree/master/plugin-gradle)
    3. Configured [Spotless Defaults](README.md#Spotless-Defaults)
    4. Added [kotlin-logging](https://github.com/MicroUtils/kotlin-logging)
    and [logback](https://github.com/qos-ch/logback) for logging
4. Added Apache License v2 in `gradle/spotless.kotlin.license`<br />**Remember to change `<insert-company-name-here>` to your company name.**
5. Set up modules in `settings.gradle`
6. Generate `.gitignore` for Kotlin, JetBrains and Gradle using Intellij plugin

# Spotless Defaults

### Kotlin
Uses [ktlint](https://github.com/diffplug/spotless/tree/master/plugin-gradle) behind the scenes. By default:
1. Max Line Length = 100
2. Inserts new line at the end of every `.kt` file
3. Puts an Apache License v2 at the top of every `.kt` file. You can change the license by modifying `gradle/spotless.kotlin.license`

### Gradle
Uses [groovy eclipse](https://github.com/diffplug/spotless/tree/master/plugin-gradle#groovy-eclipse) with the config file specified in `gradle/formatter.properties`. By default:
1. Uses 4 `space` as the indentation
2. Indentations are not inserted in empty lines
2. Inserts new line at the end of every `.gradle` file
