# Image Alpine minimale
FROM alpine:latest

# Installer uniquement les outils nécessaires
RUN apk add --no-cache gcc musl-dev cmake make gdb

# Définir le dossier de travail
WORKDIR /workspace

# Commande par défaut
CMD ["/bin/sh"]