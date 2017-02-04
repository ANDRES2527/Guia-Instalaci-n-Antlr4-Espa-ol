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

(*Thanks to Graham Wideman*)

0. Instalar Java SE Development Kit 8u121(version 1.6 o superior) desde [http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
  * Considerar que el destino de ubicación(Drive) debe ser el mismo que el del sistema operativo.
1. Descargar antlr-4.6-complete.jar (o cualquier version) de [http://www.antlr.org/download/](http://www.antlr.org/download/)
Guardar en el directorio para librerias de terceros, como: `C:\Javalib`
2. Añadir `antlr-4.6-complete.jar` al PATH, de la siguiente manera:
  * Ir a  "Cuentas de Usuario"> Cambiar las variables de entorno.
  ![](images/antlr2.png)
  * Crear o añadir una variable `PATH` para antlr `C:\Javalib\antlr-4.6.complete.jar` y para el jdk `C:\Program Files\jdk.1.8.0_111\bin`
![](images/antlr3.png)

3. Crear atajos para los comandos de las herramientas ATNRL y TestRig, usandos archivos batch o comandos doskey:
  * Archivo batch con el siguiente contenido (en el mismo direcorio agregado de 'PATH) `antlr4.bat`
```
java org.antlr.v4.Tool %*
```
 Archivo batch con el siguiente contenido (en el mismo direcorio agregado de 'PATH) `grun.bat`
```
java org.antlr.v4.gui.TestRig %*
```
![](images/antlr4.png)
  * O, usando comandos doskey:
```
doskey antlr4=java org.antlr.v4.Tool $*
doskey grun =java org.antlr.v4.gui.TestRig $*
```

### Probando la instalación en WINDOWS con un Ejemplo

En el directorio `CLASSPATH` `C:\Javalib` ejecutar el comando  :
* Siempre para empezar el uso, en la terminal de comandos (CMD) , realizar un set del PATH antlr:
```
SET CLASSPATH=.;C:\Javalib\antlr-4.6-complete.jar;%CLASSPATH%
```
* Ejectuar la siguiente instrucción para verificar la instalación
```
$ C:\Javalib>antlr4
ANTLR Parser Generator Version 4.6
-o ___ specify output directory where all output is generated
-lib ___ specify location of .tokens files
...
```
![](images/antlr5.png)
* En la misma  carpeta `CLASSPATH` colocar la siguiente gramática dentro de un archivo `Hello.g4`:

```
// Define a grammar called Hello
grammar Hello;
r  : 'hello' ID ;         // match keyword hello followed by an identifier
ID : [a-z]+ ;             // match lower-case identifiers
WS : [ \t\r\n]+ -> skip ; // skip spaces, tabs, newlines
```

Para ejectuar la herramienta ANTLR en la consola (CMD):

```
$ cd /Javalib
$ SET CLASSPATH=.;C:\Javalib\antlr-4.6-complete.jar;%CLASSPATH%
$ antlr4 Hello.g4
$ javac Hello*.java
```

Ahora para la prueba:

```
$ grun Hello r -tree
hello parrt
^Z
(r hello parrt)
// ^Z significa en Windows una salida(CTRL+Z > ENTER)). La opción -tree imprime el  árbol de parseo en notación LISP.
$ grun Hello r -gui
hello parrt
^Z
```
![](images/antlr6.png)
Esto genera una ventana que muestra la regla `r` unida a la palabra clave `hello` seguida del identificador `parrt`.

![](images/antlr7.png)

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
Esto genera una ventana que muestra la regla `r` unida a la palabra clave `hello` seguida del identificador `parrt`.

![](images/Instalacionunix4.png)

## Libro con codigo fuente

El libro posee muchos ejemplos que podrian ser utiles. Puedes descargarlos gratis de:

[http://pragprog.com/titles/tpantlr2/source_code](http://pragprog.com/titles/tpantlr2/source_code)

Tambien, en este repositorio de github hay una larga colección de gramaticas para la version 4:

[https://github.com/antlr/grammars-v4](https://github.com/antlr/grammars-v4)
