Voici le README final optimisé et mis à jour :

```markdown
# 🧠 README Agent

**Un assistant IA pour générer et maintenir automatiquement des README professionnels à partir de votre repository.**

---

## 📌 Description
Ce projet est une **application Streamlit** qui utilise des **agents IA (LangChain/DeepAgents)** pour :
- Analyser la structure et le contenu d'un repository.
- Générer un **README professionnel** et structuré basé sur les fichiers du projet.
- Permettre une **prévisualisation**, un **téléchargement** et un **push automatique** sur GitHub.

L'application est conçue pour être :
✅ **Modulaire** : Séparation claire entre la logique métier, l'interface utilisateur et les configurations.
✅ **Extensible** : Ajout facile de nouvelles fonctionnalités ou compétences pour les agents.
✅ **Automatisée** : Génération de README en quelques clics, sans écriture manuelle.

---

## 🛠 Stack Technique

### **Backend & IA**
- **Python** (3.10+) – Langage principal.
- **LangChain** & **DeepAgents** – Orchestration des agents IA et gestion des chaînes de traitement.
- **Mistral AI** – Modèle de langage pour la génération de contenu.
- **SQLite** – Base de données locale pour stocker les profils (optionnel).

### **Frontend**
- **Streamlit** – Interface utilisateur simple et interactive.

### **Outils & Bibliothèques**
- **ChromaDB** – Base de données vectorielle pour le RAG (optionnel, pour des fonctionnalités avancées).
- **GitHub CLI (`gh`)** – Pour les opérations Git (commit/push automatiques).
- **Docker** – Conteneurisation (optionnel, pour un déploiement simplifié).

### **Dépendances principales**
```text
deepagents>=0.1.0
langchain>=0.1.0
langgraph>=0.0.30
langchain-mistralai>=0.0.1
langchain-community>=0.0.1
chromadb>=0.4.0
python-dotenv>=1.0.0
streamlit>=1.28.0
```

---

## 🚀 Installation

### **Prérequis**
- Python 3.10 ou supérieur.
- Git installé et configuré.
- GitHub CLI (`gh`) configuré pour les opérations de push.
- Clé API **Mistral AI** (à ajouter dans `.env`).

### **Étapes**
1. Cloner le repository :
   ```bash
   git clone https://github.com/AlexandreCrestien/readme-agent.git
   cd readme-agent
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
     ```env
     MISTRAL_API_KEY=votre_clé_api
     ```

4. Lancer l'application Streamlit :
   ```bash
   streamlit run app/Home.py
   ```

---

## 📂 Structure du Projet
```text
.
├── .env                    # Variables d'environnement (à créer)
├── .env.exemple            # Exemple de fichier .env
├── .gitignore              # Fichiers ignorés par Git
├── README.md               # Ce fichier
├── app/
│   └── Home.py             # Interface Streamlit principale
├── data/
│   └── cv.sqlite3          # Base de données SQLite (optionnel, pour les profils)
├── requirements.txt        # Dépendances Python
├── skills/                 # Compétences des agents IA
│   └── github_readme/
│       ├── SKILL.md        # Documentation de la compétence
│       ├── repo_readme.md  # Template pour le README de projet
│       └── templates/
│           └── readme_main.md  # Template principal pour les README
└── src/
    ├── agent_build.py      # Construction de l'agent IA pour les profils
    ├── agent_build_repo.py # Construction de l'agent IA pour les repositories
    ├── config.py           # Configuration (clés API, etc.)
    ├── router_chain.py     # Routage des requêtes vers les agents
    ├── tools_db.py         # Outils pour interagir avec la base de données
    ├── tools_github.py     # Outils pour GitHub (commit/push)
    └── tools_repo.py       # Outils pour analyser le repository
```

---

## 🔧 Utilisation

### **Interface Streamlit**
1. Lancez l'application avec :
   ```bash
   streamlit run app/Home.py
   ```
2. Dans l'interface :
   - **Écrivez une demande** dans la barre de chat (ex: *"Génère un README pour ce projet"*).
   - **Prévisualisez** le résultat généré.
   - **Téléchargez** le README ou **poussez-le directement sur GitHub** via le bouton "🚀 Push".

### **Fonctionnalités clés**
- **Génération automatique** : L'agent analyse le repository et génère un README structuré et professionnel.
- **Modularité** : Deux agents distincts pour les README de **profil** et de **projet**.
- **Intégration GitHub** : Commit et push automatiques via GitHub CLI.
- **Personnalisation** : Templates modifiables dans `skills/github_readme/templates/`.
- **Extensibilité** : Ajout facile de nouvelles compétences pour les agents.

---

## ⚙️ Configuration

### **Variables d'environnement**
Ajoutez ces variables dans `.env` :
```env
MISTRAL_API_KEY=votre_clé_api_mistral
```

### **Base de données (optionnel)**
- Le fichier `data/cv.sqlite3` est utilisé pour stocker les profils (si vous utilisez l'agent de profil).
- Vous pouvez le remplacer par votre propre base de données ou désactiver cette fonctionnalité en modifiant `src/tools_db.py`.

---

## 🧪 Tests
Aucun test unitaire n'est actuellement configuré. Pour tester manuellement :
1. Lancez l'application avec :
   ```bash
   streamlit run app/Home.py
   ```
2. Testez les fonctionnalités suivantes :
   - Génération d'un README à partir d'une demande utilisateur.
   - Prévisualisation et téléchargement du README.
   - Push automatique sur GitHub (si `gh` est configuré).

---

## 🤝 Contribuer
Les contributions sont les bienvenues ! Pour contribuer :
1. Forkez le projet.
2. Créez une branche pour votre fonctionnalité :
   ```bash
   git checkout -b ma-fonctionnalite
   ```
3. Committez vos modifications :
   ```bash
   git commit -m "Ajout de ma fonctionnalité"
   ```
4. Poussez sur la branche :
   ```bash
   git push origin ma-fonctionnalite
   ```
5. Ouvrez une **Pull Request** sur GitHub.

---

## 📜 Licence
Ce projet est sous licence **MIT**. Voir le fichier [LICENSE](LICENSE) pour plus de détails.
```