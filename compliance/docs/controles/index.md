# Controles

| ID | Controle | Implementação | Automatizado? |
|----|----------|---------------|:-------------:|
| C-01 | Autenticação forte | SSO + MFA | Sim |
| C-02 | Menor privilégio | Perfis por papel, revisão trimestral | Parcial |
| C-03 | Revisão de código | PR com 1+ aprovação, branch protegida | Sim |
| C-04 | Gestão de vulnerabilidades | SCA, SAST e scan de imagem no CI | Sim |
| C-05 | Gestão de segredos | Cofre de segredos; scan de segredos no CI | Sim |
| C-06 | Criptografia | TLS 1.2+; criptografia em repouso | Sim |
| C-07 | Logs e auditoria | Logs centralizados, retenção definida | Sim |
| C-08 | Gestão de mudanças | Deploy só por pipeline, com registro | Sim |
| C-09 | Continuidade | Backups testados; RTO/RPO por criticidade | Parcial |

Os controles C-03 a C-05 e C-08 já vêm prontos no
[Golden Path para Serviços](http://localhost:3000/docs/default/component/golden-path-servicos).
