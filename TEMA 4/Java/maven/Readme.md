### 1.1. Instal·lació de Maven en Ubuntu


Per tal de comprovar si tenim Maven instal·lat al nostre sistema, podem fer:

```
$ apt-cache policy maven
maven:
  Instal·lat: (cap)
  Candidat:   3.6.0-1~18.04.1
  Taula de versió:
     3.6.0-1~18.04.1 500
        500 http://es.archive.ubuntu.com/ubuntu bionic-updates/universe amd64 Packages
        500 http://es.archive.ubuntu.com/ubuntu bionic-updates/universe i386 Packages
        500 http://security.ubuntu.com/ubuntu bionic-security/universe amd64 Packages
        500 http://security.ubuntu.com/ubuntu bionic-security/universe i386 Packages
     3.5.2-2 500
        500 http://es.archive.ubuntu.com/ubuntu bionic/universe amd64 Packages
        500 http://es.archive.ubuntu.com/ubuntu bionic/universe i386 Packages
```

Com veiem ens indica que no tenim el paquet instal·lat, però que podem instal·lar la versió 3.6.0-1~18.04.1 des dels repositoris d'Ubuntu.

Per tal d'instal·lar el paquet, ho haurem de fer com a administradors:

```
$ sudo apt update
...
$ sudo apt install maven
[sudo] contrasenya per a eljust:
S'està llegint la llista de paquets… Fet
S'està construint l'arbre de dependències
S'està llegint la informació de l'estat… Fet
...
S'instal·laran els següents paquets extres:
  libwagon-file-java libwagon-http-shaded-java
S'instal·laran els paquets NOUS següents:
  libwagon-file-java libwagon-http-shaded-java maven
0 actualitzats, 3 nous a instal·lar, 0 a suprimir i 72 no actualitzats.
S'ha d'obtenir 1787 kB d'arxius.
Després d'aquesta operació s'empraran 2261 kB d'espai en disc addicional.

Com veiem, el paquet maven arrossega algunes dependències, el que ens dóna una visió de la magnitud del projecte front a ant. Indiquem que sí que volem realitzar la instal·lació, i esperem que aquesta finalitze.

Per tal de comprova que tenim Maven instal·lat al sistema, fem:

$ mvn --version
Apache Maven 3.6.0
Maven home: /usr/share/maven
Java version: 11.0.5, vendor: Private Build, runtime: /usr/lib/jvm/java-11-openjdk-amd64
Default locale: ca_ES, platform encoding: UTF-8
OS name: "linux", version: "4.15.0-72-generic", arch: "amd64", family: "unix"
```

### 2. Primer exemple amb Maven

Anem a començar amb la creació d'aquest primer exemple. Per a això, llançarem la següent ordre:

```
$ mvn archetype:generate -DgroupId=com.ieseljust.edd -DartifactId=myHelloMVN -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

Amb tot açò, l'eixida de l'ordre anterior (i després de descarregar algun programari addicional...) és la següent:

```
$ mvn archetype:generate -DgroupId=com.ieseljust.edd -DartifactId=myHelloMVN -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
...
[INFO] Scanning for projects...
Downloading...

...
[INFO] 
[INFO] ------------------< org.apache.maven:standalone-pom >-------------------
[INFO] Building Maven Stub Project (No POM) 1
[INFO] --------------------------------[ pom ]---------------------------------
[INFO] 
[INFO] >>> maven-archetype-plugin:3.1.2:generate (default-cli) > generate-sources @ standalone-pom >>>
[INFO] 
[INFO] <<< maven-archetype-plugin:3.1.2:generate (default-cli) < generate-sources @ standalone-pom <<<
[INFO] 
[INFO] 
[INFO] --- maven-archetype-plugin:3.1.2:generate (default-cli) @ standalone-pom ---
Downloading...
...
[INFO] ----------------------------------------------------------------------------
[INFO] Using following parameters for creating project from Old (1.x) Archetype: maven-archetype-quickstart:1.0
[INFO] ----------------------------------------------------------------------------
[INFO] Parameter: basedir, Value: .../exemples_java/mvn1
[INFO] Parameter: package, Value: com.ieseljust.edd
[INFO] Parameter: groupId, Value: com.ieseljust.edd
[INFO] Parameter: artifactId, Value: myHelloMVN
[INFO] Parameter: packageName, Value: com.ieseljust.edd
[INFO] Parameter: version, Value: 1.0-SNAPSHOT
[INFO] project created from Old (1.x) Archetype in dir: .../exemples_java/mvn1/myHelloMVN
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  30.233 s
[INFO] Finished at: 2020-01-02T09:13:05+01:00
[INFO] ------------------------------------------------------------------------
...
```

Bé, veiem ara què ens ha generat aquesta ordre:

```
$ tree
.
`-- myHelloMVN
    |-- pom.xml
    `-- src
        |-- main
        |   `-- java
        |       `-- com
        |           `-- ieseljust
        |               `-- edd
        |                   `-- App.java
        `-- test
            `-- java
                `-- com
                    `-- ieseljust
                        `-- edd
                            `-- AppTest.java
```

