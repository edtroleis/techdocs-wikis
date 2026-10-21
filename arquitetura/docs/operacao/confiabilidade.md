# Confiabilidade

!!! abstract "Em uma frase"
    A criticidade define o SLO, e o SLO define réplicas, recuperação e padrões de resiliência.
    Confiabilidade é **medida**, não presumida.

## Requisitos por criticidade

| Criticidade | SLO · parada/mês | Réplicas | RTO / RPO |
|-------------|:----------------:|:--------:|:---------:|
| 🔴 Alta | 99,95% · ~22 min | 3+ multi-zona | 15 min / 5 min |
| 🟡 Média | 99,9% · ~43 min | 2+ | 1 h / 1 h |
| 🟢 Baixa | 99% · ~7 h | 1 | 1 dia |

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'pie1': '#3b82f6', 'pie2': '#f59e0b', 'pie3': '#a855f7', 'pie4': '#22c55e', 'pie5': '#ef4444', 'pieStrokeColor': '#ffffff', 'pieSectionTextColor': '#ffffff', 'pieTitleTextColor': '#94a3b8', 'pieLegendTextColor': '#94a3b8'}}}%%
pie showData
    title Causas de incidentes nos últimos 12 meses (exemplo)
    "Mudança/deploy" : 42
    "Dependência externa" : 23
    "Capacidade" : 15
    "Configuração" : 12
    "Infraestrutura" : 8
```

*Figura 11 · A maioria dos incidentes vem de mudanças, por isso deploy progressivo e rollback rápido são obrigatórios.*

## Padrões de resiliência

=== "⏱️ Timeout"

    Toda chamada remota tem timeout **menor** que o do chamador. Sem timeout, uma dependência
    lenta derruba quem a chama.

=== "🔁 Retry com backoff"

    Só para operações **idempotentes**, com backoff exponencial e jitter, e com limite de tentativas.

=== "🔌 Circuit breaker"

    Depois de N falhas, para de chamar a dependência por um tempo e usa um fallback.

=== "🪂 Degradação graciosa"

    Defina o que o sistema faz sem a dependência: cache, resposta parcial ou fila para depois.

### Circuit breaker

```plantuml
@startuml
skinparam shadowing false
hide empty description
skinparam state {
  BackgroundColor<<ok>> #DCFCE7
  BorderColor<<ok>> #22C55E
  BackgroundColor<<falha>> #FEE2E2
  BorderColor<<falha>> #EF4444
  BackgroundColor<<teste>> #FEF3C7
  BorderColor<<teste>> #F59E0B
}
state Fechado <<ok>> : chamadas passam
state Aberto <<falha>> : falha rápido (fallback)
state SemiAberto <<teste>> : poucas chamadas de teste
[*] --> Fechado
Fechado --> Aberto : falhas > limite na janela
Aberto --> SemiAberto : após tempo de espera
SemiAberto --> Fechado : testes ok
SemiAberto --> Aberto : teste falhou
@enduml
```

*Figura 12 · Estados do circuit breaker.*

### Retry com backoff

```mermaid
sequenceDiagram
    autonumber
    participant S as Serviço
    participant D as Dependência
    S->>D: tentativa 1
    D--xS: 503
    Note over S: espera 100 ms + jitter
    S->>D: tentativa 2
    D--xS: 503
    Note over S: espera 200 ms + jitter
    S->>D: tentativa 3
    D-->>S: 200 OK
```

*Figura 13 · O intervalo dobra a cada tentativa; o jitter evita que todos os clientes tentem ao mesmo tempo.*

**Leia também:** [Capacidade e custos](capacidade-custos.md) · [Golden Path: observabilidade](http://localhost:3000/docs/default/component/golden-path-servicos/4-producao/observabilidade/)
