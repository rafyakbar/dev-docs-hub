# 📚 Dev Docs Hub

> AI-ready documentation hub built from crawled official docs.

Dev Docs Hub is a structured repository that crawls official documentation websites and converts them into clean, organized Markdown files.

The result is a documentation dataset that is stable, versioned, and optimized for AI consumption.

---

## 🎯 Purpose

Dev Docs Hub is designed to:

* 🌐 Crawl official documentation websites
* 📄 Store each page as raw HTML
* 🧩 Convert HTML into individual Markdown files
* 📘 Generate a single combined Markdown file
* 🔢 Preserve order using numeric prefixes like `0001_`, `0002_`, etc.

This makes the documentation:

* Easy to index
* Easy to embed
* Easy to chunk
* Stable across time
* Fully controllable

---

## 🧠 Why This Project Exists

Modern AI assistants rely heavily on up to date documentation. However:

* Websites change
* Content updates without notice
* External retrieval systems may fail
* Version specific docs are hard to freeze

Dev Docs Hub solves this by producing **local, structured, AI-ready documentation datasets**.

Instead of depending entirely on external systems, you own the documentation snapshot.

---

## 📂 Project Structure

```
dev-docs-hub/
├── fluxui-v2.ipynb
├── livewire-v4.ipynb
├── PROMPTEN.md
├── PROMPTID.md
└── docs/
    ├── fluxui-v2/
    │   ├── htmls/
    │   ├── markdowns/
    │   │   ├── 0001_Installation.md
    │   │   ├── ...
    │   │   └── 0052_Tooltip.md
    │   └── fluxui-v2.md
    ├── livewire-4x/
    │   ├── htmls/
    │   ├── markdowns/
    │   │   ├── 0001_Quickstart.md
    │   │   ├── ...
    │   │   └── 0080_Contribution Guide.md
    │   └── livewire-4x.md
    └── on the way...
```

### 📁 Folder Explanation

* 📂 `htmls/`
  Raw HTML files downloaded directly from the official documentation.

* 📂 `markdowns/`
  Individual Markdown files per documentation page.

* 📘 `[project-name].md`
  A fully combined Markdown file containing all documentation sections.

---

## ⚙️ Crawling Pipeline

Each notebook follows a strict and reproducible structure:

### 1️⃣ Configuration

Defines project name, base URL, start URL, and output directories.

### 2️⃣ Fetch Start Page

Downloads the initial documentation page.

### 3️⃣ Extract Sidebar Links

Collects all documentation links from the sidebar menu.

### 4️⃣ Crawl Each Page

Downloads each documentation page and saves it as a numbered HTML file.

### 5️⃣ Convert HTML to Markdown

* Extracts the main documentation content
* Removes image-related tags (`img`, `svg`, `picture`, `source`)
* Converts cleaned HTML to Markdown
* Saves individual Markdown files
* Generates a single combined Markdown file

---

## 🚀 Use Cases

### 🤖 AI Coding Assistant Knowledge Base

Point your AI assistant to:

```
docs/[project]/markdowns
```

Now the assistant can read the full documentation locally and consistently.

---

### 🔎 RAG and Embedding Pipelines

* Split per file
* Split per heading
* Generate embeddings
* Store in vector database

Perfect for retrieval augmented generation systems.

---

### 🧪 Fine Tuning Dataset

Use the combined Markdown file as:

* Training corpus
* Domain specific dataset
* Structured knowledge base

---

## 🌱 Future Plans

* Support more frameworks
* CLI version of crawler
* AI-based crawler