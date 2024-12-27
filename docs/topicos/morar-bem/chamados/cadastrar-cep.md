# **Cadastrar CEP**

Este guia passo a passo irá demonstrar como Cadastrar CEP de um condomínio no **MORAR BEM**.

---

## **Passo 1: Localizar o código da etapa do condomínio**

---

    SELECT DISTINCT 
    ETP.EST_IN_CODIGO                 AS CODIGOETAPA,
    'COND. ' || ETP.est_st_codigo     AS ETAPA
    FROM 
    GRUPOJCG.DBM_ESTRUTURA EMP
    ,GRUPOJCG.DBM_ESTRUTURA ETP
    ,COM_MB_PROPOSTA P
        WHERE EMP.EST_IN_CODIGO = ETP.PAI_EST_IN_CODIGO
            AND ETP.EST_CH_TIPOESTRUTURA = 'T'
            AND ETP.EST_IN_CODIGO = P.ETP_IN_CODIGO
            AND ETP.EST_IN_CODIGO = 'NUM COND'

---

## **Passo 2: Cadastrar na tabela COM_MB_CONDOMINIO_CEP os dados informados**
- Substitua ```e.CEP_TX_NUMERO``` pelo CEP solicitado e ```e.CONDOMINIO_IN_CODIGO``` pelo código da etapa encontrado pelo SELECT acima.

---

    UPDATE COM_MB_CONDOMINIO_CEP e
    SET    e.CEP_TX_NUMERO = xx.xxx-xxx
    WHERE  e.CONDOMINIO_IN_CODIGO = xxxxx

---

