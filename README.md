This project demonstrates problems with selection of JUnit 4 / 5 parameterized tests.

According to https://maven.apache.org/surefire/maven-surefire-plugin/examples/single-test.html and https://docs.gradle.org/current/userguide/java_testing.html, the selection of parameterized runs should be possible using the index, like `[1]`, or with wildcard for all, like `[*]`.

The following configurations work:

- Gradle and JUnit 4 *without* junit-vintage-engine: `./gradlew -i clean test --tests *ExampleTestJUnit4.test[1]`

The following configurations do *not* work
- Maven and JUnit 4: `mvn clean test -Dtest=*ExampleTestJUnit4#test[1]`
- Maven and JUnit 5: `mvn clean test -Dtest=*ExampleTestJUnit5#test[1]`
- Gradle and JUnit 5: `./gradlew -b buildJUnit5.gradle -i clean test --tests *ExampleTestJUnit5.test[1]`
- Gradle and JUnit 4 *with* junit-vintage-engine: `./gradlew -b buildJUnit5.gradle -i clean test --tests *ExampleTestJUnit4.test[1]`

All configurations run without the `[1]` at the end of the selector, so it seems like its the selector itself. Using `[*]` does not solve the problem.
