---
titulo: Por que usar RAG
tipo: conceito
nivel: basico
categoria: RAG
tags: [rag, beneficios, precisao, alucinacao, atualizacao, transparencia]
resumo: "Principais benefícios do RAG: precisão, menos alucinações, atualização fácil, contexto próprio e rastreabilidade."
relacionados: ["O que é RAG", "Fontes e referências"]
fonte: https://www.oracle.com/br/artificial-intelligence/generative-ai/retrieval-augmented-generation-rag/
---

# Por que usar RAG?

Principais benefícios apontados pelas fontes:

| Benefício | Descrição |
| --- | --- |
| **Mais precisão e menos alucinações** | O modelo responde com base em documentos reais, não só no que "lembra" do treinamento |
| **Atualização fácil** | Basta atualizar a base de conhecimento, **sem retreinar** o LLM |
| **Contexto específico da organização** | Conecta o LLM aos **seus próprios dados** (manuais, políticas, código etc.) |
| **Transparência e rastreabilidade** | É possível mostrar **de onde veio** cada informação usada na resposta |

## RAG x LLM sozinho

| Critério | LLM sozinho | Com RAG |
| --- | --- | --- |
| Fonte da resposta | Conhecimento do treinamento | Documentos consultados na hora |
| Atualização | Exige retreinar/ajustar | Só atualizar a base |
| Alucinações | Mais provável | Reduzidas (resposta ancorada) |
| Dados privados | Não conhece | Conectável |
| Rastreabilidade | Difícil | Alta (cita as fontes) |

## Quando faz sentido usar

- Quando a resposta depende de **documentos que mudam** com frequência.
- Quando é preciso usar **dados internos/privados**.
- Quando a **exatidão** e a **citação das fontes** importam.
- Quando retreinar o modelo seria **caro ou lento**.
