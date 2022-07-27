API Setup
=========

Add prism-api to your maven pom.xml or build.gradle.

.. tabs::

    .. tab:: Maven

        .. code:: xml

            <repositories>
                <repository>
                    <name>addstar-maven-snapshots</name>
                    <url>https://nexus.darkhelmet.network/repository/maven-snapshots/</url>
                </repository>
                <repository>
                    <name>addstar-maven-releases</name>
                    <url>https://nexus.darkhelmet.network/repository/maven-releases/</url>
                </repository>
            </repositories>

            <dependency>
                <groupId>network.darkhelmet</groupId>
                <artifactId>prism-api</artifactId>
                <version>1.0.0-SNAPSHOT</version>
                <scope>provided</scope>
            </dependency>

    .. tab:: Gradle (Groovy)

        .. code:: groovy

            repositories {
                maven {
                    url = "https://nexus.darkhelmet.network/repository/maven-snapshots/"
                }
                maven {
                    url = "https://nexus.darkhelmet.network/repository/maven-releases/"
                }
            }

            dependencies {
                compileOnly 'network.darkhelmet.prism:prism-api:1.0.0-SNAPSHOT'
            }