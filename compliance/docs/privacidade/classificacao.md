# Classificação de dados

| Classe | Exemplos | Controles mínimos |
|--------|----------|-------------------|
| Pública | Conteúdo do site | Integridade |
| Interna | Wikis, docs | Acesso autenticado |
| Confidencial | Dados pessoais, contratos | Criptografia, acesso por necessidade, auditoria |
| Restrita | Dados sensíveis (LGPD art. 5º, II), credenciais | Criptografia forte, acesso nominal aprovado, mascaramento |

Componentes que tratam dados confidenciais ou restritos devem declarar isso na documentação
do serviço.
