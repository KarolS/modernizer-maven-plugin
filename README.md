Modernizer Maven Plugin
=======================
Modernizer Maven Plugin detects use of legacy APIs which modern Java versions
supersede.
These modern APIs are often more performant, safer, and idiomatic than the
legacy equivalents.
For example, Modernizer can detect uses of `Vector` instead of `ArrayList`,
`String.getBytes(String)` instead of `String.getBytes(Charset)`, and
Guava `Objects.equal` instead of Java 8 `Objects.equals`.
The default configuration detects
[over 50 legacy APIs](https://github.com/andrewgaul/modernizer-maven-plugin/blob/master/src/main/resources/modernizer.xml),
including third-party libraries like
[Guava](https://code.google.com/p/guava-libraries/).

Configuration
-------------
To enable Modernizer during the compilation phase of your project, add the
following to the `<plugins>` stanza in your pom.xml:

```xml
<plugin>
  <groupId>org.gaul</groupId>
  <artifactId>modernizer-maven-plugin</artifactId>
  <version>1.0.0</version>
  <configuration>
    <javaVersion>1.8</javaVersion>
  </configuration>
  <executions>
    <execution>
      <id>modernizer</id>
      <phase>compile</phase>
      <goals>
        <goal>modernizer</goal>
      </goals>
    </execution>
  </executions>
</plugin>
```

The `<configuration>` stanza can contain several elements:

* `<javaVersion>` enables violations based on target Java version, e.g., 1.8.  For example, Modernizer will detect uses of `Vector` as violations when targeting Java 1.2 but not when targeting Java 1.1.  Required parameter.
* `<failOnViolations>` fail phase if Modernizer detects any violations.  Defaults to true.
* `<violationsFile>` user-specified violation file.  Also disables standard violation checks.
* `<exclusionsFile>` disables user-specified violations.  This is a text file with one exclusion per line in the javap format: `java/lang/String.getBytes:(Ljava/lang/String;)[B`.

References
----------
[ASM](http://asm.ow2.org/) provides Java bytecode introspection which enables
Modernizer's checks.
`javac -Xlint:deprecated` can detect uses of interfaces with @Deprecated
annotations.
[Overstock.com library-detectors](https://github.com/overstock/library-detectors)
can detect uses of interfaces with @Beta annotations.
[Checkstyle](http://checkstyle.sourceforge.net/) IllegalInstantiation and
Regexp checks can mimic some of Modernizer's functionality.

License
-------
Copyright (C) 2014 Andrew Gaul

Licensed under the Apache License, Version 2.0
