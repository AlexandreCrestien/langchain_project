```markdown
# LangChain Project : Générateur README Automatisé (Agent IA)

**Agent IA pour générer et maintenir des README GitHub de manière autonome**

📌 **Projet en cours de formation Simplon (Dev IA | Python • LangChain • Streamlit)**

---

## 🎯 Description
Ce projet est un **agent IA** qui génère et met à jour automatiquement des **README GitHub** (profil ou projet) à partir :
- Du contenu d'un repository (fichiers, structure, dépendances).
- D'une base de données SQLite (`cv.sqlite3`) pour les informations de profil, compétences et projets.

L'agent est conçu pour être **sécurisé** (lecture seule) et **modulaire**, avec une interface **Streamlit** pour interagir avec l'utilisateur.

---

## ✨ Fonctionnalités
- **Génération de README** :
  - README de **profil GitHub** (basé sur les données SQLite).
  - README de **projet** (basé sur l'analyse du repository).
- **Automatisation** :
  - Détection automatique de la stack technique (Python, Django, LangChain, etc.).
  - Identification des projets clés et de leur stack.
  - Génération de sections structurées (Installation, Usage, Configuration, etc.).
- **Interface utilisateur** :
  - Chatbot Streamlit pour guider la génération.
  - Éditeur intégré pour prévisualiser et modifier le README avant validation.
- **Sécurité** :
  - **Pas d'écriture de fichiers** ni de **commit/push** automatisés (contrôlé par l'utilisateur via l'UI).
  - Outils **read-only** pour analyser le repository (`list_repo_tree`, `read_text_file`).

---

## 🛠️ Stack Technique
- **Backend** :
  - Python (Avancé)
  - LangChain / DeepAgents (pour l'orchestration de l'agent IA)
  - LangGraph (pour la gestion des états et des workflows)
  - Mistral AI (modèle LLM utilisé pour la génération de contenu)
- **Base de données** :
  - SQLite (pour stocker les informations de profil, compétences et projets)
- **Frontend** :
  - Streamlit (interface utilisateur)
- **Outils** :
  - `list_repo_tree` et `read_text_file` (pour analyser le repository)
  - `subprocess` (pour interagir avec GitHub CLI en toute sécurité, désactivé par défaut)
- **Déploiement** :
  - Docker (optionnel, pour containeriser l'application)

---

## 📦 Installation
### Prérequis
- Python 3.10+
- Git
- Un compte Mistral AI (pour l'API LLM)

### Étapes
1. Cloner le repository :
   ```bash
   git clone https://github.com/AlexandreCrestien/langchain_project.git
   cd langchain_project
   ```

2. Installer les dépendances :
   ```bash
   pip install -r requirements.txt
   ```

3. Configurer les variables d'environnement :
   - Créer un fichier `.env` à partir de `.env.exemple` :
     ```bash
     cp .env.exemple .env
     ```
   - Ajouter votre clé API Mistral dans `.env` :
     ```ini
     MISTRAL_API_KEY=votre_clé_api
     ```

4. Initialiser la base de données SQLite :
   ```bash
   python scripts/init_db.py
   python scripts/seed_db.py
   ```

5. Lancer l'application Streamlit :
   ```bash
   streamlit run app/Home.py
   ```

---

## ⚙️ Configuration
### Variables d'environnement
| Variable          | Description                          | Exemple                     |
|-------------------|--------------------------------------|-----------------------------|
| `MISTRAL_API_KEY` | Clé API pour Mistral AI              | `sk-1234567890abcdef`       |

### Structure de la base de données
La base de données SQLite (`data/cv.sqlite3`) contient les tables suivantes :
- `profile` : Informations de profil (nom, headline, description, etc.).
- `link` : Liens (GitHub, LinkedIn, email, etc.).
- `skill` : Compétences (catégorie, niveau, ordre d'affichage).
- `project` : Projets (nom, description, stack, URL GitHub, etc.).

---

## 🚀 Usage
1. Lancer l'application :
   ```bash
   streamlit run app/Home.py
   ```

2. Dans l'interface Streamlit :
   - Décrivez votre demande dans le champ de chat (ex: *"Génère un README pour mon projet"* ou *"Mets à jour mon README de profil GitHub"*).
   - L'agent génère un brouillon de README.
   - Prévisualisez et modifiez le contenu dans l'éditeur intégré.
   - Validez pour enregistrer le README (sans commit/push automatique).

---

## 📂 Structure du Projet
```
langchain_project/
├── app/                          # Interface Streamlit
│   └── Home.py                   # Point d'entrée de l'application
├── data/                         # Base de données SQLite
│   └── cv.sqlite3                # Fichier de la base de données
├── scripts/                      # Scripts utilitaires
│   ├── init_db.py                # Initialise la base de données
│   └── seed_db.py                # Peuple la base de données
├── skills/                       # Compétences et templates pour l'agent
│   └── github_readme/            # Skill dédiée à la génération de README
│       ├── SKILL.md              # Documentation de la skill
│       ├── repo_readme.md        # Stratégie pour les README de projet
│       └── templates/            # Templates Markdown
│           └── readme_main.md    # Template pour le README principal
├── src/                          # Code source de l'agent
│   ├── agent_build.py            # Construction de l'agent (profil)
│   ├── agent_build_repo.py       # Construction de l'agent (projet)
│   ├── chat/                     # Gestion du chat Streamlit
│   │   ├── messages.py           # Messages du chat
│   │   └── state.py              # État de la session
│   ├── config.py                 # Configuration (clés API, etc.)
│   ├── router_chain.py           # Routage des requêtes utilisateur
│   ├── tools_db.py               # Outils pour interagir avec la base de données
│   ├── tools_github.py           # Outils pour interagir avec GitHub (désactivés)
│   └── tools_repo.py             # Outils pour analyser le repository
├── .env                          # Variables d'environnement (à créer)
├── .env.exemple                  # Exemple de fichier .env
├── .gitignore                    # Fichiers ignorés par Git
├── README.md                     # Ce fichier
└── requirements.txt              # Dépendances Python
```

---

## 🧪 Tests
À compléter (ex: tests unitaires pour les outils `list_repo_tree` et `read_text_file`).

---

## 🤝 Contribuer
Les contributions sont les bienvenues ! Voici comment vous pouvez aider :
1. Forkez le projet.
2. Créez une branche pour votre fonctionnalité (`git checkout -b feature/ma-fonctionnalité`).
3. Committez vos modifications (`git commit -m "Ajout de ma fonctionnalité"`).
4. Pushez vers la branche (`git push origin feature/ma-fonctionnalité`).
5. Ouvrez une Pull Request.

---

## 📄 Licence
À compléter (ajoutez un fichier `LICENSE` si nécessaire).
```