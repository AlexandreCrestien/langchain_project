Voici le README mis à jour pour refléter l'architecture du projet, ses fonctionnalités et son utilisation :

```markdown
# 🧠 README Agent - Générateur Automatique de README

Un agent IA qui génère et met à jour automatiquement des **README** pour des profils GitHub ou des projets, en analysant la structure du repository et les données métiers.

---

## 🔍 Fonctionnalités

✅ **Analyse automatique du repository** :
- Exploration des fichiers (`.py`, `.md`, `.txt`, etc.)
- Détection des technologies utilisées (via `requirements.txt`, `Pipfile`, etc.)
- Ignore les fichiers binaires et les dossiers sensibles (`.git`, `venv`, etc.)

✅ **Génération de README structurés** :
- **Profil GitHub** : Présentation personnelle, compétences, projets destacados, liens.
- **Projet** : Description, stack technique, installation, utilisation, exemples.

✅ **Intégration avec GitHub** :
- Écriture du fichier `README.md` localement.
- Commit et push automatique via `gh` (GitHub CLI).

✅ **Interface Streamlit** :
- Chat interactif pour guider la génération.
- Éditeur intégré pour prévisualiser et modifier le README avant validation.

✅ **Base de données SQLite** :
- Stockage des données métiers (profil, compétences, projets, liens).
- Scripts d’initialisation et de seeding pour une configuration rapide.

---

## 🛠 Stack Technique

| Catégorie       | Technologies                                                                 |
|-----------------|------------------------------------------------------------------------------|
| **Backend**     | Python, LangChain, DeepAgents, Mistral AI                                    |
| **Frontend**    | Streamlit                                                                   |
| **Base de données** | SQLite (via `sqlite3`)                                                    |
| **DevOps**      | Docker (optionnel), GitHub CLI (`gh`)                                        |
| **Outils**      | `python-dotenv` (gestion des variables d’environnement)                     |

---

## 📂 Structure du Projet

```
.
├── .env                    # Variables d’environnement (ex: `MISTRAL_API_KEY`)
├── .env.exemple            # Exemple de fichier `.env`
├── .gitignore              # Fichiers et dossiers ignorés par Git
├── README.md               # Ce fichier (généré automatiquement)
├── app/
│   └── Home.py             # Point d’entrée Streamlit (interface utilisateur)
├── data/
│   └── cv.sqlite3          # Base de données SQLite (profil, compétences, projets)
├── requirements.txt        # Dépendances Python
├── scripts/
│   ├── init_db.py          # Initialisation de la base de données
│   └── seed_db.py          # Peuplement initial des données (profil, compétences, etc.)
├── skills/                 # Compétences personnalisées pour l’agent
│   └── github_readme/
│       ├── SKILL.md        # Documentation de la compétence
│       ├── repo_readme.md  # Template pour les README de projet
│       └── templates/
│           └── readme_main.md  # Template pour les README de profil
└── src/
    ├── agent_build.py      # Construction de l’agent DeepAgents
    ├── config.py           # Configuration (chargement des variables d’environnement)
    ├── router_chain.py     # Logique de routage des requêtes utilisateur
    ├── tools_db.py         # Outils pour interagir avec la base de données
    ├── tools_github.py     # Outils pour interagir avec GitHub (écriture, commit, push)
    ├── tools_repo.py       # Outils pour analyser le repository (fichiers, structure)
    └── ui/                 # Composants Streamlit (sidebar, layout, chat)
        ├── layout.py
        └── sidebar.py
```

---

## ⚙️ Installation

### Prérequis
- Python 3.10+
- GitHub CLI (`gh`) configuré pour les commits/pushs automatiques.
- Clé API Mistral (pour l’agent IA).

### Étapes

1. **Cloner le repository** :
   ```bash
   git clone https://github.com/AlexandreCrestien/readme-agent.git
   cd readme-agent
   ```

2. **Configurer l’environnement** :
   ```bash
   cp .env.exemple .env
   ```
   - Remplir `.env` avec ta clé API Mistral (`MISTRAL_API_KEY`).

3. **Installer les dépendances** :
   ```bash
   pip install -r requirements.txt
   ```

4. **Initialiser la base de données** :
   ```bash
   python scripts/init_db.py
   python scripts/seed_db.py
   ```

5. **Lancer l’application Streamlit** :
   ```bash
   streamlit run app/Home.py
   ```

---

## 🚀 Utilisation

1. **Accéder à l’interface** :
   - Ouvre `http://localhost:8501` dans ton navigateur.

