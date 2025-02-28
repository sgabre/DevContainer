# 🚀 Milestone 5 : Configuration de la Toolchain STM32 dans le Dev Container

Dans cette étape, nous allons configurer la toolchain STM32 dans un Dev Container pour pouvoir compiler, lier et flasher un programme sur un microcontrôleur STM32 directement depuis VS Code.

# 🎯 Objectifs

- Installer GCC ARM Embedded Toolchain dans le Dev Container.
- Ajouter OpenOCD pour le debug et le flashage.
- Configurer CMake pour utiliser la toolchain STM32.
- Compiler et déboguer un programme STM32 dans le Dev Container.

# 🛠️ 1. Modifier le Dockerfile du Dev Container

Ajoute les outils STM32 dans .devcontainer/Dockerfile :

📄 Modifier .devcontainer/Dockerfile

# Installer les outils de développement et la toolchain STM32

```
# Utiliser Alpine comme base
FROM alpine:latest

# Installer les dépendances
RUN apk add --no-cache \
    cmake make ninja g++ gcc musl-dev \
    arm-none-eabi-gcc arm-none-eabi-binutils arm-none-eabi-newlib \
    gdb-multiarch openocd bash

# Définir Ninja comme générateur par défaut pour CMake
ENV CMAKE_GENERATOR=Ninja
```


Après modification, reconstruis le container :

Ctrl + Shift + P → "Dev Containers: Rebuild and Reopen in Container"

🔧 2. Vérifier que la toolchain est bien installée

Dans le terminal du Dev Container (`Ctrl + ``), tape :

```
arm-none-eabi-gcc --version
arm-none-eabi-gdb --version
openocd --version
```
Si les commandes renvoient une version, l’installation est OK ✅.

📄 3. Configurer CMakeLists.txt pour STM32

Ajoute un CMakeLists.txt compatible STM32 :

📄 Créer/modifier CMakeLists.txt

```
cmake_minimum_required(VERSION 3.10)
project(STM32Project C ASM)

set(CMAKE_SYSTEM_NAME Generic)
set(CMAKE_SYSTEM_PROCESSOR arm)

# Définir la toolchain STM32
set(CMAKE_TRY_COMPILE_TARGET_TYPE STATIC_LIBRARY)
set(CMAKE_C_COMPILER arm-none-eabi-gcc)
set(CMAKE_CXX_COMPILER arm-none-eabi-g++)
set(CMAKE_ASM_COMPILER arm-none-eabi-gcc)

# Options de compilation
set(CMAKE_C_FLAGS "-mcpu=cortex-m4 -mthumb -O2 -ffunction-sections -fdata-sections" CACHE STRING "" FORCE)
set(CMAKE_EXE_LINKER_FLAGS "-Wl,--gc-sections" CACHE STRING "" FORCE)

# Ajouter l'exécutable

add_executable(stm32_app main.c)
```

Cela permet d’utiliser GCC ARM Embedded pour compiler du code STM32.

🔨 4. Compiler le projet STM32

Dans VS Code :

Ouvre la palette de commande (Ctrl + Shift + P).
Tape : CMake: Configure.
Ensuite, exécute CMake: Build.
Ou en ligne de commande :

```
cmake -B build
cmake --build build
```
Si tout est bien configuré, tu obtiendras un exécutable .elf.

🐞 5. Déboguer avec OpenOCD et GDB

Ajoute cette configuration dans .vscode/launch.json :

📄 Créer/modifier .vscode/launch.json

```
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Debug STM32",
      "type": "cppdbg",
      "request": "launch",
      "program": "${workspaceFolder}/build/stm32_app.elf",
      "cwd": "${workspaceFolder}",
      "MIMode": "gdb",
      "miDebuggerPath": "/usr/bin/arm-none-eabi-gdb",
      "setupCommands": [
        {
          "description": "Se connecter à OpenOCD",
          "text": "target remote localhost:3333",
          "ignoreFailures": true
        },
        {
          "description": "Charger le programme",
          "text": "load",
          "ignoreFailures": true
        }
      ]
    }
  ]
}
```
Cela permet d’utiliser OpenOCD pour flasher et déboguer le STM32 directement dans le Dev Container.

🔌 6. Flasher le microcontrôleur STM32

Démarre OpenOCD dans le terminal du Dev Container :

```
openocd -f interface/stlink.cfg -f target/stm32f4x.cfg
```

Puis, flashe le programme avec GDB :

```
arm-none-eabi-gdb build/stm32_app.elf
```

Dans GDB, tape :

target remote localhost:3333
load
continue
Le programme est maintenant exécuté sur le STM32 🎯.




```
mkdir DevContainer
cd DevContainer
```

