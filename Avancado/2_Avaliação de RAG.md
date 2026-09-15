---
titulo: Avaliação de RAG
tipo: conceito
nivel: avancado
categoria: RAG
tags: [rag, avaliacao, metricas, ragas, faithfulness, recall, ndcg, golden-dataset]
resumo: "Como avaliar um sistema de RAG: métricas de recuperação e de geração, frameworks e conjunto de teste."
relacionados: ["Recuperação (retrieval)", "Re-ranking", "Boas práticas e erros comuns"]
fonte: https://docs.llamaindex.ai/
---

# Avaliação de RAG

## O que é?

Avaliar um RAG é medir a **qualidade** em duas partes: a **recuperação** (achou os trechos certos?) e a **geração** (respondeu bem com base neles?).

## Métricas de recuperação

| Métrica | Pergunta que responde |
| --- | --- |
| **Recall@k** | A resposta estava entre os k recuperados? |
| **Hit rate@k** | Quantas perguntas tiveram acerto nos k? |
| **MRR** | Em que posição apareceu o primeiro acerto? |
| **nDCG** | Qualidade da ordenação |
| **Context relevance** | Os trechos são relevantes à pergunta? |

## Métricas de geração

| Métrica | Pergunta que responde |
| --- | --- |
| **Faithfulness** | A resposta é fiel ao contexto (sem inventar)? |
| **Answer relevance** | A resposta responde à pergunta? |
| **Context precision/recall** | O contexto usado era o ideal? |

## Frameworks

| Ferramenta | Uso |
| --- | --- |
| **RAGAS** | Métricas específicas de RAG |
| **TruLens** | Avaliação e rastreio |
| **DeepEval** | Testes de LLM/RAG |

## Conjunto de teste (golden dataset)

Monte um conjunto de **perguntas com a resposta/arquivo esperado**:

```
pergunta: "como desfazer o último commit?"
esperado: "Basico/7_Desfazer alterações.md"
```

Sem isso, não dá para medir nem comparar mudanças.

## Erros comuns

- **Não avaliar** e só "achar" que melhorou.
- **Avaliar só a geração**, ignorando a recuperação.
- **Conjunto de teste pequeno/irreal**.
- **Mudar várias coisas de uma vez**, sem saber o que ajudou.

## Casos de uso

| Situação | Foco |
| --- | --- |
| Ajustar chunking | Recall@k |
| Escolher reranker | nDCG / precisão |
| Reduzir alucinação | Faithfulness |
| Comparar modelos | Conjunto de teste fixo |
