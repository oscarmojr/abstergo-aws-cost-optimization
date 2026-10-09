# RELATÓRIO DE IMPLEMENTAÇÃO DE SERVIÇOS AWS

**Data:** 08/10/2026
**Empresa:** Abstergo Industries
**Responsável:** Oscar do Carmo Junior

## Introdução

Este relatório apresenta o processo de implementação de ferramentas na empresa **Abstergo Industries**, realizado por **Oscar do Carmo Junior**. O objetivo do projeto foi elencar 3 serviços AWS, com a finalidade de realizar diminuição de custos imediatos.

A Abstergo Industries é uma empresa farmacêutica que atua como hub de distribuição: recebe produtos, armazena, processa pedidos e se comunica com outras empresas (farmácias revendedoras) que atendem o cliente final. Hoje a empresa não possui nenhum serviço em nuvem, o que significa manter servidores próprios, licenças, energia, refrigeração, backup e equipe dedicada à infraestrutura, mesmo nos períodos em que esses recursos ficam ociosos.

A proposta é migrar gradualmente para a AWS, trocando **gasto fixo com equipamentos (CAPEX)** por **pagamento conforme o uso (OPEX)**: a empresa passa a pagar apenas pelo que realmente consome.

## Descrição do Projeto

O projeto de implementação de ferramentas foi dividido em 3 etapas, cada uma com seus objetivos específicos. A seguir, serão descritas as etapas do projeto:

### Etapa 1: Amazon EC2 (com Auto Scaling)

- **Nome da ferramenta:** Amazon EC2 – Elastic Compute Cloud, combinado com o EC2 Auto Scaling.
- **Foco da ferramenta:** Servidores virtuais sob demanda, que substituem os servidores físicos da empresa (sistema de gestão/ERP, sistema de pedidos, portal das farmácias parceiras).
- **Descrição de caso de uso:** Os sistemas que hoje rodam em máquinas próprias são migrados para instâncias EC2. O Auto Scaling aumenta automaticamente a quantidade de servidores nos horários de pico (por exemplo, quando as farmácias concentram pedidos no início da manhã ou no fim do mês) e reduz fora desses horários. Para a carga que funciona o tempo todo, a empresa pode contratar **Savings Plans** ou **Instâncias Reservadas**, que oferecem desconto em troca de um compromisso de uso de 1 ou 3 anos.
- **Como reduz custos:** Elimina a compra e a renovação de servidores, os contratos de manutenção de hardware e parte dos gastos com energia e refrigeração do data center local. A empresa deixa de dimensionar equipamentos "pelo pico" e passa a pagar pela capacidade realmente usada.
- **Principal ganho:** Infraestrutura que acompanha a demanda — sem servidor parado gerando custo e sem lentidão quando o volume de pedidos aumenta.

### Etapa 2: Amazon S3 (com classes de armazenamento e Glacier)

- **Nome da ferramenta:** Amazon S3 – Simple Storage Service, com as classes S3 Intelligent-Tiering e S3 Glacier.
- **Foco da ferramenta:** Armazenamento de arquivos e backup com alta durabilidade e custo ajustado à frequência de acesso.
- **Descrição de caso de uso:** Notas fiscais, pedidos, laudos, certificados de lote, registros de rastreabilidade de medicamentos e backups dos sistemas passam a ser guardados no S3. Documentos consultados com frequência ficam na classe padrão; documentos antigos, que precisam ser mantidos por exigência legal e regulatória (fiscal e sanitária), são movidos automaticamente — por meio de **regras de ciclo de vida** — para o S3 Glacier, cujo custo de armazenamento é muito menor.
- **Como reduz custos:** Substitui servidores de arquivos, storages e fitas/HDs de backup, que exigem compra, manutenção e espaço físico. A empresa paga apenas pelo volume armazenado, e o arquivo histórico fica na faixa de preço mais barata.
- **Principal ganho:** Armazenamento seguro, durável e praticamente ilimitado, com backup e retenção de documentos sem investimento em equipamentos.

### Etapa 3: AWS Lambda

- **Nome da ferramenta:** AWS Lambda.
- **Foco da ferramenta:** Computação *serverless* (sem servidor para gerenciar), cobrada apenas pelo tempo de execução de cada tarefa.
- **Descrição de caso de uso:** A comunicação com as farmácias revendedoras é feita por eventos: quando uma farmácia envia um pedido, uma função Lambda valida o pedido, consulta o estoque, gera a confirmação e atualiza o status. Outras funções podem processar arquivos enviados ao S3 (como XML de notas fiscais), enviar alertas de estoque baixo e gerar relatórios diários automaticamente.
- **Como reduz custos:** Tarefas que hoje exigiriam um servidor ligado 24 horas passam a ser cobradas somente quando executadas, em frações de segundo. Não há servidor ocioso, nem manutenção de sistema operacional, e a camada gratuita da AWS cobre um volume mensal de execuções.
- **Principal ganho:** Automação da integração com as farmácias parceiras a custo proporcional ao volume de pedidos, com menos trabalho manual e menos erros.

## Conclusão

A implementação de ferramentas na empresa **Abstergo Industries** tem como esperado **a eliminação de gastos com compra e manutenção de servidores e equipamentos de armazenamento (Amazon EC2 e Amazon S3), a cobrança proporcional ao uso real dos recursos, a redução do custo de guarda de documentos históricos (S3 Glacier) e a automação da comunicação com as farmácias revendedoras a baixo custo (AWS Lambda)**, o que aumentará a eficiência e a produtividade da empresa.

Para acompanhar os resultados, recomenda-se ativar desde o início o **AWS Cost Explorer** e o **AWS Budgets**, que permitem ao setor financeiro visualizar os gastos por serviço e receber alertas quando um limite de orçamento for atingido.

Recomenda-se a continuidade da utilização das ferramentas implementadas e a busca por novas tecnologias que possam melhorar ainda mais os processos da empresa.

## Anexos

- Estimativa de custos elaborada na AWS Pricing Calculator (https://calculator.aws)
- Inventário dos servidores e sistemas atuais da empresa
- Cronograma de migração por etapa
- Documentação oficial dos serviços: Amazon EC2, Amazon S3 e AWS Lambda (https://docs.aws.amazon.com)

---

**Assinatura do Responsável pelo Projeto:**

Oscar do Carmo Junior
