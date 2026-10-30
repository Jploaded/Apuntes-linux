  Comando "Whoami" sirve para ver que usuario eres.

el usuario root es el que mas privilegios tiene, puede destruir todo el sistema si quiere

Filtros para buscar palabras en un directorio ( | grep ),agregarle el parametro (-n ) para ver la linea en la que esta, el parametro (-v sirve para quitar una linea que no quieres que te muestre en el output) ejemplo: | grep -v "palabra o lineas que no quieres que te mueste en el output " y si a al "-v" le agregas el una "E" mayuscula puedes quitar multiples cosas.

El comando `tr -d` sirve para **borrar caracteres específicos** de un texto.

### Ejemplo

Imagina que tienes la dirección IP de una máquina entre comillas y quieres dejar solo los números:

Bash

```
echo '"10.10.10.121"' | tr -d '"'
```

**Resultado:** `10.10.10.121`

**En resumen:** Lo que pongas dentro de las comillas después del `-d` desaparecerá por completo del resultado final.

El comando **`sed`** (_Stream Editor_) sirve para **buscar y reemplazar** texto de forma automática. A diferencia de `tr`, este sí puede borrar o cambiar **palabras completas**.

### Ejemplo (Reemplazar una palabra)

Si tienes el nombre de una máquina y quieres cambiar "Linux" por "Windows":

Bash

```
echo "La máquina es Linux" | sed 's/Linux/Windows/'
```

**Resultado:** `La máquina es Windows`

---

### Lo más común en tu script:

1. **Borrar una palabra:** `sed 's/palabra//'` (la cambia por "nada").
    
2. **Borrar al inicio de línea:** `sed 's/^ *//'` (quita los espacios molestos del principio).
    
3. **Múltiples cambios:** `sed -e 's/a/b/' -e 's/c/d/'`.
    

**En resumen:** `tr` es para letras sueltas, `sed` es para patrones y palabras.

comando "wget" puedes descargar un archivo de internet

https://wiki.ubuntu.com/ElSalvadorTeam/eventos?action=AttachFile&do=get&target=chuleta1.pdf


comando "pwd" para ver en que ruta estas 
comando "touch" creas archivos 
comando "mkdir" creas directorios


comando "ls" para listar el contenido del directorio actual

usar "ls -l " para listar permisos 

comando "cd " para migrar de directorio, agregandole ".." te puedes ir para atras devolverte en el directorio

enseñar que la raiz del sistema operativo es "/"

https://www.fing.edu.uy/inco/cursos/sistoper/recursosLaboratorio/tutorial0.pdf

https://www.stackscale.com/es/blog/comandos-linux/?gad_source=1&gad_campaignid=23295279072&gbraid=0AAAAADit7zp73sP9qOpE5lJH8nj5_Rdv3&gclid=CjwKCAjw1N7NBhAoEiwAcPchpzcw9ffBNwCRaKK0nbhzXRKAjFxCrZdHsKy-2pkCdMJEVlyuX-BGtxoCZmQQAvD_BwE

concatenar comandos con ";" por ejemplo: whoami; ls

concatenar comandos con "&&"  por ejemplo whoami && ls, la unica diferencia que hay es que el segundo comando se ejecutara si el primer comando devuelve un codigo de estado exitoso 

como ver el codigo de estado "echo $?", un codigo de estado exitoso es cero si no fuera exitoso diera cualquier otro numero

concatenar con "||"por ejemplo whoami || ls, la diferencias que si el primer comando esta erroneo te va a ejecutar el segundo comando


comando que sirve para enviar errores al : 2>/dev/null, el /dev/null es como un agujero negro, todo lo que metamos ahi hacemos que se desaparezca, osea hace que ignores los errores.

enseñar que es "nano"


# Lectura e interpretación de permisos [1-2]


crear un archivo nano para enseñar lo de los permisos
para ver los permisos que tiene un archivo se usa el comando "ls -l"

los que tienen "R" significa que tienen permisos de lectura
los que tiene la "W" significa que tienen permisos de escritura
los que tienen la "X" significa que tienen permisos de ejecuciòn

https://www.profesionalreview.com/2017/01/28/permisos-basicos-linux-ubuntu-chmod/

poner el ejemplo viendo los permisos de /etc/passwd (ejecutar el comando ls -l /etc/passwd) ahi se puede ver que el usuario es root y grupos es el mismo (root) y si yo hago un whoami yo soy kali osea soy "otros"

con el comando "chmod" puedo cambiar los permisos de un directorio o archivos. Ejemplos:
chmod u+r (nombre del directorio o archivo) (la u significa users osea de propietario, y la r de lectura)
en fin para cambiar los permisos del propietario le pongo una "u" + el permiso que les voy agregar(chmod u+x)
para agregarlos a los grupos seria la letra "g"(chmod g+x)
y para los otros seria la letra "o" (chmod o+x)

Y para cambiar de grupo en los permisos se usa el comando "chgrp" mas el grupo al que vas a cambiar mas el nombre del archivo o directorio. Ejemplo:
(chgrp kali prueba.txt)

para cambiar el propietario de un directorio se usa el comando "chown"

comando "useradd" el comando **`useradd`** es la herramienta que usas para **crear un nuevo miembro** en el sistema.

