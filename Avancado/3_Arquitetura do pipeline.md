---
titulo: Arquitetura do pipeline
tipo: conceito
nivel: avancado
categoria: RAG
tags: [rag, arquitetura, pipeline, ingestao, orquestrador, langchain, llamaindex]
resumo: "Os componentes de um pipeline de RAG (ingestão, embeddings, banco vetorial, orquestrador, LLM) e o fluxo completo."
relacionados: ["Embeddings", "Banco vetorial", "Boas práticas e erros comuns"]
fonte: https://adentro.com.br/infraestrutura-rag-llm-empresas/
---

# Arquitetura do pipeline

## Componentes

| Componente | Papel |
| --- | --- |
| **Fonte de dados** | Documentos, páginas, PDFs, código, banco |
| **Ingestão** | Ler, limpar e dividir (chunking) |
| **Modelo de embeddings** | Transformar texto em vetores |
| **Banco vetorial** | Armazenar e buscar vetores |
| **Orquestrador** | Coordenar o fluxo |
| **LLM** | Gerar a resposta |

## Fluxo de indexação (offline)

```
Fontes → Ingestão → Chunking → Embeddings → Banco vetorial (+ metadados)
```

## Fluxo de consulta (online)

```
Pergunta → (transformação) → Embedding → Busca → (rerank)
        → Contexto + prompt → LLM → Resposta (com fontes)
```

## Orquestradores

| Ferramenta | Observação |
| --- | --- |
| **LangChain** | Muitos componentes e integrações |
| **LlamaIndex** | Focado em RAG e dados |
| **Código próprio** | Controle total, menos dependências |

## Decisões e trade-offs

- **Modelo de embeddings**: qualidade x custo/idioma.
- **Banco vetorial**: local x gerenciado; suporta híbrido?
- **Chunking**: tamanho, overlap, contexto.
- **Rerank**: precisão x latência/memória.
- **LLM**: qualidade x custo x privacidade (nuvem x local).

## Expondo como serviço

O RAG pode ser exposto como:

- **API** (HTTP).
- **Servidor MCP** (ferramentas para assistentes).
- **Biblioteca** interna.

## Erros comuns

- **Não versionar** o código e a configuração.
- **Misturar indexação e consulta** sem separar os fluxos.
- **Não guardar metadados** para citação/filtros.
- **Ignorar custo e latência** em produção.

## Casos de uso

| Situação | Arquitetura |
| --- | --- |
| Protótipo | Chroma + LangChain |
| Produção | Banco gerenciado + rerank + avaliação |
| Assistente local | MCP (stdio) |
