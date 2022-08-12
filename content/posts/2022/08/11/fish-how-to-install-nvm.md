---
title: "Fish How to Install nvm Node Version Manager"
date: 2022-08-11T20:14:11-05:00
tags:
  - fish
  - nvm
  - sh
  - iterm
  - termlove
  - selfnotes
categories:
  - Engineer
languages:
  - en
images:
  - imagenes/2022/08/11/image.png
paragraphs:
  - "Basic guide to get up and ready nvm for fish users. TL;DR in the screenshot"
---

## Step 1

Get [Bass](https://github.com/edc/bass#with-oh-my-fish), an util for running Bash stuff.

```bash
omf install bass
```

## Step 2

Creat these three first files (I didn't create the one with `load_nvm > /d...`)

```bash
# ~/.config/fish/functions/nvm.fish
function nvm
  bass source ~/.nvm/nvm.sh --no-use ';' nvm $argv
end

# ~/.config/fish/functions/nvm_find_nvmrc.fish
function nvm_find_nvmrc
  bass source ~/.nvm/nvm.sh --no-use ';' nvm_find_nvmrc
end

# ~/.config/fish/functions/load_nvm.fish
function load_nvm --on-variable="PWD"
  set -l default_node_version (nvm version default)
  set -l node_version (nvm version)
  set -l nvmrc_path (nvm_find_nvmrc)
  if test -n "$nvmrc_path"
    set -l nvmrc_node_version (nvm version (cat $nvmrc_path))
    if test "$nvmrc_node_version" = "N/A"
      nvm install (cat $nvmrc_path)
    else if test "$nvmrc_node_version" != "$node_version"
      nvm use $nvmrc_node_version
    end
  else if test "$node_version" != "$default_node_version"
    echo "Reverting to default Node version"
    nvm use default
  end
end

# ~/.config/fish/config.fish
# You must call it on initialization or listening to directory switching won't work
load_nvm > /dev/stderr
```

## Step 3

On the working directory create an `.nvmrc` with one of these options

```bash
echo "5.9" > .nvmrc

echo "lts/*" > .nvmrc # to default to the latest LTS version

echo "node" > .nvmrc # to default to the latest version
```

## Step 4

Last bun not least, run nvm install, it will read the `.nvmrc` file and intall the declared version in this file.

```bash
nvm intall

node --version

npm -v
```

See the screenshot in the top if you want a more visal guide.

cheers 🍻
