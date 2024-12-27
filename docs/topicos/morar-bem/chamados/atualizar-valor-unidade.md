# **Atualizar Valor da Unidade**

Este guia passo a passo irá demonstrar como Atualizar o Valor das Unidades no sistema do **MORAR BEM**.

---

## **Execute a Query abaixo com owner JCGCOM**

---

    UPDATE COM_MB_UNIDADE_VALOR
    SET MBUV_NR_VALOR = 'NOVO VALOR'
    WHERE UND_IN_CODIGO IN (
            SELECT V.UND_IN_CODIGO
            FROM COM_MB_UNIDADE_MATRICULA M,
                JCGWEB.VW_MG_UNIDADE_COMPLETA U,
                COM_MB_UNIDADE_VALOR V,
                COM_MB_PROPOSTA P
            WHERE M.UND_NR_CODIGO = U.codigoUnidade
                AND U.codigoUnidade = V.UND_IN_CODIGO
                AND U.CODIGOFILIAL = 39559
                AND U.ETAPA LIKE '%CONDOMÍNIO X%'
                AND v.UND_IN_CODIGO NOT IN (
                SELECT PROP.UND_IN_CODIGO FROM COM_MB_PROPOSTA PROP
            )
        )

---