---
title: "Sonoma Up and Coding"
date: 2023-11-14T20:55:07-06:00
tags:
  - MacOS
  - Setup
  - Selfnotes
categories:
  - Engineering
languages:
  - es
images: imagenes/2023/11/my-desktop.jpeg
paragraphs: Nunca me ha gustado hacer backup y restaurar, prefiero iniciar un setup desde cero. Mi setup es relativamente simple. Quiero escribir este post para compartir mis utilidades de día a día, así como algunos ajustes, y también para ahorrarme tiempo en futuros setups.
---

Recientemente cambié de laptop principal, y echar a andar una compu fresca aún me parece divertido y entretenido. Allá por el 2018 me encontré con el setup de swyx en dev.to[^1]. Me pareció una buena idea para conocer herramientas, utilidades y ajustes que otros profesionales usan y que pueden ayudar en tu día a día, y claro hay cosas que pueden servir para todos, no solo para los enfocados al desarrollo de software.

## Primeros pasos

Software que instalo de primera:

- Firefox Dev
- IVPN
- Bitwarden
- DuckDuckGo: set as default browser ✅
- Maccy
- iTerm
- Fish shell
- VS Code
- Karabiner: set `capslock` as left_ctrl and `hjkl` as arrows.
- Homebrew

```shell
echo 'eval "/opt/homebrew/bin/brew shellenv"' >> /Users/rob/.profile
eval "$(/opt/homebrew/bin/brew shellenv)"
brew analytics off
```

Me gusta usar Firefox Dev por las herramientas de desarrollo que tiene comparado con la versión normal. Un VPN nunca está de más (¿O sí?). DuckDuckGo como browser principal, ligero y minimalista, me resulta muy útil su función para limpiar todo. Maccy para manejar el historial del portapapeles, de momento va bien. iTerm porque no me he dado tiempo de mirar las terminales modernas. Fish por el autocompletado, y porque soy un quilombo (¿debería regresar a zsh?). Karabiner es genial, con Karabiner por fin uso la tecla caps_lock, siempre estaba ahí, sin usar, tan limpia, tan nueva, Karabiner cambió eso.

## Settings

Listados en orden que aparecen.

### Control Center: Nunca esconder la barra de menú

Siempre mostrar: Bluetooth, wifi, batería y porcentaje, airdrop, focus, sonido.
Siempre ocultar: Siri, spotlight, Stage manager, Time machine.
Solo mostrar en uso: música, mirroring, display.

### Siri: Apagada

Uso mucho spotlight por lo fácil del comando `cmd+space`, pero en la lap prefiero que siri esté apagada, y que busque solo en aplicaciones, calculadora, definiciones, conversiones y sugerencias. El resto preferiría buscarlo por mi cuenta.

### Desktop & Dock: Si por mí fuera le quitaría todos los efectos a las ventanas.

Primero que nada, apagar los malditos hotcorners, segundo, apagar el maldito stage manager.

Me gusta quitar toda la basura del dock y solo dejar Finder, AppLauncher, iTerm, VSCode, Firefox, Papelera. Listo, eso es todo.

### Batería

Trato de cuidar bastante la vida de la batería, aún así, **siempre termino apagando el low power mode**, las baterías ya se cuidan bien solas, prefiero tener el mejor rendimiento en todo momento y gastar más batería, que empezar a notar cómo se apendeja la computadora por querer ahorrar un poco de batería.

## Finder: Mostrar todos los archivos

```cmd+shift+.```

En settings, quito todos los tags y activo mostrar las extensiones de los archivos

### Sidebar

Simple y compacto, solo dejo activo lo siguiente:

- Airdrop
- Apps
- Downloads
- User
- Code (Esta carpeta la agrego manual, arrastrando y soltando)

## Consola o Terminal

En iTerm cargo el tema con los colores que me dan un buen contraste y quitan ese negro aburrido. Hacer Fish el shell default. En Fish instalo omf y con omf instalo z, cambio el tema por alguno minimalista y listo. 

![Captura de ventana iTerm](/imagenes/2023/11/my-iTerm.png "Mi terminal")

### Fish

También defino algunos aliases comunes para usar git.

```
alias -s gpo="git pull origin"                                     
alias -s gc="git checkout"
```

Aquí me hace falta mejorar este proceso bastante, me falta importar algunas funciones que tengo en la vieja laptop. Y todo eso que está en el repo de **<a href="https://github.com/quowtf/dotfiles" target="_blank">DotFiles</a>**.

## VS Code

Las extensiones que realmente necesito para iniciar a trabajar son:

- IntelliCode
- Material Icon Theme
- [**Metzi**: un tema que creé basado en contraste medio a alto y poca gama de colores, kiss.](/2020/05/01/mi-primer-tema-para-vs-code)

## Conclusión

Ya tengo más de 2 o 3 meses desde que hice el cambio, estoy seguro de que olvidé muchas cosas. Esto sería lo mínimo con lo que una computadora se vuelve personal. El resto de las cosas las instalo en el camino y cuando las requiera.

🍻

[^1]: <a href="https://dev.to/swyx/my-new-mac-setup-4ibi" target="_blank">Setup de swyx</a>
