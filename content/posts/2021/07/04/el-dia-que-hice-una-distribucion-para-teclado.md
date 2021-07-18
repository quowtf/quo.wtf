---
title: "El Día Que Hice Una Distribución Para Teclado"
date: 2021-07-04T19:15:49-05:00
tags:
  - layout
  - sirenato
  - v1
  - v2
categories:
  - Teclados
languages:
  - es
images:
  - "imagenes/sirenato/Screen Shot 2021-07-04 at 19.28.12.png"
paragraphs:
  - "Hice una distribución para teclados, esta basada en dvorak y arensito, enfocada al español e inglés y un twist de permutaciones"
---

Ahora les escribo con esta nueva distribución, luego de la ardua "investigación" toca probar que tan bien o mal lo hice. Esta seria la versión 1 o tal vez la 0.1.0. Es muy cagado escribir con una nueva distribución, uno escribe como niño.

Fue muy divertido.

## El problema

El problema con Dvorak, son varios jajaja, pero ahora estoy seguro: no hay distribución perfecta. O estamos usando el dispositivo incorrecto. No lo sé.

Con Dvorak el peso cae en la mano derecha, no ayuda a escribir en español (no probé con la versión de dvorak en español) y mi mano izquierda se hace bolas en las vocales.

No creo haber arreglado el problema, tal vez lo hice más grande.

## El enfoque

Quiero poder escribir en español e ingles sin muchos topes. No me interesa la velocidad. Quiero tener menos errores de dedo.

## La propuesta

Fusionar Dvorak con arensito, no quiero reaprender o reinventar todo.

### Arensito

Me llamaba mucho la atención esta distribución[^1], parece prometedora, pero, no iba a usar una distribución con la Q arriba de la A en el meñique, la U debajo de la i. Estos dos, son problemas que ya venia arrastrando usando Dvorak (con otras posiciones y letras).

Tome su enfoque e inicie mi propuesta. Con arensito se cubre bien el inglés, y si no escribiera en español más del 80% de mi tiempo quizás me quedaba con arensito.

{{< figure src="/imagenes/sirenato/distribution.gif" alt="Porcentaje de uso por letra en inglés" caption="Porcentaje de uso por letra en inglés - del articulo original de arensito">}}

## Justificacion

Tanto "permutar" me dio dolor de cabeza. Mis letras mas pesadas son E y A. Tal vez debí dejarlas en el dedo medio como arensito, pero no iba a tener las ventajas obvias de arensito, por lo que dejé una y una.

Fin de la justificación.

Arensito tiene muy buena posición para el dedo índice, incluso logra darle el peso de "solo" 5 caracteres, pero después llena esos espacios. Los meñiques también quedan muy sueltitos.

Con sirenato tampoco quería usar el mismo dedo para dos pisadas consecutivos.

## La DATA

Usé tanto los archivos de arensito (en ingles), mas lo que fui encontrando en español. El Quijote, Bodas de sangre, La divina comedia, Crónica de una muerte anunciada, un diccionario. Esas son las cosas que se encuentran en GitHub Gist cuando buscas "libro completo txt".

También agregue textos de filósofos como Séneca, poemas, y otros textos romanos. En español también, pero estos ya los tuve que "Scrapear" de una pagina.

Y por supuesto, no podía dejar fuera el contenido de mi blog.

### Agregando español

Si sabemos de que pie cojea Dvorak, y me quedaba usando arensito, bueno... Ya sabia que iba a tener un problema similar en aretsito.

Aquí mis graficas, luego de mi ardua "investigación"[^2]

{{< figure src="/imagenes/sirenato/Figure_1.png" alt="Porcentaje de uso por letra en inglés + español" caption="Porcentaje de uso por letra en inglés + español">}}

Como verán, la E sigue siendo dominante y la T pasa de ser segundo lugar a sexto, menudo lio en el que me metí. Desde el principio sabia que solo debía cambiar de lugar algunas letras. Ahora tengo que acomodar mas de 27 caracteres.

Como dice Hakon: permutar[^3] es la respuesta. Primero fui por SIRENOTA, RISENOTA, NOSERITA.

## El Resultado

Bueno, con 14 palabras por minuto, unas horas de estar escribiendo y otras mas de "investigar". Mi resultado fue mas que bueno, eso creo, eso quiero pensar. El tiempo y uso lo comprobaran.

