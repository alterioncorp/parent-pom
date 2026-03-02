# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

`parent-pom` is the shared Maven parent POM for `io.github.alterioncorp` projects. It centralizes plugin versions, build configuration, GPG signing, and Maven Central publishing.

## Build Commands

```bash
mvn clean verify    # Validate the POM
```

## Versioning

- `develop` and feature branches always use a `SNAPSHOT` version (e.g. `1.0-SNAPSHOT`)
- Release process:
  1. Merge `develop` into `main`
  2. Change version on `main` to release version (e.g. `1.0.0`)
  3. Tag `main` with the release version
  4. Push `main`

## Architecture

This is a `pom`-packaging project with no source code. Key things it provides to child projects:

- **Plugin versions** — managed in `<pluginManagement>` for compiler, surefire, source, javadoc, gpg, jacoco, and `central-publishing-maven-plugin`
- **GPG signing** — `sign` profile activates `maven-gpg-plugin`; use `-Psign` to enable
- **Maven Central publishing** — `central-publishing-maven-plugin` active in all child builds; uses `publishingServerId=central` and `waitUntil=published`
- **Developer info** — `<developers>` inherited by all children
- **License** — Apache 2.0, inherited by all children

## Java & Maven

- Java 21 (compiler compliance via `version.java.major` property)
- Artifacts published to Maven Central (`io.github.alterioncorp:parent-pom`)
- Child projects reference this as `<parent>` and inherit all plugin management and profiles
