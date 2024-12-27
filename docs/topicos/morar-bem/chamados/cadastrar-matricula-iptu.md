# **Cadastrar Matrícula / IPTU de Unidade**

Este guia passo a passo irá demonstrar como Cadastrar Matrícula / IPTU de Unidade no sistema **MORAR BEM**.

---

## **Passo 1: Inserir o código das unidades**
- **OBS: Se o condomínio já estiver cadastro não precisa executar essa etapa.**

---

    INSERT INTO COM_MB_UNIDADE_MATRICULA (UND_NR_CODIGO)
        SELECT UND_IN_CODIGO
        FROM GRUPOJCG.JCG_CODHAB_UNIDADE U
        WHERE U.UND_IN_CODIGO  IN (
            SELECT A.codigoUnidade
            FROM JCGWEB.VW_MG_UNIDADE_COMPLETA A
            WHERE A.codigoFilial = 39559
                AND ETAPA like '%CONDOMÍNIO X%'
            )

---

## **Passo 2: Atualizar na tabela**
- Pegar as matrículas da planilha e atualizar no campo UND_NR_MATRICULA da tabela COM_MB_UNIDADE_MATRICULA.

---

    SELECT
    M.*,
    U.ETAPA,
    U.BLOCO,
    U.NUMERO,
    M.ROWID

    FROM
    COM_MB_UNIDADE_MATRICULA M,
    JCGWEB.VW_MG_UNIDADE_COMPLETA U
        WHERE
        M.UND_NR_CODIGO               = U.codigoUnidade
            AND U.CODIGOFILIAL        = 39559
            AND U.ETAPA               LIKE '%CONDOMÍNIO X%'
        ORDER BY U.ETAPA, U.BLOCO, U.NUMERO ASC

---