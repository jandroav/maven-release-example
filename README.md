# Building Java Projects with Maven

## Prepare a Release

`release:prepare` goal ensures the project is ready to be released and then prepares SCM to eventually contain a tagged version of the release. This is expected to be followed by a call to `release:perform`* .

Preparing a release goes through the following release phases by default:

* Check that there are no uncommitted changes in the sources
* Check that there are no SNAPSHOT dependencies
* Change the version in the POMs from x-SNAPSHOT to a new release version (you will be prompted (unless you use `-B` - batch mode -) for the versions to use, with a default value proposed by version policy configured as projectVersionPolicyId)
* Transform the SCM information in the POM to include the final destination of the tag
* Run the project tests (preparation goals) against the modified POMs to confirm everything is in working order
* Commit the modified POMs
* Tag the code in the SCM with a version name (this will be prompted for unless you use `-B`)
* Bump the version in the POMs to a new value y-SNAPSHOT (these values will also be prompted for, with a default value proposed by version policy configured as projectVersionPolicyId)
* Eventually run completion goal(s) against the project (since 2.2)
* Commit the modified POMs
  
To prepare a release execute this command:

```bash
mvn -B release:prepare
```

## Perform a Release

`release:perform` goal performs a release from SCM, either from a specified tag, or usually the tag representing the previous release in the working copy created by `release:prepare`.

Performing a release runs the following release phases by default:

* Checkout from an SCM URL with optional tag to workingDirectory (target/checkout by default)
* Run the perform Maven goals to release the project (by default, deploy site-deploy), eventually with release profile(s) active

To perform a release, execute this command:

```bash
mvn -B release:perform
```

## All in one commnad

```bash
mvn -B release:clean release:prepare release:perform -Darguments="-Dmaven.javadoc.skip=true -Dmaven.test.skipTests=true -Dmaven.test.skip=true" -Dusername=<GIT_USER> -Dpassword=<GIT_PASSWORD>
```
