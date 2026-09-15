---
titulo: Banco vetorial
tipo: conceito
nivel: intermediario
categoria: RAG
tags: [rag, banco-vetorial, vector-database, hnsw, busca-vetorial, metadados]
resumo: "O que é um banco vetorial, como faz busca por similaridade (ANN), principais opções e o uso de metadados."
relacionados: ["Embeddings", "Recuperação (retrieval)", "Arquitetura do pipeline"]
fonte: https://www.pinecone.io/learn/
---

# Banco vetorial

## O que é?

Um **banco vetorial** (vector database) armazena **embeddings** e permite buscar os vetores **mais parecidos** com um vetor de consulta. É o "coração" da etapa de recuperação no RAG.

Diferente de um banco comum, ele é otimizado para **busca por similaridade** em vetores de alta dimensão.

## Como funciona?

1. Cada chunk da base é convertido em embedding e armazenado com seus **metadados**.
2. A pergunta também vira um embedding.
3. O banco busca os vetores **mais próximos** (os vizinhos mais próximos).

Para ser rápido, usa **busca aproximada** (ANN - Approximate Nearest Neighbors):

| Índice | Ideia |
| --- | --- |
| **HNSW** | Grafo de vizinhança (rápido e preciso) |
| **IVF** | Divide o espaço em grupos |
| **Flat (exato)** | Compara com todos (lento, mas exato) |

## Metadados e filtros

Além do vetor, guarda-se informações úteis:

```json
{
  "texto": "...",
  "arquivo": "Basico/3_Git commit.md",
  "nivel": "basico",
  "categoria": "Git",
  "tags": "git,commit"
}
```

Assim é possível **filtrar** antes/depois da busca (ex.: buscar só em `nivel = basico`).

## Principais opções

| Banco | Observação |
| --- | --- |
| **Chroma** | Simples, local, ótimo para começar |
| **Qdrant** | Open source, recursos avançados, híbrido |
| **Weaviate** | Open source, híbrido, com módulos |
| **Pinecone** | Gerenciado (nuvem) |
| **pgvector** | Extensão do PostgreSQL |
| **Milvus** | Escala grande |
| **FAISS** | Biblioteca (não é servidor) |

## Busca híbrida

Muitos bancos combinam:

- **Densa** (embeddings) — significado.
- **Esparsa** (BM25/palavra-chave) — termos exatos.

E fundem os resultados (ex.: RRF).

## Erros comuns

- **Reindexar só parte** da base ao trocar o modelo de embeddings.
- **Não guardar metadados**, perdendo filtros e citação de fontes.
- **Escolher índice errado** para o volume de dados.
- **Confundir banco vetorial com biblioteca** (ex.: FAISS é biblioteca, não servidor).

## Casos de uso

| Situação | Escolha |
| --- | --- |
| Protótipo local | Chroma |
| Produção com filtros/híbrido | Qdrant / Weaviate |
| Já usa PostgreSQL | pgvector |
| Gerenciado na nuvem | Pinecone |
