API Setup
=========

Add prism-api to your maven pom.xml or build.gradle.

.. tabs::

   .. group-tab:: Maven

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
            <groupId>me.botsko</groupId>
            <artifactId>prism-api</artifactId>
            <version>1.0.0-SNAPSHOT</version>
            <scope>provided</scope>
        </dependency>

   .. group-tab:: Gradle (Groovy)

      .. code:: groovy

        repositories {
            maven {
                url = "https://nexus.darkhelmet.network/repository/maven-snapshots/t"
            }
            maven {
                url = "https://nexus.darkhelmet.network/repository/maven-releases/"
            }
        }

        dependencies {
            compileOnly 'network.darkhelmet.prism:prism-api:1.0.0-SNAPSHOT'
        }