# 1. Image slim : Version allégée de Debian
FROM python:3.11-slim

# 2. Sécurité : Création d'un utilisateur non-root (Challenge du prof)
RUN useradd -m apiuser

WORKDIR /app

# 3. Ordre des layers : On copie UNIQUEMENT le fichier de dépendances d'abord
COPY app/requirements.txt .

# 4. Suppression des caches : On empêche pip de stocker les fichiers d'installation temporaires
RUN pip install --no-cache-dir -r requirements.txt

# Ensuite seulement on copie le code source (qui change plus souvent)
COPY app/ /app/

# On donne la propriété des fichiers à notre utilisateur sécurisé et on bascule dessus
RUN chown -R apiuser:apiuser /app
USER apiuser

EXPOSE 8000
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
