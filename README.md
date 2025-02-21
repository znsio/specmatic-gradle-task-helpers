# Specmatic Gradle Task Helpers

This repo contains common gradle tasks to be used by the specmatic team when creating a new project

## Usage

In the `build.gradle` file of your root project, add the following:

```groovy
buildscript {
    // use the main branch (with a query param to bust cache every 600 seconds)
    apply from: "https://raw.githubusercontent.com/znsio/specmatic-gradle-task-helpers/refs/heads/main/build.gradle?_=${(int) (new Date().toInstant().epochSecond / 600)}"
    // OR use a specific SHA
    apply from: "https://raw.githubusercontent.com/znsio/specmatic-gradle-task-helpers/<GIT_COMMITISH>/build.gradle"
}
```

This plugin will apply a few policies to the gradle project:

* Ensure that licenses being used are permissive in nature (BSD, Apache, MIT, etc.)

## What does this provide/how do I use this?

* Sets JDK version in the build
* Invoking `jar`/`assemble`/`build` task(s) will cause `licenseCheck` task to be invoked, which will generate a license
  report, along with a violation report.
* Adds the [test-logger-plugin](https://github.com/radarsh/gradle-test-logger-plugin) which pretty prints tests as they run
* Adds the [gradle-release plugin](https://github.com/researchgate/gradle-release) to automate versioning and tagging. To use this in your build:
    * Add the following snippet to your `build.gradle[.kts]` file
  
  ```groovy
    // Run tests before running the release build, add any other tasks here  
    tasks.getByName("beforeReleaseBuild").dependsOn("check")
    // after the release build, hook any "publish" tasks here.
    tasks.getByName("afterReleaseBuild").dependsOn("core:publish")
  ```
  
  * To release a new version, run the following command:
  ```bash
  ./gradlew release \
      -Prelease.useAutomaticVersion=true \
      -Prelease.releaseVersion=1.0.0 \ # Specifies the version to be released. This is optional. If not provided, the plugin will use the version defined in `gradle.properties` (excluding the `-SNAPSHOT` suffix).
      -Prelease.newVersion=1.1.0-SNAPSHOT # Specifies the version for the next development cycle. Be sure to include the `-SNAPSHOT` suffix.
  ```