{{< figure src="/imagenes/sirenato/14wpm.png" alt="Grafica que muestra lo veloz que escribo con la nueva distribución" caption="14 palabras por minuto">}}

En algún momento se me acabo la ~~imaginación~~ justificación para darle un lugar a cada carácter, y el español parece tener mayores retos que al acomodar los mismos caracteres solo para ingles. No tengo una firma bonita de presentarles la distribución, les dejo el excel y el archivo con que compilo el firmware de mi teclado: Sirenato Layout.

{{< figure src="/imagenes/sirenato/sirenato.png" alt="Distribución para teclado SIRENATO" caption="Distribución para teclado SIRENATO">}}

## Conclusión

Es probable que haga otra permutación, aun se puede llegar a algo mas optimo. Pero ya será para otro fin de semana. Me gusto que la mayoría de los comandos básicos (como copiar, cerrar ventana o pestaña y guardar) quedaran en la mano izquierda. Aun así, la C, J y E son un problema, del otro lado la U y N podrían serlo también. Sin contar que `ok` lo escribiría con el mismo dedo (y es el meñique).

Cortar no esta de moda, por eso se va al meñique.

Se ve una bien en proporción, 51.34% para la mano izquierda y un 51.02% para la mano derecha.

A estas alturas cualquier cambio es un juego de quitar y poner, y ustedes que creían que esto se llama _quid pro quo_ nomas por que si... Si es tan básico.

## Actualización 6 Julio

¿Muy rapido para una versión 2? No lo creo...

{{< figure src="/imagenes/sirenato/v2.png" alt="Distribución para teclado SIRENATO" caption="Distribución para teclado SIRENATO">}}

La columna en rojo son las posibles coincidencias de usar el mismo dedo, segun mi logica la _U_ y la _Y_ nunca se usan juntas jajaja. ¿Cual fue la primer palabra con que inicie el parrafo anterior?

¿Mejora mucho? No lo se...

Tengo dos espacios en blanco, eso si es emocionante.

```c
[_QWERTY] = LAYOUT(
    KC_TAB,   KC_Q,   KC_L,   KC_O,   KC_C,   XXXXXXX,         XXXXXXX,   KC_D,   KC_I,   KC_P,   KC_K,  KC_BSPC,
    MOUSE,    KC_B,   KC_R,   KC_E,   KC_S,   KC_X,               KC_H,   KC_N,   KC_A,   KC_T,   KC_U,  KC_RALT,
    KC_LCTL,  KC_Z,   KC_M,   KC_DOT, KC_V,   KC_W,               KC_G,   KC_J,   KC_COMM,KC_F,   KC_Y,   KC_ESC,
  //|------------------------------------------------------------------------------------------------------------|
                                KC_LGUI, LOWER,   KC_ENT,/* */KC_SPC,  LT(_RAISE, KC_RALT), KC_RSFT
  ),

```

## 7 Julio

Versión **2.1.0**

```c
  [_QWERTY] = LAYOUT(
    KC_TAB,   KC_Q,   KC_L,   KC_O,   KC_C,   KC_SCLN,         KC_QUOT,   KC_D,   KC_I,   KC_P,   KC_K,  KC_BSPC,
  //|------------------------------------------------------------------------------------------------------------|

    MOUSE,    KC_B,   KC_R,   KC_E,   KC_S,   KC_X,               KC_H,   KC_N,   KC_A,   KC_T,   KC_U,  KC_RALT,
  //|------------------------------------------------------------------------------------------------------------|
    
    KC_LCTL,  KC_G,   KC_M,   KC_DOT, KC_V,   KC_W,               KC_Y,   KC_J,   KC_COMM,KC_F,   KC_Z,   KC_ESC,
  //|------------------------------------------------------------------------------------------------------------|

                                KC_LGUI, LOWER,   KC_ENT,/* */KC_SPC,  LT(_RAISE, KC_RALT), KC_RSFT
  ),
```

[^1]: [Arensito](http://pvv.org/~hakonhal/main.cgi/keyboard/)
[^2]: Investigación de un día, unas horas mejor dicho 😜
[^3]: [some permutation of arensito. The layout found by trial and error](http://pvv.org/~hakonhal/main.cgi/keyboard/arensito_devel/)
