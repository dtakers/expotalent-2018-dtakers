# ExpoTALENT 2018 - Reto dTakers - #become_dtakers

![XIV Feria de Empleo](http://empzar.unizar.es/files/users/organizador2/BANNER_2018.jpg)

Si te gusta programar, y aprender nuevos lenguajes de programación, entonces este es tu reto. ¡Bienvenido al reto de [dTakers](http://www.dtakers.com) para [ExpoTALENT 2018](http://empzar.unizar.es)!

Una de las preguntas que podrías estar haciéndote (con bastante frecuencia) es si lo que estás aprendiendo tiene
algún tipo de relación con la realidad. Nosotros nos hacemos esa pregunta todos los días ;)

Así que hemos decido aplicar algo de realidad al reto de este año.
Normalmente cuando aprendemos programación siempre se escoge un lenguaje de programación (ADA, Pascal, JAVA, C, ...)
y como estudiantes nos surge la duda de si es el que realmente usan las empresas y si realmente lo usan así.

Este año nos gustaría aprender un nuevo lenguaje y el criterio que hemos escogido es... el preferido por los programadores ;)

Es probable que conozcas [stackoverflow](https://stackoverflow.com/), una comunidad en la que puedes pedir ayuda o ayudar en casi cualquier tecnología.
Todos los años publican una encuesta en la que preguntan a los programadores cual es su lenguaje de programación favorito (entre otras cosas) y
nosotros nos hemos sorprendido al descubrir que no es ninguno de los "de siempre", es [Rust](https://www.rust-lang.org/es-ES/).  

Básicamente vamos a aprender [Rust](https://www.rust-lang.org/es-ES/) juntos.

## ¿En qué consiste el reto?

Dado que estamos aprendiendo vamos a intentar no complicar mucho las cosas (de hecho es probable que ya hayas hecho lo mismo con otros lenguajes de programación).

Consiste en descifrar un mensaje que ha sido cifrado mediante [cifrado por sustitución](https://es.wikipedia.org/wiki/Cifrado_por_sustituci%C3%B3n).

El mensaje a descifrar se encuentra en el fichero [mensaje.txt](https://github.com/dtakers/expotalent-2018-dtakers/blob/master/mensaje.txt) de este repositorio y debería tener un aspecto parecido a:
```
Rime1efozi9
Ñqui1ñq1cd12ñdqeañ1hokwevi9
```

El conjunto de caracteres originales utilizados es:

|Carácter|Nombre|
| ------ | ------ |
| |Espacio|
|,|Coma|
|.|Punto|
|:|Dos puntos|
|;|Punto y coma|
|a|a|
|b|b|
|c|c|
|d|d|
|e|e|
|f|f|
|g|g|
|h|h|
|i|i|
|j|j|
|k|k|
|l|l|
|m|m|
|n|n|
|ñ|ñ|
|o|o|
|p|p|
|q|q|
|r|r|
|s|s|
|t|t|
|u|u|
|v|v|
|w|w|
|x|x|
|y|y|
|z|z|

Es decir el texto original solo incluye esos caracteres, y por ejemplo no incluye @ ni &.

El texto cifrado también utiliza el mismo conjunto de caracteres, es decir en el [mensaje.txt](https://github.com/dtakers/expotalent-2018-dtakers/blob/master/mensaje.txt) no deberían aparecer caracteres como @ ni & (por ejemplo).

Además la modalidad de cifrado ha sido sustitución simple: una letra se ha cambiado por otra. Por ejemplo en el texto original la h se ha cambiado por r.

Así que en resumen, a la vez que aprendemos [Rust](https://www.rust-lang.org/es-ES/) debemos desarrollar un programa que:
- Lea el fichero [mensaje.txt](https://github.com/dtakers/expotalent-2018-dtakers/blob/master/mensaje.txt)
- Descifre el contenido del fichero y lo muestre por pantalla

El mensaje contiene las instrucciones para continuar con el reto :)
 
## ¿Necesitas más ayuda?

Si necesitas más ayuda puedes continuar leyendo :) En caso contrario ya habrás terminado el programa ;P

Nos ha pasado a todos, hemos leído un enunciado de un problema, o alguien nos ha contado un problema y no hemos entendido por donde empezar.

Puedes estudiar (¿alguien ha dicho discreta y/o algebra?), también puedes volver a leer mil veces el reto, preguntar varias personas, buscar en internet, o aprender mucho [Rust](https://www.rust-lang.org/es-ES/)
pero al final puede ocurrir que todavía no entiendas nada. No te preocupes, vamos a intentar ayudarte.

Por un momento imagina que tu paga semanal o tu sueldo, o si puedes salir los próximos 54 fines de semana, dependen de lo que hay escrito en el mensaje. Un poquito de motivación no viene mal ;)

Al margen de bromas, una de las primeras cosas que se te pueden ocurrir es ir probando cambios de letras hasta que el mensaje tenga algo de sentido. Es lo que se conoce como [ataque de fuerza bruta](https://es.wikipedia.org/wiki/Ataque_de_fuerza_bruta).
Es bastante entretenido y si has perdido la llave de un candado alguna vez, entonces sabrás de lo que hablamos (si el candado es de combinación y no tiene más de 3 dígitos).
Nosotros no hemos estudiado muchas matemáticas pero gente que ha estudiado dice que dependiendo del número de caracteres y la longitud del mensaje podría llevar bastante tiempo.

Podemos darle vueltas al problema, pero vamos a intentar aplicar un método (aunque podría hacerse de otra manera ;) ).
Nosotros vamos a intentar utilizar el [análisis de frecuencias](https://es.wikipedia.org/wiki/An%C3%A1lisis_de_frecuencias).

Dicho de otra forma (por favor que nos perdonen los que han estudiado), imagina por momento que el texto original solo incluye las letras a y b (bastante aburrido, si).
Imagina que además sabemos que 20 caracteres y que el 75% son a y el 25% restante son b. Dado un texto cifrado como el siguiente:
```
siii
``` 
Mirándolo con atención vemos que la letra i aparece un 75% de veces y la letra s aparece un 25% de veces. Por lo que, podemos deducir (en tiempo decían por [regla de tres](https://es.wikipedia.org/wiki/Regla_de_tres)) que
la letra original "a" se ha cambiado por la letra cifrada "i" y que la letra original "b" se ha cambiado por la letra cifrada "s".
Por tanto el mensaje original es:
```
baaa
``` 
Pregunta del millón ¿cómo sabemos las frecuencias? A priori no podemos y tenemos que dar por supuesto algunas cosas para intentar resolver el problema:

- Suponemos que el mensaje original está en idioma español
- Suponemos que el mensaje original tiene una longitud "relevante" (suficiente para que tenga sentido utilizar el [análisis de frecuencias](https://es.wikipedia.org/wiki/An%C3%A1lisis_de_frecuencias))
- Suponemos que existe una tabla de [análisis de frecuencias](https://es.wikipedia.org/wiki/An%C3%A1lisis_de_frecuencias) para los caracteres del alfabeto español y que esta tabla es fiable (se puede aplicar a cualquier texto y no hay mucha diferencia en porcentajes)

Así que, el trabajo que tienes que hacer es:
- Aprender [Rust](https://www.rust-lang.org/es-ES/). Puedes descargar un PDF de [El libro de Rust](https://www.gitbook.com/book/goyox86/el-libro-de-rust)
- Encontrar una tabla de [análisis de frecuencias](https://es.wikipedia.org/wiki/An%C3%A1lisis_de_frecuencias) para idioma español que incluya los caracteres que hemos indicado en la tabla
- Programar "algo" que cuente las veces (y/o calcule el porcentaje) que aparece cada caracter en [mensaje.txt](mensaje.txt)
- Programar "algo" que itente aproximar el número de veces (porcentaje) de cada letra cifrada a un porcentaje similar de cada letra en la tabla [análisis de frecuencias](https://es.wikipedia.org/wiki/An%C3%A1lisis_de_frecuencias) que hayas encontrado
- Descifrar el mensaje :)

## ¿Qué pasa si no lo consigo?

No pasa nada. Nosotros ni siquiera lo hemos programado todavía, y es probable que tardemos un tiempo. Es bastante normal :)

Lo importante es aprender algo.

Haremos una demostración en nuestro stand, en la que intentaremos resolver el reto ;) 

¡¡Te animamos a que acudas a nuestro stand a mostrarnos tu resultado, los 10 primeros en venir, se llevarán una sorpresa dTakers!! 

## Contacto en caso de más dudas

Puedes contactar con dTakers vía [email](mailto:ricardo.barcelona@dtakers.com) indicando en el asunto "ExpoTALENT 2018" o
en el teléfono +34 876 535408

Síguenos en nuestras redes sociales y cuéntanos cómo te está resultando el reto a través de #become_dtakers

- [LinkedIn](http://bit.ly/2Eey2d9)
- [Twitter](http://bit.ly/2EcA9Ow)
- [Facebook](http://bit.ly/2EaKLgS)

## Licencia
<a rel="license" href="http://creativecommons.org/licenses/by/4.0/">
	<img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" />
</a><br />
<span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">ExpoTALENT 2018 - Reto dTakers</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="http://www.dtakers.com" property="cc:attributionName" rel="cc:attributionURL">Digital Takers S.L.</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International License</a>.<br />
Based on a work at <a xmlns:dct="http://purl.org/dc/terms/" href="http://github.com/dtakers/expotalent-2018-dtakers" rel="dct:source">http://github.com/dtakers/expotalent-2018-dtakers</a>.