# Avaliação

Sem avaliação não há como saber se uma mudança de prompt ou modelo melhorou ou piorou.

| Tipo | Como | Quando |
|------|------|--------|
| Conjunto de referência | Perguntas com respostas esperadas | Toda mudança de prompt/modelo |
| Avaliação automática | Métricas e LLM como avaliador | No CI |
| Avaliação humana | Amostragem revisada por especialistas | Periódica |
| Testes adversariais | Prompt injection, vazamento de dados | Antes de produção |

Critérios típicos: **correção**, **fundamentação nas fontes**, **segurança** e **formato**.
