# Kotlin with VSCode

## Standalone compiler

1. Download the standalone Kotlin [compiler](https://github.com/JetBrains/kotlin/releases/tag/v1.4.20)

2. Add its bin/ directory to your path

3. Verify it's in your path by running `kotlinc` from VSCode's terminal

4. Make sure you have a JDK available

5. Install the [Java Extension Pack](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack) in VSCode - this adds the Java Debugger

6. Install the [Kotlin Language Extension](https://marketplace.visualstudio.com/items?itemName=mathiasfrohlich.kotlin) in VSCode for syntax highlighting, etc

7. Create `.vscode/tasks.json` and define a build task:

```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Build Kotlin",
      "type": "shell",
      "command": "kotlinc main.kt -include-runtime -d out/main.jar"
    }
  ]
}
```

Replace `main.kt` with wherever your Kotlin file is.

8. Create `.vscode/tasks.json` and define the debug config:

```json
{
  "configurations": [
    {
      "type": "java",
      "name": "Debug (Launch)",
      "request": "launch",
      "classPaths": [
        "./out/main.jar"
      ],
      "mainClass": "MainKt",
      "preLaunchTask": "Build Kotlin"
    }
  ]
}
```

9. Try running the debug launch profile, it should attempt to build the JAR
before launching the debugger.

## Alternative With Maven/Gradle

I don't know much about using Maven or Gradle, but if you have a project set up
with it one of them, this other [Kotlin Extension](https://marketplace.visualstudio.com/items?itemName=fwcd.kotlin)
is supposed to provide a full debugging experience.  I tried to get it to work
with the standalone compiler, but had little success.