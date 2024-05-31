# Compas Assistant
Template de Compas Assistant: https://github.com/DenezG/compas-assistant.git
<br/>
<br/>


## Rapide Setup

### 1. Clone repo
```shell
git clone https://github.com/DenezG/compas_assistant_langchain_python_ragV3.5.git
cd .\compas_assistant_langchain_python_ragV3.5\
```

### 2. Configurer votre [OpenAI API key](https://platform.openai.com/api-keys)
```shell
OPENAI_API_KEY = 'sk-proj-...'
ASSISTANT_ID = 'asst_...'
```
(Dans un fichier `.env.local` que vous devez créer).

### 3. Install dependencies
```shell
npm install
```

### 4. Run
```shell
npm run dev
```

### 5. Naviger à [http://localhost:3000](http://localhost:3000).

## Overview

Ce projet représente un assistant Openai qui utilise les données du compas afin de répondre au questions des utilisateurs.
Nous vous conseillons d'utiliser la page 'Chat avec Images' car c'est la plus avancée et elle regroupe les fonctionnalités des deux autres pages.


### Main Components

- `app/components/chat.tsx` - handles chat rendering, [streaming](https://platform.openai.com/docs/assistants/overview?context=with-streaming), and [function call](https://platform.openai.com/docs/assistants/tools/function-calling/quickstart?context=streaming&lang=node.js) forwarding
- `app/components/file-viewer.tsx` - handles uploading, fetching, and deleting files for [file search](https://platform.openai.com/docs/assistants/tools/file-search)

### Endpoints

- `api/assistants` - `POST`: create assistant (only used at startup)
- `api/assistants/threads` - `POST`: create new thread
- `api/assistants/threads/[threadId]/messages` - `POST`: send message to assistant
- `api/assistants/threads/[threadId]/actions` - `POST`: inform assistant of the result of a function it decided to call
- `api/assistants/files` - `GET`/`POST`/`DELETE`: fetch, upload, and delete assistant files for file search
- `api/assistants/image` - `POST` : fetch an image by using the fileId of the image


# Python Langchain RAG Setup

## Créer un environnement virtuel Python à la base de votre projet
```sh
cd..
python -m venv lang_rag
cd lang_rag
.\Scripts\Activate.ps1
```

## Importer les fichiers du projet
```sh
git clone https://github.com/DenezG/python_rag.git
```
Déplacer manuellement les fichiers et dossiers contenues dans python_rag à l'intérieur de lang_rag car sinon l'environnement ne retrouvera pas les fichiers

## Installer les dépendances
L'installation des modules peut prendre plusieurs minutes :

```sh
pip install -r requirements.txt
```

## Ajouter vos documents
Ajoutez vos documents .xls dans le dossier data. Les fichiers .xlsm semblent moins pertinents.

On ne peut ajouter qu'un type de fichier, on ne peut pas ajouter des pdf et des xlsx il faut faire un choix,
pour changer vers pdf il y a des commentaire explicatif dans populate_database.py

## Installer Ollama et le langage embedding souhaité
Rendez-vous sur Ollama pour l'installation: https://ollama.com/ 

Exemple d'installation de l'embedding nomic-embed-text :
```sh
ollama pull nomic-embed-text
```
Lancez le logiciel Ollama

## Créer la base de données
```sh
python .\populate_database.py --reset
```
L'option '--reset' permet de supprimer les données existantes de la base de données.

## Pour voir les résultats d'une requête dans le terminal :

```sh
python query_data.py "Bonjour"
```

## Lancer le serveur API
```sh
uvicorn backend:app --reload
```

## Accéder aux résultats
Par défaut, si vous n'avez pas changé l'adresse uvicorn, le résultat est disponible ici :
http://127.0.0.1:8000/query/
