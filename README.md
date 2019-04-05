# spotless-kotlin
A template modular Kotlin (Java) project configured with Gradle and Spotless plugin for Klean Kotlin Kode.

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


# Steps used to create this project
1. Created a new Gradle project in Intellij checking the Kotlin (Java) checkbox 
in the "Additional Libraries and Frameworks" section
2. Set up git - in the project directory
    1. `git init`
    2. `git remote add origin https://github.com/iikirilov/spotless-kotlin.git`
3. Modify `build.gradle`
    1. Removed the `version` label
    2. Adding [spotless gradle plugin](https://github.com/diffplug/spotless/tree/master/plugin-gradle)
    3. Configured [Spotless Defaults](Spotless-Defaults)
    4. Added [kotlin-logging](https://github.com/MicroUtils/kotlin-loggingw)
    and [logback](https://github.com/qos-ch/logback) for logging
4. Added Apache License v2 in `gradle/spotless.kotlin.license`<br />**Remember to change `<insert-company-name-here>` to your company name.**
5. Set up modules in `settings.gradle`
6. Add `.gitignore` from kethereum
