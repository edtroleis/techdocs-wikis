# Engenharia de prompts

1. **Seja específico**: papel, tarefa, formato de saída e restrições.
2. **Dê contexto**: inclua os dados necessários em vez de esperar que o modelo saiba.
3. **Mostre exemplos** do resultado esperado.
4. **Peça estrutura** (JSON com schema) quando a saída for consumida por código.
5. **Versione os prompts** junto do código e avalie mudanças antes de publicar.

```text
Você é um assistente que responde dúvidas sobre a documentação interna.
Responda apenas com base nos trechos abaixo. Se a resposta não estiver neles, diga que não sabe.
Cite a fonte de cada afirmação.

<trechos>
...
</trechos>
```
