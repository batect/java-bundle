# java-bundle

[![Build Status](https://img.shields.io/github/workflow/status/batect/java-bundle/Pipeline/master)](https://github.com/batect/java-bundle/actions?query=workflow%3APipeline+branch%3Amaster)
[![License](https://img.shields.io/github/license/batect/java-bundle.svg)](https://opensource.org/licenses/Apache-2.0)

A bundle for [batect](https://batect.dev) that provides a development container for JVM-based languages that use Gradle, with sensible default configuration.

## Usage

### Setup

Add the following to your `batect.yml`:

```yaml
include:
  - type: git
    repo: https://github.com/batect/java-bundle.git
    ref: XXX # Replace with latest version from https://github.com/batect/java-bundle/releases
```

### Containers

#### `java-build-env`

A container (based on the [AdoptOpenJDK images](https://hub.docker.com/_/openjdk)) with sensible defaults for use with Gradle.

It mounts the project directory into the container, enables run as current user mode and configures a cache for dependencies downloaded by Gradle.

The Gradle daemon is disabled, as starting the daemon is counterproductive in an ephemeral container.

Note that the container does not contain Gradle itself - use the [Gradle wrapper](https://docs.gradle.org/current/userguide/gradle_wrapper.html).

### Example

```
tasks:
  build:
    description: Build the project.
    group: Build tasks
    run:
      container: java-build-env
      command: ./gradlew build

include:
  - type: git
    repo: https://github.com/batect/java-bundle.git
    ref: XXX # Replace with latest version from https://github.com/batect/java-bundle/releases
```

The [Java sample project](https://github.com/batect/batect-sample-java) also demonstrates how to use this bundle.

## Development

Run `./batect --list-tasks` to see a list of available tasks for this project.
