---
titulo: Recuperação (retrieval)
tipo: conceito
nivel: intermediario
categoria: RAG
tags: [rag, retrieval, busca-vetorial, busca-hibrida, bm25, top-k, rrf, mmr]
resumo: "A etapa de recuperação no RAG: busca densa, esparsa e híbrida, top-k, filtros, RRF e diversidade (MMR)."
relacionados: ["Embeddings", "Banco vetorial", "Re-ranking"]
fonte: https://www.pinecone.io/learn/
---

# Recuperação (retrieval)

## O que é?

A **recuperação** é a primeira etapa do pipeline do RAG: dado o embedding da pergunta, buscar na base os **trechos mais relevantes** para servir de contexto ao LLM.

## Tipos de busca

| Tipo | Base | Vantagem |
| --- | --- | --- |
| **Densa (vetorial)** | Embeddings | Entende significado e sinônimos |
| **Esparsa (BM25/palavra-chave)** | Termos exatos | Excelente para termos raros/código |
| **Híbrida** | As duas | Melhor resultado na prática |

## Top-k

- **k** é quantos chunks recuperar (ex.: 5, 10, 20).
- **k pequeno**: menos contexto, mais rápido.
- **k grande**: mais contexto, mas pode incluir ruído.
- Prática comum: recuperar **muitos** (ex.: 20–50) e depois aplicar **re-ranking**.

## Filtros por metadados

Permite restringir a busca:

```python
collection.query(query_embeddings=emb, n_results=8, where={"nivel": "basico"})
```

- Útil para separar por nível, categoria, idioma, data etc.

## Fusão de resultados (RRF)

A **Reciprocal Rank Fusion (RRF)** combina rankings de buscas diferentes (ex.: vetorial + BM25) em um só, sem precisar comparar as pontuações diretamente.

```
pontuação(item) = Σ  1 / (k + posição_no_ranking)
```

## Diversidade (MMR)

**MMR** (Maximal Marginal Relevance) escolhe resultados relevantes **e** diferentes entre si, evitando vários chunks quase iguais.

## Erros comuns

- **Só busca vetorial** e perder termos exatos (código, siglas).
- **k fixo** sem avaliar a qualidade.
- **Não usar filtros**, trazendo trechos irrelevantes.
- **Ignorar a diversidade** e receber chunks repetidos.

## Casos de uso

| Situação | Abordagem |
| --- | --- |
| Perguntas conceituais | Busca densa |
| Comandos/código | Busca híbrida (BM25 + vetorial) |
| Base com níveis | Filtro por metadados |
| Muitos resultados parecidos | MMR |
