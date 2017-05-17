# Overview

The goal of this project is to be a "decorator" to the org.apache.avro project for custom builds.
Directly changing the avro pom not only causes conflicts when merged with upstream, but also causes the build to fail
due to the OSGI magic being used by Avro.  Below are the instructions to build a TLP distro.

# Setup

Set up your maven env for deploying to central following [these instructions](http://central.sonatype.org/pages/apache-maven.html).

# Building

Change the version of avro to be a custom distro.  This is required so we pick up our source build and don't accidentlaly
include the default Apache version.

```bash
   mvn versions:set -DnewVersion=<avro version>-tlp.<tlp build #>
```

You can try `mvn clean install`, however as of 1.8.2 the tests cases for IPC require external services running, and I can't find
the documentation on how to get those started.  The main avro package is the one we care about, so that can be installed with tests
for every other paackage, unless modifies, skip tests and install maven in `${AVRO_ROOT}/lang/java`

```bash
mvn clean install -DskipTests=true
```
 
Now change working directory to `${AVRO_ROOT}`.  Modify our release version and the avro dependency version.

Optional: Set this in your term to sign the GPG key if you're unable to sign the key

```bash
export GPG_TTY=$(tty)
```

Deploy the key to maven central


 
