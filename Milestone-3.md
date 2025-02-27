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

{
    "cmake.configureOnOpen": true,
    "cmake.generator": "Unix Makefiles",
    "cmake.buildDirectory": "${workspaceFolder}/build"
}
