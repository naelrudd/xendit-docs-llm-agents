# Xendit Docs for LLM Agents

An unofficial, machine-readable mirror of the official [Xendit developer documentation](https://docs.xendit.co/) — **336 pages** mirrored as plain Markdown for **LLM ingestion, RAG pipelines, and knowledge graph exploration**.

Xendit is a payment gateway for Southeast Asia (Indonesia, Philippines, Malaysia, Vietnam, Thailand). This repo lets AI assistants answer integration questions — payment methods, APIs, webhooks, and more — directly from first-party documentation text.

## Contents

| Section | Pages | Notes |
|---------|-------|-------|
| **Guides** | 253 | [`docs/`](docs/) — payment methods, integration guides, account setup |
| **API Reference** | 83 | [`apidocs/`](apidocs/) — v1 API endpoint documentation |

Each page carries YAML frontmatter with `title`, `slug`, `updated`, and `canonical` metadata, plus a link back to the original URL.

## Quick Start

```bash
git clone https://github.com/naelrudd/xendit-docs-llm-agents.git
cd xendit-docs-llm-agents

# Feed the markdown files directly to your LLM
cat docs/*.md | your-llm-prompt

# Or use with LangChain / LlamaIndex
python - <<'PY'
from langchain_community.document_loaders import DirectoryLoader
loader = DirectoryLoader("docs", glob="**/*.md")
docs = loader.load()
PY
```

For discovery, start from the curated [`INDEX.md`](INDEX.md) or the official [`llms.txt`](llms.txt).

## Updating

Re-mirror from the official index:

```bash
curl -sL -o llms.txt https://docs.xendit.co/llms.txt
# parse each https://docs.xendit.co/*.md link and download, preserving the URL path
```

## License & attribution

- This repository is **not affiliated with, endorsed by, or sponsored by Xendit (PT Xendit Teknologi Indonesia).**
- All documentation content is © Xendit and belongs to its respective owners. It is mirrored "as is" from the official [Xendit docs](https://docs.xendit.co/), which serves these pages as Markdown for AI consumption.
- Refer to [docs.xendit.co](https://docs.xendit.co/) for authoritative, always-current documentation.
- No API keys, secrets, or credentials are (or should be) stored here.
