# **Mailing**

O processo de Mailing consiste em captar novos clientes a partir de uma planilha gerada pela CODHAB e enviada para a JC Gontijo. Atualmente, o fluxo segue os seguintes passos. Primeiramente, a planilha é recebida e seus dados são analisados, sendo então cruzados com as informações já existentes no banco de dados interno utilizando o CPF como critério principal. Esse cruzamento tem como objetivo identificar quais registros que vão ser convocados para agendamento. Após essa verificação, para os CPFs encontrados no banco, a situação é alterada para "AGUARDA AGENDAMENTO". Esse procedimento garante que os interessados estejam devidamente classificados e prontos para a próxima etapa do processo.

---

## **Passo 1: Criar uma tabela no banco de dados com os dados da planilha**
1. Ao receber a planilha o primeiro passo é criar uma nova tabela de acordo com a planilha recebida, geralmente, a planilha contém dados como: CPF, Nome, Data de Nascimento, Celular etc.
2. Após criar a tabela popule a mesma com os dados da planilha.

## **Passo 2: Atualizar  a Tela de Cadastro**
1. Relacione a tabela criada com a tabela "COM_MB_INTRESSADO", como na planilha não é enviado o ID do Morar Bem dos candidatos é necessária fazer o relacionamento por meio do CPF, e atualizar a situação dos candidatos, abaixo estará um query de exemplo.

---

     UPDATE COM_MB_INTERESSADO I
     SET    I.MBAN_NR_CODIGO = 401 -- CÓDIGO DE "AGUARDA AGENDAMENTO"
     WHERE TABELA_CRIADA T =
     (SELECT CPF FROM TABELA_CRIADA T
        INNER JOIN COM_MB_INTERESSADO I
            ON I.MBCL_TX_CHAVE = T.CPF)

---

## **Passo 3: Gravar histórico de Interessados**
1. Após fazer os passos acima, vá para o tópico **[Gravar Histórico](topicos/morar-bem/chamados/gravar-historico.md):** e siga as intruções para **Gravar Histórico**.

---

## **Passo 4: Enviar Mailing para Email**
1. Feito todos os passos corretamente, exporte as colunas de **NOME, CPF, EMAIL, TELEFONE, DATA NASCIMENTO** da tabela **"COM_MB_INTERESSADO"** para Excel e envie-a para os seguintes emails:
    - marilia.venceslau@jcgontijo.com.br
    - pedro@ideatechnology.com.br

2. Copie para:
    - carla.vale@jcgontijo.com.br
    - edlene.damascena@jcgontijo.com.br
    - vanda.gois@jcgontijo.com.br
    - queila.miranda@jcgontijo.com.br
    - maycon@ideatechnology.com.br

---