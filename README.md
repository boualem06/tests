# Realtime Election Voting System

This repository contains the code for a realtime election voting system. The system is built using Python, Kafka, Spark Streaming, Postgres, and Streamlit. The system utilizes Docker Compose to easily spin up the required services in Docker containers.

---

## System Components
- **`main.py`**: 
  - Creates the required tables in Postgres (`candidates`, `voters`, and `votes`).
  - Sets up the Kafka topic and creates a copy of the `votes` table in the Kafka topic.
  - Contains the logic to consume votes from Kafka and produce data to the `voters_topic` on Kafka.

- **`voting.py`**: 
  - Consumes votes from the Kafka topic (`voters_topic`).
  - Generates voting data and produces data to the `votes_topic` on Kafka.

- **`spark-streaming.py`**: 
  - Consumes votes from the Kafka topic (`votes_topic`).
  - Enriches the data using Postgres and aggregates the votes.
  - Produces aggregated data to specific topics on Kafka.

- **`streamlit-app.py`**: 
  - Consumes aggregated voting data from Kafka and Postgres.
  - Displays the voting data in realtime using Streamlit.

---

### Prerequisites
- Python 3.9 or above installed on your machine.
- Docker Compose installed on your machine.
- Docker installed on your machine.

---

### Steps to Run
1. Clone this repository:
   ```bash
   git clone <repository-url>
   cd <repository-folder>```

2. Start the services using the following command:
   ```bash
   docker compose up -d
```
3. Install the required Python packages using the following command:
```bash
  pip install -r requirements.txt
```

4.Creating the required tables on Postgres and generating voter information on Kafka topic:
```bash
  python main.py
```

5. Consuming the voter information from Kafka topic, generating voting data and producing data to Kafka topic:
```bash
  python voting.py
```

6.Consuming the voting data from Kafka topic, enriching the data from Postgres and producing data to specific topics on Kafka:
```bash
  python spark-streaming.py
```

7. Running the Streamlit app:
   ```bash
  streamlit run streamlit-app.py
```






















