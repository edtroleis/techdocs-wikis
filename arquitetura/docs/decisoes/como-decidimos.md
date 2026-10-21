# Como decidimos

!!! abstract "Em uma frase"
    O tamanho do fórum acompanha o tamanho do impacto: o time decide o que é local, e a arquitetura
    decide o que é transversal ou irreversível.

```mermaid
flowchart TD
    inicio([💡 Preciso tomar uma decisão]):::inicio --> escopo{Afeta outros times?}:::pergunta
    escopo -- Não --> reversivel{É reversível?}:::pergunta
    reversivel -- Sim --> time[👥 Time dono decide<br/>ADR no repo do serviço]:::time
    reversivel -- Não --> forum
    escopo -- Sim --> transversal{É transversal<br/>ou irreversível?}:::pergunta
    transversal -- Não --> envolvidos[🤝 Times envolvidos + arquitetura<br/>ADR + comunicação]:::envolvidos
    transversal -- Sim --> forum[🏛️ Fórum de arquitetura<br/>ADR nesta wiki]:::forum
    time --> registro[(📜 Registro de decisões)]:::registro
    envolvidos --> registro
    forum --> registro

    classDef inicio fill:#e2e8f0,stroke:#64748b,color:#0f172a
    classDef pergunta fill:#fef3c7,stroke:#f59e0b,color:#78350f
    classDef time fill:#dcfce7,stroke:#22c55e,color:#14532d
    classDef envolvidos fill:#dbeafe,stroke:#3b82f6,color:#1e3a8a
    classDef forum fill:#f3e8ff,stroke:#a855f7,color:#581c87
    classDef registro fill:#fee2e2,stroke:#ef4444,color:#7f1d1d
```

*Figura 7 · Árvore de decisão: quem decide depende do alcance e da reversibilidade.*

| Tipo de decisão | Quem decide | Registro |
|-----------------|-------------|----------|
| Local ao serviço, reversível | Time dono | ADR no repo do serviço |
| Afeta outros times | Times envolvidos + arquitetura | ADR + comunicação |
| Transversal ou irreversível | Fórum de arquitetura | ADR nesta wiki |

## Do rascunho à decisão

```mermaid
gantt
    title Ciclo típico de um ADR transversal
    dateFormat YYYY-MM-DD
    axisFormat %d/%m
    section Proposta
    Rascunho e PR             :a1, 2026-10-01, 2d
    section Comentários
    Período de comentários    :a2, after a1, 5d
    section Decisão
    Fórum de arquitetura      :milestone, a3, after a2, 0d
    Comunicação e registro    :a4, after a3, 1d
```

*Figura 8 · Uma decisão transversal leva cerca de duas semanas, com prazo fixo de comentários.*

!!! tip "Na prática"
    1. Escreva o ADR como **proposto** e abra um PR.
    2. Divulgue o link e fixe o prazo de comentários.
    3. Decida no fórum adequado e atualize o status.
    4. Registre no [registro de decisões](registro.md).

**Leia também:** [Modelo de ADR](modelo-adr.md) · [Wiki de Governança](http://localhost:3000/docs/default/component/wiki-governanca)
