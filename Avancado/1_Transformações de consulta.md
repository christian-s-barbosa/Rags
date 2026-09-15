---
titulo: Transformações de consulta
tipo: conceito
nivel: avancado
categoria: RAG
tags: [rag, query-transformation, multi-query, hyde, decomposicao, reescrita, roteamento]
resumo: "Técnicas para melhorar a pergunta antes da busca: reescrita, expansão, decomposição, HyDE, step-back e roteamento."
relacionados: ["Recuperação (retrieval)", "Re-ranking", "Avaliação de RAG"]
fonte: https://codelabs.developers.google.com/codelabs/production-ready-ai-with-gc/8-advanced-rag-methods/advanced-rag-methods?hl=pt-br
---

# Transformações de consulta

## O que é?

São técnicas que **melhoram a pergunta** do usuário antes de buscar na base. Perguntas curtas, ambíguas ou muito específicas recuperam mal; transformá-las aumenta a chance de achar os trechos certos.

## Principais técnicas

| Técnica | O que faz |
| --- | --- |
| **Reescrita (rewrite)** | Reformula a pergunta para ficar mais clara |
| **Expansão (multi-query)** | Gera várias versões da pergunta e busca todas |
| **Decomposição** | Quebra uma pergunta complexa em subperguntas |
| **HyDE** | Gera uma resposta "hipotética" e busca por ela |
| **Step-back** | Pergunta mais genérica primeiro (conceito) |
| **Roteamento (routing)** | Decide qual base/índice usar |

## Multi-query (exemplo)

Pergunta: "como desfazer um commit já enviado?"

Variações geradas:

- "reverter commit publicado"
- "git revert commit remoto"
- "desfazer push"

Busca-se por todas e funde-se os resultados (RRF).

## HyDE

1. O LLM escreve uma **resposta fictícia** para a pergunta.
2. Usa-se o embedding **dessa resposta** para buscar.
3. Motivo: a resposta fictícia se parece mais com os documentos reais do que a pergunta curta.

## Decomposição

Pergunta: "qual a diferença entre merge e rebase e quando usar cada um?"

Subperguntas:

- "o que é merge?"
- "o que é rebase?"
- "quando usar merge ou rebase?"

## Erros comuns

- **Aplicar transformações caras** em toda pergunta (aumenta latência/custo).
- **Multi-query demais**, trazendo ruído.
- **Não avaliar** se a transformação realmente ajuda.
- **Perder a intenção original** ao reescrever.

## Casos de uso

| Situação | Técnica |
| --- | --- |
| Perguntas curtas/ambíguas | Reescrita |
| Perguntas complexas | Decomposição |
| Vocabulário diferente do documento | HyDE |
| Várias bases | Roteamento |
