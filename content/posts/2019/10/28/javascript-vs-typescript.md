---
title: "Javascript vs Typescript"
date: 2019-10-28T21:12:47-06:00
draft: false
toc: true
images:
  - imagenes/IMG_6283.jpg
tags: 
  - Development
  - Backend
categories:
  - Engineer
languages:
  - es
---

## Guía para programadores no-js no-ts

Acabo de entrar al mundo web con JS, y mi principal duda es: ¿Es mejor TypeScript que JavaScript? Para el desarrollo de aplicaciones "grandes". Respuesta rápida: no. Respuesta corta: sí.

## Respuesta rápida

No, si eres un desarrollador JavaScript con años de experiencia, leer código JS es algo habitual para ti y estás al día con las actualizaciones de ECMAScript.

## Respuesta corta

Sí, TypeScript tiene buenas ventajas sobre JavaScript, y si digo ventajas posiblemente solo aplique para programadores nuevos en estos lenguajes. Por no decir programadores amantes de los lenguajes tipados, programadores que prefieren control sobre sus estructuras, objetos, clases, programadores que buscan más legibilidad, y ojo no estoy diciendo que en JS no lo puedas hacer pero entre poder y deber, TypeScript te "obliga" a definir el tipo, JS no y si no te obliga no lo haces, simplemente porque lo puedes omitir, digamos que el pretexto es el tiempo. ¿TypeScript te obliga a escribir más? No.

### Tipado dinámico opcional

TypeScript te permite omitir el tipo de tu variable, pero (esto es una comparativa, no lo olvides) comparando con JS si hay un error en el tipo de variable que envías y la variable que tu función evalúa, es decir, estas variables son diferentes, este error en JS lo verás hasta que hagas pruebas de tu código, y si este error es obvio, está bien, pero si no, este error lo verás hasta que tus usuarios te reporten algún comportamiento extraño en tu aplicación. Por otro lado, con TS este error lo ves al momento de compilar.

Gran punto a favor para TS.

### Clases e Interfaces

Otra gran ayuda de TS son las clases e interfaces, que nos permiten definir y conocer en todo momento la estructura instanciadas con las que estamos trabajando y las propiedades que la componen, en todo momento.

Por esto, si buscamos una propiedad que no existe, TS nos lo hará saber y con esto damos seguridad de que las propiedades que esperamos encontrar dentro de nuestra estructura existen, en JS esto no lo puedes saber hasta que tu app truena con algún `undefined`.

## La otra cara de la moneda

Si hay que mencionar algo que no ayuda mucho a TS es que se vuelve una dependencia más en tu proyecto, hay que mantenerla viva, y todo lo que implique la gestión de dependencias en tu proyecto. Porque si hay algún puritano programador en tu equipo que le molesta hasta el hecho de instalar un plugin más en su editor de texto, bueno...

## Conclusion

Apoyo el uso de TS sobre JS, si eres nuevo la curva de aprendizaje es casi la misma, si vienes de un lenguaje tipado te sentirás más seguro entrando a programar con TS.
