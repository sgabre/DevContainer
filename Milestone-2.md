# Milestone #2:  Ajouter CMake

# 📄 CMakeLists.txt

```
cmake_minimum_required(VERSION 3.10)
project(MyCProject C)

set(CMAKE_C_STANDARD 99)

add_executable(main src/main.c)
```

# 📄 .devcontainer/Dockerfile (mise à jour)

```
# Image Alpine minimale
FROM alpine:latest

# Installer GCC, CMake et Make
RUN apk add --no-cache gcc musl-dev cmake make

# Définir le dossier de travail
WORKDIR /workspace

# Commande par défaut
CMD ["/bin/sh"]
```

# 📄 .devcontainer/devcontainer.json (mise à jour)

```
{
  "name": "C Dev Container with CMake",
  "build": {
    "dockerfile": "Dockerfile"
  },
  "customizations": {
    "vscode": {
      "extensions": [
        "ms-vscode.cpptools",
        "twxs.cmake"
      ]
    }
  }
}
```

# 🔹 Compiler avec CMake

Dans le terminal du container :

```
mkdir build
cd build
cmake ..
make
./main
```

# ✅ Sortie attendue :

Hello, Dev Container!

