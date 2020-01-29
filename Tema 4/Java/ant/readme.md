### Creamos la estructura para el archivo Calculadora.java y Calcula.java:

```
Visual_Studio
`--EDD
    `-- TEMA 4
        `--Java
            `-- com
                `-- ieseljust
                        `-- edd
                            `-- calc
                                    |-- Calculadora.java
                                    `-- Calcula.java
```

### Codigo Calculadora.java original:

Aquesta classe s'implementa al fitxer com/ieseljust/edd/calc/Calculadora.java:

```
package com.ieseljust.edd.calc;

public class Calculadora {

    private float lastResult;
    private String lastOp;

    public float getLastResult(){
        return this.lastResult;
    }

    public String getLastOp(){
        return this.lastOp;
    }

    public float suma(float op1, float op2){
        float result=op1+op2;
        this.lastResult=result;
        this.lastOp="Suma";

        return result;
    }

    public float resta(float op1, float op2){
        float result=op1-op2;
        this.lastResult=result;
        this.lastOp="Resta";

        return result;
    }

    public float multiplica(float op1, float op2){
        // Fem els càlculs
        float result=op1*op2;

        // Actualitzem els atributs de la classe
        this.lastResult=result;
        this.lastOp="Multiplica";

        // I finalment retornem els resultats
        return result;
    }

    public float divideix(float op1, float op2){
        // Fem els càlculs
        float result=op1/op2;

        // Actualitzem els atributs de la classe
        this.lastResult=result;
        this.lastOp="Divideix";

        // I finalment retornem els resultats
        return result;
    }

}
```

### Codigo Calculadora.java modificado para la practica:


```
package com.ieseljust.edd.calc;

public class Calculadora {

    private float lastResult;
    private String lastOp;

    public float getLastResult(){
        return this.lastResult;
    }

    public String getLastOp(){
        return this.lastOp;
    }

    public float suma(float op1, float op2){
        float result=op1+op2;
        this.lastResult=result;
        this.lastOp="Suma";

        return result;
    }

    public float resta(float op1, float op2){
        float result=op1-op2;
        this.lastResult=result;
        this.lastOp="Resta";

        return result;
    }

    public float multiplica(float op1, float op2){
        // Fem els càlculs
        float result=op1*op2;

        // Actualitzem els atributs de la classe
        this.lastResult=result;
        this.lastOp="Multiplica";

        // I finalment retornem els resultats
        return result;
    }

    public float divideix(float op1, float op2){
        // Fem els càlculs
        float result=op1/op2;

        // Actualitzem els atributs de la classe
        this.lastResult=result;
        this.lastOp="Divideix";

        // I finalment retornem els resultats
        return result;
    }

    public float mitja(float op1, float op2){

        float result=op1+op2/2;

        return result;

    }
    
    public boolean major(float n1, float n2){
        
        /*return(n1>n2);*/
        boolean major;
        
        if (n1 > n2){
            major = true;
        }
        else{
            major = false;
        }

        return major;
    }

    public boolean menor(float n1, float n2){

        return(n1<n2);

     }

}
```

### Codigo Calcula.java original:

El fitxer corresponent a la classe és el com/ieseljust/edd/calc/Calcula.java:


```
package com.ieseljust.edd.calc;

import com.ieseljust.edd.calc.Calculadora;

public class Calcula {
    private static float operand1;
    private static float operand2;

    public static void main(String[] args) {
        if (args.length != 2) {
            System.out.println("\nSintaxi incorrecta. Necessite dos números.");
            System.exit(-1);
        }

        operand1=Float.parseFloat(args[0]);
        operand2=Float.parseFloat(args[1]);

        Calculadora myCalc=new Calculadora();

        System.out.println("La suma entre "+operand1+" i "+operand2+" és "+myCalc.suma(operand1, operand2));
        System.out.println("La resta entre "+operand1+" i "+operand2+" és "+myCalc.resta(operand1, operand2));
        System.out.println("La multiplicació entre "+operand1+" i "+operand2+" és "+myCalc.multiplica(operand1, operand2));
        System.out.println("La divisió entre "+operand1+" i "+operand2+" és "+myCalc.divideix(operand1, operand2));
        System.out.println("Última operació realitzada: "+myCalc.getLastOp()+"; Últim resultat: "+myCalc.getLastResult());
    }
}
```

### Codigo Calcula.java modificado para la practica:

