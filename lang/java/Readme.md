# Overview

The goal of this project is to be a "decorator" to the org.apache.avro project for custom builds.
Directly changing the avro pom not only causes conflicts when merged with upstream, but also causes the build to fail
due to the OSGI magic being used by Avro.  Below are the instructions to build a TLP distro.

# Setup

Set up your maven env for deploying to central following [these instructions](http://central.sonatype.org/pages/apache-maven.html).

# Building

We've modified the pom to support building only the java portions we need.  Below is the command to perform a release to maven central via Sonatype Nexus

```bash
   mvn install deploy -DskipTests=true -P new-jdk,interop-data-test,sign
```

You can try `mvn clean install`, however as of 1.8.2 the tests cases for IPC require external services running, and I can't find
the documentation on how to get those started.  


Optional: Set this in your term to sign the GPG key if you're unable to sign the key with the maven plugin

```bash
export GPG_TTY=$(tty)
```
