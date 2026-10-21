# Camadas e integrações

!!! abstract "Em uma frase"
    Três camadas (canais, domínio e dados) e três estilos de integração (síncrono, eventos e batch),
    sempre por contrato e nunca por banco compartilhado.

```mermaid
flowchart TB
    subgraph canais [Canais]
        web[🌐 Web · CDN]:::canal
        mobile[📱 Mobile]:::canal
        parceiros[🤝 Parceiros]:::canal
    end
    gw{{🛡️ API gateway}}:::gateway
    subgraph dominio [Serviços de domínio]
        a[Serviço A]:::servico
        b[Serviço B]:::servico
        c[Serviço C]:::servico
    end
    bus[[📨 Barramento de eventos]]:::evento
    subgraph dados [Dados]
        dba[(Banco A)]:::dados
        dbb[(Banco B)]:::dados
        dbc[(Banco C)]:::dados
        dw[(Data lake)]:::dados
    end

    web & mobile & parceiros -- HTTP/JSON --> gw
    gw --> a & b & c
    a & b & c <-.-> bus
    a --> dba
    b --> dbb
    c --> dbc
    bus -- ingestão --> dw

    classDef canal fill:#dbeafe,stroke:#3b82f6,color:#1e3a8a
    classDef gateway fill:#fef3c7,stroke:#f59e0b,color:#78350f
    classDef servico fill:#dcfce7,stroke:#22c55e,color:#14532d
    classDef evento fill:#ecfccb,stroke:#84cc16,color:#365314
    classDef dados fill:#f3e8ff,stroke:#a855f7,color:#581c87
```

*Figura 4 · De cima para baixo: canais passam pelo gateway, cada serviço tem o próprio banco, os serviços conversam por eventos e os eventos alimentam o data lake.*

## Estilos de integração

=== "🔁 Síncrono (HTTP)"

    **Quando usar:** consulta que precisa de resposta imediata.

    | Faça | Evite |
    |------|-------|
    | Timeout em toda chamada | Cadeias longas de chamadas síncronas |
    | Retry com backoff, só se idempotente | Retry infinito |
    | Circuit breaker para dependência instável | Chamar o banco de outro serviço |

=== "📨 Assíncrono (eventos)"

    **Quando usar:** notificar uma mudança de estado a quem interessar.

    | Faça | Evite |
    |------|-------|
    | Consumidores idempotentes | Assumir ordem global |
    | Schema de evento versionado | Evento com o "banco inteiro" no payload |
    | Dead-letter queue monitorada | Ignorar mensagens com erro |

=== "📦 Batch"

    **Quando usar:** grandes volumes sem urgência.

    | Faça | Evite |
    |------|-------|
    | Janela e SLA definidos | Rodar em horário de pico |
    | Reprocessamento seguro | Arquivos sem checksum |

## Síncrono x assíncrono lado a lado

```plantuml
@startuml
skinparam shadowing false
skinparam sequenceMessageAlign center
actor Cliente
participant "Serviço A" as A #DCFCE7
participant "Serviço B" as B #DCFCE7
queue "Eventos" as E #ECFCCB
participant "Serviço C" as C #DCFCE7

== Síncrono: resposta imediata ==
Cliente -> A : GET /pedidos/42
A -> B : GET /clientes/7 (timeout 2s)
B --> A : 200 {cliente}
A --> Cliente : 200 {pedido + cliente}

== Assíncrono: notificação de mudança ==
Cliente -> A : POST /pedidos
A --> Cliente : 202 Accepted
A -> E : pedido.criado
E -> C : pedido.criado
C -> C : processa (idempotente)
@enduml
```

*Figura 5 · No síncrono o cliente espera a cadeia toda; no assíncrono ele recebe `202` e o trabalho segue por eventos.*

!!! danger "Banco compartilhado"
    Serviços **não** acessam o banco de outro serviço. Integração é sempre por contrato.

**Leia também:** [Princípios](principios.md) · [Confiabilidade](../operacao/confiabilidade.md)