Si tú eres el administrador de la computadora, `useradd` es como el formulario de inscripción para que alguien nuevo tenga su propia cuenta, su propia carpeta y sus propios permisos

agregandole el parametro "-s" le puedes indicar el tipo de shell y despues de eso le agregas una la shell que quieras por ejemplo "/bin/bash"

y al agregarle el parametro "-d" el parámetro `-d` es el que usas para elegir **en qué dirección exacta** va a vivir esa persona.

Por defecto, cuando creas un usuario en Linux, el sistema le construye su habitación en `/home/nombre_del_usuario`. Pero con `-d`, tú mandas y decides dónde ponerla.

para asignarle una contraseña a un usuario lo puedes hacer con el comando "passwd" seguido del nombre del directorio ¿

NOTACIÓN OCTAL DE PERMISOS

r= 4  
w= 2  
x= 1  
  
Si quiero agregar todos los permisos por ejemplo, simplemente los sumo que seria 7, el permiso que quiera quitar, simplemente le quito su numero por ejemplo el de escritura (w) simplemente sumo 4 (de r) y 1 (de x). Considera que es una mejor manera de cambiar los permisos por octal.

https://jesusmarin.dev/blog/entendiendo-la-notacion-octal-de-los-permisos-del-sistema-en-linux/


permisos especiales Sticky bit


## 1. ¿Qué es el Sticky Bit?

Es un permiso especial para **carpetas compartidas**.

- **El problema:** Si una carpeta tiene permiso de escritura para un grupo, cualquiera en ese grupo puede borrar archivos de los demás.
    
- **La solución:** El Sticky Bit hace que **solo el dueño** del archivo (o el administrador) pueda borrarlo o renombrarlo.
    

---

## 2. ¿Cómo se ve en la terminal?

Lo reconocerás por una **`t`** (minúscula) al final de la cadena de permisos cuando haces `ls -ld`:

> `drwxrwxrwt` <-- Esa **t** es el vigilante.

---

## 3. Los Comandos Clave

### A. Para activar el Sticky Bit

Tienes dos formas de hacerlo sobre una carpeta:

- **Modo Letras (más fácil):**
    
    Bash
    
    ```
    chmod +t nombre_carpeta
    ```
    
- **Modo Números (Octal):** Se le añade un **1** al principio de los permisos normales (777 es control total para todos).
    
    Bash
    
    ```
    chmod 1777 nombre_carpeta
    ```
    

### B. Para quitar el Sticky Bit

Si ya no quieres esa restricción y prefieres que todos puedan borrar todo:

Bash

```
chmod -t nombre_carpeta
```

### C. Para verificar si funcionó

Bash

```
ls -ld nombre_carpeta
```

---

## 4. Ejemplo  (Paso a paso)

1. **Creas la carpeta:** `mkdir compartida`
    
2. **Das permisos totales:** `chmod 777 compartida` (Aquí cualquiera puede borrar lo que sea).
    
3. **Pones el vigilante:** `chmod +t compartida` (Ahora tus amigos pueden meter archivos, pero **no pueden borrar los tuyos**).
    

---

### Resumen en una frase:

> "Todos pueden entrar y escribir, pero cada quien solo puede borrar **su propia basura**".


trucos:si quereis hacer más rápido lo del sticky bit. Si añadís los permisos con notación octal y le añadís un 1 justo enfrente de la notación, funciona igual  
Ej: en lugar de poner 777, poneis 1777.


# Control de atributos de ficheros en Linux - Chattr y Lsattr


El comando `+i` no es un permiso estándar de Linux (como los que se cambian con `chmod`), sino un **atributo de sistema de archivos**. Se gestiona con una herramienta diferente llamada `chattr` (change attributes).

La **i** viene de **Inmutable**. Cuando le pones este atributo a un archivo, se convierte en una "caja fuerte" que nadie, ni siquiera el usuario **root** (administrador), puede modificar, borrar o renombrar hasta que se le quite el atributo.

---

### 1. ¿Para qué sirve?

Imagina que tienes un archivo de configuración crítico o una tarea de la **UNESR** que ya terminaste y no quieres que nadie (ni tú mismo por error) borre.

Al hacerlo inmutable:

- No se puede borrar (`rm`).
    
- No se puede renombrar (`mv`).
    
- No se puede escribir en él o modificar su contenido.
    
- No se puede crear un enlace (link) hacia él.
    

---

### 2. Cómo usarlo (Sintaxis)

Como es un atributo de sistema, necesitas usar `sudo` (permisos de superusuario):

- **Para proteger un archivo:**
    
    `sudo chattr +i nombre_archivo.txt`
    
- **Para quitar la protección (cuando necesites editarlo):**
    
    `sudo chattr -i nombre_archivo.txt`
    
- **Para ver si un archivo tiene este atributo:**
    
    El comando `ls -l` **no lo muestra**. Debes usar:
    
    `lsattr nombre_archivo.txt`
    

---

### 3. Diferencia clave: `chmod` vs `chattr`

Es muy común confundirlos, pero funcionan en niveles diferentes:

