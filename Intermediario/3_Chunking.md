---
titulo: Chunking
tipo: conceito
nivel: intermediario
categoria: RAG
tags: [rag, chunking, chunk, divisao, overlap, contexto]
resumo: "O que é chunking, por que dividir documentos em pedaços e as principais estratégias e cuidados."
relacionados: ["Embeddings", "Recuperação (retrieval)", "Arquitetura do pipeline"]
fonte: https://codelabs.developers.google.com/codelabs/production-ready-ai-with-gc/8-advanced-rag-methods/advanced-rag-methods?hl=pt-br
---

# Chunking

## O que é?

**Chunking** é dividir documentos longos em **pedaços menores (chunks)** antes de gerar embeddings e indexar. Cada chunk é a unidade que será recuperada e enviada ao LLM.

## Por que é importante?

- Os modelos têm **limite de contexto**.
- Chunks muito grandes **diluem** o significado e pioram a busca.
- Chunks muito pequenos **perdem contexto**.
- A qualidade do chunk define a qualidade da recuperação.

## Estratégias

| Estratégia | Como funciona |
| --- | --- |
| **Tamanho fixo** | Corta a cada N caracteres/tokens |
| **Por parágrafo** | Respeita os parágrafos |
| **Por seção (markdown)** | Corta em títulos (`#`, `##`) |
| **Recursivo** | Tenta separadores em ordem (título → parágrafo → frase) |
| **Semântico** | Agrupa por mudança de significado |
| **Por sentença** | Cada sentença é um chunk |

## Tamanho e sobreposição (overlap)

- Tamanho comum: **200 a 800 tokens** por chunk.
- **Overlap**: repetir um trecho entre chunks vizinhos (ex.: 10–20%) para não cortar ideias no meio.

## Contexto no chunk

Um bom chunk é **autocontido**. Uma técnica simples é **prefixar** cada chunk com um cabeçalho:

```
[Git > Git commit > Alterar e desfazer commits]
git commit --amend  # corrige o último commit...
```

Isso melhora muito a recuperação, principalmente com tabelas.

## Erros comuns

- **Cortar tabelas/código no meio** (quebram o sentido).
- **Chunks grandes demais**, que misturam assuntos.
- **Sem overlap**, perdendo a ligação entre trechos.
- **Ignorar os títulos** como contexto.
- **Não reindexar** após mudar a estratégia de chunking.

## Casos de uso

| Situação | Estratégia |
| --- | --- |
| Documentação em Markdown | Por seção (`##`) + breadcrumb |
| PDFs longos | Recursivo + overlap |
| Código-fonte | Por função/classe |
| Base com tabelas | Manter a tabela inteira no chunk |
