---
titulo: Base de Conhecimento RAG
tipo: indice
nivel: basico
categoria: RAG
tags: [rag, indice, sumario, retrieval-augmented-generation, llm]
resumo: "Índice da base de conhecimento sobre RAG (Retrieval-Augmented Generation)."
relacionados: ["O que é RAG", "Embeddings", "Arquitetura do pipeline"]
fonte: https://aws.amazon.com/pt/what-is/retrieval-augmented-generation/
---

# Base de Conhecimento RAG

**RAG** (Retrieval-Augmented Generation, ou geração aumentada por recuperação) é uma técnica que combina a **busca em bases de conhecimento externas** com **grandes modelos de linguagem (LLMs)** para gerar respostas mais **precisas, atualizadas e fundamentadas**.

## Estrutura

| Pasta | Conteúdo | Arquivos |
| --- | --- | --- |
| `Basico/` | Fundamentos do RAG | 3 |
| `Intermediario/` | Componentes técnicos | 5 |
| `Avancado/` | Técnicas e produção | 4 |

## Basico

- [O que é RAG](<Basico/1_O que é RAG.md>) — definição, pipeline e conceitos-chave.
- [Por que usar RAG](<Basico/2_Por que usar RAG.md>) — principais benefícios.
- [Fontes e referências](<Basico/3_Fontes e referências.md>) — materiais em português e inglês.

## Intermediario

- [Embeddings](<Intermediario/1_Embeddings.md>) — texto em vetores e busca semântica.
- [Banco vetorial](<Intermediario/2_Banco vetorial.md>) — armazenar e buscar vetores.
- [Chunking](<Intermediario/3_Chunking.md>) — dividir documentos em pedaços.
- [Recuperação (retrieval)](<Intermediario/4_Recuperação.md>) — busca densa, esparsa e híbrida.
- [Re-ranking](<Intermediario/5_Re-ranking.md>) — reordenar os resultados.

## Avancado

- [Transformações de consulta](<Avancado/1_Transformações de consulta.md>) — melhorar a pergunta antes de buscar.
- [Avaliação de RAG](<Avancado/2_Avaliação de RAG.md>) — métricas e conjunto de teste.
- [Arquitetura do pipeline](<Avancado/3_Arquitetura do pipeline.md>) — componentes e fluxos.
- [Boas práticas e erros comuns](<Avancado/4_Boas práticas e erros comuns.md>) — o que fazer e o que evitar.

## Resumo em uma frase

Em vez de responder só com o que o modelo "decorou" no treinamento, o RAG **consulta documentos externos antes de responder**.