|**Característica**|**chmod 444 (Solo lectura)**|**chattr +i (Inmutable)**|
|---|---|---|
|**¿Quién lo puede saltar?**|El dueño o Root (fácilmente)|**Nadie** (primero hay que hacer `-i`)|
|**¿Se puede borrar?**|Sí, si tienes permiso en la carpeta|**No**, bajo ninguna circunstancia|
|**Uso principal**|Gestión de permisos diaria|Seguridad extrema / Evitar accidentes|

---

### 4. Un caso de uso real

Si estás practicando **hacking ético** o configurando un servidor, a veces se le pone el atributo `+i` al archivo `/etc/resolv.conf` para evitar que el sistema o algún programa cambie automáticamente tus servidores DNS.

**Un pequeño ejercicio para ti:**

Si intentas borrar un archivo y la terminal te dice: _"Operation not permitted"_, incluso usando `sudo rm -f`, ¿qué comando usarías para verificar si tiene el atributo de inmutabilidad?

¿Te gustaría que te enseñe otros atributos interesantes, como el de "solo añadir" (`+a`), que sirve para que un archivo de log crezca pero no se pueda borrar lo anterior?



El comando `which` es una herramienta pequeña pero fundamental en sistemas tipo Unix (como Linux o macOS). Su función principal es **localizar la ruta completa del archivo ejecutable** que se está utilizando cuando escribes un comando en la terminal.

Aquí tienes los detalles de cómo funciona y para qué te sirve:

### 1. ¿Cómo funciona?

Cuando escribes un comando (por ejemplo, `python3`), el sistema no sabe mágicamente dónde está ese programa. Lo busca en una lista de carpetas llamada **PATH**. El comando `which` hace exactamente ese recorrido por ti y te dice en qué carpeta encontró el archivo.

### 2. Casos de uso comunes

- **Saber qué versión estás usando:** Si tienes varias versiones de un programa instaladas, `which` te dirá cuál tiene prioridad.
    
    - _Ejemplo:_ `which python` podría devolver `/usr/bin/python` o `/home/usuario/anaconda/bin/python`.
        
- **Verificar si un programa está instalado:** Si `which` no devuelve nada, significa que el ejecutable no está en tu PATH (o no está instalado).
    
- **Para scripts de automatización:** Se usa mucho dentro de scripts para asegurarse de que una herramienta existe antes de intentar usarla.
    

---

### Ejemplo práctico

Si ejecutas: `which ls`

La respuesta típica será: `/usr/bin/ls`



Comando Find 

Si `which` es un bisturí para encontrar ejecutables, el comando **`find`** es una navaja suiza (y un detector de metales) para buscar **cualquier cosa** en todo tu sistema de archivos.

A diferencia de otros comandos, `find` no busca en una base de datos indexada, sino que recorre las carpetas en tiempo real basándose en los criterios que tú le des.

### 1. Estructura básica

La sintaxis de `find` sigue este orden lógico: `find [dónde buscar] [criterio de búsqueda] [qué hacer con el resultado]`

### 2. ¿Para qué se usa normalmente?

Estas son las búsquedas más comunes que puedes hacer:

- **Por nombre:** Buscar un archivo específico (ignora mayúsculas con `-iname`).
    
    - `find /home/usuario -name "documento.pdf"`
        
- **Por tipo:** Buscar solo directorios (`d`) o solo archivos (`f`).
    
    - `find . -type d` (busca todas las carpetas en el directorio actual).
        
- **Por tamaño:** Encontrar archivos que ocupan mucho espacio.
    
    - `find /var/log -size +50M` (archivos mayores a 50 megabytes).
        
- **Por tiempo:** Buscar archivos modificados recientemente.
    
    - `find . -mtime -2` (archivos modificados en las últimas 48 horas).
        
- **Por permisos:** Buscar archivos que tengan permisos específicos (como el 777 que mencionaste antes).
    
    - `find /usr/bin -perm 755`

en resumen Mientras que `which` es un especialista con una única misión, `find` es un explorador todo terreno. Aquí te detallo las diferencias clave para que no las olvides, la diferencia es la flexibilidad find puede buscar por tamaño, por tiempo y por otras cosas y Which no.


el parámetro **`-perm`** es el que usas cuando quieres buscar archivos basándote en sus **permisos de seguridad**.

Esto es fundamental en **Kali Linux**, porque te permite encontrar archivos que podrían ser un riesgo (como los que tienen demasiados permisos).

### 1. ¿Cómo funciona?

La estructura básica es: `find [ruta] -type f -perm [modo]`

### 2. Formas de usar el número de permiso

Hay tres formas principales de pedirle los permisos a `find`:

#### A. Permiso Exacto (Sin signos)

Busca archivos que tengan **exactamente** esos permisos, ni más ni menos.

- **Ejemplo:** `find . -type f -perm 644`
    
- **Qué hace:** Busca archivos donde el dueño lee/escribe, y el resto solo lee.
    

#### B. Con el signo menos (`-`)

Busca archivos que tengan **al menos** esos permisos. Es decir, si el archivo tiene más permisos de los que pides, también te lo muestra.

- **Ejemplo:** `find / -type f -perm -4000`
    
- **Para qué sirve en Kali:** Se usa muchísimo para buscar archivos con el bit **SUID** (archivos que se ejecutan con privilegios de root), algo clave en auditorías de seguridad.
    

