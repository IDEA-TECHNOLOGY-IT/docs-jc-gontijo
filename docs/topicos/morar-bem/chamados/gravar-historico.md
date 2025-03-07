# **Gravar Histórico/Nota de Interessados**

Este guia passo a passo irá demonstrar como Gravar Histórico/Nota de Interessados no sistema do **MORAR BEM**.

---

## **Gravar Histórico**
- A gravação de histórico é feita quando há mudanças na situação do Interessado, onde todas essas mudanças são armazenadas em uma tabela chamada de **COM_MB_PROVIDENCIA**.
- O histórico mais solicitado que seja gravado é o de **"Aguarda Agendamento"**, que nada mais é quando um Interessado está apto para receber uma proposta. Para gravar tal histórico, essas demandas geralmente são solicitadas após o processamento do Mailing. Para gravar o histórico basta executar a Query abaixo:

---
     DECLARE
         v_codigo NUMBER;
         BEGIN
            FOR rec IN (SELECT ID FROM TABELA_CRIADA) LOOP
                SELECT MAX(MBPR_NR_CODIGO) + 1
                INTO v_codigo
                FROM JCGCOM.COM_MB_PROVIDENCIA;
         INSERT INTO JCGCOM.COM_MB_PROVIDENCIA 
         (MBPR_NR_CODIGO, MBCL_NR_CODIGO, MBPR_DT_PROVIDENCIA, MBPR_TX_DESCRICAO, 
         MBPR_DT_REGISTRO, USUA_NR_CODIGO, MBPR_TX_ORIGEM, MBAN_NR_CODIGO, 
         MBPR_DT_CONCLUSAO, MBPR_DT_CONCLUSAO_LIMITE) 
         VALUES 
         (v_codigo, 
         rec.ID, 
         SYSDATE, 
         'CANDIDATO COM SITUAÇÃO ALTERADA PARA AGUARDA AGENDAMENTO EM 05/12/2024.', 
         SYSDATE, 
         23, 
         'M', 
         401, 
         NULL, 
         NULL);
     END LOOP;
     END; 
---

- **OBS: CASO SEJA SOLICITADO A GRAVAÇÃO DE OUTRO TIPO DE ANDAMENTO, CONSULTAR O CÓDIGO NA TABELA "COM_MB_TIPO_ANDAMENTO".**

---
## **Gravar Nota Informativa**
- A gravação de nota é feita quando é necessário informar a resposta obtida após entrar em contato com o Interessado, onde essas notas também são armazenadas na tabela **COM_MB_PROVIDENCIA**. Para grava-las basta executar a Query abaixo:

---
     DECLARE
       v_codigo NUMBER;
       v_total_registros NUMBER; 
     BEGIN
       SELECT COUNT(*)
       INTO v_total_registros
       FROM COM_MB_PROPOSTA P
       INNER JOIN COM_MB_INTERESSADO I
         ON P.MBCL_NR_CODIGO = I.MBCL_NR_CODIGO
       INNER JOIN INFO_PARA_NOTA IPN
         ON IPN.CPF = I.MBCL_TX_CHAVE;

       FOR rec IN (
         SELECT I.MBCL_NR_CODIGO, IPN.*
         FROM COM_MB_PROPOSTA P
         INNER JOIN COM_MB_INTERESSADO I
           ON P.MBCL_NR_CODIGO = I.MBCL_NR_CODIGO
         INNER JOIN INFO_PARA_NOTA IPN
           ON IPN.CPF = I.MBCL_TX_CHAVE
       ) LOOP
         SELECT MAX(MBPR_NR_CODIGO) + 1
         INTO v_codigo
         FROM JCGCOM.COM_MB_PROVIDENCIA;

         INSERT INTO JCGCOM.COM_MB_PROVIDENCIA 
         (MBPR_NR_CODIGO, MBCL_NR_CODIGO, MBPR_DT_PROVIDENCIA, MBPR_TX_DESCRICAO, 
          MBPR_DT_REGISTRO, USUA_NR_CODIGO, MBPR_TX_ORIGEM, MBAN_NR_CODIGO, 
          MBPR_DT_CONCLUSAO, MBPR_DT_CONCLUSAO_LIMITE) 
         VALUES 
         (
           v_codigo, 
           rec.MBCL_NR_CODIGO, 
           SYSDATE, 
           ' NOTA: Tel.: ' || rec.telefone || 
           ' Operador: ' || rec.operador || 
           ' Obs: ' || rec.obs_temp || 
           ' Data: ' || TO_CHAR(rec.dt_abertura, 'DD/MM/YYYY') || ' ' || rec.hora_abertura,
           SYSDATE, 
           23, 
           'M', 
           9090, 
           NULL, 
           NULL
         );
       END LOOP;
     END;

