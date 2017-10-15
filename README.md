See below for the original jersey readme...

In order to use this patched version, you need to change dependencies to jersey from (for instance)
```xml
<dependency>
    <groupId>org.glassfish.jersey.core</groupId>
    <artifactId>jersey-server</artifactId>
    <version>${jerseyVersion}</version>
</dependency>
```
to
```xml
<dependency>
    <groupId>org.glassfish.jersey.core</groupId>
    <artifactId>jersey-server</artifactId>
    <version>${jerseyVersion}</version>
    <exclusions>
        <exclusion>
            <groupId>org.glassfish.jersey.core</groupId>
            <artifactId>jersey-common</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```       
And add a dependency to
```xml
<dependency>
    <groupId>org.glassfish.jersey.core</groupId>
    <artifactId>jersey-common-FIX-1</artifactId>
    <version>${jerseyVersion}</version>
</dependency>
```
In order to fulfill the dependency you may run ```mvn -DskipTests -pl common-core``` and find the outcome jar in ```common-core/target```.

When you put the jar file to the directory ```libs``` and add the following to you pom.xml
```xml
 <plugin>
    <artifactId>maven-install-plugin</artifactId>
    <version>2.3.1</version>
    <inherited>false</inherited>
    <executions>
        <execution>
            <id>jersey-fix</id>
            <goals>
                <goal>install-file</goal>
            </goals>
            <phase>initialize</phase>
            <configuration>
                <file>libs/jersey-common-FIX-1-2.26.jar</file>
                <groupId>org.glassfish.jersey.core</groupId>
                <artifactId>jersey-common-FIX-1</artifactId>
                <packaging>jar</packaging>
                <version>2.26</version>
            </configuration>
        </execution>
    </executions>
</plugin>
```
then you can deploy jar file to your local repository by calling ```mvn initialize```.
After that the dependency is found by maven.



### About Jersey

Jersey is a REST framework that provides JAX-RS Reference Implementation and more.
Jersey provides its own [APIs][jersey-api] that extend the JAX-RS toolkit with
additional features and utilities to further simplify RESTful service and client
development. Jersey also exposes numerous extension SPIs so that developers may
extend Jersey to best suit their needs.

Goals of Jersey project can be summarized in the following points:

*   Track the JAX-RS API and provide regular releases of production quality
    Reference Implementations that ships with GlassFish;
*   Provide APIs to extend Jersey & Build a community of users and developers;
    and finally
*   Make it easy to build RESTful Web services utilising Java and the
    Java Virtual Machine.

### Licensing and Governance
Jersey is licensed under a dual license - [CDDL 1.1 and GPL 2.0 with Class-path Exception](LICENSE.txt).
That means you can choose which one of the two suits your needs better and use it under those terms.

We use [GlassFish Governance Policy](GovernancePolicy.md), which means we can only accept contributions under
 the terms of [OCA][oca].

### More Info on Jersey
Follow [Jersey on Twitter][jersey-twitter] to get JAX-RS and Jersey related updates.
See the [Jersey website][jersey-web] to access Jersey documentation. If you run into any issues or have questions,
ask at [jersey@javaee.groups.io][jersey-users], [StackOverflow][jersey-so] or file an issue on [Jersey GitHub Project][jersey-issues].

[oca]: http://oracle.com/technetwork/goto/oca
[jersey-api]: https://jersey.github.io/apidocs/latest/jersey/index.html
[jersey-issues]: https://github.com/jersey/jersey/issues
[jersey-so]: http://stackoverflow.com/questions/tagged/jersey
[jersey-twitter]: http://twitter.com/gf_jersey
[jersey-users]: mailto:jersey@javaee.groups.io
[jersey-web]: http://jersey.github.io