#### C. Con la barra (`/`) o el signo más (`+`)

Busca archivos donde **cualquiera** de los permisos coincida (dueño, grupo o otros).

- **Ejemplo:** `find . -type f -perm /222`
    
- **Qué hace:** Busca cualquier archivo que sea "escribible" por alguien (dueño, grupo o el resto del mundo).



el id de root es (0)


# Estructura de directorios del sistema

A modo de sumario, te dejamos por aquí unos apuntes con la descripción de cada ruta del sistema:

### Directorio Raíz

El directorio raíz, simbolizado por el símbolo (/), es el **directorio principal a partir del cual se ramifican todo el resto de directorios**.

### Directorio /bin

El directorio /bin es un **directorio estático y compartible en el que se almacenan archivos binarios/ejecutables necesarios para el funcionamiento del sistema**. Estos archivos binarios los pueden usar la totalidad de usuarios del sistema operativo.

### Directorio /boot

Es un directorio estático no compartible que **contiene la totalidad de archivos necesarios para el arranque del ordenador excepto los archivos de configuración**. Algunos de los archivos indispensables para el arranque del sistema que acostumbra a almacenar el directorio /boot son el kernel y el gestor de arranque Grub.

### Directorio /dev

El sistema operativo Gnu-Linux trata los dispositivos de hardware como si fueran un archivo. **Estos archivos que representan nuestros dispositivos de hardware se hallan almacenados en el directorio /dev**.

Algunos de los archivos básicos que podemos encontrar en este directorio son:

- **cdrom** que representa nuestro dispositivo de CDROM.
- **sda** que representa nuestro disco duro sata.
- **audio** que representa nuestra tarjeta de sonido.
- **psaux** que representa el puerto PS/2.
- **lpx** que representa nuestra impresora.
- **fd0** que representa nuestra disquetera.

### Directorio /etc

El directorio /etc es un **directorio estático que contiene los archivos de configuración del sistema operativo**. Este directorio también contiene archivos de configuración para controlar el funcionamiento de diversos programas.

Algunos de los archivos de configuración de la carpeta /etc pueden ser sustituidos o complementados por archivos de configuración ubicados en nuestra carpeta personal /home.

### Directorio /home

El directorio /home se trata de un **directorio variable y compartible**. Este directorio está **destinado a alojar la totalidad de archivos personales de los distintos usuarios del sistema operativo a excepción del usuario root**. Algunos de los archivos personales almacenados en la carpeta /home son fotografías, documentos de ofimática, vídeos, etc.

### Directorio /lib

El directorio /lib es un **directorio estático y que puede ser compartible**. Este directorio **contiene bibliotecas compartidas que son necesarias para arrancar los ejecutables que se almacenan en los directorios /bin y /sbin**.

### Directorio /mnt

El directorio /mnt **tiene la finalidad de albergar los puntos de montaje de los distintos dispositivos de almacenamiento** como por ejemplo discos duros externos, particiones de unidades externas, etc.

### Directorio /media

La función del directorio /media es similar a la del directorio /mnt. Este directorio **contiene los puntos de montaje de los medios extraíbles de almacenamiento** como por ejemplo memorias USB, lectores de CD-ROM, unidades de disquete, etc.

### Directorio /opt

El contenido almacenado en el directorio /opt **es estático y compartible**. **La función de este directorio es almacenar programas que no vienen con nuestro sistema operativo** como por ejemplo Spotify, Google-earth, Google Chrome, Teamviewer, etc.

### Directorio /proc

El directorio /proc **se trata de un sistema de archivos virtual**. Este sistema de archivos virtual **nos proporciona información acerca de los distintos procesos y aplicaciones que se están ejecutando en nuestro sistema operativo**.

### Directorio /root

El directorio /root se trata de un **directorio variable no compartible**. El directorio /root **es el directorio /home del administrador del sistema** (usuario root).

### Directorio /sbin

El directorio /sbin se trata de un **directorio estático y compartible**. Su función es similar al directorio /bin, pero a diferencia del directorio /bin, el directorio /sbin **almacena archivos binarios/ejecutables que solo puede ejecutar el usuario root** o administrador del sistema.

### Directorio /srv

El directorio /srv se usa **para almacenar directorios y datos que usan ciertos servidores que podamos tener instalados en nuestro ordenador**.

### Directorio /tmp

El directorio /tmp es **donde se crean y se almacenan los archivos temporales y las variables para que los programas puedan funcionar de forma adecuada**.

### Directorio /usr

El directorio /usr es un **directorio compartido y estático**. Este directorio es el que **contiene la gran mayoría de programas instalados** en nuestro sistema operativo.

Todo el contenido almacenado en la carpeta /usr es accesible para todos los usuarios y **su contenido es solo de lectura**.

### Directorio /var

El directorio /var **contiene archivos de datos variables y temporales como por ejemplo los registros del sistema (logs), los registros de programas que tenemos instalados en el sistema operativo, archivos spool, etc.**

**La principal función del directorio /var es la detectar problemas y solucionarlos**. Se recomienda ubicar el directorio /var en una partición propia, y en caso de no ser posible es recomendable ubicarlo fuera de la partición raíz.

