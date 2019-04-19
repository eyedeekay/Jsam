Jsam
====

Jsam is a library for interacting with the I2P network via the SAM API using an
interface resembling Java Sockets.

Building
--------

Simply run

        gradle build

and the compiled .jar file will be in

        build/libs/Jsam.jar

Including in an Application
---------------------------

Copy the jar file from the build folder to the 'libs' directory in your
application project.

        cp ./build/libs/Jsam.jar $PROJECT_DIRECTORY/libs/Jsam.jar

Add a compile dependency in the build.gradle file.

        dependencies {
            compile files('libs/Jsam.jar')
        }

Usage
-----

