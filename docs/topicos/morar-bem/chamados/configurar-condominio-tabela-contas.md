# **Configurar Condomínio na Tabela de Contas**

Este guia passo a passo irá demonstrar como Configurar Condomínio na Tabela de Contas no sistema **MORAR BEM**.

---

## **Passo 1: Obter Código da Unidade (EST_IN_CODIGO)**

---

    SELECT MAX(U.CODIGOETAPA) EST_IN_CODIGO  FROM  JCGWEB.VW_MG_UNIDADE_COMPLETA U 
     WHERE  U.CODIGOFILIAL  = 39559 
     AND U.ETAPA            LIKE '%CONDOMÍNIO X%' 

---

## **Passo 2: Inserir na Tabela "TEMP_MB_CONDOMINIO_CONTAS "**

---

    INSERT INTO TEMP_MB_CONDOMINIO_CONTAS C (C.CONDOMINIO, C.CODIGO_EMPREENDIMENTO, C.EST_IN_CODIGO, C.BANCO_BOLETO)
    VALUES ('CONDOMÍNIO X', '39559', 'EST_IN_CODIGO', 'CEF')

---

## **Passo 3: Verificar se a Inserção foi Bem Sucedida**

---

    SELECT C.*, ROWID
    FROM TEMP_MB_CONDOMINIO_CONTAS C
                    WHERE C.EST_IN_CODIGO = EST_IN_CODIGO

---