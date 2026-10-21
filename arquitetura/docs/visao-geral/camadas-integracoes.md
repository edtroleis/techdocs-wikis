# Camadas e integrações

```mermaid
flowchart TB
    subgraph canais [Canais]
        web[Web · CDN]
        mobile[Mobile]
        parceiros[Parceiros · API gateway]
    end
    subgraph dominio [Serviços de domínio]
        a[Serviço A]
        b[Serviço B]
        c[Serviço C]
        a <-. eventos .-> b
        b <-. eventos .-> c
    end
    subgraph dados [Dados]
        db[(Bancos por serviço)]
        dw[(Data lake / warehouse)]
        cache[(Cache)]
    end
    canais -- HTTP/JSON --> dominio
    dominio --> dados
```

## Estilos de integração

| Estilo | Quando usar | Cuidado |
|--------|-------------|---------|
| Síncrono (HTTP) | Consulta com resposta imediata | Timeouts e retries com backoff |
| Assíncrono (eventos) | Notificar mudanças de estado | Idempotência e ordem |
| Batch | Grandes volumes sem urgência | Janela e reprocessamento |

### Síncrono x assíncrono

```plantuml
@startuml
skinparam shadowing false
actor Cliente
participant "Serviço A" as A
participant "Serviço B" as B
queue "Eventos" as E
participant "Serviço C" as C

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

!!! warning "Banco compartilhado"
    Serviços não acessam o banco de outro serviço. Integração é sempre por contrato.
