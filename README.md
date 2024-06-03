# Source-Code-Analysis-using-GenAI

# How to run?
### STEPS:

Clone the repository

```bash
Project repo: https://github.com/
```
### STEP 01- Create a conda environment after opening the repository

```bash
conda create -n llmapp python=3.8 -y
```

```bash
conda activate llmapp
```


### STEP 02- install the requirements
```bash
pip install -r requirements.txt
```


### Create a `.env` file in the root directory and add your OPENAI_API_KEY credentials as follows:

```ini
OPENAI_API_KEY = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
```


```bash
# Finally run the following command
python app.py
```

Now,
```bash
open up localhost:
```


# Explanation:

# GitHub Repository QA System

This project is a powerful integration of multiple technologies and tools for analyzing and interacting with GitHub repositories. It allows users to input a GitHub repository URL and ask questions about the repository. The system processes the repository's content and provides relevant answers based on the repository's data.

## Technologies Used

- **Flask**: Web framework for serving the user interface and handling requests.
- **LangChain**: Framework for combining language models with a memory system and a retriever to provide coherent answers.
- **Chroma**: Vector database for storing and retrieving embeddings.
- **OpenAI Embeddings**: Pre-trained embeddings from OpenAI for document representation.
- **GitPython**: Library for interacting with Git repositories.


![![Screenshot 2024-06-03 194818](https://github.com/adityach007/Source-Code-Analysis-using-LLM/assets/108794914/26544dfd-c4eb-4718-a1ef-876e22771f69)]




## User Interface

The user interface consists of a simple HTML page (`index.html`) served by Flask. The user can input a GitHub repository URL and ask questions about the repository.

## Flask Server (`app.py`)

The Flask server handles user requests and serves the interface. It includes two main routes:

- `/chatbot`: Handles POST requests with a GitHub repository URL.
- `/get`: Handles POST requests with user messages for the chatbot.

### Chatbot Route (`/chatbot`)

1. **Accepts Repository URL**: The user submits a GitHub repository URL.
2. **Calls `repo_ingestion`**: The `repo_ingestion` function in `helper.py` is called to clone the repository.
3. **Calls `store_index.py`**: This script processes the cloned repository to prepare it for question-answering by performing the following steps:
    - **Load Repo Files**: Uses `GenericLoader` to load Python files from the cloned repository.
    - **Text Splitter**: Splits the loaded files into smaller chunks for better processing.
    - **Load Embeddings**: Loads pre-trained embeddings from OpenAI.
    - **Store Vectors**: Stores the processed vectors in a vector database (Chroma).

### Get Route (`/get`)

1. **Accepts User Message**: The user submits a question about the repository.
2. **Processes Message with QA Chain**: Uses the `ConversationalRetrievalChain` to process the user's question. This chain retrieves relevant information from the vector database and generates an answer.

## Helper Functions (`helper.py`)

- **`repo_ingestion`**: Clones the provided GitHub repository into a local directory.
- **`load_repo`**: Loads the cloned repository's files into documents.
- **`text_splitter`**: Splits the loaded documents into smaller chunks.
- **`load_embedding`**: Loads pre-trained embeddings for the documents.

## Store Index Script (`store_index.py`)

This script prepares the repository files for the QA system:

1. Loads the repository files.
2. Splits the text into manageable chunks.
3. Loads embeddings for the chunks.
4. Stores the embeddings in a vector database (Chroma) for later retrieval during QA.

## Conversational Retrieval Chain

This component of LangChain combines language models with a memory system and a retriever to provide coherent answers based on the repository's content.

## Workflow

### User Interaction

1. User opens the web interface and submits a GitHub repository URL.
2. User asks questions about the repository.

### Repository Processing

1. Flask server handles the URL submission, calls `repo_ingestion` to clone the repository, and runs `store_index.py` to prepare the data.
2. `store_index.py` loads, splits, and embeds the repository's content, storing it in a vector database.

### Question Answering

1. Flask server handles user questions, using the QA chain to retrieve and generate answers based on the processed repository data.

### Response

The system returns the answer to the user's question, displayed in the web interface.

# Future Uses

### Code Review Assistance

- **Automated Reviews**: Enhance the system to perform automated code reviews, providing suggestions for improvements, detecting potential bugs, and ensuring coding standards are met.
- **Collaborative Reviews**: Integrate with platforms like GitHub to assist in collaborative code reviews by summarizing changes and providing insights.

### Developer Documentation

- **Generate Documentation**: Automatically generate documentation from code comments and docstrings, helping maintain up-to-date and comprehensive documentation.
- **Interactive Docs**: Allow developers to interactively ask questions about the codebase and receive explanations and usage examples.

### Onboarding New Developers

- **Learning Tool**: Serve as an educational tool for new developers to understand the architecture, design patterns, and implementation details of a project.
- **Guided Tours**: Provide guided tours of the codebase, highlighting key components and their interactions.

### Codebase Search

- **Enhanced Search**: Enable advanced search capabilities within the codebase, allowing developers to find specific functions, classes, or patterns quickly.
- **Contextual Search**: Offer context-aware search results, showing not only the code snippets but also related documentation and usage examples.

### Legacy Code Understanding

- **Refactoring Support**: Assist in understanding and refactoring legacy code by providing summaries, detecting code smells, and suggesting modern alternatives.
- **Migration Assistance**: Help in migrating codebases to new technologies or frameworks by identifying dependencies and suggesting migration paths.

## Support

If you like this project, please follow and give a star ⭐!
