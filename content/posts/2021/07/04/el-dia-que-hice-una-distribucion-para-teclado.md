---
title: "El Día Que Hice Una Distribución Para Teclado"
date: 2021-07-04T19:15:49-05:00
tags:
  - crkbd
categories:
  - Teclados
languages:
  - es
images: "imagenes/sirenato/Screen Shot 2021-07-04 at 19.28.12.png"
paragraphs: "Hice una distribución para teclados, está basada en Dvorak y Arensito, enfocada al español e inglés con un twist de permutaciones."
---

Ahora les escribo con esta nueva distribución, luego de la ardua "investigación" toca probar qué tan bien o mal lo hice. Esta sería la versión 1 o tal vez la 0.1.0. Es muy cagado escribir con una nueva distribución, uno escribe como niño.

EL proceso fue muy divertido.

## El problema

El problema con Dvorak, son varios jajaja, pero ahora estoy seguro que no hay distribución perfecta. O estamos usando el dispositivo incorrecto. No lo sé...

Con Dvorak el peso cae en la mano derecha, Dvorak no ayuda a escribir en español (no probé con la versión de Dvorak en español) y mi mano izquierda se hace bolas en las vocales.

No creo haber arreglado el problema, tal vez lo hice más grande.

## El enfoque

Quiero poder escribir en español e inglés sin muchos topes. No me interesa la velocidad. Quiero tener menos errores de dedo.

## La propuesta

Fusionar Dvorak con Arensito, no quiero reaprender o reinventar todo.

### Arensito

Me llamaba mucho la atención esta distribución[^1], parece prometedora, pero, no iba a usar una distribución con la Q arriba de la A,  en el columna del dedo meñique, la U debajo de la i. Estos dos, son problemas que ya venía arrastrando usando Dvorak (con otras posiciones y otras letras).

Así que tomé su enfoque e inicié mi propuesta. Con Arensito se cubre bien el inglés, y si no escribiera en español más del 80% de mi tiempo quizás me quedaba con Arensito.

{{< figure src="/imagenes/sirenato/distribution.gif" alt="Porcentaje de uso por letra en inglés" caption="Porcentaje de uso por letra en inglés - del artículo original de Arensito">}}

## Justificación

Tanto "permutar" me dio dolor de cabeza. Mis letras más pesadas son E y A. Tal vez debí dejarlas en el dedo medio como Arensito, pero no tendria las ventajas obvias de Arensito, por lo que dejé una y una.

Con esta nueva distribución quiero evitar usar el mismo dedo en pisadas consecutivas.

## La DATA

Usé tanto los archivos de Arensito (en inglés), más lo que fui encontrando en español. El Quijote, Bodas de sangre, La divina comedia, Crónica de una muerte anunciada, un diccionario. Esas son las cosas que se encuentran en GitHub Gist cuando buscas "libro completo txt".

También agregué textos de filósofos como Séneca, poemas, y otros textos romanos. En español también, pero estos ya los tuve que "Scrapear" de una página.

Y por supuesto, no podía dejar fuera el contenido de mi blog.

### Agregando español

Ya sabia de qué pie cojea Dvorak, por lo que no podia quedarme usando Arensito. Ya que iba a tener el mismo problema.

Aquí mis gráficas, luego de mi ardua "investigación"[^2]

{{< figure src="/imagenes/sirenato/Figure_1.png" alt="Porcentaje de uso por letra en inglés + español" caption="Porcentaje de uso por letra en inglés + español">}}

Como verán, la E sigue siendo dominante y la T pasa de ser segundo lugar a sexto, menudo lío en el que me metí. Desde el principio sabía que solo debía cambiar de lugar algunas letras. Ahora tengo que acomodar más de 27 caracteres.

Como dice Hakon: permutar[^3] es la respuesta. Primero fui por SIRENOTA, RISENOTA, NOSERITA.

## El Resultado

Bueno, con 14 palabras por minuto, unas horas de estar escribiendo y otras más de "investigar". Mi resultado fue más que bueno, eso creo, eso quiero pensar. El tiempo y uso lo comprobarán.

{{< figure src="/imagenes/sirenato/14wpm.png" alt="Gráfica que muestra lo veloz que escribo con la nueva distribución" caption="14 palabras por minuto">}}

En algún momento se me acabó la ~~imaginación~~ justificación para darle un lugar a cada carácter, y el español parece tener mayores retos que al acomodar los mismos caracteres solo para inglés. No tengo una forma bonita de presentarles la distribución, les dejo el excel y un archivo de texto: quowtf layout.

{{< figure src="/imagenes/sirenato/sirenato.png" alt="Distribución para teclado QUOWTF" caption="Distribución para teclado quowtf">}}

## Conclusión

Es probable que haga otra permutación, aún se puede llegar a algo más óptimo. Pero ya será para otro fin de semana. Me gustó que la mayoría de los comandos básicos (como copiar, cerrar ventana o pestaña y guardar) quedaran en la mano izquierda. Aun así, la C, J y E son un problema, del otro lado la U y N podrían serlo también. Sin contar que `ok` lo escribiría con el mismo dedo (y es el meñique).

