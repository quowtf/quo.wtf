---
title: "Javascript vs Typescript"
date: 2019-10-28T21:12:47-06:00
draft: false
toc: true
images:
  - imagenes/IMG_6283.jpg
tags: 
  - javascript
  - vs
  - typescript
categories:
  - Engineer
languages:
  - es
---

## Guia para programadores no-js no-ts

Acabo de entrar al mundo web con JS, y mi principal duda es: ¿Es mejor typescript que javascript? Para desarrollo de aplicaciones "grandes". Respuesta rápida: no. Respuesta corta: si.

## Respuesta rapida

No, si eres un desarrollador javascript con años de experiencia, leer código js para ti es algo usual y estas al día con las actualizaciones de ECMAScript.

## Respuesta corta

Si, typescript tiene buenas ventajas sobre javascript, y si digo ventajas posiblemente solo aplique para programadores nuevos en estos lenguajes. Por no decir programadores amantes de los lenguajes tipados, programadores que prefieren control sobre sus estructuras, objetos, clases, programadores que buscan mas legibilidad, y ojo no estoy diciendo que en JS no lo puedas hacer pero entre poder y deber, typescript te "obliga" a definir el tipo, JS no y si no te obliga no lo haces, simplemente porque lo puedes omitir, digamos que el pretexto es el tiempo. ¿Typescript te obliga a escribir más?, no.

### Tipado dinamico opcional

Typescript te permite omitir el tipo de tu variable, pero (esto es una comparativa no lo olvides) comparando con JS si hay un error en el tipo de variable que envías y la variable que tu función evalúa, es decir estas variables son diferentes, este error en JS lo verás hasta que hagas pruebas de tu código, y si este error es obvio que bueno, pero si no, este error lo veras hasta que tus usuarios te reporter algún comportamiento extraño en tu aplicación. Por otro lado con TS este error lo ves al momento de compilar.

Gran punto a favor para TS.

### Clases e Interfaces

Otra gran ayuda de TS son las clases e interfaces, que nos permiten definir y conocer en todo momento la estructura instanciadas con las que estamos trabajando y las propiedades que la componen, en todo momento.

Por esto si nosotros buscamos una propiedad que no existe TS nos lo hará saber y con esto damos seguridad que las propiedades que esperamos encontrar dentro de nuestra estructura existe, en JS esto no lo puedes saber hasta que tu app truena con algún `undefined`.

## La otra cara de la moneda

Si hay que mencionar algo que no ayuda mucho a TS es que se vuelve una dependencia mas en tu proyecto, hay que mantenerla viva, y todo lo que implique la gestión de dependencias en tu proyecto. Porque si hay algún puritano programador en tu equipo que le molesta hasta el hecho de instalar un plugin mas en su editor de texto bueno...

## Conclusion

Apoyo el uso de TS sobre JS, si eres nuevo la curva de aprendizaje es casi la misma, si vienes de un lenguaje tipado te sentirás más seguro entrando a programar con TS.
