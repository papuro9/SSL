731.1 Secuencias de pasos
1. PREPROCESADOR
b. gcc -E hello2.c -o hello2.i .
Dentro del archivo hello2.i estan todo el contenido de <stdio.h> y al final de todo se encuentra el codigo de hello2.c pero con los comentarios reempalzados por el espacio
las concluciones que se puede obtener es que el preprocesador expande directivas, condiciona bloques y elimina comentarios 

d. Se declara un prototipo de la función printf que recibe un carácter al cual apunta un puntero fijo, este apuntará constantemente a esa misma dirección física. También, el prototipo podrá recibir una cantidad variable de argumentos además del mencionado.

e. gcc -E hello3.c -o hello3.i .La principal diferencia que encontramos entre hello3.c y hello3.i es el agregado de directivas del preprocesador en el hello3.i que controlan el flujo de origen.

2. COMPILACION
b. gcc -S hello4.c -o hello4.s 
cc1.exe: fatal error: heelo3.i: No such file or directory 
compilation terminated.
c. -c hello4.s -o hello4.o .El .s es la traducción en lenguaje ensamblador del C: muestra, instrucción a instrucción, cómo el procesador ejecutará la lógica y gestionará llamadas a funciones y estructuras de datos.

3. Vinculacion
a. gcc hello4.o -o hello4
b. gcc hello5.o -o hello5
c. ./hello5 
Corregimos en el paso de hello4.c a hello5.c el uso de prontf a printf, permitiéndonos vincular con la librería estándar. Obtuvimos un archivo ejecutable que al ejecutarlo retorna “La respuesta es <numero basura de la memoria>”, esta respuesta tiene todo el sentido ya que nunca le especificamos a printf que valor ubicar en el lugar donde se le indica colocar un valor entero decimal.

4. Correccion de Bug
a. El ejecutable generado por hello6.c cumple satisfactoriamente con la consigna (Mostrar por pantalla “La respuesta es 42”)

5. Remocion de prototipo
I. Arroja dos warnings: warning: implicit declaration of function 'printf' y warning: incompatible implicit declaration of built-in function 'printf'. Sin embargo, desde otro entorno arrojó los mismo, pero el primer warning fue tratado como error.
II. Un prototipo de función es una declaración del nombre, el tipo de parámetros que recibe, así como el tipo de dato que retorna una función, Se genera incluyendo una librería o escribiendo explícitamente el prototipo que se quiere declarar.
III. Si en C usamos una función, pero no la declaramos, se asume que retorna un entero y que puede recibir cualquier tipo de parámetros en cualquier orden. Esto es conocido como declaración implícita.
IV. Según las especificaciones anteriores a C99, el compilador ante una llamada a una función la cual no tiene un prototipo declarado asume que la función recibe parámetros con tipos definidos y devuelve un variable de tipo entero. Si nos fijamos en las especificaciones post C99 este tipo de declaraciones implícitas están prohibidas.
V. Las principales implementaciones, es decir los compiladores, trabajan de acuerdo a especificaciones. Sin embargo, no de manera tan estricta ya que para algunas funciones bien conocidas determinadas se permite la declaración implícita.
VI. Las funciones “built in” o función incorporada es un término que refiere a funciones que no se necesitan definir o incluir desde una librería externa en el código, sea porque las reconoce el compilador o ya se encuentra en la librería estándar, la cual es vinculada por defecto en algunos compiladores como gcc.
VII. Concluimos que gcc tiene este comportamiento debido a la conveniencia que trae el definir la función implícitamente y el vincular automáticamente con la librería estándar incluso si no se le fue indicado, pues esta se ve incluida en la gran mayoría de códigos y posee las definiciones de las funciones más usadas. Es lógico pensar que un código que no incluya la librería estándar de C sea así porque esta fue olvidada antes que sea el caso que no se quiera vincular con la librería estándar a voluntad propia.
Esto va en contra de las especificaciones de C, pero facilita el uso de C.

6. Compilacion separada: Contrato y modulos
-gcc -c hello8.c -o hello8.o
-gcc -c studio1.c -o studio1.o
-gcc hello8.o studio1.o -o programa
./programa

c.Luego de ejecutar esos comandos Al compilar y vincular estos dos archivos obtenemos uno que al ejecutarlo retorna “La respuesta es 42"
d.La principal ventaja es la de que ambos puedan conocer el nombre de la función, los tipos que recibe como parámetros y la cantidad de y lo que devuelve esa función. Esto ayuda al compilar principalmente a detectar errores como que faltaron argumentos a la hora de llamar a la función o se excede los argumentos que recibe la función de parte del consumidor, y por la parte del proveedor facilita la detección de errores del tipo conflicto de tipo sobre un parámetro que recibe la función. Como conclusión se puede decir que esto ayuda a que se cumpla con lo establecido en el archivo cabecera en dos unidades de traducción diferentes. 