Ara posem en companyia de App.java, els arxius que creem de Calcula.java i Calculadora.java.

Fem ús de la comanda tree altra vegada i veiem l'estructura nova:

```
$ tree
.
`-- myHelloMVN
    |-- pom.xml
    `-- src
        |-- main
        |   `-- java
        |       `-- com
        |           `-- ieseljust
        |               `-- edd
        |                   `-- App.java
        |                      |-Calcula.java
        |                      |-Calculadora.java
        `-- test
            `-- java
                `-- com
                    `-- ieseljust
                        `-- edd
                            `-- AppTest.java
```

Com veiem, ha creat la carpeta del projecte myHelloMVN amb el fitxer pom.xml, que descriu el projecte segons el Project Ojbect Model (POM). Dins d'aquesta carpeta tenim la carpeta src, amb els fitxers font i de tests, degudament organitzats en carpetes segons el nom de domini completament qualificat.

### 2.2. El fitxer pom.xml

El fitxer pom.xml descriu la configuració del projecte en Maven, i proporciona la major part d'informació necessària per a la seua construcció. Pot arribar a ser un fitxer llarg i complex, però no és necessari entendre tot el seu contingut per traure tota l'efectivitat de Maven.

Veiem el contingut dle nostre fitxer:

```
xml <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd"> <modelVersion>4.0.0</modelVersion> <groupId>com.ieseljust.edd</groupId> <artifactId>myHelloMVN</artifactId> <packaging>jar</packaging> <version>1.0-SNAPSHOT</version> <name>myHelloMVN</name> <url>http://maven.apache.org</url> <dependencies> <dependency> <groupId>junit</groupId> <artifactId>junit</artifactId> <version>3.8.1</version> <scope>test</scope> </dependency> </dependencies> </project>
```

### Realitzant alguns ajustos al fitxer:

Les últimes versions de Maven no suporten ja la compilació per a Java 1.5, pel que si no indiquem el contrari, obtindrem un missatge de compilació del tipus:

[ERROR] Source option 1.5 is no longer supported. Use 1.6 or later.
[ERROR] Target option 1.5 is no longer supported. Use 1.6 or later.

Per tal d'evitar açò, cal especificar un parell de propietats per al projecte. Concretament el source i el target del compilador de Maven. Per a això, editem el fitxem pom.xml i afegim la següent etiqueta <properties>, abans d'especificar l'etiqueta de dependències:

```
 [...]
 <url>http://maven.apache.org</url>

  <properties>
    <maven.compiler.source>1.6</maven.compiler.source>
    <maven.compiler.target>1.6</maven.compiler.target>
  </properties>

  <dependencies>
  [...]
```

### 2.3. Hola Món!

L'arquetipus que hem utilitzat per generar l'aplicació, maven-archetype-quickstart, ens crea directament un esquelet d'aplicació del tipus Hola Món, directament. Si accedim al fitxer src/main/java/com/ieseljust/app/App.java, veurem un codi bastant familiar:

```
package com.ieseljust.edd;

/**
 * Hello world!
 *
 */
