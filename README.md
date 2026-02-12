```markdown
# README Agent - Automatisation de Génération de README

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![LangChain](https://img.shields.io/badge/LangChain-0.1+-green.svg)
![Streamlit](https://img.shields.io/badge/Streamlit-1.29+-red.svg)

---

## 📌 Description

Ce projet est une **application Streamlit** qui automatise la génération et la maintenance de fichiers **README** pour des projets GitHub ou des profils GitHub. Il utilise des **agents IA** (via LangChain et Mistral) pour :
- **Analyser un repository** (fichiers, structure, dépendances).
- **Générer un README structuré** à partir des données extraites.
- **Modifier un README existant** via une interface de chat interactive.
- **Écrire et pousser** le README généré directement sur GitHub.

---

## 🛠 Tech Stack

| Catégorie       | Technologies                                                                 |
|-----------------|------------------------------------------------------------------------------|
| **Backend**     | Python, LangChain, Mistral AI, SQLite                                        |
| **Frontend**    | Streamlit                                                                    |
| **Outils**      | GitHub CLI (`gh`), `python-dotenv`                                           |
| **Sécurité**    | Protection contre les traversées de chemin, outils read-only pour les agents |

---

## 📂 Structure du Projet

```plaintext
.
├── app/
│   └── Home.py                  # Point d'entrée Streamlit (interface utilisateur)
├── data/
│   └── cv.sqlite3               # Base de données SQLite (profil, projets, compétences)
├── scripts/
│   ├── init_db.py               # Initialisation de la base de données
│   └── seed_db.py               # Peuplement initial de la base de données
├── src/
│   ├── agent_build.py           # Construction de l'agent IA (profil)
│   ├── agent_build_repo.py      # Construction de l'agent IA (repository)
│   ├── chat/
│   │   ├── deepagent.py         # Extraction du texte généré par l'agent
│   │   ├── messages.py          # Gestion des messages du chat
│   │   ├── prompts.py           # Prompts système pour les agents
│   │   └── state.py             # Gestion de l'état Streamlit
│   ├── config.py                # Configuration (clés API, chemins)
│   ├── router_chain.py          # Routage automatique entre profil et repository
│   ├── tools_db.py              # Outils pour interroger la base de données
│   ├── tools_github.py          # Outils pour écrire/commiter/pusher le README
│   ├── tools_repo.py            # Outils pour lister/lire les fichiers du repo
│   ├── ui/
│   │   ├── layout.py            # Interface principale (chat + éditeur)
│   │   └── sidebar.py           # Barre latérale (contrôles)
│   └── utils/
│       └── paths.py             # Gestion des chemins du projet
├── skills/
│   └── github_readme/           # Compétences personnalisées pour les agents
│       ├── SKILL.md             # Documentation de la compétence
│       ├── repo_readme.md       # Stratégie pour générer un README de projet
│       └── templates/           # Modèles de README
├── .env                         # Variables d'environnement (ex: MISTRAL_API_KEY)
├── .env.exemple                 # Exemple de fichier .env
├── .gitignore                   # Fichiers ignorés par Git
├── requirements.txt             # Dépendances Python
└── README.md                    # Ce fichier
```

---

## ⚙️ Fonctionnalités

### 1. **Génération Automatique de README**
- **Pour un profil GitHub** : Utilise les données d'une base SQLite (`profile`, `skills`, `projects`, `links`).
- **Pour un projet** : Analyse les fichiers du repository via `list_repo_tree()` et `read_text_file()`.

### 2. **Interface Interactive**
- **Chat** : Permet de demander des modifications incrémentales au README.
- **Éditeur** : Affiche un brouillon modifiable du README.
- **Actions** :
  - Écrire le README localement (`README.md`).
  - Commiter et pousser directement sur GitHub.

### 3. **Routage Intelligent**
- Détecte automatiquement si la demande concerne un **README de profil** ou un **README de projet**.
- Utilise le bon agent IA en fonction du contexte.

### 4. **Sécurité**
- **Outils read-only** : Les agents n'ont pas accès aux outils d'écriture de fichiers ou de Git (sauf via l'interface Streamlit).
- **Protection contre les traversées de chemin** : Vérification des chemins pour éviter les accès non autorisés.

---

## 🚀 Installation et Lancement

### Prérequis
- Python 3.8+
- Git
- Un compte Mistral AI (pour l'API)

### Étapes

1. **Cloner le repository** :
   ```bash
   git clone https://github.com/AlexandreCrestien/readme-agent.git
   cd readme-agent
   ```

2. **Installer les dépendances** :
   ```bash
   pip install -r requirements.txt
   ```

3. **Configurer l'environnement** :
   - Copier `.env.exemple` vers `.env` et ajouter votre clé API Mistral :
     ```plaintext
     MISTRAL_API_KEY=votre_clé_api
     ```

4. **Initialiser la base de données** (pour le README de profil) :
   ```bash
   python scripts/init_db.py
   python scripts/seed_db.py
   ```

5. **Lancer l'application** :
   ```bash
   streamlit run app/Home.py
   ```

---

## 📝 Exemples d'Utilisation

### 1. Générer un README de Profil
- **Demande** : *"Génère un README pour mon profil GitHub avec mes projets et mes compétences."*
- **Résultat** : Un README basé sur les données de la base SQLite (`profile`, `projects`, `skills`).

### 2. Générer un README de Projet
- **Demande** : *"Génère un README pour mon projet en analysant les fichiers du repository."*
- **Résultat** : Un README basé sur la structure et le contenu des fichiers du projet.

### 3. Modifier un README Existant
- **Demande** : *"Ajoute une section 'Fonctionnalités' au README actuel."*
- **Résultat** : Le README est mis à jour avec la nouvelle section.

---

## 🤖 Agents IA

### 1. **Agent Repository**
- **Rôle** : Génère un README de projet à partir des fichiers du repository.
- **Outils** : `list_repo_tree()`, `read_text_file()`.
- **Stratégie** :
  - Liste les fichiers du repository.
  - Lit les fichiers clés (`README.md`, `requirements.txt`, `Dockerfile`, etc.).
  - Déduit la stack technique, les commandes d'installation, et la structure du projet.

### 2. **Agent Profil**
- **Rôle** : Génère un README de profil à partir des données SQLite.
- **Outils** : `get_profile_data()` (interrogation de la base de données).
- **Stratégie** :
  - Récupère les informations personnelles, compétences, projets et liens.
  - Structure le README avec une introduction, une stack technique, et une liste de projets.

### 3. **Router**
- **Rôle** : Détermine quel agent utiliser en fonction de la demande utilisateur.
- **Logique** : Défini dans `src/router_chain.py`.

---

## 📌 Roadmap
- [ ] Ajouter la génération de **CV** et **lettres de motivation**.
- [ ] Intégrer **GitHub Actions** pour automatiser les mises à jour du README.
- [ ] Supporter d'autres formats (PDF, HTML) pour le README.
- [ ] Ajouter un **mode batch** pour générer plusieurs README en une seule fois.

---

## 📬 Contact
Pour toute question ou suggestion, n'hésitez pas à ouvrir une **issue** ou à me contacter directement :
- **GitHub** : [AlexandreCrestien](https://github.com/AlexandreCrestien)
- **Email** : alexandre.crestien@gmail.com