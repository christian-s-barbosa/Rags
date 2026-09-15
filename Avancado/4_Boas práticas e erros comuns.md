---
titulo: Boas práticas e erros comuns
tipo: conceito
nivel: avancado
categoria: RAG
tags: [rag, boas-praticas, erros-comuns, producao, qualidade]
resumo: "Boas práticas para construir um RAG de qualidade e os erros mais comuns a evitar."
relacionados: ["Arquitetura do pipeline", "Avaliação de RAG", "Chunking"]
fonte: https://adentro.com.br/infraestrutura-rag-llm-empresas/
---

# Boas práticas e erros comuns

## Boas práticas

- **Comece simples**: embeddings + banco vetorial + LLM; melhore depois.
- **Chunks autocontidos**: prefixe com título/breadcrumb.
- **Guarde metadados** (arquivo, seção, nível, tags) para filtrar e citar.
- **Use busca híbrida** (vetorial + palavra-chave).
- **Aplique re-ranking** quando houver muitos candidatos.
- **Cite as fontes** na resposta.
- **Avalie com um conjunto de teste** fixo.
- **Versione** código, configuração e base.
- **Reindexe** sempre que mudar o modelo/estratégia de chunking.

## Erros comuns

| Erro | Consequência |
| --- | --- |
| Modelos de embedding diferentes na indexação e na consulta | Resultados ruins |
| Chunks grandes demais | Contexto diluído |
| Cortar tabelas/código | Perda de sentido |
| Só busca vetorial | Perde termos exatos |
| Sem metadados | Sem filtros nem citação |
| Sem avaliação | Não se sabe se melhorou |
| Contexto demais no prompt | Custo alto e ruído |
| Não tratar atualização da base | Respostas desatualizadas |
| Ignorar segurança/privacidade | Vazamento de dados |

## Checklist rápido

- [ ] Base indexada e versionada
- [ ] Chunks com contexto
- [ ] Metadados preenchidos
- [ ] Busca híbrida (se fizer sentido)
- [ ] Re-ranking configurado
- [ ] Conjunto de teste criado
- [ ] Fontes citadas na resposta
- [ ] Custos e latência monitorados

## Casos de uso

| Situação | Prática-chave |
| --- | --- |
| Base que muda muito | Reindexação automatizada |
| Dados sensíveis | LLM local / controle de acesso |
| Muitas perguntas repetidas | Cache de respostas |
| Qualidade instável | Avaliação contínua |
