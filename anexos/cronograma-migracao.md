# Cronograma de migração

| Fase | Semanas | Atividades | Entregável |
|---|---|---|---|
| 0. Preparação | 1–2 | Criar conta AWS, configurar acessos (IAM) e MFA; ativar Cost Explorer e Budgets; preencher o inventário de servidores | Conta pronta com alertas de orçamento |
| 1. Armazenamento (S3) | 3–5 | Criar buckets, migrar arquivos e backups, configurar regras de ciclo de vida para o Glacier | Arquivos e backups na nuvem |
| 2. Computação (EC2) | 6–10 | Migrar o portal e o sistema de pedidos; configurar Auto Scaling; migrar o ERP em janela de manutenção | Sistemas rodando na AWS |
| 3. Automação (Lambda) | 11–13 | Criar funções de recebimento de pedidos, processamento de NF-e e alertas de estoque | Integração automática com as farmácias |
| 4. Otimização | 14–16 | Analisar uso real, contratar Savings Plans para a carga fixa, desligar servidores antigos | Relatório de economia ao financeiro |

**Por que começar pelo S3:** é a etapa de menor risco, gera economia imediata em storage e backup e serve de aprendizado para a equipe antes de migrar os sistemas críticos.
