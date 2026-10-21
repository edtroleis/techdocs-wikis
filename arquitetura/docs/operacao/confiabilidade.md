# Confiabilidade

## Requisitos mínimos por criticidade

| Criticidade | SLO de disponibilidade | Réplicas | Recuperação (RTO / RPO) |
|-------------|------------------------|----------|--------------------------|
| Alta | 99,95% | ≥ 3, multi-zona | 15 min / 5 min |
| Média | 99,9% | ≥ 2 | 1 h / 1 h |
| Baixa | 99% | 1 | 1 dia / 1 dia |

## Padrões de resiliência

- Timeouts em toda chamada remota.
- Retries com backoff exponencial e jitter, só para operações idempotentes.
- Circuit breaker para dependências instáveis.
- Degradação graciosa: o que o sistema faz quando a dependência cai?

### Circuit breaker

```plantuml
@startuml
hide empty description
[*] --> Fechado
Fechado : chamadas passam
Fechado --> Aberto : falhas > limite\nna janela
Aberto : chamadas falham rápido\n(fallback)
Aberto --> SemiAberto : após tempo de espera
SemiAberto : poucas chamadas de teste
SemiAberto --> Fechado : testes ok
SemiAberto --> Aberto : teste falhou
@enduml
```

### Retry com backoff

```mermaid
sequenceDiagram
    participant S as Serviço
    participant D as Dependência
    S->>D: tentativa 1
    D--xS: erro 503
    Note over S: espera 100 ms + jitter
    S->>D: tentativa 2
    D--xS: erro 503
    Note over S: espera 200 ms + jitter
    S->>D: tentativa 3
    D-->>S: 200 OK
```