### Directorio /sys

Directorio que **contiene información similar a la del directorio /proc**. Dentro de esta carpeta podemos encontrar **i****nformación estructurada y jerárquica acerca del kernel de nuestro equipo, de nuestras particiones y sistemas de archivo, de nuestros drivers**, etc.

### Directorio /lost-found

Directorio que se crea en las particiones de disco con un sistema de archivos ext después ejecutar herramientas para restaurar y recuperar el sistema operativo como por ejemplo fsch.

Si nuestro sistema no ha presentado problemas este directorio estará completamente vacío. En el caso que hayan habido problemas **este directorio contendrá ficheros y directorios que han sido recuperados tras la caída del sistema operativo**.



el ls -la la "a" te hace encontrar archivos o directorios ocultos
estan ocultos por que en el nombre llevan un punto al principio si tu te creas un directorio y le pones un punto al principio ese directorio va a quedar oculto


para ver mi direccion ip se usa el comando "hostname -I", o tambien puedes hacer un ifconfig pero ahi vas a listar las intefaces de red


El comando `awk` es como un **robot que solo sabe leer por columnas**.

### 1. ¿Qué significa cada parte?

- **`awk`**: Es el nombre del robot. Él agarra un texto y lo pica en pedazos (columnas).
    
- **`' '`**: Las comillas simples son como una "cajita". Todo lo que esté adentro es la **orden** que le vas a dar al robot.
    
- **`{ }`**: Las llaves significan: "Adentro de esto está la **acción** que quiero que hagas".
    
- **`print`**: Es la orden de "Muéstrame esto en la pantalla" (el **output** que hablamos antes).
    
- **`$1`**: Esta es la clave. El signo **$** seguido de un número le dice al robot **qué columna** quieres ver.
    
    - `$1` = La primera columna.
        
    - `$2` = La segunda columna.
        
    - `$0` = ¡Toda la línea completa!
        

---

### 2. ¿Cómo funciona en la vida real?

Si tú tienes un archivo de texto o un resultado de un comando y le lanzas el `awk '{print $1}'`, el robot va a pasar línea por línea, va a ignorar todo lo demás y **solo te va a mostrar lo que esté al principio (la primera palabra)**.

**Ejemplo con lo que tú haces en Kali:** Si haces un `ls -l` (que te da mucha información como permisos, dueño, tamaño, fecha), y solo quieres ver los **permisos** (que es lo primero que sale a la izquierda), pondrías:

`ls -l | awk '{print $1}'`

**Resultado:** El robot "se come" el tamaño, el nombre y la fecha, y solo te vomita en la pantalla la lista de permisos.

---

### 3. En resumen (Para el burro):

- `awk` = El carnicero.
    
- `$1` = El primer tajo de carne.
    
- `print` = Ponlo en el mostrador.



Para que funcione, tienes que meter el comando completo dentro de la sustitución `$( )`. Aquí te dejo cómo se escribe exactamente:

### El Comando Maestro:

Bash

```
echo "Tu ip privada es: $(hostname -I | awk '{print $1}')"
```

---

### Explicación "para el burro" (paso a paso):

1. **`hostname -I`**: Este comando suelta todas tus IPs (a veces salen varias si usas Wi-Fi y cable).
    
2. **`|` (El Tubo/Pipe)**: Agarra ese montón de IPs y se las pasa por un tubo directamente al robot `awk`.
    
3. **`awk '{print $1}'`**: El robot recibe el montón de texto, corta la **primera columna** (tu IP principal) y tira el resto a la basura.
    
4. **`$( ... )` (La Bolsa Mágica)**: Todo lo anterior pasa adentro de la bolsa. El resultado final (solo tu IP, por ejemplo `192.168.1.15`) es lo que sale de la bolsa.
    
5. **`echo`**: Finalmente, el comando `echo` imprime tu frase bonita junto con el número que salió de la bolsa.
    

---

### ¿Cómo escribirlo con tu teclado configurado?

Aquí es donde brilla tu nueva configuración de **Kali Linux**:

- **Para abrir el paréntesis:** Usa el **Shift + 8** (o como lo tengas por defecto).
    
- **Para el `|` (tubo):** Suele ser la tecla a la izquierda del 1 o con `Alt Gr + 1`.
    
- **Para las llaves `{ }`:** Usa tu **Alt Gr + 7** para abrir y la que encontraste para cerrar (o la que mapeamos en el **0**).
    
- **Para cerrar el paréntesis `)`:** ¡Usa tu nueva combinación **Shift + 9**!

en Resumen para devolver el ouput de un comando en la terminal tienes que poner un signo de dolar y poner unos parentesis ejemplo:echo "Tu ip privada es: $(hostname -I | awk '{print $1}')"


utlidades del comando "find " para cuando quieres buscar un archivo pero no te recuerdas de su nombre completo: find / -name \*exdump\* 2>/dev/null 


comando "tail":El comando `tail` (que significa "cola" en inglés) es el gemelo opuesto de `head`. Su función es mostrar la **parte final** de un archivo de texto.

Es la herramienta favorita de cualquier administrador de sistemas o entusiasta de la ciberseguridad porque permite ver lo más reciente que ha ocurrido en un sistema (como los registros de ataques o errores).

