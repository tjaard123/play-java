# Java

This is a small reference repo for experienced coders but Java noobs, still WIP.

- [Java Minimum Survival Guide](https://hadihariri.com/2013/12/29/jvm-minimal-survival-guide-for-the-dotnet-developer/)
- [Great for Kotlin Learning](https://play.kotlinlang.org/koans)

## Gradle & Java -> New

If you're like me you're use to something like `npm init` or `dotnet new`.  If you read the survival guide above you'll know there's different tools & languages to get this done.  I've come to prefer Gradle:

Create a single file: `build.gradle`, here's a kotlin example:

```groovy
plugins {
    id 'org.jetbrains.kotlin.jvm' version '1.2.51'
}

repositories {
    mavenCentral()
}

dependencies {
    compile "org.jetbrains.kotlin:kotlin-stdlib-jdk8"
}

compileKotlin {
    kotlinOptions.jvmTarget = "1.8"
}
compileTestKotlin {
    kotlinOptions.jvmTarget = "1.8"
}
```

Depending on your `build.gradle` file you'll have several tasks at your disposal.  For stock standard java you'll run `gradle build` which creates a JAR file.

Directory structure:

```
src
  - main
    - java
      - HelloWorld.java
    - kotlin
      - HelloWorld.kt
build.gradle
settings.gradle
```

## Switching between 10 & 8 on linux

```sh
$ java -version

openjdk version "1.8.0_181"

# openjdk - Open JDK implementation of JVM, not Oracle
# 1.8 - Java 8

# List java versions
$ update-java-alternatives --list

java-1.11.0-openjdk-amd64
java-1.8.0-openjdk-amd64

# Switch versions
$ sudo update-alternatives --config java
```

## Start scripts

I'm playing with start scripts:

build.gradle

```groovy
mainClassName = "dummy"

task BlueprintServiceStartScript(type:CreateStartScripts) {
    applicationName = 'BlueprintService'
    mainClassName = 'BlueprintService'
    classpath = startScripts.classpath
    outputDir = startScripts.outputDir
}
applicationDistribution.from(BlueprintServiceStartScript) { into 'bin' }
```

src/main/java/BlueprintService.java

```java
public class BlueprintService {
    public static void main(String[] args) throws Exception {
        System.out.println("Blueprint service ready...");
    }
}
```

```sh
$ gradle installDist
$ build/install/blueprint/bin/BlueprintService
```

