- History

- Show all project folders. Not going to go over all of them, but you can see the basics of each framework,
as well as some more complicated examples.

- Projects
    - old-school
    - java-util-logging - no dependency required!
    - log4j - show config
    - logback - show config
    - What if I pull in a library that is using another framework? What do I have to do?
        - log4j2-and-library-with-log4j
    - Well, what if I only want to configure one implementation?
        - You could use JCL, but don't. Instead, use SLF4J.
        - Go over the `Using SLF4J` section in the README, including bridges and bindings.
        - slf4j-noop
        - slf4j-simple
        - slf4j-logback-and-library-with-log4j
            - I only have to configure one library (unlike the log4j2-and-library-with-log4j project). Yay!
    - That seems so simple! Just you wait...
        - Binding problems
            - Go over first gotcha
            - Show slf4j-simple-and-log4j-bindings
            - Check this here:
            `The way SLF4J picks a binding is determined by the JVM and for all practical purposes should be considered random. As of version 1.6.6, SLF4J will name the framework/implementation class it is actually bound to.`
            https://www.slf4j.org/codes.html#multiple_bindings
            - I think 'nondeterministic' would be a better description
        - Bridging problems
            - Go over second gotcha
            - Don't need to run it, but show build.gradle from slf4j-logback-and-library-with-jcl
            - Explain again what the bridge library does (translates to slf4j api) and that not excluding
              the commons logging library could cause those logs to be lost
            - This is hard to debug
        - Infinite loop
            - Don't go over the gotcha yet...
            - Show the build.gradle for the project
            - Now that we've explained bridges and bindings, can anybody tell me what will happen and how?
        - Libraries can cause you pain
            - This is really a more specific example of the first gotcha
            - TODO!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
    - Spring Boot
        - We use spring boot frequently, so let's talk about how it handles logging
        - spring-boot-with-default-config
            - Show build.gradle. I have only included org.springframework.boot:spring-boot-starter
            - Run this: `./gradlew spring-boot-with-default-config:dependencies --configuration compile`
            - Show that this version (2.x) transitively includes:
                - Logback
                - slf4j api
                - log4j2 bridging library
                - java util bridging library
            - The 1.x version will bridge JUL, JCL, and Log4j1
            - Explain that if I pull in a library with commons logging, I would need to exclude the real implementation
              and then include the JCL bridge (if I'm using `spring-boot-starter` 2.x)
        - spring-boot-with-log4j2
            - TODO!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
    