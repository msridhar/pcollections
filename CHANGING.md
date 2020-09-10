To release:
- run `java -jar google-java-format-1.7-all-deps.jar -i src/**.java`
- remove -SNAPSHOT from the version in pom.xml and build.gradle
- commit with a tag

Then:

    mvn package
    mvn source:jar
    mvn javadoc:jar -DadditionalJOption=-Xdoclint:none
    cp pom.xml target/pcollections-<VERSION>.pom
    cd target
    bash -c 'for f in pcollections-<VERSION>*; do gpg -ab $f; done'
    jar cvf bundle.jar pcollections-<VERSION>*

Then follow the instructions at http://central.sonatype.org/pages/manual-staging-bundle-creation-and-deployment.html

Finally, increment the version in build.gradle and pom.xml and add back -SNAPSHOT, and commit.

Finally finally, once the new version is available in Maven Central (takes a few hours), update the version in the Maven and Gradle snippets in the README and update CHANGELOG.md.