# Utiliser l'image officielle Python comme base
FROM python:3.10-slim

# Installer les dépendances système nécessaires pour PyMySQL
RUN apt-get update && apt-get install -y \
    libmariadb-dev gcc \
    && apt-get clean

# Définir le répertoire de travail
WORKDIR /app

# Copier les fichiers nécessaires pour l'installation des dépendances Python
COPY eduplateforme/requirements.txt /app/

# Installer les dépendances Python
RUN pip install --no-cache-dir -r requirements.txt

# Copier tout le projet dans le conteneur
COPY . /app/

# Ajouter un script Python pour attendre que la base de données soit prête
COPY eduplateforme/wait_for_db.py /app/

# Exposer le port pour l'application Django
# EXPOSE 8000

# Commande par défaut pour exécuter le script d'attente, puis démarrer le serveur Django
CMD ["sh", "-c", "python wait_for_db.py && python manage.py runserver 0.0.0.0:8000"]
