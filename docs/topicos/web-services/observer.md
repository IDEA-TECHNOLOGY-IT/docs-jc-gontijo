# **Observer Morar Bem**

O Observer do Morar Bem, foi desenvolvido para monitorar a saúde de um sistema hospedado em um servidor com limitações de memória. O principal objetivo é evitar que o sistema trave devido à alta exigência de Memória RAM, garantindo que o servidor possa se recuperar automaticamente.

## **Problema**
O sistema Morar Bem está hospedado em um servidor com baixa capacidade de memória, o que ocasionalmente faz com que o sistema trave quando há muita demanda por RAM. Quando isso ocorre, o sistema não "morre" completamente, mas fica travado, necessitando de uma reinicialização manual do serviço IIS (Internet Information Services) para retomar o funcionamento normal.

## **Solução**
Foi desenvolvido um script em Python que realiza requisições HTTP periódicas para monitorar o status do sistema. Com base no código de resposta HTTP retornado, o script toma as seguintes ações:

- Código HTTP 200: Indica que o sistema está funcionando corretamente. O script simplesmente recomeça o ciclo de monitoramento sem tomar qualquer ação.
- Código HTTP 500: Indica um erro no servidor. Quando o script detecta este código, ele reinicia o serviço IIS automaticamente para garantir que o sistema volte a funcionar.

## **Estrutura do Projeto**
O projeto é composto pelos seguintes arquivos:

main.py: Script principal que realiza as requisições HTTP e reinicia o serviço IIS quando necessário.
requirements.txt: Lista de dependências do projeto (caso necessário).

## **Como Funciona**
O script faz uma requisição HTTP a cada 15 segundos para verificar a saúde do sistema.
Se o status da resposta for 200, o sistema está saudável e o ciclo de monitoramento continua após 15 segundos.
Se o status da resposta for 500, o script reinicia o serviço IIS no servidor, garantindo a recuperação do sistema.
Após reiniciar o IIS, o script continua o ciclo de monitoramento, verificando novamente o status da aplicação de 15 em 15 segundos.

<p>
    <div align="center">
        <img src="/docs/assets/diagramas/observer.jpg" alt="Diagrama Observer">
        <h6>Diagrama Observer.</h6>
    </div>
</p>

### Link do Repositório: https://github.com/IDEA-TECHNOLOGY-IT/servico-monitoramento-morar-bem