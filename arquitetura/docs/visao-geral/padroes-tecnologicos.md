# Padrões tecnológicos

Radar simplificado de tecnologias:

| Situação | Significado | Exemplos |
|----------|-------------|----------|
| **Adotar** | Padrão; suportado pela plataforma | Containers (Podman/K8s), PostgreSQL, OpenTelemetry |
| **Experimentar** | Pode usar com ADR e acompanhamento | Novos frameworks, bancos especializados |
| **Avaliar** | Estudo/PoC, fora de produção | Tecnologias emergentes |
| **Evitar** | Não usar em novos projetos | Bibliotecas sem manutenção, runtimes fora de suporte |

```mermaid
quadrantChart
    title Radar tecnológico
    x-axis Pouca maturidade --> Muita maturidade
    y-axis Pouco valor --> Muito valor
    quadrant-1 Adotar
    quadrant-2 Experimentar
    quadrant-3 Evitar
    quadrant-4 Avaliar
    Containers: [0.9, 0.9]
    PostgreSQL: [0.85, 0.75]
    OpenTelemetry: [0.7, 0.8]
    Agentes de IA: [0.25, 0.8]
    Banco vetorial: [0.35, 0.6]
    WebAssembly no servidor: [0.6, 0.3]
    Lib sem manutenção: [0.2, 0.15]
```

Mudanças no radar passam pelo fórum de arquitetura e viram um ADR.