El comando para cortar no está de moda, por eso se va al meñique.

El posible peso de uso para cada lado se ve parejo, 51.34% para la mano izquierda y un 51.02% para la mano derecha.

A estas alturas cualquier cambio es un juego de quitar y poner.

## Actualización 6 Julio

¿Muy rápido para una versión 2? No lo creo...

{{< figure src="/imagenes/sirenato/v2.png" alt="Distribución para teclado QUOWTF" caption="Distribución para teclado QUOWTF">}}

La columna en rojo son las posibles coincidencias de usar el mismo dedo, según mi lógica la _U_ y la _Y_ nunca se usan juntas jajaja. ¿Cuál fue la primer palabra con que inicié el párrafo anterior?

¿Mejora mucho? No lo sé...

Tengo dos espacios en blanco, eso sí es emocionante.


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

## Versión **2.1.1**

Un ligero cambio, creo que la `F` debe estar en la mano izquierda (más que la `Z`).
Tambien separe la `D` de la `N`, para palabras como `end` no ayudaba.

```c
  [_QUOWTF] = LAYOUT(
    KC_TAB,   KC_Q,   KC_L,   KC_O,   KC_C,   KC_SCLN,         KC_QUOT,   KC_B,   KC_I,   KC_P,   KC_K,  KC_BSPC,
  //|------------------------------------------------------------------------------------------------------------|

    MOUSE,    KC_F,   KC_R,   KC_E,   KC_S,   KC_X,               KC_H,   KC_N,   KC_A,   KC_T,   KC_U,  KC_RALT,
  //|----------------------------------------------------------------------------------------------------------|
    
    KC_LCTL,  KC_G,   KC_M,   KC_DOT, KC_V,   KC_W,               KC_Y,   KC_J,   KC_COMM,KC_D,   KC_Z,   KC_ESC,
  //|------------------------------------------------------------------------------------------------------------|

                                KC_LGUI, LOWER,   KC_ENT,/* */KC_SPC,  LT(_RAISE, KC_RALT), KC_RSFT
  ),
```

## Versión **2.2.0**

Uops! Ese `BY` se me fue en la version anterior 😜

```c
  [_QUOWTF] = LAYOUT(
    KC_TAB,   KC_B,   KC_L,   KC_O,   KC_V,   KC_SCLN,         KC_QUOT,   KC_Y,   KC_I,   KC_D,   KC_K,  KC_BSPC,
  //|------------------------------------------------------------------------------------------------------------|

    MOUSE,    KC_F,   KC_R,   KC_E,   KC_S,   KC_X,               KC_Q,   KC_N,   KC_A,   KC_T,   KC_U,  KC_RALT,
  //|------------------------------------------------------------------------------------------------------------|
    
    KC_LCTL,  KC_G,   KC_M,   KC_DOT, KC_C,   KC_W,               KC_J,   KC_H,   KC_COMM,KC_P,   KC_Z,   KC_ESC,
  //|------------------------------------------------------------------------------------------------------------|
                                KC_LGUI, LOWER,   KC_ENT,/* */KC_SPC,  LT(_RAISE, KC_RALT), KC_RSFT
  ),
```

## Versión **2.2.1**

Aun tiene varias colisiones, pero me divierte mucho usar este layout.
La palabra con más colisiones hasta el momento es `T-E-O-R-I-A`. Se las dejo de tarea 🥲.
Ya llegue a las 30 palabras por minuto, con todo y los diversos (y radicales) cambios.

```c
  [_QUOWTF] = LAYOUT(
    KC_TAB,   KC_Y,   KC_L,   KC_O,   KC_V,   KC_SCLN,         KC_QUOT,   KC_B,   KC_I,   KC_D,   KC_K,  KC_BSPC,
  //|------------------------------------------------------------------------------------------------------------|

    MOUSE,    KC_F,   KC_R,   KC_E,   KC_S,   KC_W,               KC_Q,   KC_N,   KC_A,   KC_T,   KC_U,  KC_RALT,
  //|------------------------------------------------------------------------------------------------------------|
    
    KC_LCTL,  KC_G,   KC_M,   KC_DOT, KC_C,   KC_X,               KC_J,   KC_H,   KC_COMM,KC_P,   KC_Z,   KC_ESC,
  //|------------------------------------------------------------------------------------------------------------|
                                KC_LGUI, LOWER,   KC_ENT,/* */KC_SPC,  LT(_RAISE, KC_RALT), KC_RSFT
  ),
```

[^1]: [Arensito](http://pvv.org/~hakonhal/main.cgi/keyboard/)
[^2]: Investigación de un día, unas horas mejor dicho 😜
[^3]: [some permutation of arensito. The layout found by trial and error](http://pvv.org/~hakonhal/main.cgi/keyboard/arensito_devel/)