```
package com.ieseljust.edd.calc;

import com.ieseljust.edd.calc.Calculadora;

public class Calcula {
    private static float operand1;
    private static float operand2;

    public static void main(String[] args) {
        if (args.length != 2) {
            System.out.println("\nSintaxi incorrecta. Necessite dos números.");
            System.exit(-1);
        }

        operand1=Float.parseFloat(args[0]);
        operand2=Float.parseFloat(args[1]);

        Calculadora myCalc=new Calculadora();

        System.out.println("La suma entre "+operand1+" i "+operand2+" és "+myCalc.suma(operand1, operand2));
        System.out.println("La resta entre "+operand1+" i "+operand2+" és "+myCalc.resta(operand1, operand2));
        System.out.println("La multiplicació entre "+operand1+" i "+operand2+" és "+myCalc.multiplica(operand1, operand2));
        System.out.println("La divisió entre "+operand1+" i "+operand2+" és "+myCalc.divideix(operand1, operand2));
        System.out.println("Última operació realitzada: "+myCalc.getLastOp()+"; Últim resultat: "+myCalc.getLastResult());
        System.out.println("La mitja de les operacions es: "+myCalc.mitja(operand1, operand2));
        System.out.println("Es "+operand1+" major que "+operand2+"? " +myCalc.major(operand1, operand2));
        System.out.println("Es "+operand1+" menor que "+operand2+"? " +myCalc.menor(operand1, operand2));
    }
}
```

### Para compilar el archivo Calculadora.java y Calcula.java:


Compilar de forma individual els dos fitxers:

```
$ javac com/ieseljust/edd/calc/Calculadora.java
$ javac com/ieseljust/edd/calc/Calcula.java
```
Compilar directament tots els fitxers .java del directori calc:

$ javac com/ieseljust/edd/calc/*.java


### Para ejecutar la calculadora:

```
$ java com.ieseljust.edd.calc.Calcula num1 num2
```

### Creamos el fichero build.xml:

```
<project>
    <target name="clean">
        <delete dir="classes" />
    </target>

    <target name="compile" depends="clean">
        <mkdir dir="classes" />
    <javac includeantruntime="false" srcdir="com/ieseljust/edd/calc" destdir="classes" />
    </target>

    <target name="run" depends="compile">
        <java classpath="classes" classname="com.ieseljust.edd.calc.Calcula">
            <arg value="${arg0}"/>
            <arg value="${arg1}"/>
        </java>

    </target>
</project>
```

### La estructura se queda de este modo:

```
calculadora
    |-- build.xml
    |-- classes
    `-- com
        `-- ieseljust
            `-- edd
```
### Instalacion de ant:

### 1 Comprobamos si tenemos instalado la herramienta ant:

```
$ apt-cache policy ant
ant:
  Instal·lat: (cap)
  Candidat:   1.10.5-3~18.04
  Taula de versió:
     1.10.5-3~18.04 500
        500 http://archive.ubuntu.com/ubuntu bionic-updates/universe amd64 Packages
        500 http://archive.ubuntu.com/ubuntu bionic-updates/universe i386 Packages
        500 http://security.ubuntu.com/ubuntu bionic-security/universe amd64 Packages
        500 http://security.ubuntu.com/ubuntu bionic-security/universe i386 Packages
     1.10.3-1 500
        500 http://archive.ubuntu.com/ubuntu bionic/universe amd64 Packages
        500 http://archive.ubuntu.com/ubuntu bionic/universe i386 Packages
```

### Si no la tenemos, la instalamos con:

```
$ sudo apt install ant
```

### Uso de la herramienta ant:

### Primero compilamos:

```
$ ant compile
Buildfile: /home/joamuran/Dropbox/Docencia/curs_19-20/EDD/Unitats/UD4. Automatitzacio/exemples_java/calcula/build.xml

clean:

compile:
    [mkdir] Created dir: ./calcula/classes
    [javac] Compiling 2 source files to /home/joamuran/Dropbox/Docencia/curs_19-20/EDD/Unitats/UD4. Automatitzacio/exemples_java/calcula/classes

BUILD SUCCESSFUL
Total time: 0 seconds
```
### Se nos creara esta estructura:

```
|-- build.xml
|-- classes
|   `-- com
|       `-- ieseljust
|           `-- edd
|               `-- calc
|                   |-- Calcula.class
|                   `-- Calculadora.class
`-- com
    `-- ieseljust
        `-- edd
            `-- calc
                |-- Calculadora.java
                `-- Calcula.java
```

### Lo ejecutamos con:

```
$ ant run -Darg0=3 -Darg1=4
Buildfile: /home/joamuran/Dropbox/Docencia/curs_19-20/EDD/Unitats/UD4. Automatitzacio/exemples_java/calcula/build.xml

clean:
   [delete] Deleting directory /home/joamuran/Dropbox/Docencia/curs_19-20/EDD/Unitats/UD4. Automatitzacio/exemples_java/calcula/classes

compile:
    [mkdir] Created dir: /home/joamuran/Dropbox/Docencia/curs_19-20/EDD/Unitats/UD4. Automatitzacio/exemples_java/calcula/classes
    [javac] Compiling 2 source files to /home/joamuran/Dropbox/Docencia/curs_19-20/EDD/Unitats/UD4. Automatitzacio/exemples_java/calcula/classes

run:
     [java] La suma entre 3.0 i 4.0 és 7.0
     [java] La resta entre 3.0 i 4.0 és -1.0
     [java] La multiplicació entre 3.0 i 4.0 és 12.0
     [java] La divisió entre 3.0 i 4.0 és 0.75
     [java] Última operació realitzada: Divideix; Últim resultat: 0.75

BUILD SUCCESSFUL
Total time: 1 second
```