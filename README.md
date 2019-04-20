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

Import the new class

        import jsam.Jsam;

Instantiate an object of type Jsam

        private Jsam appSocket = new Jsam();

Set up the connection

        appSocket.HelloSAM();
        appSocket.CreateSession(id, "");
        appSocket.ConnectSession(id, url);

And the various objects required to read from and write to the socket

        PrintWriter pw = new PrintWriter(appSocket.getOutputStream());
        InputStreamReader ir = new InputStreamReader(appSocket.getInputStream());
        BufferedReaderbr = new BufferedReader(ir);

To send a GET, write to the socket with the PrintWriter

        pw.println("GET / HTTP/1.1");
        pw.println("Host: " + url);
        pw.flush();

To read a response, loop until readLine() is non-null.

        while((t = br.readLine()) != null) {
            System.out.println(t);
        }

Example
-------

        import jsam.Jsam;
        import java.io.PrintWriter;
        import java.io.BufferedReader;
        import java.io.InputStreamReader;

        public class App {
            private Jsam appSocket = new Jsam();
            private PrintWriter pw;
            private InputStreamReader ir;
            private BufferedReader br;
            private String url = "i2p-projekt.i2p";
            private String t = "false";
            private String id = "test";
            public App() {
                appSocket.HelloSAM();
                appSocket.CreateSession(id, "");
                appSocket.ConnectSession(id, url);
                try {
                    System.out.println("Instantiating application");
                    pw = new PrintWriter(appSocket.getOutputStream());
                    ir = new InputStreamReader(appSocket.getInputStream());
                    br = new BufferedReader(ir);
                } catch(Exception e) {
                    System.out.println("Instantiation Error: " + e);
                }
            }
            public String get(String url) {
                try {
                    pw = new PrintWriter(appSocket.getOutputStream());
                    br = new BufferedReader(new InputStreamReader(appSocket.getInputStream()));
                    System.out.println("Trying to get " + url);
                    pw.println("GET / HTTP/1.1");
                    pw.println("Host: " + url);
                    pw.flush();
                    System.out.println("Sent request to " + url);
                    while((t = br.readLine()) != null) {
                        System.out.println(t);
                    }
                    br.close();
                    return "true";
                } catch(Exception e) {
                    System.out.println(e);
                    System.out.println("Failed to get " + url);
                }
                return t;
            }
            //public static void main(String[] args) {
            public void main(String[] args) {
                url = args[0];
                get(url);
            }
        }
