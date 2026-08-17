# AI Engineer Learning Roadmap

## Goal

Become a production-ready **AI Engineer / LLM Engineer** who can build, evaluate, deploy, and maintain AI systems using:

- Python
- Machine Learning
- Deep Learning
- Transformers
- LLMs
- RAG
- Vector Databases
- AI Agents
- MCP
- OCR / Document AI
- FastAPI
- Docker
- Cloud
- Evaluation
- Guardrails
- Monitoring

The focus should be on **building real AI applications**, not only learning theory.

> **Reviewed:** August 17, 2026  
> **Learning philosophy:** learn enough theory to understand failure modes, then prove the concept by building, testing, measuring, and deploying something.

## How to Use This Roadmap

Do not treat every bullet as something you must master before moving forward. Use a spiral approach:

```text
Understand the idea
      ↓
Build the smallest working example
      ↓
Measure what succeeds and fails
      ↓
Improve the design
      ↓
Use it inside a real project
      ↓
Return later for deeper theory
```

For each phase, aim to produce an **observable outcome**: working code, a test, a benchmark, a deployed service, an architecture diagram, or a short technical explanation you can defend in an interview.

## Table of Contents

1. [AI Engineer Skill Map](#1-ai-engineer-skill-map)
2. [Recommended Learning Order](#2-recommended-learning-order)
3. [Phase 1 - Python](#3-phase-1---python)
4. [Phase 2 - Mathematics for AI](#4-phase-2---mathematics-for-ai)
5. [Phase 3 - NumPy, Pandas and Scikit-learn](#5-phase-3---numpy-pandas-and-scikit-learn)
6. [Phase 4 - Deep Learning](#6-phase-4---deep-learning)
7. [Phase 5 - Transformers](#7-phase-5---transformers)
8. [Phase 6 - LLM Fundamentals](#8-phase-6---llm-fundamentals)
9. [Important LLM Company Mapping](#9-important-llm-company-mapping)
10. [LLM Runtimes vs LLM Models](#10-llm-runtimes-vs-llm-models)
11. [Phase 7 - LLM Application Engineering](#11-phase-7---llm-application-engineering)
12. [Phase 8 - Embeddings](#12-phase-8---embeddings)
13. [Phase 9 - Vector Databases](#13-phase-9---vector-databases)
14. [Phase 10 - RAG](#14-phase-10---rag)
15. [Phase 11 - AI Agents](#15-phase-11---ai-agents)
16. [Phase 12 - MCP](#16-phase-12---mcp)
17. [Phase 13 - OCR and Document AI](#17-phase-13---ocr-and-document-ai)
18. [Phase 14 - Fine-Tuning](#18-phase-14---fine-tuning)
19. [Phase 15 - Evaluation](#19-phase-15---evaluation)
20. [Phase 16 - AI Safety and Guardrails](#20-phase-16---ai-safety-and-guardrails)
21. [Phase 17 - AI Backend Development](#21-phase-17---ai-backend-development)
22. [Phase 18 - Docker and Deployment](#22-phase-18---docker-and-deployment)
23. [Phase 19 - Cloud](#23-phase-19---cloud)
24. [Phase 20 - AI Inference Engineering](#24-phase-20---ai-inference-engineering)
25. [Recommended 24-Week Learning Plan](#25-recommended-24-week-learning-plan)
26. [Recommended Learning Ratio](#26-recommended-learning-ratio)
27. [Portfolio Projects](#27-portfolio-projects)
28. [Target AI Engineer Technology Stack](#28-target-ai-engineer-technology-stack)
29. [What Not to Spend Too Much Time On Initially](#29-what-not-to-spend-too-much-time-on-initially)
30. [Interview Topics You Must Know](#30-interview-topics-you-must-know)
31. [Final Learning Path](#31-final-learning-path)
32. [Main Goal](#32-main-goal)
33. [Mastery Checklist](#33-mastery-checklist)

---

# 1. AI Engineer Skill Map

```text
                    AI ENGINEER
                         |
        +----------------+----------------+
        |                |                |
        v                v                v
   Programming          AI/ML          Production
        |                |                |
     Python         Transformers       Docker
     APIs           LLMs               Cloud
     SQL            Embeddings         Monitoring
     Git            RAG                Evaluation
                    Agents             Security
                    Vision/OCR
```

An AI engineer sits between model knowledge and software engineering. In most product teams, you are not expected to invent a new transformer architecture. You are expected to turn models into a reliable system.

| Role | Typical primary focus | Where it overlaps with AI engineering |
|---|---|---|
| Data scientist | Analysis, experiments, statistical models | Evaluation, ML prototypes, data quality |
| ML engineer | Training/deployment pipelines for ML models | Serving, monitoring, feature/data pipelines |
| AI/LLM engineer | LLM/RAG/agent/document-AI applications | APIs, evaluation, deployment, security |
| Research engineer | New model techniques and experiments | Deep learning, training, benchmarking |
| Backend engineer | Reliable application/services architecture | APIs, databases, queues, authentication |

You do not need equal depth in every branch. A strong production AI engineer usually has **deep software fundamentals**, strong LLM-system knowledge, and enough ML theory to understand what the system is doing and how to measure it.

---

# 2. Recommended Learning Order

1. Python
2. NumPy and Pandas
3. Machine Learning Fundamentals
4. Deep Learning
5. PyTorch
6. Transformers
7. LLM Fundamentals
8. LLM APIs and Local Models
9. Prompt Engineering
10. Structured Outputs
11. Embeddings
12. Vector Databases
13. RAG
14. Tool Calling
15. AI Agents
16. MCP
17. Evaluation
18. Guardrails and AI Security
19. Vision and OCR
20. FastAPI
21. Docker
22. Cloud Deployment
23. Monitoring and Optimization
24. Portfolio and Interview Preparation

## Why this order works

The sequence deliberately moves from **deterministic engineering → model fundamentals → retrieval/tool use → production operations**. For example, RAG is much easier to understand after embeddings, and agents are much easier to build safely after you understand structured output and tool calling.

You may learn topics in parallel, but avoid skipping foundations just because an orchestration framework can hide them. Framework code is easier to debug when you understand the underlying HTTP request, schema, retrieval step, and model response.

---

# 3. Phase 1 - Python

Python should be your strongest programming language for AI engineering.

## Topics

- Variables
- Data types
- Lists
- Tuples
- Sets
- Dictionaries
- Conditions
- Loops
- Functions
- Classes
- Objects
- Inheritance
- Exception handling
- Modules
- Packages
- Virtual environments
- pip
- File handling
- JSON
- Type hints
- async / await
- HTTP requests
- Decorators
- Generators

## Important Example

```python
invoice = {
    "invoice_number": "INV001",
    "vendor": "ABC Ltd",
    "amount": 12000
}
```

You should be comfortable manipulating nested dictionaries, lists, JSON responses, and API data.

### What “ready to move on” looks like

You should be able to:

- create and use a virtual environment;
- install and pin dependencies;
- read/write JSON and CSV files;
- call a REST API and handle non-200 responses;
- define typed functions and data models;
- use exceptions without hiding errors;
- write basic async code for concurrent I/O;
- organize a small project into modules;
- write tests with `pytest`;
- use logging instead of relying only on `print()`.

A useful mini-project is an API client that reads invoice records from JSON, validates them, calls a mock service, retries transient failures, and writes a structured result. This teaches the same plumbing used around LLM APIs later.

### Common mistake

Do not learn Python only through notebook cells. Production AI code also needs packages, configuration, tests, command-line execution, type checking, logging, and error handling.

---

# 4. Phase 2 - Mathematics for AI

You do not need research-level mathematics.

## Linear Algebra

Understand these ideas conceptually and be able to manipulate small examples:

| Concept | Beginner meaning | Why AI engineers care |
|---|---|---|
| Scalar | One number | Loss, score, learning rate |
| Vector | Ordered list of numbers | Embeddings and feature representations |
| Matrix | 2D grid of numbers | Batches and neural-network transformations |
| Tensor | N-dimensional array | Core data structure in PyTorch |
| Dot product | Combines two vectors into one similarity/interaction score | Attention and similarity calculations |
| Matrix multiplication | Applies many weighted combinations efficiently | Fundamental neural-network operation |
| Dimension/shape | Size along each axis | Prevents common tensor-shape bugs |

Example:

```text
Text
 |
 v
Embedding Model
 |
 v
[0.14, -0.72, 0.91, ...]
```

## Statistics

Statistics helps you reason about noisy data and whether an improvement is real rather than anecdotal. Understand:

- Mean
- Median
- Variance
- Standard deviation
- Probability
- Distribution
- Correlation

## Calculus

You usually do not need to solve long derivatives by hand for application engineering. Understand the intuition behind:

- Derivatives
- Gradients
- Gradient descent
- Loss functions
- Learning rate

### Practical checkpoint

Be able to explain why gradient descent changes model weights, why a learning rate that is too high can make training unstable, and why correlation does not prove causation. If you can connect the math to model behavior, the phase has done its job.

---

# 5. Phase 3 - NumPy, Pandas and Scikit-learn

## NumPy

Learn:

- Arrays
- Shapes
- Indexing
- Slicing
- Vector operations
- Matrix operations

## Pandas

Learn:

- DataFrame
- Filtering
- groupby
- merge
- Missing values
- CSV
- JSON

## Scikit-learn

Learn:

- Data preprocessing
- Train/test split
- Feature engineering
- Model training
- Model evaluation

## Machine Learning Concepts

Understand:

- Supervised learning
- Unsupervised learning
- Classification
- Regression
- Clustering
- Features
- Labels
- Training set
- Validation set
- Test set
- Overfitting
- Underfitting
- Cross-validation

## Metrics

Know not only the formula name, but **when a metric is misleading**:

| Metric | Typical use | Watch out for |
|---|---|---|
| Accuracy | Balanced classification | Misleading on heavily imbalanced classes |
| Precision | Costly false positives | Can ignore missed positives |
| Recall | Costly false negatives | Can increase false positives |
| F1 | Balance precision and recall | Hides class-specific trade-offs |
| Confusion matrix | Inspect error types | Must interpret per class |
| MAE | Regression with interpretable average error | Treats all error linearly |
| MSE/RMSE | Regression where larger errors should hurt more | Sensitive to outliers |

### Mini-project

Build one small classification project end to end:

```text
Raw CSV → cleaning → train/validation/test split → baseline → model → metrics → error analysis → saved model
```

Do not stop at “accuracy = 95%.” Inspect which examples fail and why. This habit transfers directly to LLM evaluation.

---

# 6. Phase 4 - Deep Learning

Learn Deep Learning with **PyTorch**.

## Concepts

- Neural Networks
- Input Layer
- Hidden Layers
- Output Layer
- Weights
- Bias
- ReLU
- Sigmoid
- Softmax
- Forward Propagation
- Backpropagation
- Loss
- Optimizer
- Epoch
- Batch
- Learning Rate
- GPU
- CUDA

## Basic PyTorch

```python
import torch

x = torch.tensor([1, 2, 3])
print(x)
```

You do not need to build GPT from scratch.

Your goal is to understand how neural networks and training work. In particular, be able to follow this loop:

```text
Batch of inputs
   ↓
Forward pass
   ↓
Predictions
   ↓
Loss function
   ↓
Backpropagation computes gradients
   ↓
Optimizer updates weights
   ↓
Repeat for more batches/epochs
```

### PyTorch skills to practice

Learn tensors, shapes/dtypes/devices, `Dataset`/`DataLoader`, `nn.Module`, loss functions, optimizers, `model.train()` vs `model.eval()`, `torch.no_grad()`/inference contexts, saving/loading weights, and moving tensors/models to a GPU when available.

### Common mistake

A model with falling training loss is not automatically good. Always inspect validation performance and learn the signs of overfitting.

---

# 7. Phase 5 - Transformers

Transformers are fundamental to modern LLM systems because attention lets a model build contextual representations by relating tokens to one another. You do not need to memorize every matrix equation before using transformers, but you should understand the data flow well enough to reason about context length, tokenization, attention cost, and model architecture.

## Learn

- Tokenization
- Tokens
- Embeddings
- Positional information
- Attention
- Self-attention
- Multi-head attention
- Feed-forward networks
- Transformer layers
- Next-token prediction

## Conceptual Flow

```text
Input
 |
 v
Tokenizer
 |
 v
Tokens
 |
 v
Embeddings
 |
 v
Transformer Layers
 |
 v
Attention
 |
 v
Output Probabilities
 |
 v
Generated Response
```

## Transformer Types

### Encoder-only

Examples:

- BERT

### Decoder-only

Examples:

- GPT
- Llama
- Qwen
- Mistral
- DeepSeek

### Encoder-Decoder

Examples:

- T5

### What to be able to explain

- Why tokenization affects cost and context usage.
- Why positional information is necessary.
- Conceptually, how query/key/value attention determines which tokens influence one another.
- Why decoder-only models naturally fit autoregressive text generation.
- Why an LLM produces probabilities over next tokens rather than looking up a stored answer.

A good learning exercise is to inspect tokenization for the same sentence across two tokenizers and then trace tensor shapes through a small pretrained transformer model.

---

# 8. Phase 6 - LLM Fundamentals

Know these terms well enough to explain them without relying on buzzwords.

| Term | Practical meaning |
|---|---|
| LLM | Large language model trained to model/generate token sequences |
| SLM | Smaller language model, often chosen for lower cost/latency or local deployment |
| Parameters | Learned numerical weights in the model |
| Tokens | Units the tokenizer converts input/output into |
| Tokenizer | Maps text to token IDs and back |
| Context window | Maximum working input/history budget for a model request/session behavior |
| Prompt | Task instruction/input supplied to the model |
| System/developer instruction | Higher-priority behavioral guidance supplied by an application/provider |
| Temperature / Top-P | Sampling controls; support varies by model |
| Inference | Running a trained model to produce outputs |
| Training / pretraining | Optimizing model weights from data; pretraining is the broad initial stage |
| Fine-tuning | Further training for narrower behavior/task/domain objectives |
| Quantization | Representing weights/activations at lower precision to reduce resource use |
| Distillation | Training a smaller model to imitate useful behavior of a stronger system/model |
| Hallucination | Confident-looking output not adequately supported by facts/context |
| Structured output | Constraining output to a machine-readable schema |
| Function/tool calling | Model selects a defined operation; application/runtime executes it |
| Multimodal model | Works with more than one modality, such as text and images |
| VLM | Vision-language model that jointly processes visual and language information |

Also understand that model capabilities and supported controls are provider/model specific. Do not assume every LLM supports the same sampling parameters, tool schema, image input, or structured-output guarantees.

---

# 9. Important LLM Company Mapping

This mapping helps you distinguish **model families/brands** from the organizations that develop them. Product names, ownership, and available model generations can change, so verify current details before making procurement or architecture decisions.

```text
GPT / Codex   -> OpenAI
Claude        -> Anthropic
Gemini        -> Google
Gemma         -> Google
Llama         -> Meta
Qwen          -> Alibaba
DeepSeek      -> DeepSeek
Grok          -> xAI
Mistral       -> Mistral AI
Phi           -> Microsoft
Command       -> Cohere
Nemotron      -> NVIDIA
GLM           -> Z.ai / Zhipu AI
Kimi          -> Moonshot AI
MiniMax       -> MiniMax
```

---

# 10. LLM Runtimes vs LLM Models

Do not confuse model runners with models. A **model** is the learned artifact/weights and architecture; a **runtime or serving engine** loads a model, manages memory, token generation, batching, device placement, and exposes a CLI/API to applications.

## Model Runtimes

```text
Ollama
vLLM
llama.cpp
LM Studio
```

## Models

```text
Llama
Qwen
Gemma
Mistral
DeepSeek
GLM
Phi
```

Example:

```bash
ollama run llama3.2
```

Here:

```text
Ollama    = Model Runtime
Llama 3.2 = Model
```

A third concept is a **model format/quantization artifact**, such as a GGUF file. Do not use “GGUF,” “Ollama,” and “Llama” as synonyms; they describe different layers.

---

# 11. Phase 7 - LLM Application Engineering

Learn how to integrate LLMs into applications. This phase is where “I can chat with a model” becomes “I can build a service around a model.” Focus on contracts, errors, observability, and validation—not only the happy-path SDK call.

## Cloud Models

Understand how to use:

- OpenAI API
- Anthropic API
- Gemini API
- Other model APIs

## Local Models

Understand:

```text
Application
    |
    v
Ollama
    |
    v
Qwen / Llama / Gemma / Mistral
    |
    v
CPU / GPU
```

## Important Topics

- Prompt engineering
- System prompts
- User prompts
- Few-shot prompting
- Structured JSON
- JSON Schema
- Streaming
- Retries
- Timeouts
- Rate limits
- Token counting
- Caching
- Model routing
- Fallback models
- Cost optimization
- Error handling

### Production request pattern

```text
Validate input
   ↓
Choose model/config
   ↓
Call model with timeout
   ↓
Handle rate-limit/transient errors
   ↓
Validate structured response
   ↓
Apply business rules
   ↓
Log latency/tokens/result metadata
   ↓
Return application response
```

Never put a raw model response directly into an irreversible business action merely because the API call succeeded.

---

# 12. Phase 8 - Embeddings

Embeddings convert information into vectors designed so that useful relationships can be measured numerically. For text retrieval, semantically similar passages tend to be closer under the similarity measure the model/index expects.

Example:

```text
"Samsung invoice"
        |
        v
Embedding Model
        |
        v
[0.42, -0.31, 0.85, ...]
```

Learn:

- Embeddings
- Vectors
- Dimensions
- Cosine similarity
- Euclidean distance
- Semantic similarity
- Semantic search
- Nearest neighbors

## Important practical rules

- Use the **same embedding model/space** for indexed documents and queries unless a model explicitly supports asymmetric encoders.
- Know the model's embedding dimension and the index's distance metric.
- Normalize only when the chosen model/metric expects it.
- Store source metadata so retrieved chunks can be filtered and cited.
- Re-embed data when changing to an incompatible embedding model.

Mini-project: embed 100 short documents, search them with five natural-language queries, and manually inspect both correct and incorrect nearest neighbors.

---

# 13. Phase 9 - Vector Databases

Learn at least one vector database properly.

## Recommended Learning Order

A useful progression is:

```text
FAISS (learn similarity/index basics locally)
  |
  v
Qdrant or another dedicated vector DB (learn service + metadata filtering)
  |
  v
pgvector (learn how vector search fits an existing PostgreSQL system)
```

This is a learning sequence, not a claim that one product is universally “better” than another. Choose based on scale, operational environment, filtering, consistency, latency, and whether you already depend on PostgreSQL.

Other options:

- Chroma
- Weaviate
- Milvus
- Pinecone

## Important Concepts

- Collections
- Vectors
- Metadata
- Indexes
- Similarity search
- Filtering
- Top-K

Also learn **indexing trade-offs**: exact vs approximate nearest-neighbor search, recall vs latency, metadata filtering, persistence, backup, multi-tenancy, and how deletion/update of source documents propagates into the index.

---

# 14. Phase 10 - RAG

RAG means **Retrieval-Augmented Generation**. It retrieves external evidence at request time and places that evidence in the model's working context so the answer can be grounded in data that may be private, recent, or too large to memorize in a prompt.

RAG is not “put PDFs in a vector database and trust the answer.” It is a pipeline whose extraction, chunking, retrieval, ranking, prompt construction, generation, and citation stages must each be evaluated.

## Document Ingestion

```text
PDF
 |
 v
Extract Text
 |
 v
Chunk Text
 |
 v
Create Embeddings
 |
 v
Store in Vector Database
```

## User Query

```text
User Question
 |
 v
Create Query Embedding
 |
 v
Vector Search
 |
 v
Retrieve Relevant Chunks
 |
 v
Prompt + Context
 |
 v
LLM
 |
 v
Answer
```

## Learn

- Document loaders
- Chunking
- Chunk size
- Chunk overlap
- Embeddings
- Vector search
- Metadata filtering
- Hybrid search
- Reranking
- Top-K retrieval
- Context construction
- Grounding
- Citations

### Failure modes to practice

| Failure | Typical cause | Possible improvement |
|---|---|---|
| Relevant document never retrieved | Poor chunking/query/index | Better chunks, query rewriting, hybrid search |
| Correct chunk ranks too low | Weak first-stage ranking | Reranker or tuned retrieval |
| Answer ignores evidence | Prompt/model behavior | Strong grounding instructions + answer evaluation |
| Citation is wrong | Citation assembled after generation or IDs lost | Preserve chunk/source IDs through the pipeline |
| Stale answer | Index not synchronized | Explicit ingestion/update/deletion workflow |

Build an evaluation set of real questions with expected supporting passages. Measure retrieval separately from final answer quality; otherwise you will not know which stage failed.

---

# 15. Phase 11 - AI Agents

An AI agent is a system in which a model can choose actions—usually tool calls—based on a goal and the observations returned by previous actions. The model is only one component; the runtime controls actual execution, permissions, state, retries, and stopping.

## Agent Flow

```text
User
 |
 v
LLM
 |
 v
Decides Action
 |
 v
Tool
 |
 v
Tool Result
 |
 v
LLM
 |
 v
Final Answer
```

## Example

```text
User:
"Find invoice INV001 and tell me payment status."

Agent
 |
 +--> get_invoice()
 |
 +--> database
 |
 +--> get_payment_status()
 |
 +--> PAID
 |
 v
Final Response
```

## Learn

- Function calling
- Tool calling
- Agent loops
- State
- Memory
- Planning
- Workflows
- Human-in-the-loop
- Retry handling
- Tool permissions

### Agent vs workflow

Use a deterministic workflow when the sequence is known:

```text
validate → OCR → extract → validate → save
```

Use an agent when the next step genuinely depends on model judgment:

```text
inspect incident → choose diagnostic tool → observe → choose next diagnostic
```

Do not add autonomy when a normal function or state machine is clearer. For write/delete/publish/payment/production actions, design human approval and least privilege before adding more autonomy.

### Practical checkpoint

Build one agent with only 2–3 narrow tools. Log every tool call and result, define a maximum number of steps, handle tool failures, and require approval for one high-impact action.

---

# 16. Phase 12 - MCP

MCP means **Model Context Protocol**. It standardizes how an AI application can discover and interact with external context/capabilities through an MCP server instead of inventing a one-off integration contract for every client.

Understand:

- MCP Client
- MCP Server
- Tools
- Resources
- Prompts
- Model-to-tool communication
- Connecting AI agents to external systems

Conceptually:

```text
LLM Application
      |
      v
  MCP Client
      |
      v
  MCP Server
      |
      +--> Database
      +--> GitHub
      +--> Files
      +--> Internal APIs
```

## What MCP does not replace

MCP does not replace the database, REST API, authentication system, or business authorization behind a tool. It is an integration protocol at the AI/application boundary. You still need normal security controls, input validation, auditability, and least-privilege credentials.

Learn how capabilities are discovered, how schemas are described, how a client invokes a tool, how results return to the model, and how trust changes when you connect a new server.

---

# 17. Phase 13 - OCR and Document AI

Document AI can become a strong specialization because real documents combine text recognition, layout, tables, images, business rules, and uncertain extraction. Treat OCR as one signal in a pipeline rather than assuming OCR alone understands a document.

Useful distinction:

| Layer | Main job | Example output |
|---|---|---|
| PDF text extraction | Read embedded text when present | characters/positions |
| OCR | Recognize text from pixels | text + boxes/confidence |
| Layout analysis | Identify regions/reading structure | header/table/paragraph regions |
| VLM/LLM extraction | Map evidence to semantic fields | `invoice_number`, `total` |
| Deterministic validation | Enforce schema/business rules | valid date, totals reconcile |

## Recommended Architecture

```text
                 Invoice
                    |
         +----------+----------+
         |                     |
         v                     v
    Native PDF               Image
         |                     |
         |                Preprocessing
         |                     |
         |                 PaddleOCR
         |                     |
         +----------+----------+
                    |
                    v
              Layout Analysis
                    |
                    v
             Candidate Fields
                    |
                    v
               LLM / VLM
                    |
                    v
              JSON Schema
                    |
                    v
          Evidence Validation
                    |
                    v
            Business Rules
                    |
                    v
               Final JSON
```

## Learn

- PaddleOCR
- OpenCV
- PyMuPDF
- Image preprocessing
- Bounding boxes
- Layout analysis
- Table extraction
- OCR confidence
- VLMs
- Document classification
- Key-value extraction
- Line-item extraction

### Evaluation mindset

Measure field-level exact/normalized accuracy, table row/cell accuracy, evidence correctness, document-level success rate, latency, and human-review rate. Keep the original bounding box/page or source span for important extracted fields so reviewers can verify where the value came from.

### Common mistake

Do not ask an LLM/VLM to “fix” an OCR value without retaining evidence. A plausible correction can become an undetectable hallucination.

---

# 18. Phase 14 - Fine-Tuning

Do not start your AI journey with fine-tuning.

Recommended order:

```text
Prompt Engineering
       |
       v
RAG
       |
       v
Evaluation
       |
       v
Fine-Tuning
```

## Learn Later

- Supervised Fine-Tuning
- SFT
- LoRA
- QLoRA
- PEFT
- Dataset preparation
- Instruction tuning
- Training/validation
- Quantization

### Fine-tuning decision test

Before training, ask:

1. Is the problem missing knowledge? Try retrieval first.
2. Is the problem inconsistent output shape? Try schema-constrained output and validation.
3. Is the problem behavior/style/task performance that examples can teach? Fine-tuning may help.
4. Do you have a representative, licensed, clean train/validation dataset? If not, fix the data first.
5. Can you prove improvement on a held-out evaluation set? If not, you cannot know whether tuning helped.

Fine-tuning does not guarantee factual freshness and should not be used as a replacement for an updatable knowledge source.

---

# 19. Phase 15 - Evaluation

AI systems must be measured because model output is probabilistic and application quality is multi-dimensional. A system can be “more accurate” yet too slow, too expensive, unsafe, or bad on a critical subset.

Do not evaluate systems with:

```text
"It looks correct."
```

Use measurable tests.

## Measure

- Accuracy
- Hallucination rate
- Retrieval precision
- Retrieval recall
- Structured output validity
- Latency
- Token usage
- Cost
- Failure rate

## Invoice Evaluation Example

Expected:

```json
{
  "invoice_number": "INV001",
  "invoice_date": "2026-08-12",
  "total": 15000
}
```

Create a test dataset:

```text
invoice_001.pdf -> expected.json
invoice_002.pdf -> expected.json
invoice_003.pdf -> expected.json
...
invoice_100.pdf -> expected.json
```

Then calculate metrics:

```text
invoice_number accuracy = 99%
invoice_date accuracy   = 97%
vendor accuracy         = 96%
total accuracy          = 99%
line_item accuracy      = 91%
```

### Build two evaluation layers

- **Component evals:** OCR accuracy, retrieval recall, schema validity, tool-call correctness.
- **End-to-end evals:** did the complete application satisfy the user's/business goal?

Keep a fixed regression set for release comparisons and a growing failure set containing bugs found in production. Record dataset version, model/configuration, prompt/instruction version, and code version so results are reproducible.

For subjective tasks, define a rubric and calibrate human/model graders against examples. Do not report a single “LLM accuracy” number without explaining what was measured.

---

# 20. Phase 16 - AI Safety and Guardrails

Guardrails are not one magic filter. Production safety is layered: identity, authorization, tool scope, input handling, model policy, output validation, application business rules, audit logs, and human review for high-impact actions.

Learn:

- Prompt injection
- Indirect prompt injection
- Jailbreaking
- Data leakage
- PII handling
- Secret protection
- Tool permissions
- Input validation
- Output validation
- SQL injection
- Hallucination prevention
- Rate limiting

## Never Blindly Trust an LLM

Bad:

```text
LLM
 |
 v
amount = 900000
 |
 v
Save to Database
```

Better:

```text
LLM Prediction
      |
      v
Evidence Validation
      |
      v
Business Rule Validation
      |
      v
Confidence Check
      |
      v
Accept / Human Review / Reject
```

### Security rule

Treat retrieved documents, webpages, emails, repository text, and tool output as potentially untrusted data. They may contain prompt-injection instructions. Data should not silently grant itself higher authority or broader tool permissions.

---

# 21. Phase 17 - AI Backend Development

The backend turns model calls into a service other applications can rely on. Learn normal backend engineering first: request validation, authentication, database transactions, concurrency, queues, idempotency, logs, metrics, and failure handling. AI does not remove these requirements.

Learn:

- FastAPI
- REST APIs
- Pydantic
- Async Python
- WebSockets
- Streaming
- PostgreSQL
- MySQL
- Redis
- Background jobs
- Queues

Typical architecture:

```text
Angular / React
       |
       v
    FastAPI
       |
       v
    AI Layer
 +-----+------+------+
 |            |      |
 v            v      v
LLM          OCR   Vector DB
 |            |      |
 +------------+------+
              |
              v
       Database / Storage
```

## When to use async, streaming, queues

- Use **async I/O** when waiting on concurrent network/storage operations.
- Use **streaming** when partial model output improves user experience.
- Use a **background job/queue** when work may take longer than a normal HTTP request, needs retries, or should survive a web-worker restart.

For every endpoint, define timeout behavior and what the client sees when the downstream model provider fails.

---

# 22. Phase 18 - Docker and Deployment

Learn:

- Linux
- Git
- Docker
- Docker Compose
- Environment variables
- GPU containers
- NVIDIA CUDA basics
- Nginx
- Reverse proxy
- CI/CD
- Logging
- Monitoring

Recommended learning order:

```text
Docker
  |
  v
Docker Compose
  |
  v
Cloud VM
  |
  v
CI/CD
  |
  v
Kubernetes
```

Do not start Kubernetes too early. First be able to build a reproducible image, run it with configuration/secrets outside the image, add a health check, persist data correctly, inspect logs, and deploy one service safely.

A production container should not contain hard-coded API keys. Prefer a non-root user where practical, pin dependencies/base images deliberately, scan dependencies/images, and separate build-time secrets from runtime secrets.

---

# 23. Phase 19 - Cloud

Learn the basics of at least one cloud deeply enough to deploy and operate a small AI service. The cloud-specific product names matter less initially than understanding the underlying capability and security boundary.

Learn the basics of at least one:

- AWS
- Azure
- Google Cloud Platform

Understand:

- Virtual Machines
- Containers
- Object Storage
- Managed Databases
- Secrets
- IAM
- Logging
- Monitoring
- Autoscaling
- GPU instances

## Be able to design this path

```text
Internet / internal client
        ↓
TLS + authentication
        ↓
Load balancer / API service
        ↓
AI application
   ├── managed model API
   └── self-hosted model service
        ↓
Database / object storage / vector store
        ↓
Logs + metrics + traces + alerts
```

Learn cost controls, budgets, IAM/service identities, network exposure, backups, and region/data-governance requirements alongside deployment.

---

# 24. Phase 20 - AI Inference Engineering

Understand how models consume hardware and how serving decisions change latency, throughput, memory use, quality, and cost. This matters when deciding whether a model can run locally, on a single GPU, or needs a serving cluster/API.

Learn:

- CPU vs GPU
- VRAM
- Model parameters
- FP32
- FP16
- BF16
- INT8
- INT4
- Quantization
- GGUF
- KV Cache
- Context Length
- Tokens per second
- Batching
- Latency
- Throughput

Example:

```text
Qwen 7B
   |
   v
4-bit Quantization
   |
   v
Lower Memory Usage
   |
   v
Easier Local Deployment
```

## Key trade-offs

- **Quantization:** lower memory/cost, sometimes lower quality or different kernel support.
- **Longer context:** higher memory/compute and often higher latency; more context is not automatically more useful.
- **Batching:** improves throughput but can worsen per-request latency.
- **KV cache:** speeds autoregressive generation but consumes memory that grows with active sequences/context.
- **CPU vs GPU:** CPUs are flexible and inexpensive for small workloads; GPUs provide much higher parallel throughput for many neural operations.

Measure **time to first token**, generation tokens/second, end-to-end latency percentiles, throughput, peak memory, and cost per successful task—not just a model's parameter count.

---

# 25. Recommended 24-Week Learning Plan

| Weeks | Focus |
|---|---|
| 1-3 | Python |
| 4 | NumPy + Pandas |
| 5-6 | Machine Learning Fundamentals |
| 7-8 | Neural Networks + PyTorch |
| 9-10 | Transformers + Hugging Face |
| 11-12 | LLM APIs + Ollama |
| 13 | Prompt Engineering + Structured Output |
| 14 | Embeddings |
| 15-16 | Vector Databases + RAG |
| 17-18 | Agents + Tool Calling + MCP |
| 19 | Evaluation + Guardrails |
| 20 | Vision + VLMs |
| 21 | OCR + Document AI |
| 22 | Docker + Deployment |
| 23 | Monitoring + Optimization |
| 24 | Portfolio + Interview Preparation |

This is a sequencing template, not a promise that every learner becomes production-ready in exactly 24 weeks. If Python, backend engineering, or ML foundations are new to you, extend those phases rather than rushing into agents. If you already have strong software experience, spend more time on evaluation, retrieval, security, and production operations.

Each two-week block should include a tangible deliverable and a short retrospective: what worked, what failed, what metric improved, and what you would design differently.

---

# 26. Recommended Learning Ratio

```text
30% Learning
70% Building
```

Avoid spending months only watching courses.

Every major topic should produce a small project. “Building” includes testing, debugging, measuring, documenting, and operating—not merely generating code until it runs once.

---

# 27. Portfolio Projects

Build 4 strong projects rather than many basic tutorials. A strong portfolio project should demonstrate a problem statement, architecture, reproducible setup, tests, evaluation dataset/metrics, failure analysis, security decisions, deployment, and a clear README.

Avoid presenting a thin wrapper around a model API as a production AI project. Show the engineering around the model.

---

## Project 1 - Machine Learning API

Example:

```text
Customer Churn Dataset
        |
        v
Scikit-learn Model
        |
        v
FastAPI
        |
        v
Docker
```

Demonstrate:

- Data preprocessing
- Model training
- Evaluation
- REST API
- Docker

---

## Project 2 - Production RAG Application

```text
PDF Upload
   |
   v
PyMuPDF
   |
   v
Chunking
   |
   v
Embeddings
   |
   v
Qdrant
   |
   v
LLM
   |
   v
Answer + Citation
```

Include:

- Multiple PDFs
- Metadata
- Reranking
- Citations
- Evaluation
- Docker

---

## Project 3 - AI Agent

Example:

```text
Finance Assistant
       |
       v
      LLM
       |
 +-----+-----+------+
 |           |      |
 v           v      v
SQL         API   Search
```

Include:

- Tool calling
- State
- Memory
- Logging
- Human approval
- Error handling

---

## Project 4 - Invoice Intelligence System

This should be a flagship AI project.

```text
PDF / JPG / PNG
       |
       v
Preprocessing
       |
       v
PaddleOCR
       |
       v
Layout Analysis
       |
       v
Candidate Extraction
       |
       v
LLM / VLM
       |
       v
Vendor-specific Mapping
       |
       v
JSON Schema
       |
       v
Evidence Validator
       |
       v
Confidence Scoring
       |
       v
Line Item Extraction
       |
       v
Final JSON
```

Add:

- FastAPI
- Docker
- pytest
- Logging
- Vendor-specific aliases
- Default aliases
- Confidence scores
- Human review
- Model comparison
- Latency benchmark
- Accuracy benchmark
- Structured output validation
- Retry strategy
- OCR fallback
- VLM fallback
- Local and cloud LLM support

Possible models:

- Qwen
- Gemma
- Llama
- Mistral
- DeepSeek
- GPT
- Claude
- Gemini

---

# 28. Target AI Engineer Technology Stack

Treat this as a **representative stack**, not a checklist of mandatory brands. Learn the capability deeply, then substitute equivalent tools when a project or employer uses something else.

## Programming

```text
Python             ★★★★★
SQL                ★★★★
JavaScript/TS      ★★★
```

## Data

- NumPy
- Pandas
- Scikit-learn

## Deep Learning

- PyTorch

## LLM

- Hugging Face Transformers
- OpenAI API
- Anthropic API
- Gemini API
- Ollama

## Local Models

- Qwen
- Gemma
- Llama
- Mistral
- DeepSeek
- GLM

## RAG

- Embeddings
- FAISS
- Qdrant
- pgvector
- Reranking

## Agents

- Tool Calling
- MCP
- One orchestration approach/framework such as LangGraph when a stateful graph is actually useful

Start framework-agnostic first so you understand the agent loop, state, tool schema, permissions, and failure handling beneath the framework.

## Document AI

- PaddleOCR
- OpenCV
- PyMuPDF
- VLMs

## Backend

- FastAPI
- Pydantic

## Database

- PostgreSQL
- MySQL
- Redis

## Deployment

- Git
- Linux
- Docker
- Docker Compose
- AWS / Azure / GCP

## Production AI

- Evaluation
- Observability
- Caching
- Guardrails
- Security
- Cost Optimization
- Latency Optimization

---

# 29. What Not to Spend Too Much Time On Initially

Avoid over-investing in:

- Building GPT from scratch
- Advanced calculus
- Research-level statistics
- CUDA kernel programming
- Training billion-parameter models from scratch
- GAN mathematics
- Kubernetes at the beginning
- Learning every vector database
- Learning every agent framework
- Memorizing every LLM available

Learn the core concepts and become very strong with a smaller set of tools.

---

# 30. Interview Topics You Must Know

You should be able to explain these clearly **and connect each answer to a design trade-off or failure case**. Interview strength comes from reasoning about systems, not memorizing definitions.

## LLM Fundamentals

- What is an LLM?
- What is a token?
- What is context window?
- What is inference?
- What is hallucination?
- What is temperature?
- What is quantization?
- What is fine-tuning?
- What is LoRA?
- What is structured output?

## Transformer Fundamentals

- What is attention?
- What is self-attention?
- What is an embedding?
- Encoder vs decoder
- Why are Transformers powerful?

## RAG

- What is RAG?
- RAG vs fine-tuning
- How chunking works
- Chunk size vs overlap
- What is reranking?
- What is hybrid search?
- How do you evaluate RAG?

## Vector Databases

- What is a vector?
- What is cosine similarity?
- What is semantic search?
- What is Top-K?
- Vector database vs relational database

## Agents

- What is an AI agent?
- Agent vs chatbot
- Function calling
- Tool calling
- Agent state
- Agent memory
- Workflow vs agent
- MCP

## Production AI

- How do you reduce hallucinations?
- How do you validate LLM output?
- How do you monitor an AI application?
- How do you reduce latency?
- How do you reduce API cost?
- How do you secure LLM tools?
- Local LLM vs cloud LLM

## OCR / Document AI

- OCR vs VLM
- Bounding boxes
- OCR confidence
- Image preprocessing
- Table extraction
- Key-value extraction
- Line-item extraction
- Evidence validation

### Practice answer structure

For an architecture question, answer in this order:

```text
1. Clarify requirements and risks
2. Establish a simple baseline
3. Describe components and data flow
4. Explain trade-offs
5. Describe failure handling/security
6. Define evaluation and monitoring
7. Explain how you would scale only when needed
```

---

# 31. Final Learning Path

```text
Python
   |
   v
NumPy / Pandas
   |
   v
Machine Learning
   |
   v
PyTorch
   |
   v
Transformers
   |
   v
LLMs
   |
   v
Prompt Engineering
   |
   v
Structured Output
   |
   v
Embeddings
   |
   v
Vector Databases
   |
   v
RAG
   |
   v
Tool Calling
   |
   v
Agents
   |
   v
MCP
   |
   v
Evaluation
   |
   v
Guardrails
   |
   v
Vision / OCR
   |
   v
FastAPI
   |
   v
Docker
   |
   v
Cloud
   |
   v
Production AI Systems
```

---

# 32. Main Goal

At the end of this roadmap, you should be capable of independently building systems such as:

```text
                    Production AI Application

Frontend
   |
   v
FastAPI
   |
   +-------------------+-------------------+
   |                   |                   |
   v                   v                   v
LLM API            Local LLM             OCR/VLM
   |                   |                   |
   +---------+---------+-------------------+
             |
             v
         AI Pipeline
             |
     +-------+-------+
     |               |
     v               v
Vector DB         SQL Database
     |               |
     +-------+-------+
             |
             v
       Validation Layer
             |
             v
         Evaluation
             |
             v
        Monitoring
             |
             v
       Production Output
```

The objective is not simply to know how to call an LLM API. A production-ready AI engineer should be able to explain **why the system can be trusted enough for its intended use**, how failures are detected, what happens when a dependency is unavailable, how data is protected, and how quality/cost/latency are measured over time.

The objective is to become an engineer who can build:

- Reliable AI systems
- Secure AI systems
- Measurable AI systems
- Cost-efficient AI systems
- Scalable AI systems
- Production-ready AI systems

---

# 33. Mastery Checklist

## Foundation

- [ ] Python
- [ ] NumPy
- [ ] Pandas
- [ ] Scikit-learn
- [ ] Basic Mathematics
- [ ] Machine Learning Fundamentals

## Deep Learning

- [ ] Neural Networks
- [ ] PyTorch
- [ ] Transformers
- [ ] Attention
- [ ] Tokenization
- [ ] Embeddings

## LLM Engineering

- [ ] LLM APIs
- [ ] Ollama
- [ ] Hugging Face
- [ ] Prompt Engineering
- [ ] Structured Outputs
- [ ] Tool Calling
- [ ] Quantization

## RAG

- [ ] Vector Databases
- [ ] FAISS
- [ ] Qdrant
- [ ] pgvector
- [ ] Chunking
- [ ] Embeddings
- [ ] Reranking
- [ ] Hybrid Search
- [ ] RAG Evaluation

## Agents

- [ ] Function Calling
- [ ] Tool Calling
- [ ] Agent State
- [ ] Memory
- [ ] Workflows
- [ ] Human-in-the-loop
- [ ] MCP
- [ ] LangGraph

## Document AI

- [ ] PaddleOCR
- [ ] OpenCV
- [ ] PyMuPDF
- [ ] Layout Analysis
- [ ] Table Extraction
- [ ] VLMs
- [ ] Key-value Extraction
- [ ] Line-item Extraction
- [ ] Confidence Scoring

## Production

- [ ] API authentication and authorization
- [ ] Timeouts, retries, and idempotency
- [ ] Background jobs / queues
- [ ] FastAPI
- [ ] Pydantic
- [ ] PostgreSQL
- [ ] Redis
- [ ] Docker
- [ ] Docker Compose
- [ ] Linux
- [ ] Cloud
- [ ] CI/CD
- [ ] Logging
- [ ] Monitoring
- [ ] Tracing / request correlation
- [ ] Evaluation
- [ ] Versioned eval datasets
- [ ] Guardrails
- [ ] Security
- [ ] Cost Optimization
- [ ] Latency Optimization
- [ ] Backups / recovery basics
- [ ] Least-privilege secrets and IAM

## Portfolio

- [ ] ML API Project
- [ ] RAG Project
- [ ] AI Agent Project
- [ ] Invoice Intelligence Project
- [ ] GitHub Documentation
- [ ] Architecture Diagrams
- [ ] Test Cases
- [ ] Benchmarks
- [ ] Failure analysis / known limitations
- [ ] Reproducible setup and architecture decisions
- [ ] Resume Update
- [ ] Interview Preparation

---

**Recommended rule: Learn a concept, build something with it, evaluate it, and then move to the next concept.**
