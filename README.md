# idea-gradle-bug

## Tested with:

```
IntelliJ IDEA 2016.1.2
Build #IC-145.972, built on May 14, 2016
JRE: 1.8.0_76-release-b162 x86_64
JVM: OpenJDK 64-Bit Server VM by JetBrains s.r.o
```

## Problems:

1. **IDEA always ignores `.iml` files during Gradle project import**  
  When importing a Gradle project that has existing IDEA project files (iml files),
  IDEA now ignores any existing `.iml` files (such as those generated by Gradle),
  and instead generates new `.iml` files under the `.idea/modules` directory.

  **How to Replicate Problem:**

  1. Checkout the test project
     ```
     $ git clone https://github.com/wcraigtrader/idea-gradle-bugs.git
     $ cd idea-gradle-bugs
     ```
  1. Create IDEA project files
     ```
     $ ./gradlew idea
     :ideaModule
     :ideaProject
     :ideaWorkspace
     :idea
     :bar:ideaModule
     :bar:idea
     :foo:ideaModule
     :foo:idea

     BUILD SUCCESSFUL
     ```
  1. Open with IDEA / Import Project from Gradle
     ![Import Project from Gradle](/screenshots/import-project-from-gradle.png)
     * Uncheck `Create separate module per source set`
     * Make sure `Project format` is `.ipr (file based)`
     * Click `OK`.
  1. Set modules to include in the project
     ![Gradle Project Data to Import](/screenshots/gradle-project-data-to-import.png)
     * Select all modules.
     * Click `OK`.

  At this point the `idea-gradle-bugs.iml`, `foo/foo.iml`, and `bar/bar.iml` files have been removed,
  and replacements have been created under `.idea/modules`.

1. **
