Health Chatbot with Retrieval-Augmented Generation (RAG)
This project is an intelligent, locally-run Health Chatbot built with Python. It uses a Retrieval-Augmented Generation (RAG) pipeline to provide safe, accurate, and context-aware answers to health-related questions. The user interface is built with Gradio, providing an easy-to-use platform for interaction and knowledge base management.

Demo
(This GIF shows the user asking the question "What is a healthy diet?". The chatbot, using its internal knowledge, provides a detailed answer and displays the source of the information as the base AI model since the question was not in its FAQ database. The confidence score is also shown.)

✨ Features
Retrieval-Augmented Generation (RAG): Grounds responses in a factual knowledge base (SQLite) to reduce hallucinations and improve accuracy.

Interactive Web UI: A user-friendly interface built with Gradio that includes a chat window and a knowledge base management tab.

Dynamic Knowledge Base: Easily add new questions and answers to the chatbot's knowledge base directly through the UI. The database automatically updates.

Switchable AI Models: Flexibility to switch between different sizes of the core language model (google/flan-t5-base and google/flan-t5-small) to balance performance and quality.

Customizable Prompts: Choose between different prompt templates ("Cautious Assistant" vs. "Direct Assistant") to change the chatbot's tone and behavior.

Built-in Safety: Includes a disclaimer with every response and uses prompt engineering to prevent providing medical diagnoses.

Smart Feedback Loop: Automatically flags frequently asked questions that aren't in the knowledge base, suggesting them for review and addition.

🛠️ How It Works
The chatbot operates on a RAG pipeline, which ensures that the answers are not just generated from the model's general knowledge but are based on a verified source of information.

Indexing: On startup, all questions in the FAQ database are converted into vector embeddings using a SentenceTransformer model and are stored in memory.

User Query: When a user asks a question, their query is also converted into a vector embedding.

Retrieval: The system performs a cosine similarity search between the user's query embedding and the indexed FAQ embeddings.

Conditional Augmentation:

If a similar question is found in the database (above a confidence threshold), its answer is retrieved and used as the primary context for the language model.

If no similar question is found, the model is informed and uses its general knowledge to answer.

Generation: A carefully crafted prompt, containing the context and the user's question, is sent to the Flan-T5 model, which generates the final, human-readable answer.

🚀 Setup and Installation
To run this project locally, follow these steps:

Clone the Repository

git clone [https://github.com/your-username/health-chatbot.git](https://github.com/your-username/health-chatbot.git)
cd health-chatbot

Create a Virtual Environment

python -m venv venv
source venv/bin/activate  # On Windows, use `venv\Scripts\activate`

Install Dependencies
It is recommended to create a requirements.txt file with the following content:

torch
transformers
sentence-transformers
gradio
numpy

Then, install the packages:

pip install -r requirements.txt

Run the Application
Launch the application by running the Jupyter Notebook (new.ipynb) or by converting it to a Python script and running it. The first time you run the script, it will automatically create and populate the faq_database.db file.

jupyter notebook new.ipynb

Usage
Once the application is running, open the local URL provided by Gradio in your browser.

ChatBot Tab:

Type your health-related question in the input box.

Select a prompt template to define the chatbot's persona.

Click "Submit" to get an answer.

You can also switch the underlying AI model and see the status of the switch.

Manage Knowledge Base Tab:

Add new Question/Answer pairs to the database to expand the chatbot's knowledge.

Refresh the "Pending Review" list to see which questions users have asked frequently that are not yet in the knowledge base.

💻 Technologies Used
Backend: Python

AI/ML: PyTorch, Hugging Face Transformers, Sentence-Transformers

Language Model: Google Flan-T5

Database: SQLite

Web UI: Gradio