Aquí tienes el resumen "para el burro":

---

### 1. La estructura básica

`tail [OPCIONES] [ARCHIVO]`

- **Por defecto:** Si escribes `tail archivo.txt`, te mostrará las **últimas 10 líneas**.
    

---

### 2. Las opciones que más vas a usar

#### A. Ver un número específico de líneas (`-n`)

Si solo quieres ver las últimas 3 líneas de tus apuntes de la **UNEFA**: `tail -n 3 notas.txt`

#### B. El "Modo Espía" o Tiempo Real (`-f`)

Esta es la opción más importante. `f` viene de _follow_ (seguir). Sirve para dejar la terminal abierta y ver cómo se escribe el archivo en vivo. `tail -f /var/log/syslog` _(Muy útil para ver si alguien intenta entrar a tu Kali mientras haces prácticas de hacking)._

#### C. Empezar desde una línea específica (`+`)

Si quieres ver todo el archivo a partir de la línea 20 en adelante: `tail -n +20 archivo.txt`

---

### 3. ¿Para qué te sirve a ti en Kali?

Como estás con el curso de **S4vitar** y actualizando paquetes, `tail` es útil para:

- **Revisar errores de instalación:** Si un proceso falla, puedes ver el final del log para entender por qué.
    
- **Auditoría de red:** Ver quién se conecta a tu máquina en tiempo real.
    
- **Ver tus funciones:** Si quieres ver las últimas líneas de tu `.zshrc` para confirmar tus cambios del teclado: `tail -n 15 ~/.zshrc`
    

---

### 4. Combinación Pro (El Tubo `|`)

Puedes combinarlo con otros comandos. Por ejemplo, para ver solo las últimas 5 IPs que encontraste con tu función `vermiip` (si la guardaras en un archivo): `cat historial_ips.txt | tail -n 5`

---

### Resumen para el "burro":

- **`tail`**: Mira el final.
    
- **`-n`**: ¿Cuántas líneas?
    
- **`-f`**: No te cierres, quédate mirando (en vivo).
    

**Un detalle de tu teclado:** Si vas a usar el símbolo `+` para la opción `-n +20`, recuerda que en la mayoría de los teclados está cerca del Enter. Y si necesitas el `|` (la tubería), suele estar en la tecla a la izquierda del 1 o con **Alt Gr + 1**.



uso de nvim
para poder escribir en el editor de presiona la letra "i" de insert 

para cerrar y guardar lo que escribiste en el editor se presiona la tecla esc y se ponen ":"
y wq



comando sort hace un ordenamiento alfabetico ejemplo: sort data.txt

comando "uniq -u" sirve para listar lineas unicas 




# Interpretación de archivos binarios

comando "strings":Su función principal es **extraer y mostrar las secuencias de caracteres imprimibles** (texto legible) que están escondidas dentro de un archivo binario, como un ejecutable, una imagen, una base de datos o un volcado de memoria.




Codificacion y decodificacion en base 64

El comando `base64` es esencial en Linux para codificar y decodificar datos binarios en formato de texto. Esto es especialmente útil en ciberseguridad cuando quieres transmitir archivos, scripts o "payloads" sin que se corrompan por protocolos que solo aceptan texto.

Aquí tienes todos los parámetros (flags) estándar que utiliza este comando:

### Parámetros Principales

- **`-d` o `--decode`**: Es el parámetro más usado. Sirve para convertir una cadena en Base64 de vuelta a su formato original (binario o texto plano).
    
    - _Ejemplo:_ `echo "SGVsbG8=" | base64 -d`
        
- **`-w` o `--wrap=COLS`**: Por defecto, `base64` corta las líneas a los 76 caracteres. Con este parámetro puedes cambiar ese límite o eliminarlo.
    
    - `base64 -w 0`: Desactiva el salto de línea (escribe todo en una sola línea continua). Muy útil para copiar y pegar tokens largos.
        
    - `base64 -w 10`: Salta de línea cada 10 caracteres.
        
- **`-i` o `--ignore-garbage`**: Cuando estás decodificando, este parámetro le dice al comando que ignore cualquier carácter que no sea parte del alfabeto Base64 (como espacios o saltos de línea extraños).


# Cifrado césar y uso de tr para la traducción de caracteres



para decifrar un codigo que tenga rotacion hay una pagina que se llama "rot13"




como descomprimir archivos 
para archivos .gz se usa el comando gunzip o 7z que es mucho mas comodo y usas el parametro x vas a poder descomprimir cualquier tipo de archivo ya sea gz ,tar etc, y con el parametro L pero miniscula puedo ver lo que hay dentro del comprimido como una vista previa 




cuando veo que hay un puerto abierto  y quiero ver que servicio esta corriendocon el comando lsof  -i(el puerto que esta abierto )



comando diff

El comando diff (short for difference) es una herramienta fundamental en la terminal de Linux que se utiliza para comparar dos archivos línea por línea y mostrar las diferencias entre ellos. Es el "abuelo" de lo que hoy conocemos como las comparaciones de código en GitHub o VS Code.

Aquí tienes el resumen de cómo funciona y cómo leerlo:

