---
title: "Programmer Dvorak"
date: 2021-02-21T20:00:24-06:00
tags:
  - Dvorak
categories:
  - Teclados
languages:
  - es
images:
  - imagenes/dvorak.jpg
paragraphs:
  - "La vida ya es demasiado aleatoria como para escribir en un teclado con distribución :<>PY" 
---

El teclado, y principalmente la distribución QWERTY, fue diseñada sin diseño. En otras palabras QWERTY fue resultado del azar, la posición se decidió aleatoriamente. Aunque QWERTY no es mala, tampoco es la mejor justificada.

## Y por eso...

Me mudo a distribución Dvorak, en su derivación para programador. Así que este post lo escribo a tientas y con mucha cautela, sin mirar el teclado pero con mucha lentitud...

## El porqué

Vivo de la programación, jaja!

## Fin

Dejo el keymap que estaré usando:

```c
[_QWERTY] = LAYOUT(
    KC_TAB,   KC_SCLN,  KC_COMM, KC_DOT,  KC_P,  KC_Y,               KC_F,    KC_G,  KC_C,  KC_R,  KC_L, KC_BSPC,
    COMMANDS, KC_A,     KC_O,    KC_E,    KC_U,  KC_I,               KC_D,    KC_H,  KC_T,  KC_N,  KC_S, KC_RALT,
    KC_LCTL,  KC_QUOT,  KC_Q,    KC_J,    KC_K,  KC_X,               KC_B,    KC_M,  KC_W,  KC_V,  KC_Z,  KC_ESC,
                                    KC_LGUI, LOWER,   KC_ENT,  KC_SPC,  RAISE, KC_RSFT
),

[_LOWER] = LAYOUT(
    LCTL(KC_GRAVE), KC_7,    KC_5,    KC_3,    KC_1,    KC_9,          KC_0,      KC_2,    KC_4,    KC_6,     KC_8,   KC_DEL,
    XXXXXXX,        KC_F7,   KC_F5,   KC_F3,   KC_F1,   KC_F9,        KC_F10,    KC_F2,   KC_F4,   KC_F6,    KC_F8,  KC_BSPC,
    KC_LCTL,        XXXXXXX, XXXXXXX, XXXXXXX, XXXXXXX, KC_F11,       KC_F12,  XXXXXXX, XXXXXXX, XXXXXXX,  XXXXXXX,   KC_ESC,
                                    KC_LGUI, LOWER,   KC_ENT,  KC_SPC,  RAISE, KC_RSFT
),

[_RAISE] = LAYOUT(
    KC_BSPC,  KC_LBRC,  KC_LCBR, KC_RCBR, KC_LPRN,  KC_EQL,                 KC_ASTR, KC_RPRN, KC_PLUS,  KC_RBRC,  KC_EXLM, KC_DEL,
    LOWER,    KC_DLR,   KC_AMPR, XXXXXXX, XXXXXXX, KC_CIRC,                 KC_LEFT, KC_DOWN, KC_UP,    KC_RIGHT, KC_HASH, KC_GRV,
    KC_LSFT,  KC_TILD,  KC_PERC, XXXXXXX, XXXXXXX, XXXXXXX,                 KC_MINS, KC_UNDS, KC_SLSH,  KC_AT,   KC_BSLS, KC_RSFT,
                                    KC_LGUI, KC_LALT,   KC_LCTL,  KC_SPC,  RAISE, KC_RSFT
),
```