2. **Décrire ta demande** :
   - Exemple pour un **README de profil GitHub** :
     ```
     "Génère un README pour mon profil GitHub. Je suis en formation Simplon, je travaille sur des projets Python/Django et LangChain."
     ```
   - Exemple pour un **README de projet** :
     ```
     "Génère un README pour mon projet d’assistant RAG. Le projet utilise LangChain, ChromaDB et Mistral."
     ```

3. **Valider le brouillon** :
   - Modifie le contenu dans l’éditeur intégré si nécessaire.
   - Clique sur **"Push to GitHub"** pour commiter et pousser le README.

---

## 📝 Exemples de README Générés

### 1. README de Profil GitHub
[Voir le README actuel](#) (celui-ci est un exemple !).

### 2. README de Projet
```markdown
# 🤖 Assistant RAG - Recherche dans Documents Internes

Un assistant IA pour retrouver des procédures et résolutions d’incidents via **recherche vectorielle**.

---

## 🔧 Stack Technique
- **Backend** : Python, LangChain
- **Vector Store** : ChromaDB
- **Modèle** : Mistral (via API)
- **Base de données** : SQLite (pour les métadonnées)

---

## ⚙️ Installation
```bash
git clone https://github.com/ton-utilisateur/assistant-rag.git
cd assistant-rag
pip install -r requirements.txt
```

---

## 🚀 Utilisation
```python
from langchain.chains import RetrievalQA
from langchain.vectorstores import Chroma

# Charger le vector store
vectorstore = Chroma(persist_directory="data/chroma")

# Créer l’assistant
qa_chain = RetrievalQA.from_chain_type(
    llm=mistral_llm,
    chain_type="stuff",
    retriever=vectorstore.as_retriever()
)

# Poser une question
response = qa_chain.run("Comment résoudre l’erreur 500 ?")
print(response)
```

---

## 📂 Structure du Projet
```
.
├── data/
│   ├── chroma/            # Vector store ChromaDB
│   └── documents/         # Documents sources (PDF, TXT, etc.)
├── src/
│   ├── ingest.py          # Script d’ingestion des documents
│   └── query.py           # Script de requêtage
└── requirements.txt
```

---

## 📌 Roadmap
- [ ] Ajouter une interface Streamlit.
- [ ] Supporter d’autres formats de documents (Word, Excel).
- [ ] Améliorer le chunking pour des réponses plus précises.
```

---

## 🛠 Personnalisation

### 1. Modifier les templates
Les templates de README sont stockés dans `skills/github_readme/templates/` :
- `readme_main.md` : Template pour les README de profil.
- `repo_readme.md` : Template pour les README de projet.

### 2. Ajouter des données métiers
- Modifie `scripts/seed_db.py` pour mettre à jour ton profil, tes compétences ou tes projets.
- Exécute `python scripts/seed_db.py` pour appliquer les changements.

### 3. Configurer GitHub CLI
Assure-toi que `gh` est configuré pour éviter les prompts lors des commits :
```bash
gh auth login
gh config set git_protocol https
```

---

## 🤝 Contribuer
Les contributions sont les bienvenues ! Voici comment tu peux aider :
1. **Signaler des bugs** ou suggérer des améliorations via les [issues GitHub](https://github.com/AlexandreCrestien/readme-agent/issues).
2. **Proposer des templates** pour d’autres types de README (CV, documentation technique, etc.).
3. **Améliorer l’agent** :
   - Ajouter des outils pour analyser d’autres fichiers (ex: `package.json` pour les projets Node.js).
   - Intégrer d’autres modèles d’IA (ex: Ollama, OpenAI).

---

## 📄 Licence
Ce projet est sous licence **MIT**. Voir le fichier [LICENSE](LICENSE) pour plus de détails.

---

*Dernière mise à jour : {{date}}*
*Généré automatiquement par [README Agent](https://github.com/AlexandreCrestien/readme-agent).*
```