1. Funcionamiento Básico
Cuando ejecutas diff archivo1 archivo2, el comando te dirá qué cambios tendrías que hacer en el archivo1 para que sea idéntico al archivo2.

Bash
diff archivo1.txt archivo2.txt
2. Cómo leer la salida (Los símbolos)
La salida de diff puede parecer confusa al principio, pero sigue una lógica simple:

< (Menor que): Indica una línea que está en el primer archivo pero NO en el segundo (línea eliminada).

> (Mayor que): Indica una línea que está en el segundo archivo pero NO en el primero (línea añadida).

Letras de cambio:

a (add): Añadir.

c (change): Cambiar.

d (delete): Borrar.

Números: Indican el número de línea afectado (ej. 5c5 significa "la línea 5 del archivo 1 debe cambiar por la línea 5 del archivo 2").

3. Formatos más usados
El formato estándar es un poco difícil de leer. Por eso, casi todo el mundo usa estos parámetros:

Formato Unificado (-u): Es el estándar en programación (el que usa git diff). Muestra el contexto y usa + o -.

Bash
diff -u archivo1 archivo2
Formato en Columnas (-y): Muestra los dos archivos lado a lado. Es mucho más visual para humanos.

Bash
diff -y archivo1 archivo2
Ignorar espacios (-w): Muy útil si solo quieres ver cambios en el texto y no te importa si alguien puso un espacio de más o un tabulador.

4. ¿Para qué se usa en Ciberseguridad/Bandit?
En niveles avanzados de Bandit o en auditorías reales, diff es vital para:

Comparar archivos de configuración: Ver qué cambió un atacante en el sistema.

Analizar logs: Comparar un log limpio contra uno sospechoso.

Encontrar la flag: A veces te dan dos archivos enormes que parecen iguales, pero al hacer diff, la única línea distinta es la contraseña que buscas.

Dato Pro: Existe un comando llamado sdiff que es básicamente diff -y por defecto, ideal para comparar archivos rápidamente de forma visual.


netcat 
para ponerme en escucha por un puerto por netcat se usa el comando 

nc -nlvp (y el puerto por el cual quiero escuchar)

nlvp: la letra "n" es para que no te aplique resolucion dns, la letra "v" es de verbose, la letra "p" de puerto, y la letra "L" es listen mode 


tareas cron 

as **tareas cron** son uno de los pilares de la automatización en sistemas operativos tipo Unix (como Linux y macOS). En términos sencillos, es un **programador de tareas** que ejecuta comandos o scripts de forma automática en intervalos de tiempo específicos.

Aquí tienes un resumen de cómo funcionan y para qué sirven:

---

## 1. ¿Cómo funciona?

El sistema utiliza un "demonio" (un proceso que corre permanentemente en segundo plano) llamado **crond**. Este proceso revisa cada minuto unos archivos de configuración llamados **crontabs** (cron tables) para ver si hay alguna tarea programada para ese momento exacto.

## 2. La estructura del Crontab

Para programar una tarea, se utiliza una línea con cinco asteriscos seguidos del comando. Cada asterisco representa una unidad de tiempo:

$$* * * * * \text{ comando_a_ejecutar}$$

| **Campo**            | **Descripción**            | **Valores posibles** |
| -------------------- | -------------------------- | -------------------- |
| **Minuto**           | Momento exacto del minuto  | 0 - 59               |
| **Hora**             | Hora del día (formato 24h) | 0 - 23               |
| **Día**              | Día del mes                | 1 - 31               |
| **Mes**              | Mes del año                | 1 - 12               |
| **Día de la semana** | Día específico             | 0 - 6 (0 es domingo) |


**Ejemplos Comunes de Cron Jobs**

- **Cada 15 minutos:** `*/15 * * * * /ruta/al/script.sh`
- **A las 5:00 a.m. todos los días:** `0 5 * * * /ruta/al/script.sh`
- **De lunes a viernes a las 22:00 horas:** `0 22 * * 1-5 /ruta/al/script.sh`
- **El día 1 de cada mes a medianoche:** `0 0 1 * * /ruta/al/script.sh`
- **Cada domingo a las 11:59 PM:** `59 23 * * 0 /ruta/al/script.sh`
- **Al iniciar el sistema:** `@reboot /ruta/al/script.sh` ![Carrera Linux](data:image/png;base64,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)Carrera Linux +4

**Sintaxis y Comodines**

- `*`: Cualquier valor.
- `,`: Lista de valores (ej. `1,3,5`en día de la semana).
- `-`: Rango de valores (ej. `1-5`para lunes a viernes).
- `/`: Valores intermedios/intervalos (ej. `*/10`cada 10 unidades).

Cron es un administrador de tareas de Linux que permite ejecutar comandos en un momento determinado, por ejemplo, cada minuto, día, semana o mes. Si queremos trabajar con cron, podemos hacerlo a través del comando **crontab**.

El formato de configuración de cron es el siguiente: **Minuto Hora Dia-del-Mes Mes Dia-de-la-Semana Comando-a-Ejecutar**

El intervalo de tiempo se especifica mediante 5 campos que representan, de izquierda a derecha:

- **Minutos**: de 0 a 59.
- **Horas**: de 0 a 23.
- **Día del mes**: de 1 a 31.
- **Mes**: de 1 a 12.
- **Día de la semana**: de 1 a 6 lunes a sábado (1=lunes, 2=martes, etc.) y 0 o 7 el domingo.

