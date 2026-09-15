---
titulo: Re-ranking
tipo: conceito
nivel: intermediario
categoria: RAG
tags: [rag, reranking, cross-encoder, bi-encoder, precisao, latencia]
resumo: "O que é re-ranking, a diferença entre bi-encoder e cross-encoder, e como melhora a precisão do RAG."
relacionados: ["Recuperação (retrieval)", "Embeddings", "Avaliação de RAG"]
fonte: https://www.pinecone.io/learn/
---

# Re-ranking

## O que é?

**Re-ranking** é uma segunda etapa de ordenação: depois de recuperar vários candidatos, um modelo mais preciso **reordena** esses resultados e mantém só os melhores.

## Bi-encoder x cross-encoder

| Aspecto | Bi-encoder (embeddings) | Cross-encoder (reranker) |
| --- | --- | --- |
| Como funciona | Vetores calculados separadamente | Lê **pergunta + trecho juntos** |
| Velocidade | Muito rápido | Mais lento |
| Precisão | Boa | Melhor |
| Uso | Busca inicial (milhares) | Reordenar poucos (dezenas) |

## Fluxo típico

```
Base (milhares) --bi-encoder--> top 50 --cross-encoder--> top 5 --> LLM
```

1. **Recuperar** muitos candidatos (ex.: 50) com embeddings.
2. **Reordenar** com o reranker.
3. Enviar os **melhores** (ex.: 5) ao LLM.

## Modelos comuns

| Modelo | Observação |
| --- | --- |
| `BAAI/bge-reranker-v2-m3` | Multilíngue, muito usado |
| `BAAI/bge-reranker-base` | Menor e mais leve |
| Cohere Rerank | Comercial |

## Custo e trade-offs

- Aumenta a **precisão** dos trechos enviados ao LLM.
- Aumenta **latência** e consumo de **memória** (mais um modelo).
- Em máquinas com pouca RAM, pode ser melhor usar um reranker **menor** ou desligar.

## Erros comuns

- **Reordenar poucos** candidatos (não há o que melhorar).
- **Confundir rerank com a busca inicial**.
- **Ignorar o custo** de memória/latência.
- **Não medir** se o rerank realmente melhora (use avaliação).

## Casos de uso

| Situação | Benefício |
| --- | --- |
| Muitos chunks parecidos | Escolhe os mais relevantes |
| Respostas imprecisas | Melhora o contexto enviado |
| Base grande | Filtra ruído da busca inicial |
