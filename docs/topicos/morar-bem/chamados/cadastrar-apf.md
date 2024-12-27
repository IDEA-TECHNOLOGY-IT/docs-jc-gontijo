# **Cadastrar APF**

Este guia passo a passo irá demonstrar como Cadastrar APF no sistema **MORAR BEM**.

---

## **Passo 1: Localizar o código da etapa do condomínio**

---

    SELECT DISTINCT u.codigoetapa
    FROM COM_MB_UNIDADE_MATRICULA M,
         JCGWEB.VW_MG_UNIDADE_COMPLETA U,
         COM_MB_UNIDADE_VALOR V, COM_MB_PROPOSTA P
             WHERE M.UND_NR_CODIGO = U.codigoUnidade
             AND U.codigoUnidade = V.UND_IN_CODIGO
             AND U.CODIGOFILIAL = 39559
             AND U.ETAPA LIKE '%CONDOMÍNIO X%'

---

## **Passo 2: Cadastrar na tabela COM_MB_APF os dados informados**

---

    INSERT INTO COM_MB_APF 
        SELECT EST_IN_CODIGO, 'CONDOMINIO X',   '060604911'
        FROM GRUPOJCG.DBM_ESTRUTURA  
            WHERE FIL_IN_CODIGO = 39559  
                AND EST_CH_TIPOESTRUTURA = 'T' 
                AND EST_IN_CODIGO NOT IN (
        SELECT etp_in_codigo
        FROM com_mb_apf )
                AND EST_ST_NOME LIKE '%CONDOMÍNIO X%'

---

## **Passo 3: Verificar na tabela COM_MB_APF se registrou**

---

    SELECT APF.* 
    FROM COM_MB_APF APF 
        WHERE APF.ETP_TX_ETAPA LIKE '%CONDOMÍNIO X%'

---