Si quisiéramos especificar todos los valores posibles de un parámetro (minutos, horas, etc.) podemos hacer uso del asterisco (*****). Esto implica que si en lugar de un número utilizamos un asterisco, el comando indicado se ejecutará cada minuto, hora, día de mes, mes o día de la semana, como en el siguiente ejemplo:

*** * * * * /home/user/script.sh**

@reboot Ejecuta una vez, al inicio  
@yearly ejecuta sólo una vez al año: 0 0 1 1 *  
@annually igual que @yearly  
@monthly ejecuta una vez al mes, el día primero: 0 0 1 * *  
@weekly Semanal el primer minuto de la primer hora de la semana. 0 0 * * 0″.  
@daily diario, a las 12:00A.M. 0 0 * * *  
@midnight igual que @daily  
@hourly al primer minuto de cada hora: 0 * * * *


Otra funcion del "grep " es el parameto -v, que sirve si por ejemplo quieres quitar alguna palabra de un output que no te interese, ejemplo: grep -v "wrong"
RECORDAR SIEMPRE USAR EL "|" antes de usar "grep"
 y para quitar otra palabra aparte de "wrong" por ejemplo a el parametro "-v"se le agrega una "E" mayuscula

 otra peculiaridad de nc es que si le pasas un diccionario puede hacer ataques de fuerza bruta, ejemplo:cat diccionario.txt | nc localhost "el puerto al que te quieres poner por escucha" 

un ejemplo mas claro esta en la plataforma de over the wire, en bandit en el nivel 25 que te proporcionaba una contraseña pero le tenias que agregar un pin code de 4 digitos lo que se hizo fue crear las combinaciones del 0000..9999 en un archivo txt y pasar el comando deje arriba


Para por ejemplo crear un archivo txt con todas las combinaciones de 4 digitos

### Importancia del comando

La relevancia de `more` radica en la gestión de la legibilidad. Cuando un archivo es demasiado grande para la ventana de la terminal, usar un comando como `cat` simplemente "desbordaría" el texto hasta el final, obligándote a subir manualmente para leer.

- **Prevención de saturación:** Evita que la terminal se llene de texto a una velocidad ilegible.
    
- **Eficiencia de memoria:** A diferencia de algunos editores de texto, `more` no carga necesariamente todo el archivo en la memoria RAM de inmediato, lo que lo hace útil para archivos grandes.
    
- **Compatibilidad:** Es un estándar presente en prácticamente cualquier distribución de Linux y versiones de Windows, lo que lo hace una herramienta universal.
    

---

### Uso y sintaxis básica

La sintaxis general es: `more [opciones] [nombre_del_archivo]`

#### Comandos de navegación frecuentes:

Una vez que estás dentro del visor de `more`, puedes usar las siguientes teclas:

- **Espacio:** Avanza a la siguiente página (pantalla completa).
    
- **Enter:** Avanza una sola línea.
    
- **b:** Retrocede una página (solo disponible en algunos sistemas Linux).
    
- **/**: Permite buscar un término específico dentro del texto.
    
- **q:** Sale del comando y regresa al prompt de la terminal.
    

---

### Ejemplos comunes de aplicación

1. **Lectura de archivos de configuración:** Para revisar archivos del sistema que son extensos: `more /etc/ssh/ssh_config`
    
2. **Uso con tuberías (Pipes):** Es muy común usarlo junto a otros comandos que generan mucha información, como `ls` o `ps`: `ls -l /etc | more` _(Esto permite ver la lista de archivos de un directorio denso paso a paso)._
    
3. **Visualización desde una línea específica:** Si quieres empezar a leer un archivo a partir de la línea 50: `more +50 archivo.txt`



el comando "mktemp -d" sirve para crear directorios temporales 


cuando este usando git con el comando "log" puedes ver los cambios que ah tenido el proyecto

y con el comando "git show mas el commit que tien cada repositorio"

El comando '**git branch**' nos permite crear, enumerar y eliminar ramas, así como cambiar sus nombres. Es importante recalcar que no nos permite cambiar entre ramas o volver a unir un historial bifurcado. Por este motivo, '**git branch**' está estrechamente integrado con los comandos '**git checkout**' y '**git merge**'.

En Git, una etiqueta o **tag** sirve básicamente como una rama firmada que no permuta, es decir, siempre se mantiene inalterable. Sencillamente es una cadena arbitraria que apunta a un Commit específico. Puede decirse que un tag es un nombre que puedes usar para marcar un punto específico en la historia de un repositorio.



En Bash se pueden usar argumentos desde la línea de comandos, los cuales son enviados a los scripts como variables. Estos quedarían representados de la siguiente forma:

**[$0]**: Representa el nombre del script que se invocó desde la terminal.

**[$1]**: Es el primer argumento desde la línea de comandos.

**[$2]**: Es el segundo argumento desde la línea de comandos y así sucesivamente.

**[$#]**: Contiene el número de argumentos que son recibidos desde la línea de comandos.

**[$*]**: Contiene todos los argumentos que son recibidos desde la línea de comandos, guardados t