# **Problema de condomínio não configurado na Tabela de Contas**

Este guia passo a passo irá demonstrar como Incluir Boletos de Taxa de Catório que sempre são solicitados pelos próprios usuários do sistema **MORAR BEM**.

---

## **Passo 1: Executar a Query abaixo para obter o código da Etapa** 
     SELECT DISTINCT u.codigoetapa
     FROM COM_MB_UNIDADE_MATRICULA M,
             JCGWEB.VW_MG_UNIDADE_COMPLETA U,
             COM_MB_UNIDADE_VALOR V, COM_MB_PROPOSTA P
                 WHERE M.UND_NR_CODIGO = U.codigoUnidade
                 AND U.codigoUnidade = V.UND_IN_CODIGO
                 AND U.CODIGOFILIAL = 39559
                 AND U.ETAPA LIKE '%CONDOMÍNIO X%'

## **Passo 2: Executar a Query abaixo para Inserir o condomínio**
     INSERT INTO TEMP_MB_CONDOMINIO_CONTAS cc (condominio, codigo_empreendimento, banco_boleto, est_in_codigo)
     VALUES (CONDOMÍNIO X, 39559, 'CEF', AQUI INSERIR O CÓDIGO OBTIDO DA CONSULTA ACIMA).

---