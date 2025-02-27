# Milestone #3: Compilation et exécution dans le Dev Container depuis VS Code

# 🎯 Objectif

Configurer VS Code pour compiler et exécuter un projet C dans le Dev Container en utilisant CMake et Make.


# 🛠️ 1. Vérifier que CMake et Make sont installés dans le Dev Container

Dans le terminal du Dev Container (Ctrl + \`` ou Terminal > New Terminal`), tape :

```
cmake --version
make --version
```

Si une des commandes est introuvable, ajoute ces paquets dans le Dockerfile du Dev Container :

📄 Modifier .devcontainer/Dockerfile

```
RUN apt-get update && apt-get install -y cmake make gdb
```

Puis recharge le container :

```
Ctrl + Shift + P → "Dev Containers: Rebuild and Reopen in Container"
```

# 📄 2. Configurer .vscode/settings.json

Ajoute ce fichier pour que VS Code reconnaisse CMake :

📄 Créer ou modifier .vscode/settings.json

```
{
    "cmake.configureOnOpen": true,
    "cmake.generator": "Unix Makefiles",
    "cmake.buildDirectory": "${workspaceFolder}/build"
}
```

# 🔧 3. Configurer CMakeLists.txt

📄 Créer/modifier CMakeLists.txt à la racine du projet

```
cmake_minimum_required(VERSION 3.10)
project(MyProject C)

set(CMAKE_C_STANDARD 99)

add_executable(my_program main.c)
```

# 🏗️ 4. Générer le projet avec CMake

Dans VS Code :

Ouvre la palette de commande (Ctrl + Shift + P).

Tape : CMake: Configure.

Sélectionne "Unix Makefiles" comme générateur.

Vérifie que les fichiers de build sont créés dans le dossier build/.

# 🔨 5. Compiler et Exécuter depuis VS Code

## ➤ Compiler avec CMake Tools

Ouvre la palette de commande (Ctrl + Shift + P).
Tape CMake: Build et exécute la commande.

Ou dans le terminal :

```
cmake --build build
```

## ➤ Exécuter le programme
Après la compilation, exécute le programme dans le terminal du Dev Container :

```
./build/main
```

# 🐞 6. Ajouter le Débogage (launch.json)

Pour déboguer le code en mode pas à pas, configure .vscode/launch.json :

📄 Créer/modifier .vscode/launch.json

```
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Debug C Program in Dev Container",
      "type": "cppdbg",
      "request": "launch",
      "program": "${workspaceFolder}/build/my_program",
      "args": [],
      "stopAtEntry": false,
      "cwd": "${workspaceFolder}",
      "environment": [],
      "externalConsole": false,
      "MIMode": "gdb",
      "setupCommands": [
        {
          "description": "Enable pretty-printing for gdb",
          "text": "-enable-pretty-printing",
          "ignoreFailures": true
        }
      ],
      "preLaunchTask": "CMake Build",
      "miDebuggerPath": "/usr/bin/gdb"
    }
  ]
}
```

## ➤ Déboguer dans VS Code

Place un point d’arrêt (F9) dans main.c.
Ouvre Run and Debug (Ctrl + Maj + D).
Sélectionne "Debug C Program in Dev Container".
Clique sur ▶ Lancer (F5).

✅ Le programme démarre en mode débogage avec GDB dans le Dev Container ! 🎯
