**CLINICAL REPORT SIMILARITY FINDER
HI 744 – Text Retrieval & Its Application in Biomedicine
Google Colab Execution**

**Authors:
Atharva Pradeep Vaishnav
Rushikesh Ganesh Deshpande**

**Course: HI 744**
**Execution Environment: Google Colab**

**PROJECT OVERVIEW**
This project implements a clinical report similarity retrieval system that retrieves the most similar clinical case reports given a free-text clinical query. The system compares lexical retrieval (TF-IDF) and semantic retrieval (ClinicalBERT) approaches and evaluates their performance using standard information retrieval metrics. The task is formulated as a document ranking (information retrieval) problem rather than a text classification task. All experiments were developed and executed in Google Colab due to the size of the dataset and GPU requirements.

**IMPORTANT NOTES (PLEASE READ FIRST)**
NGROK TOKEN REQUIREMENT (FOR UI DEMO)
  -To run the Streamlit demo UI inside Google Colab, you must provide an ngrok authentication token.

Steps:
1. Create a free ngrok account at: https://ngrok.com/
2. Copy your ngrok authtoken from the ngrok dashboard.
3. Open the notebook cell number 28
      Replace the placeholder line: "YOUR_NGROK_TOKEN_HERE" with your token 
      eg: !ngrok config add-authtoken 3d...

Note:
Ngrok is required only for the Streamlit UI demo. The core retrieval experiments do NOT require ngrok.

**TASK DESCRIPTION**
**Input**
  -A free-text clinical case report or clinical note (e.g., a patient case description). 
  -Internally, the system also takes a corpus of clinical case reports sampled from the PMC-Patients dataset.

**Output**
  -A ranked list of the top-k most similar clinical case reports from the corpus.
  -Similarity scores for each retrieved report.
  -LLM-generated summary/explanation describing why the retrieved cases are similar to the query.
  -Evaluation metrics comparing retrieval methods:Precision@5 and Recall@5
      
Relevance Definition:
A retrieved document is considered relevant if it shares the same disease label as the query document.

**DATASET**
**Source:**
  -PMC-Patients dataset (de-identified clinical case reports)

**Dataset Size:**
  -Full dataset size: approximately 161,000 reports

**Sampling Strategy:**
  -For reproducibility, internal sampling is performed inside the notebook.
  -No absolute file paths are hard-coded.
  -All file handling is done dynamically within Google Colab.

**NOTEBOOK FILES INCLUDED**
-This project includes two Google Colab notebooks.

**MAIN EXPERIMENT NOTEBOOK (USED FOR FINAL REPORT)**
Filename:
  -Text_Retrieval_Final_Project_10000Sample_cases.ipynb

Description:
  -Uses 10,000 sampled clinical case reports
  -All results reported in the final project PDF are generated from this notebook

Includes:
  -TF-IDF lexical retrieval
  -ClinicalBERT semantic retrieval
  -Evaluation using Precision@5 and Recall@5
  -Clustering and visualization (PCA and t-SNE)
  -LLM-based query expansion

Important:
  -This notebook is computationally heavier
  -Intended for full experimental runs and final reporting

**QUICK DEMO NOTEBOOK**
Filename:
  -Text_Retrieval_Final_Project_100Sample_Cases.ipynb 

Description:
  -Uses 100 sampled clinical case reports

Designed for:
  -Fast execution
  -Demonstration without long runtime
  -Produces the same pipeline outputs as the main notebook, but on a smaller scale

Important:
  -Results from this notebook are NOT used in the final report

**CHANGING THE SAMPLE SIZE**
  -The dataset sample size is configurable directly in the notebook.
    -Where to change:
      -In cell 7 - Baseline Retrieval Using TF-IDF and BM25
      -Example:
        nlp = spacy.load("en_core_web_sm")
        df = df_all.sample(n=100, random_state=42).reset_index(drop=True)
        print("Using sample of dataset:", df.shape)

**HOW TO RUN THE PROJECT IN GOOGLE COLAB**
Step 1: Open the Notebook
        -Upload the notebook to Google Colab

Step 2: Run all cells

Step 3: For final output open external link for UI (last cell)

Step 4: Provide a query in the text box titled "Enter a clinical note"

Example query: A 58-year-old male with long-standing alcohol use presents with progressive abdominal distension, jaundice, and right upper quadrant pain. Examination shows ascites, spider angiomas, and hepatomegaly. Laboratory studies reveal elevated AST and ALT, hyperbilirubinemia, and prolonged INR. CT imaging demonstrates a nodular liver with portal hypertension consistent with cirrhosis.

**Important Note: 
If it appears that google colab is stuck when you click on "Run all", we recommend you to run the cells one by one.**


**EXPECTED OUTPUT**
  -After running the notebook, the following outputs are produced:
    -Top-k similar clinical reports for sample queries
    -Precision@5 and Recall@5 scores for:
      -TF-IDF
      -ClinicalBERT
      -PCA and t-SNE embedding visualizations
    -LLM-based query expansions

**REPRODUCIBILITY NOTES**
  -Random seeds are fixed where applicable
  -No external APIs are required for core functionality
  -LLM usage (FLAN-T5) is runs locally
  -Final report results correspond ONLY to the 10,000-sample main notebook
