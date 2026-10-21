# Padrões de arquitetura

## RAG

```text
Pergunta ─▶ busca (índice vetorial/textual) ─▶ trechos relevantes ─▶ LLM ─▶ resposta + fontes
```

## Agente com ferramentas

```text
Objetivo ─▶ LLM decide ─▶ chama ferramenta (API) ─▶ observa resultado ─▶ repete ─▶ resposta
```

## Boas práticas

- Isole o acesso ao modelo atrás de um serviço interno (gateway de IA): autenticação, logs,
  limites e troca de provedor sem alterar os clientes.
- Ferramentas de agentes com **menor privilégio** e confirmação humana para ações irreversíveis.
- Trate a saída do modelo como **entrada não confiável**: valide antes de usar.
