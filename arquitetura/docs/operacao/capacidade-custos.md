# Capacidade e custos

!!! abstract "Em uma frase"
    Dimensione por **medição**, escale automaticamente e dê a todo recurso um **dono** e uma **etiqueta
    de custo**.

```mermaid
xychart-beta
    title "CPU média por hora e alvo do autoscaling (exemplo)"
    x-axis [00h, 03h, 06h, 09h, 12h, 15h, 18h, 21h]
    y-axis "CPU %" 0 --> 100
    bar [20, 15, 25, 60, 72, 68, 55, 30]
    line [40, 40, 40, 70, 70, 70, 70, 40]
```

*Figura 14 · Barras: CPU média; linha: alvo de utilização. Fora do horário comercial, o mínimo de
réplicas deixa a utilização baixa, e é aí que está a economia.*

<div class="grid cards" markdown>

-   📏 __Meça antes__

    ---

    Teste de carga define requests e limits, não a estimativa.

-   📈 __Escale sozinho__

    ---

    Autoscaling horizontal com mínimo e máximo definidos.

-   🏷️ __Etiquete tudo__

    ---

    `owner`, `system` e `ambiente` em todo recurso.

-   🔍 __Revise todo mês__

    ---

    Recursos ociosos e right-sizing na revisão mensal.

</div>

| Indicador | Meta |
|-----------|:----:|
| Utilização média de CPU | 40–70% |
| Recursos sem etiqueta de owner | 0 |
| Ambientes de dev desligados fora do horário | 100% |

**Leia também:** [Confiabilidade](confiabilidade.md) · [Princípios](../visao-geral/principios.md)
