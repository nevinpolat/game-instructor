# 🎮 Game4Every1

Welcome to **Game4Every1**, a comprehensive web application designed to help users explore, analyze, and interact with a vast collection of games. Whether you're looking to discover new games, understand their mechanics, or analyze user feedback, Game4Every1 provides the tools you need.


## 🚀 Features

- **User Registration & Login**: Create a profile or log in with your username.
- **Ask Questions**: Get insights, rules, strategies, and more about various games.
- **Comprehensive Analytics Dashboard**: Analyze user data, feedback, game searches, and more.
- **Search Performance Metrics**: Evaluate the effectiveness of different search methods.
- **Chat History Management**: Keep track of your interactions and feedback.

## 🛠️ Technologies Used

- **Backend**:
  - Python 3.11
  - SQLAlchemy
  - PostgreSQL
  - Weaviate (Vector Database)
  - OpenAI GPT-4o-mini
- **Frontend**:
  - Streamlit
  - Plotly
- **Others**:
  - Docker & Docker-Compose
  - Sentence Transformers
  - Conda

## 🗂️ Code Structure

The project follows a modular structure, with each file serving a specific purpose.

```
game-instructor/
├── app.py                # Main application entry point
├── analytics.py    # Analytics dashboard implementation
├── define_schema.py        # Weaviate schema definition
├── ingest_games.py   # ingest game data into Weaviate
├── models.py               # SQLAlchemy ORM models
├── rag_flow.py      #rag using Weaviate and GPT-4o-mini
├── requirements.txt   # List of required dependencies
├── Dockerfile    # Dockerfile to build the image
├── docker-compose.yml      # Docker-Compose config.
├── .streamlit/        
│   └── secrets.toml    # OpenAI keys
├── data/                # Main data file
|   └── game-dataset.csv    
└── README.md               # Documentation file
```

## 🔧 Prerequisites

Before you begin, ensure you have the following installed:

- **Conda**: [Install Conda](https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html)
- **Docker**: [Install Docker](https://docs.docker.com/get-docker/)
- **Docker-Compose**: [Install Docker-Compose](https://docs.docker.com/compose/install/)
- **Git**: [Install Git](https://git-scm.com/downloads)
- **Streamlit Secrets Configuration**: You'll need to set up your `streamlit` secrets for database and OpenAI API keys.

## 📂 Installation

### 1. Clone the Repository

Clone the repository to your local machine:

```bash
git clone https://github.com/yourusername/game4every1.git
cd game4every1
```

### 2. Set Up Conda Environment

Create a Conda environment for managing dependencies.

1. **Create the Conda Environment**:

   ```bash
   conda create -n game4every1_env python=3.11
   ```

2. **Activate the Environment**:

   ```bash
   conda activate game4every1_env
   ```

### 3. Configure Environment Variables

Create a `.env` file in the root directory to store your environment variables.

```bash
touch .env
```

Add the following variables to the `.env` file:

```env
# Database Configuration
DB_USER=your_db_username
DB_PASSWORD=your_db_password
DB_NAME=game4every1_db
DB_HOST=db
DB_PORT=5432

# Weaviate Configuration
WEAVIATE_URL=http://weaviate:8080

# OpenAI API Key
OPENAI_API_KEY=your_openai_api_key
```

Replace placeholders with actual values.

### 4. Install Dependencies

1. **Ensure the Conda Environment is Activated**:

   ```bash
   conda activate game4every1_env
   ```

2. **Install Dependencies**:

   ```bash
   pip install --upgrade pip
   pip install -r requirements.txt
   ```

## 🔑 Database Configuration

### Using Docker-Compose

With Docker-Compose, PostgreSQL service creates `game4every1_db` automatically.

1. **Start Services with Docker-Compose**:

   ```bash
   docker-compose up --build
   ```

2. **Verify Database Creation**:

   ```bash
   docker exec -it game4every1-db psql -U your_db_username -d game4every1_db
   ```

### Running Locally

1. **Install PostgreSQL**:

   - [Download PostgreSQL](https://www.postgresql.org/download/).

2. **Create the Database**:

   ```bash
   psql -U your_db_username -c "CREATE DATABASE game4every1_db;"
   ```

## 🗂️ Streamlit Configuration

### Setting Up `.streamlit`

1. **Create `.streamlit` Directory**:

   ```bash
   mkdir .streamlit
   ```

2. **Add Secrets to `.streamlit/secrets.toml`**:

   ```toml
   [DB]
   USER = "your_db_username"
   PASSWORD = "your_db_password"
   NAME = "game4every1_db"
   HOST = "db"
   PORT = "5432"

   [WEAVIATE]
   URL = "http://weaviate:8080"

   [OPENAI]
   API_KEY = "your_openai_api_key"
   ```

## 🏃 Running the Application

### Running with Docker-Compose

1. **Start Services**:

   ```bash
   docker-compose up --build
   ```

   Access at `http://localhost:8501`.

2. **Stop Services**:

   ```bash
   docker-compose down
   ```

### Running Locally (Without Docker)

1. **Activate Environment**:

   ```bash
   conda activate game4every1_env
   ```

2. **Run Streamlit**:

   ```bash
   streamlit run app.py
   ```

### Running with Docker (Without Compose)

1. **Start PostgreSQL & Weaviate**:

   ```bash
   docker run -d --name game4every1-db -e POSTGRES_USER=your_db_username ...
   docker run -d --name weaviate -p 8080:8080 semitechnologies/weaviate:latest
   ```

2. **Run the Application**:

   ```bash
   docker run -p 8501:8501 game4every1-app
   ```

## 📊 Ingesting Data

1. **Ensure Weaviate is Running**.

2. **Run Ingestion**:

   ```bash
   python ingest_games.py
   ```

## 🛡️ Security Considerations

- **Environment Security**: Secure sensitive data in `.env`.
- **API Keys**: Do not hardcode API keys.

## ❓ Troubleshooting

- **Connection Issues**: Verify Weaviate and PostgreSQL URLs.
- **Docker Failures**: Rebuild with `docker-compose up --build`.

## 📄 License

MIT License.
