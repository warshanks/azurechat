# Azure Services Overview for AzureChat

## Required Services

| Service | Purpose | Pricing Model | Rough Cost |
|---------|---------|--------------|------------|
| **Azure OpenAI** | Chat completions, embeddings, DALL-E image generation | Per 1K tokens | Varies by model (e.g. GPT-4o ~$2.50/$10 per 1M input/output tokens) |
| **Azure Cosmos DB** | Stores chat history, config, and user data | RU/s + storage (serverless available) | ~$0 idle on serverless; ~$24/mo minimum on provisioned |
| **Azure Storage Account** | Stores uploaded files | Per GB stored + operations | ~$0.02/GB/mo — negligible for dev |

## Required for "Chat Over Your Data" Feature

| Service | Purpose | Pricing Model | Rough Cost |
|---------|---------|--------------|------------|
| **Azure AI Search** | Indexes documents for retrieval-augmented generation | Per tier | Free tier: 50MB, 3 indexes; Basic: ~$75/mo |
| **Azure AI Document Intelligence** | Extracts content from uploaded documents (PDF, etc.) | Per page processed | Free tier: 500 pages/mo; then ~$1.50/1K pages |

## Optional Services

| Service | Purpose | Pricing Model | Rough Cost |
|---------|---------|--------------|------------|
| **Azure Speech Service** | Speech-to-text for voice input | Per audio hour | Free tier: 5 hrs/mo; then ~$1/hr |
| **Azure Key Vault** | Secure storage for secrets/keys | Per operation | ~$0.03/10K operations — negligible |

## Tips for Minimizing Dev Costs

- **Cosmos DB**: Use the **serverless** tier for low-usage/dev scenarios (pay per request, no idle cost)
- **AI Search**: The **Free tier** works for testing (limited to 50MB / 3 indexes)
- **Document Intelligence & Speech**: Both have free tiers sufficient for development
- **Storage**: Costs are negligible for dev workloads

## Provisioning

The fastest way to deploy all required services is with the [Azure Developer CLI](https://learn.microsoft.com/en-us/azure/developer/azure-developer-cli/overview):

```bash
azd init
azd provision
```

This runs the Bicep templates in this repo and populates `.azure/<env-name>/.env` with connection details.
