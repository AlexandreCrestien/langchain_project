Here is the final Markdown for your project's README:

```markdown
# README Agent - Automatisation de Génération de README

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![LangChain](https://img.shields.io/badge/LangChain-0.1+-green.svg)
![Streamlit](https://img.shields.io/badge/Streamlit-1.29+-red.svg)

---

## 📌 Description

Ce projet est une application **Streamlit** qui automatise la génération et la maintenance de fichiers **README** pour des projets GitHub ou des profils GitHub. Il utilise des **agents IA** (via LangChain et Mistral) pour analyser le repository ou une base de données SQLite, et produire un README structuré et à jour.

L'application permet de :
- **Générer un README** à partir des fichiers du repository ou d'une base de données de profil.
- **Modifier incrémentalement** un README existant via une interface de chat.
- **Écrire et pousser** le README généré directement sur GitHub.

---

## 🛠 Tech Stack

| Catégorie       | Technologies                                                                 |
|-----------------|------------------------------------------------------------------------------|
| **Backend**     | Python, LangChain, Mistral AI, SQLite                                        |
| **Frontend**    | Streamlit                                                                    |
| **Outils**      | GitHub CLI (`gh`), `python-dotenv`, `chromadb` (pour extensions futures)     |
| **Déploiement** | Docker (optionnel), GitHub Actions (optionnel)                               |

---

## 📂 Structure du Projet

```plaintext
.
├── app/
│   └── Home.py                  # Point d'entrée Streamlit
├── data/
│   └── cv.sqlite3               # Base de données SQLite (profil, projets, skills)
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
│   ├── config.py                # Configuration (clés API)
│   ├── router_chain.py          # Routage automatique entre profil et repository
│   ├── tools_db.py              # Outils pour interroger la base de données
│   ├── tools_github.py          # Outils pour écrire/commiter/pusher le README
│   ├── tools_repo.py            # Outils pour lister/lire les fichiers du repo
│   ├── ui/
│   │   ├── layout.py            # Interface principale (chat + éditeur)
│   │   └── sidebar.py           # Barre latérale (contrôles)
│   └── utils/
│       └── paths.py             # Gestion des chemins du projet
├── skills/                      # Compétences personnalisées pour les agents
│   └── github_readme/
│       ├── SKILL.md
│       ├── repo_readme.md
│       └── templates/
│           └── readme_main.md
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
- **Demande** : *"Génère un README pour mon profil GitHub avec mes projets et mes skills."*
- **Résultat** : Un README basé sur les données de la base SQLite (`profile`, `projects`, `skills`).

### 2. Générer un README de Projet
- **Demande** : *"Génère un README pour mon projet en analysant les fichiers du repository."*
- **Résultat** : Un README basé sur la structure et le contenu des fichiers du projet.

### 3. Modifier un README Existant
- **Demande** : *"Ajoute une section 'Fonctionnalités' au README actuel."*
- **Résultat** : Le README est mis à jour avec la nouvelle section.

---

## 🔧 Configuration de la Base de Données

La base de données SQLite (`data/cv.sqlite3`) contient les tables suivantes :
- `profile` : Informations personnelles (nom, headline, description, etc.).
- `link` : Liens (GitHub, LinkedIn, email, etc.).
- `skill` : Compétences (nom, catégorie, niveau).
- `project` : Projets (nom, description, stack, URL GitHub).

Pour modifier les données :
1. Utilisez `scripts/seed_db.py` pour peupler la base.
2. Modifiez directement le fichier `seed_db.py` pour ajouter/supprimer des entrées.

---

## 🤖 Agents IA

### 1. **Agent Profil**
- **Rôle** : Génère un README de profil à partir des données SQLite.
- **Outils** : `get_profile_data()`.
- **Prompt** : Défini dans `src/chat/prompts.py` (`SYSTEM_RULES`).

### 2. **Agent Repository**
- **Rôle** : Génère un README de projet à partir des fichiers du repository.
- **Outils** : `list_repo_tree()`, `read_text_file()`.
- **Prompt** : Défini dans `src/chat/prompts.py` (`SYSTEM_RULES_REPO`).

### 3. **Router**
- **Rôle** : Détermine quel agent utiliser en fonction de la demande utilisateur.
- **Logique** : Défini dans `src/router_chain.py`.

---

## 📌 Roadmap
- [ ] Ajouter la génération de **CV** et **lettres de motivation**.
- [ ] Intégrer **GitHub Actions** pour automatiser les mises à jour du README.
- [ ] Ajouter un **mode batch** pour générer plusieurs README en une seule fois.
- [ ] Supporter d'autres formats (PDF, HTML) pour le README.

---

## 📬 Contact
Pour toute question ou suggestion, n'hésitez pas à ouvrir une **issue** ou à me contacter directement :
- **GitHub** : [AlexandreCrestien](https://github.com/AlexandreCrestien)
- **Email** : alexandre.crestien@gmail.com
```