public class App
{
    public static void main( String[] args )
    {
        System.out.println( "Hello World!" );
    }
}
```

### 2.4. Compilació, neteja i construcció del projecte

Una vegada tenim l'esquelet de l'aplicació generat, ja podem realitzar la seua compilació i construcció.

Per tal de fer la compilació, des de la carpeta arrel del projecte (la que conté el pom.xml), llancem la següent ordre:

```
$ mvn compile
...
[INFO] Scanning for projects...
[INFO] 
[INFO] --------------------< com.ieseljust.edd:myHelloMVN >--------------------
[INFO] Building myHelloMVN 1.0-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
[INFO] 
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ myHelloMVN ---
[WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[INFO] skip non existing resourceDirectory /home/joamuran/Dropbox/Docencia/curs_19-20/EDD/Unitats/UD4. Automatitzacio/exemples_java/mvn1/myHelloMVN/src/main/resources
[INFO] 
[INFO] --- maven-compiler-plugin:3.1:compile (default-compile) @ myHelloMVN ---
[INFO] Changes detected - recompiling the module!
[WARNING] File encoding has not been set, using platform encoding UTF-8, i.e. build is platform dependent!
[INFO] Compiling 1 source file to /home/joamuran/Dropbox/Docencia/curs_19-20/EDD/Unitats/UD4. Automatitzacio/exemples_java/mvn1/myHelloMVN/target/classes
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  1.643 s
[INFO] Finished at: 2020-01-02T09:27:04+01:00
[INFO] ------------------------------------------------------------------------
```

Amb açò s'haurà generat una nova carpeta target a l'arrel del projecte, amb les classes generades, amb la següent estructura:

```
$ tree target
target
|-- classes
|   `-- com
|       `-- ieseljust
|           `-- edd
|               `-- App.class
|                 |-calc
|                      |-Calcula.class
|                      |-Calculadora.class
|-- generated-sources
|   `-- annotations
`-- maven-status
    `-- maven-compiler-plugin
        `-- compile
            `-- default-compile
                |-- createdFiles.lst
                `-- inputFiles.lst
```

Per tal d'executar l'aplicació App:

```
$ java -cp target/classes com.ieseljust.edd.App 
Hello World!
```

Per tal d'executar l'aplicació Calcula:

```
diec85@diec85-PL62-7RC:~/Escritorio/Visual_Studio/EDD/Tema 4/Java/maven/projecte/myHelloMVN$ java -cp target/classes/ com.ieseljust.edd.calc.Calcula 7 6
La suma entre 7.0 i 6.0 és 13.0
La resta entre 7.0 i 6.0 és 1.0
La multiplicació entre 7.0 i 6.0 és 42.0
La divisió entre 7.0 i 6.0 és 1.1666666
Última operació realitzada: Divideix; Últim resultat: 1.1666666
La mitja de les operacions es: 10.0
Es 7.0 major que 6.0? true
Es 7.0 menor que 6.0? false

```

Per altra banda, si el que volem és netejar el projecte, farem:

```
mvn clean
```

Que com veurem, ens haurà esborrat la carpeta target anterior.

Finalment, per fer la construcció i empaquetat en jar del projecte, farem:

```
$ mvn package
```

O si bé volem fer la neteja i la construcció tot d'una, podem fer:

```
$ mvn clean package
```

Veiem-ne el resultat de l'empaquetat:

```
$ mvn package
...
[INFO] Building jar: .../exemples_java/mvn1/myHelloMVN/target/myHelloMVN-1.0-SNAPSHOT.jar
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  8.220 s
[INFO] Finished at: 2020-01-02T09:32:27+01:00
[INFO] ------------------------------------------------------------------------
```

Amb açò s'ha realitzat la compilació i els tests corresponents, generant tota l'estrucura de directoris següent:

```
target
|-- classes
|   `-- com
|       `-- ieseljust
|           `-- edd
|               `-- App.class
|                 |-calc
|                      |-Calcula.class
|                      |-Calculadora.class
|-- generated-sources
|   `-- annotations
|-- generated-test-sources
|   `-- test-annotations
|-- maven-archiver
|   `-- pom.properties
|-- maven-status
|   `-- maven-compiler-plugin
|       |-- compile
|       |   `-- default-compile
|       |       |-- createdFiles.lst
|       |       `-- inputFiles.lst
|       `-- testCompile
|           `-- default-testCompile
|               |-- createdFiles.lst
|               `-- inputFiles.lst
|-- myHelloMVN-1.0-SNAPSHOT.jar
|-- surefire-reports
|   |-- com.ieseljust.edd.AppTest.txt
|   `-- TEST-com.ieseljust.edd.AppTest.xml
`-- test-classes
    `-- com
        `-- ieseljust
            `-- edd
                `-- AppTest.class
```

20 directories, 10 files

Si ens fixem, dins la carpeta target es troba el fitxer myHelloMVN-1.0-SNAPSHOT.jar, amb l'aplicació empaquetada. Per tal d'executar l'aplicació des del jar, establirem aquest com al classpath i llançarem l'aplicació:

App:

```
$ java -cp target/myHelloMVN-1.0-SNAPSHOT.jar com.ieseljust.edd.App
Hello World!
```

Calcula:

```
diec85@diec85-PL62-7RC:~/Escritorio/Visual_Studio/EDD/Tema 4/Java/maven/projecte/myHelloMVN$ java -cp target/myHelloMVN-1.0-SNAPSHOT.jar com.ieseljust.edd.calc.Calcula 8 3
La suma entre 8.0 i 3.0 és 11.0
La resta entre 8.0 i 3.0 és 5.0
La multiplicació entre 8.0 i 3.0 és 24.0
La divisió entre 8.0 i 3.0 és 2.6666667
Última operació realitzada: Divideix; Últim resultat: 2.6666667
La mitja de les operacions es: 9.5
Es 8.0 major que 3.0? true
Es 8.0 menor que 3.0? false
```
