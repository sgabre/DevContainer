# Milestone #3: Compilation et exécution dans le Dev Container depuis VS Code

# 🎯 Objectif

Configurer VS Code pour compiler et exécuter un projet C dans le Dev Container en utilisant CMake et Make/Ninja.


# 🛠️ 1. Vérifier que CMake et Make sont installés dans le Dev Container

Dans le terminal du Dev Container (Ctrl + \`` ou Terminal > New Terminal`), tape :

cmake --version
make --version

Si une des commandes est introuvable, ajoute ces paquets dans le Dockerfile du Dev Container :

📄 Modifier .devcontainer/Dockerfile

RUN apt-get update && apt-get install -y cmake make ninja-build gdb

Puis recharge le container :

Ctrl + Shift + P → "Dev Containers: Rebuild and Reopen in Container"

