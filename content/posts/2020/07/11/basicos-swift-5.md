---
title: "Basicos Swift 5"
date: 2020-07-11T13:13:28-05:00
tags:
  - Development
  - Backend
categories:
  - Engineering
languages:
  - es
images:
paragraphs: Swift promete ser rápido, seguro y expresivo. Aunque es un lenguaje de propósito general, es mejor conocido como el lenguaje moderno que debes aprender para desarrollar aplicaciones en el ecosistema de la familia Manzana.
---

Leí un poco de la documentación y de primera entrada tiene conceptos que no se ven en todos lados a todas horas, algunos no los entendí del todo, eso los vuelve más interesantes para mí, tanto los conceptos como el lenguaje en sí. Aquí mis notas 😜

- Swift es un lenguaje de tipado-seguro.

{{< figure src="/imagenes/basicos-swift-5/swift-type-safety.png" alt="Resumen de type safety en ingles" caption="Este es lo que la wiki nos dice del tipado \"seguro\", en ingles :)">}}

## Let y Var

La forma de crear constantes, para asegurar la inmutabilidad en variables, se usa `let`.

Por otro lado, para tener variables mutables podemos usar `var`.

## Tipado explicito y tipado inferido

{{< figure src="/imagenes/basicos-swift-5/swift-org-doc.png" alt="tipado explicito en swift" caption="Inferencia de tipos, de la documentacion en <https://swift.org/>" >}}

Swift nos permite dejarle el trabajo de inferir los tipos en nuestras declaraciones, o también podemos definirlas explícitamente.

{{< figure src="/imagenes/basicos-swift-5/swift-tipado.png" alt="codigo ejemplo de tipado explicito" >}}

## Opcionales

Esta funcionalidad en los lenguajes modernos es una ventaja para lidiar contra cosas nulas o indefinidas (undefined).

En el caso de Swift, podemos usarlas con un signo de interrogación, por ejemplo:

{{< figure src="/imagenes/basicos-swift-5/swift-opcional-linea1.png" alt="codigo ejemplo para decalrar variables opcionales" >}}

Listo, tenemos nuestra variable opcional, `constanteOpcional`, que está declarada como cadena explícitamente y como opcional al mismo tiempo.

## Algunos operadores utiles

- If con asignación en la misma línea

{{< figure src="/imagenes/basicos-swift-5/swift-if-inline.png" alt="codigo ejemplo if con asignacion en la misma linea" >}}

La asignación a la constante 'nuevaConstante' sucede si, solo si, 'constanteOpcional' existe y es diferente de 'nil' (nulo).

- El hermano menor de la típica operación condicional ternaria, el popular y útil: si-algo ? esto : si-no-esto

Swift tiene una versión renovada del operador ternario para las declaraciones opcionales:

{{< figure src="/imagenes/basicos-swift-5/swift-ejemplo-nil-coalesing.png" alt="ejemplo del operador ??" >}}

En la última línea se evalúa la variable opcional `colorBase`. Si `colorBase` es nula, se asigna `colorDefault`; de lo contrario, se asigna `colorBase`. Como se darán cuenta, este operador es muy práctico.

{{< figure src="/imagenes/basicos-swift-5/swift-hermano-ternario.png" alt="extracto de la documentacion sobre nil coalesing" caption="ss de la documentacion sobre nil coalesing">}}

- Guard - else

{{< figure src="/imagenes/basicos-swift-5/swift-guard.png" alt="ejemplo del operador guard-else" >}}

`guard`, a diferencia de `if`, siempre debe llevar un else. Me parece muy ventajoso entrar en este contexto que se abre gracias al `else`.

`guard` debe llevar un return o throw: "guard body must not fall through, consider using a return or throw to exit the scope".
