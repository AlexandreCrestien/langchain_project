Voici le README final pour le projet **LangChain Agent – Générateur Automatique de README** :

```markdown
# 📄 LangChain Agent – Générateur Automatique de README

**Un agent IA pour générer et maintenir des README professionnels à partir du contenu d'un repository.**

---

## 🎯 Description
Ce projet utilise **LangChain** et **Mistral AI** pour créer un agent capable de :
- **Analyser un repository** (fichiers, structure, dépendances).
- **Générer un README clair et structuré** basé sur le contenu réel du projet.
- **Maintenir automatiquement** le README à jour en fonction des modifications du code.

L'agent est conçu pour être **intégré dans un workflow CI/CD** ou utilisé localement via une interface **Streamlit**.

---

## 🛠️ Stack Technique

### **Backend & IA**
- **Python** (3.10+)
- **LangChain** (Agents, Tools, Runnables)
- **LangGraph** (Orchestration des workflows)
- **Mistral AI** (LLM pour la génération de contenu)
- **DeepAgents** (Framework pour la création d'agents autonomes)

### **Outils & Bibliothèques**
- **SQLite** (Stockage des données de profil)
- **ChromaDB** (Optionnel pour des fonctionnalités RAG avancées)
- **Streamlit** (Interface utilisateur)
- **GitHub CLI (`gh`)** (Intégration GitHub pour le push automatique)
- **Docker** (Optionnel pour le déploiement)

### **Développement & Qualité**
- **Python-dotenv** (Gestion des variables d'environnement)
- **Tests unitaires** (À compléter)
- **Clean Code** (Architecture modulaire, séparation des responsabilités)

---

## 📂 Structure du Projet

```
langchain_project/
├── .env                    # Variables d'environnement (ex: MISTRAL_API_KEY)
├── .env.exemple            # Exemple de configuration
├── .gitignore              # Fichiers ignorés par Git
├── README.md               # Ce fichier (généré automatiquement)
├── requirements.txt        # Dépendances Python
├── app/
│   └── Home.py             # Interface Streamlit (à compléter)
├── data/
│   └── cv.sqlite3          # Base de données SQLite pour les données de profil
├── skills/
│   └── github_readme/      # Templates et règles pour la génération de README
│       ├── SKILL.md        # Documentation de la skill
│       ├── readme_main.md  # Template pour le README de profil
│       └── repo_readme.md  # Template pour le README de projet
├── src/
│   ├── agent_build.py      # Construction de l'agent pour le README de profil
│   ├── agent_build_repo.py # Construction de l'agent pour le README de projet
│   ├── config.py           # Configuration (chargement des variables d'environnement)
│   ├── router_chain.py     # Routage des requêtes vers le bon agent
│   ├── tools_db.py         # Outils pour interagir avec la base de données SQLite
│   ├── tools_github.py     # Outils pour écrire et pousser le README sur GitHub
│   └── tools_repo.py       # Outils pour analyser le repository (list_repo_tree, read_text_file)
```

---

## ⚙️ Installation

### Prérequis
- Python 3.10+
- Git
- Un compte Mistral AI (pour l'API)

### Étapes
1. Cloner le repository :
   ```bash
   git clone https://github.com/AlexandreCrestien/langchain-project.git
   cd langchain-project
   ```

2. Installer les dépendances :
   ```bash
   pip install -r requirements.txt
   ```

3. Configurer les variables d'environnement :
   - Copier `.env.exemple` vers `.env` :
     ```bash
     cp .env.exemple .env
     ```
   - Ajouter votre clé API Mistral dans `.env` :
     ```ini
     MISTRAL_API_KEY=votre_clé_api
     ```

4. (Optionnel) Initialiser la base de données SQLite pour les données de profil :
   ```bash
   sqlite3 data/cv.sqlite3 < data/schema.sql
   ```

---

## 🚀 Usage

### Générer un README pour un projet
1. Lancer l'agent pour analyser le repository :
   ```python
   from src.router_chain import readme_auto_chain

   user_request = "Génère un README pour ce projet."
   result = readme_auto_chain.invoke({"user_request": user_request})
   print(result)  # Affiche le Markdown du README généré
   ```

2. (Optionnel) Écrire et pousser le README sur GitHub :
   ```python
   from src.tools_github import write_readme, git_commit_push_readme

   write_readme(result)  # Écrit le README dans le fichier README.md
   git_commit_push_readme("Update README via agent")  # Commit et push
   ```

### Lancer l'interface Streamlit
```bash
streamlit run app/Home.py
```

---

## 🔧 Configuration

### Variables d'environnement
| Variable          | Description                          | Exemple                     |
|-------------------|--------------------------------------|-----------------------------|
| `MISTRAL_API_KEY` | Clé API pour Mistral AI              | `mistral-1234567890abcdef`  |

### Fichiers clés
- **`requirements.txt`** : Liste des dépendances Python.
- **`data/cv.sqlite3`** : Base de données SQLite pour les données de profil (optionnel).
- **`skills/github_readme/`** : Templates et règles pour la génération de README.

---

## 🧪 Tests
À compléter.
*Exemple de commande pour lancer les tests (une fois implémentés) :*
```bash
pytest tests/
```

---

## 📜 Licence
À compléter.
*Exemple : MIT, Apache 2.0, etc.*

---

## 🤝 Contribuer
Les contributions sont les bienvenues ! Voici comment vous pouvez aider :
1. Forker le projet.
2. Créer une branche pour votre fonctionnalité (`git checkout -b feature/ma-fonctionnalité`).
3. Committer vos modifications (`git commit -m "Ajout de ma fonctionnalité"`).
4. Pusher la branche (`git push origin feature/ma-fonctionnalité`).
5. Ouvrir une Pull Request.

---

## 📬 Contact
- **GitHub** : [github.com/AlexandreCrestien](https://github.com/AlexandreCrestien)
- **LinkedIn** : [linkedin.com/in/alexandre-crestien](https://www.linkedin.com/in/alexandre-crestien/)
- **Email** : [alexandre.crestien@gmail.com](mailto:alexandre.crestien@gmail.com)
```