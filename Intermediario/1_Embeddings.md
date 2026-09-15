---
titulo: Embeddings
tipo: conceito
nivel: intermediario
categoria: RAG
tags: [rag, embeddings, vetores, similaridade, busca-semantica]
resumo: "O que são embeddings, como transformam texto em vetores e como são usados para buscar por significado."
relacionados: ["Banco vetorial", "Chunking", "Recuperação (retrieval)"]
fonte: https://www.pinecone.io/learn/
---

# Embeddings

## O que é?

Um **embedding** é a representação de um texto (palavra, frase ou documento) como um **vetor de números** (uma lista de valores). Esse vetor captura o **significado** do texto.

Textos com significado parecido geram vetores **próximos** entre si, mesmo que usem palavras diferentes. É isso que permite a **busca semântica**.

## Como funciona?

1. Um **modelo de embeddings** recebe um texto.
2. Ele devolve um vetor, por exemplo com **1024 dimensões**.
3. A comparação entre vetores é feita por **similaridade**.

```
"como desfazer um commit"  ->  [0.12, -0.98, 0.44, ...]
"reverter um commit"       ->  [0.11, -0.95, 0.47, ...]   (próximos)
"receita de bolo"          ->  [-0.77, 0.21, -0.33, ...]  (distante)
```

## Medidas de similaridade

| Medida | Uso |
| --- | --- |
| **Similaridade de cosseno** | Mais comum; mede o ângulo entre vetores |
| **Produto escalar** | Rápido; usado quando os vetores são normalizados |
| **Distância euclidiana** | Mede a distância "reta" entre os pontos |

## Modelos comuns

| Modelo | Observação |
| --- | --- |
| `BAAI/bge-m3` | Multilíngue, ótimo para português (open source) |
| `intfloat/multilingual-e5` | Multilíngue, leve |
| `text-embedding-3` (OpenAI) | Comercial |
| `embed-multilingual` (Cohere) | Comercial, multilíngue |
| `voyage-3` (Voyage) | Comercial |

## Embeddings x busca por palavra-chave

| Critério | Palavra-chave (BM25) | Embeddings |
| --- | --- | --- |
| Busca por | Termo exato | Significado |
| Sinônimos | Não entende | Entende |
| Termos raros/código | Muito bom | Pode errar |
| Custo | Baixo | Requer modelo |

> Na prática, a **busca híbrida** (vetorial + palavra-chave) costuma dar o melhor resultado.

## Erros comuns

- **Usar modelos diferentes para indexar e consultar** (os vetores ficam incompatíveis).
- **Ignorar o idioma**: para português, prefira modelos multilíngues.
- **Trocar o modelo sem reindexar** a base.
- **Não normalizar** os vetores quando a métrica exige.

## Casos de uso

| Situação | Uso |
| --- | --- |
| Busca semântica em documentos | Embeddings + banco vetorial |
| Deduplicação de textos | Comparar similaridade |
| Agrupamento (clustering) | Agrupar por proximidade |
| RAG | Indexar chunks e buscar os relevantes |
