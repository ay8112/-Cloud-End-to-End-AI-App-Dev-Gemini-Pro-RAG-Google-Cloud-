## 🔍🤖 RAG-Terraform-Vertex

Deploy a modern Retrieval-Augmented Generation (RAG) stack on Google Cloud using Terraform, Vertex AI, Discovery Engine, and GCS.

---

### 🚦 Deployment Options

You can deploy this RAG solution on Google Cloud in two ways:

- **Option 1: Terraform/CLI** (Recommended for automation)
- **Option 2: Google Cloud Console** (No CLI, UI only)

---

### 📚 What is RAG?

Retrieval-Augmented Generation (RAG) enhances Large Language Models (LLMs) by combining information retrieval with generative capabilities. Instead of relying solely on model parameters, RAG retrieves relevant external documents from a knowledge base or data store, resulting in more accurate, contextual, and up-to-date responses.

---

### 🚦 Prerequisites

- 🏢 Google Cloud project with billing enabled  
- 👤 IAM Role: Project Owner or Editor  
- 🧑‍💻 Basic knowledge: Google Cloud, Terraform, Generative AI, LLMs, Embeddings  

---

### ⚙️ Deployment Steps

#### 1️⃣ Open Google Cloud Shell or Local Terminal

Use Google Cloud Shell or your local terminal (with gcloud CLI configured).

#### 2️⃣ Clone the Repository

```bash
git clone https://github.com/anudishu/RAG-Terraform-Vertex.git
cd RAG-Terraform-Vertex
```

#### 3️⃣ Enable Required Google Cloud APIs

```bash
gcloud services enable \
  compute.googleapis.com \
  aiplatform.googleapis.com \
  storage.googleapis.com \
  discoveryengine.googleapis.com
```

Verify APIs via Google Cloud Console → Search for "AI Application" → Activate if prompted.

#### 4️⃣ Set Environment Variables

```bash
export PROJECT_ID="your-gcp-project-id"
export REGION="us-central1"
gcloud config set project $PROJECT_ID
```

#### 5️⃣ Authenticate with Google Cloud

```bash
gcloud auth application-default login
```

Follow the browser-based authentication flow.

#### 6️⃣ Initialize and Apply Terraform Configuration

Update `terraform.tfvars`:

```hcl
project_id = "your-gcp-project-id"
```

Then run:

```bash
terraform init
terraform plan
terraform apply -auto-approve
```

Note the outputs:

```hcl
test_data_store_id = "demo_store_id"
test_engine_id = "demo_engine_app"
```

---

### 📥 Load Data into RAG Data Store

#### 🔧 1. Update `loaddata.py`

Set your project ID:

```python
PROJECT_ID = "your-gcp-project-id"
```

#### ▶️ 2. Run the Data Loader

```bash
python loaddata.py
```

Uploads documents from:

```
gs://cloud-samples-data/gen-app-builder/search/alphabet-investor-pdfs
```

---

### 🧪 Test the RAG Application

- Send test queries via deployed app or Vertex AI API
- Ensure responses reflect uploaded content

#### 🖥️ Run a Query from Terminal

Update `query.py` with your project ID, then run:

```bash
python query.py
```

#### 💡 Sample Queries

```python
QUERY = "who is ceo of google? what is total revenue of google?"
QUERY = "What were Google Cloud earnings in 2024?"
QUERY = "Google Cloud vs AWS market share comparison"
QUERY = "YouTube revenue and user engagement statistics"
```

---

### 🧹 Clean Up Resources

```bash
terraform destroy -auto-approve
```

---

### 📌 Additional Notes

- Ensure IAM permissions are sufficient
- For issues, refer to Google Cloud docs or open a GitHub issue

---

### 🖱️ Option 2: Google Cloud Console Way

No CLI or Terraform required. Use the UI:

1. Create/select a Google Cloud project  
2. Enable required APIs  
3. Set up Vertex AI Search  
4. Create a Search Engine  
5. Test and clean up  
