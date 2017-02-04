# Guia-Instalación-Antlr4- v4 Español
Esta guia te mostrará como instalar Antlr4 un potente generador de parser para todas las plataformas.

Es la nueva versión de ANTLR una mejora de las versiones antiguas es el hecho de poder escribir gramaticas mas naturales y estandarizadas como lo realiza yacc! Mira [prefacio del libro de ANTLR v4](http://media.pragprog.com/titles/tpantlr2/preface.pdf) como una guía mas detallada.

## Descripción

ANTLR es realmente dos cosas: una herramienta que traduce su gramática a un parser/lexer en Java (u otro lenguaje de programación) y las rutinas necesarias para los analizadores / lexers generados. Incluso si está utilizando el complemento ANTLR Intellij o ANTLRWorks para ejecutar la herramienta ANTLR, el código generado seguirá necesitando la biblioteca con las rutinas.

## Instalación


Antes de comenzar con la instalación es necesario descargar lo siguiente:
<br>
Java JDK [http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
<br>
antlr-4.5.3-complete.jar [http://www.antlr.org/download.html](http://www.antlr.org/download.html)


### UNIX

0. Instalar Java JDK (versión 1.6 o superior)
1. Descargar
```
$ cd /Users/tu_Usuario/Library
$ curl -O http://www.antlr.org/download/antlr-4.6-complete.jar
```
O descargalo desde el navegador desde:
    [http://www.antlr.org/download.html](http://www.antlr.org/download.html)
y ponlo en algun lugar racional como `/Users/tu_Usuario/Library`.
2. Agrega `antlr-4.6-complete.jar` a tu `CLASSPATH`:
```
$ export CLASSPATH=".:/Users/Library/antlr-4.6-complete.jar:$CLASSPATH"
```

3. Create alias para ANTLR, y para `TestRig`.
```
$ alias antlr4='java -Xmx500M -cp "/usr/local/lib/antlr-4.5.3-complete.jar:$CLASSPATH" org.antlr.v4.Tool'
$ alias grun='java org.antlr.v4.gui.TestRig'
```
![](images/Instalacionunix.png)

### WINDOWS


0. Instalar Java SE Development Kit 8u121(version 1.6 o superior) desde [http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
  * Considerar que el destino de ubicación(Drive) debe ser el mismo que el del sistema operativo.
1. Descargar antlr-4.6-complete.jar (or whatever version) from [http://www.antlr.org/download/](http://www.antlr.org/download/)
Guardar en el directorio para librerias de terceros, como: `C:\Javalib`
2. Añadir `antlr-4.6-complete.jar` al CLASSPATH, de forma:
  * Permanente: Presionar el boton de Start, escrbir y elegir  "Cuentas de Usuario" en la barra de búsqueda > Cambiar variables de entorno >.
  ![](images/antlr2.1.PNG)
Using System Properties dialog > Environment variables > Create or append to `CLASSPATH` variable
![](images/hello-parrt.png)
  * Temporal con el comando, at command line:
```
SET CLASSPATH=.;C:\Javalib\antlr-4.6-complete.jar;%CLASSPATH%
```
3. Create short convenient commands for the ANTLR Tool, and TestRig, using batch files or doskey commands:
  * Batch files (in directory in system PATH) antlr4.bat and grun.bat
```
java org.antlr.v4.Tool %*
```
```
java org.antlr.v4.gui.TestRig %*
```
  * Or, use doskey commands:
```
doskey antlr4=java org.antlr.v4.Tool $*
doskey grun =java org.antlr.v4.gui.TestRig $*
```

### Probando la instalación

La primera forma es poniendo el comando org.antlr.v4.Tool directamente:

```
$ java org.antlr.v4.Tool
ANTLR Parser Generator Version 4.6
-o ___ specify output directory where all output is generated
-lib ___ specify location of .tokens files
...
```

o usa la opción -jar en java:

```
$ java -jar /Users/Library/antlr-4.6-complete.jar
ANTLR Parser Generator Version 4.6
-o ___ specify output directory where all output is generated
-lib ___ specify location of .tokens files
...
```
![](images/Instalacionunix2.png)
## Un primer ejemplo

En un directorio temporal, colocar la siguiente gramática dentro de un archivo llamado Hello.g4:

```
// Define a grammar called Hello
grammar Hello;
r  : 'hello' ID ;         // match keyword hello followed by an identifier
ID : [a-z]+ ;             // match lower-case identifiers
WS : [ \t\r\n]+ -> skip ; // skip spaces, tabs, newlines
```

Ahora corre la herramienta ANTLR:

```
$ cd /tmp
$ antlr4 Hello.g4
$ javac Hello*.java
```
![](images/Instalacionunix3.png)
Ahora lo probaremos:

```
$ grun Hello r -tree
hello parrt
^D
(r hello parrt)
(That ^D means EOF on unix; it's ^Z in Windows.) The -tree option prints the parse tree in LISP notation.
It's nicer to look at parse trees visually.
$ grun Hello r -gui
hello parrt
^D
```
![](images/Instalacionunix5.png)
Esto genera una ventana qye muestra la regle `r` unida a la palabra clave `hello` seguida del identificador `parrt`.

![](images/Instalacionunix4.png)

## Libro con codigo fuente

El libro posee muchos ejemplos que podrian ser utiles. Puedes descargarlos gratis de:

[http://pragprog.com/titles/tpantlr2/source_code](http://pragprog.com/titles/tpantlr2/source_code)

Tambien, en este repositorio de github hay una larga colección de gramaticas para la version 4:

[https://github.com/antlr/grammars-v4](https://github.com/antlr/grammars-v4)
