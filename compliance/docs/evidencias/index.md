# Evidências

Evidência boa é **gerada automaticamente**, **datada** e **guardada fora do alcance de quem a
produz**.

| Controle | Evidência | Fonte |
|----------|-----------|-------|
| C-03 Revisão de código | Histórico de PRs aprovados | GitHub |
| C-04 Vulnerabilidades | Relatórios de scan por build | CI |
| C-07 Logs | Configuração de retenção + amostras | Plataforma de logs |
| C-08 Mudanças | Registro de deploys com versão e aprovador | Pipeline |
| C-09 Continuidade | Relatório do último teste de restore | Time dono |

## Boas práticas

- Não gere evidência manualmente às vésperas da auditoria.
- Guarde por pelo menos o período exigido pela obrigação.
- Associe cada evidência ao ID do controle.
