# Docker

> ❌ A travailler

> ✔️ Auto validation par l'étudiant

## 🎓 J'ai compris et je peux expliquer

- la création d'une image docker ✔️
- l'éxécution d'un container ✔️
- l'orchestration de containers avec docker-compose ✔️


## 💻 J'utilise

### Un exemple personnel commenté ❌ / ✔️

### Utilisation dans un projet ❌ / ✔️

[lien github vers The Good Corner](https://github.com/FlorenceBuchelet/the-good-corner)

Description :

Front, back et BDD ont chacun leur Dockerfile et sont orchestrés par un docker-compose.

```yml
services:

  back:
    build: ./backend
    restart: unless-stopped
    ports:
      - 4000:4000
    volumes:
      - ./backend:/app
    environment:
      TGC_DBPASS: ${DBPASS}

  front:
    build: ./frontend
    restart: unless-stopped
    ports:
      - 3000:3000
    volumes:
      - ./frontend:/webapp

  db:
    image: postgres:16
    restart: unless-stopped
    shm_size: 128mb
    volumes:
      - /c/Users/ce pc/quests/ALTERNANCE/the-good-corner-db-data:/var/lib/postgresql/data
    environment:
      POSTGRES_PASSWORD: ${DBPASS_ADMIN}
    ports:
      - 5432:5432
```

### Utilisation en production si applicable❌ / ✔️

[lien du projet](...)

Description :

### Utilisation en environement professionnel ❌ / ✔️

Description :

## 🌐 J'utilise des ressources

### Titre

- lien
- description

## 🚧 Je franchis les obstacles

### Point de blocage ❌ / ✔️

Description: ✨Windows 10✨

Plan d'action : (à valider par le formateur)

- Fix propres à Windows 10 pour le hot reload ✔️
- Envisager le partitionnement pour coder sous Linux ✔️

Résolution : Fixs propres à Windows 10 en cours, passage sous Linux en entreprise.

```yml
    environment:
    # le serveur doit se connecter sur localhost
      - WDS_SOCKET=127.0.0.1
    # active la lib chokidar pour surveiller les changements
      - CHOKIDAR_USEPOLLING=true
    # active également la surveillance de changements pour watchpack
      - WATCHPACK_POLLING=true
    # "polling" = pollinisation
```

## 📽️ J'en fais la démonstration

- J'ai ecrit un [tutoriel](...) ❌ / ✔️
- J'ai fait une [doc sur Docker](...) ❌ / ✔️
