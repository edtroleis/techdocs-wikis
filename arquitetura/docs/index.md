# Wiki de Arquitetura

!!! note "Conteúdo demonstrativo"
    Referência de arquitetura técnica. Adapte princípios e padrões às decisões aprovadas pelo
    fórum de arquitetura da organização.

Tudo o que você precisa saber sobre **Arquitetura Técnica**: os princípios que orientam as
escolhas, como as decisões são tomadas e registradas, e o que se espera de um sistema em operação.

## Arquitetura de referência

![Arquitetura de referência: canais, gateway, serviços de domínio, eventos, dados e capacidades transversais](assets/arquitetura-referencia.svg)

*Figura 1: visão de referência. Canais chegam aos serviços pelo gateway; serviços integram por
eventos e têm dados próprios; plataforma, observabilidade e segurança atravessam todas as camadas.*

## Conteúdo

| Seção | Para quê |
|-------|----------|
| [Visão geral](visao-geral/principios.md) | Princípios, camadas e padrões tecnológicos |
| [Decisões](decisoes/como-decidimos.md) | Como decidir, modelo e registro de ADRs |
| [Operação](operacao/confiabilidade.md) | Confiabilidade, capacidade e custos |

O caminho prático para aplicar esta wiki está nos golden paths de
[Serviços](http://localhost:3000/docs/default/component/golden-path-servicos) e
[Frontend](http://localhost:3000/docs/default/component/golden-path-frontend).
