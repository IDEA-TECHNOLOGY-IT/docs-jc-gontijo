# Tabelas 

| Nome da Tabela            | Chave Primária      |   Chave Estrangeira       | Descrição                         |
|---------------------------|---------------------|---------------------------|-----------------------------------|
| COM_MB_INTERESSADO        | MBCL_NR_CODIGO      | Não                       | Tabela de Interessados/Candidatos |
| COM_MB_PROPOSTA           | MBPO_NR_CODIGO      | Sim -> COM_MB_INTERESSADO | Tabela de Propostas               |
| COM_MB_PROPOSTA_PROSOLUTO | MBPS_NR_CODIGO      | Sim -> COM_MB_PROPOSTA    | Tabela de Parcelas/Boletos        |
| COM_MB_PROPOSTA_CONTRATO  | MBPO_NR_CODIGO      | Sim -> COM_MB_PROPOSTA    | Tabela de Contrato                |
| COM_MB_TIPO_ANDAMENTO     | MBAN_NR_CODIGO      | Não                       | Tabela de Situações               |
| COM_MB_PROVIDENCIA        | MBPR_NR_CODIGO      | Sim -> COM_MB_INTERESSADO | Tabela de Histórico de Cliente    |

