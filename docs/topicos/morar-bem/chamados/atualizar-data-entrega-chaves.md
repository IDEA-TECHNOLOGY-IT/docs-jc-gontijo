# **Atualizar Data de Entrega de Chaves**

Este guia passo a passo irá demonstrar como Atualizar a Data de Entrega de Chaves no sistema do **MORAR BEM**.

---

## **Execute a Query abaixo com owner JCGCOM**

     UPDATE COM_MB_PROPOSTA 
     SET mbpo_dt_entrega_chave = (DATA SOLICITADA) 
     WHERE COM_MB_PROPOSTA.MBPO_NR_CODIGO = (SELECT PRO.MBPO_NR_CODIGO FROM COM_MB_PROPOSTA_CONTRATO CON 
        INNER JOIN COM_MB_PROPOSTA PRO 
            ON CON.MBPO_NR_CODIGO = PRO.MBPO_NR_CODIGO 
        INNER JOIN COM_MB_INTERESSADO I 
            ON I.MBCL_NR_CODIGO = PRO.MBCL_NR_CODIGO 
     WHERE I.MBCL_TX_CHAVE = 'CPF DO INTERESSADO')

---

