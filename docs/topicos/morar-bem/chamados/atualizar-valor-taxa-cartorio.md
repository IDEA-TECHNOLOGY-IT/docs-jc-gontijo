# **Atualizar Valor Taxa de Cartório**

Este guia passo a passo irá demonstrar como atualizar o valor da Taxa de Cartório sistema do **MORAR BEM**.

A atualização é feita em 3 etapas, são elas:
    - Atualizar nos Termos de Ciência e Agendamento com o Correspondente Bancário (COBAN).
    - Atualizar no email de apresentação.
    - Atualizar valor do boleto gerado pelo Morar Bem.

---

## **1º Passo: Atualizar nos Termos de Ciência e Agendamento com o Correspondente Bancário (COBAN)**
- Entre no servidor ```10.1.1.104```.
- Vá para o diretório: ```C:\WEB\JCG\MorarBem\Web\MorarBem\Reports\MorarBem```.
- Identifique os relatórios:
    - JCG_REL_MB_TERMO_CIENCIA_ITAPOA.rpt2
    - JCG_REL_MB_TERMO_AGENDA_COBAN_ITAPOA_v2.rpt2
- Faça uma cópia dos relatórios acima na Área de Trabalho, e altere a extensão dos arquivos de ```.rpt2``` para ```.rpt``` para que seja possível alterar o corpo do relatório.
- Após realizar a alteração, abra o relatório e localize o tópico que trata da taxa de cartório. Para facilitar a identificação, abaixo estão imagens que destacam o local exato onde o valor da taxa de cartório está mencionado.

<p>
    <div align="center">
        <img src="/docs/assets/atualizar-valor-taxa-cartorio/1.png" alt="Termo Ciência">
        <h6>Imagem 1: Termo Ciência.</h6>
    </div>
</p>

<p>
    <div align="center">
        <img src="/docs/assets/atualizar-valor-taxa-cartorio/2.png" alt="Agendamento COBAN">
        <h6>Imagem 2:Agendamento COBAN.</h6>
    </div>
</p>

- Após concluir a mudança de valor, renomeie novamente a extensão de ```.rpt``` para ```.rpt2``` e substitua os arquivos no diretório ```C:\WEB\JCG\MorarBem\Web\MorarBem\Reports\MorarBem``` pelos arquivos atualizados.
    - **Observação: É recomendado realizar o backup do relatório antes de efetuar a substituição.**

---

## **2º Passo: Atualizar no email de apresentação**
- Entre no servidor ```10.10.10.84```.
- Execute a consulta abaixo:

---

     SELECT e.*, e.rowid FROM COM_MB_TIPO_EMAIL e
                    WHERE e.mbte_nr_codigo IN (3, 7)

- Localize na coluna ```MBTE_TX_CORPO``` o valor antigo da taxa de cartório e altere para o novo valor.

---

## **3º Passo: Atualizar valor do boleto gerado pelo Morar Bem**
- Acesse o código fonte do Morar Bem.
- Na página ```MorarBemContratoController.cs```, procure o método ```InserirProSolutoTaxa```.

---
     public void InserirProSolutoTaxa(string ref_Gerenciador, int codigoInteressado) 
    {
	    InserirBoletoProsoluto(ref_Gerenciador, codigoInteressado, "1764,50", "T");
    }

---

- Atualize o 3º parâmetro, no exemplo acima representado por 1764.50, para o novo valor da taxa de cartório.
- Faça o **[Deploy](processos/deploy.md)** e faça a validação pelo Morar Bem.

---