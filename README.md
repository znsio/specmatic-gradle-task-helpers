# Specmatic Gradle Task Helpers

This repo contains common gradle tasks to be used by the specmatic team when creating a new project

## Usage

In the `build.gradle` file of your root project, add the following:

```groovy
// use the main branch (with a query param to bust cache every 600 seconds)
apply from: "https://raw.githubusercontent.com/znsio/specmatic-gradle-task-helpers/refs/heads/main/build.gradle?_=${(int) (new Date().toInstant().epochSecond / 600)}"
// OR use a specific SHA
apply from: "https://raw.githubusercontent.com/znsio/specmatic-gradle-task-helpers/<GIT_COMMITISH>/build.gradle"
```

This plugin will apply a few policies to the gradle project:

* Ensure that licenses being used are permissive in nature (BSD, Apache, MIT, etc.) 
