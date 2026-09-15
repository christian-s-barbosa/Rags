---
titulo: O que é RAG
tipo: conceito
nivel: basico
categoria: RAG
tags: [rag, retrieval, augmentation, generation, pipeline, llm, memoria-nao-parametrica]
resumo: "Definição de RAG, o pipeline de três etapas (recuperação, aumentação, geração) e os conceitos-chave."
relacionados: ["Por que usar RAG", "Fontes e referências"]
fonte: https://pt.wikipedia.org/wiki/Gera%C3%A7%C3%A3o_aumentada_por_recupera%C3%A7%C3%A3o
---

# O que é RAG?

RAG (**Retrieval-Augmented Generation**) é um **framework de IA** que une sistemas tradicionais de **recuperação de informação** (como pesquisa e bancos de dados) aos recursos **generativos** dos LLMs.

Em vez de depender apenas do conhecimento **parametrizado** (armazenado nos pesos do modelo), o RAG **consulta documentos externos antes de responder**, incorporando uma **memória não paramétrica** — verificável e atualizável.

## Pipeline básico

O pipeline tem três etapas:

| Etapa | Nome | O que faz |
| --- | --- | --- |
| 1 | **Recuperação (retrieval)** | Busca trechos relevantes em uma base externa (páginas, docs, banco vetorial etc.) |
| 2 | **Aumentação (augmentation)** | Injeta esses trechos no prompt do LLM como contexto adicional |
| 3 | **Geração (generation)** | O LLM produz a resposta com base na pergunta + contexto recuperado |

Fluxo:

```
Pergunta → Recuperação (busca na base) → Aumentação (contexto no prompt) → Geração (LLM) → Resposta
```

## Conceitos-chave

| Conceito | Significado |
| --- | --- |
| **Conhecimento paramétrico** | O que o modelo aprendeu no treinamento (guardado nos pesos) |
| **Memória não paramétrica** | Conhecimento externo consultado na hora (a base de conhecimento) |
| **Base de conhecimento** | Conjunto de documentos que o sistema pode consultar |
| **Embeddings / banco vetorial** | Forma de buscar por **significado**, e não só por palavra exata |
| **Contexto** | Trechos recuperados que são entregues ao LLM junto com a pergunta |

## Em uma frase

RAG = **buscar** os trechos certos na sua base **+** **entregar** esses trechos ao LLM **+** **gerar** a resposta fundamentada neles.
