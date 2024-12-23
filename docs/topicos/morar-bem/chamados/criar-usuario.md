# **Como Criar um Usuário**

Este guia passo a passo irá demonstrar como criar um novo usuário no sistema **MORAR BEM**, com ilustrações de cada etapa para facilitar o entendimento.

---

## **Passo 1: Acessar o Menu de Usuários**
1. Após fazer login no sistema, vá até o **menu principal**.
2. Clique na opção **"Configurações"** no painel superior.
3. Acesse a opção **"Usuário (JCG)"** 

<p><div align="center">
  <img src="../../assets/criar-usuario/1.png" alt="Menu de Usuários">
  <h6>Imagem 1: Menu de Usuários</h6>
</div></p>

---

## **Passo 2: Acessar a Tela de Cadastro**
1. Na tela de listagem de usuários, clique no botão **"Incluir Usuário"**.
2. Você será redirecionado para o formulário de cadastro.

<p>
  <div align="center">
    <img src="../../assets/criar-usuario/2.png" alt="Botão Incluir Usuário">
    <h6>Imagem 2: Botão Incluir Usuário</h6>
  </div>
</p>

---

## **Passo 3: Preencher os Dados do Usuário**
1. Complete os campos obrigatórios no formulário:
   - **Login**: Insira o Login que o usuário utilizará para acessar o MORAR BEM (Geralmente utilizamos o primeiro e o último nome do usuário).
      - **Exemplo**: exemplo.teste.
   - **Nome**: Adicione o Nome do usuário que será informado no chamado.
   - **Perfil**: Escolha o tipo de usuário.
   - **Senha**:  A senha utilizamos nossa senha padrão (123456), que será demonstrado como inseri-la nos próximos passos.

<p><div align="center">
  <img src="../../assets/criar-usuario/3.png" alt="Formulário Cadastro de Usuário">
  <h6>Imagem 3: Formulário Cadastro de Usuário.</h6>
</div></p>

---

## **Passo 4: Verificar o Novo Usuário**
1. Acesse o Banco de Dados no Servidor com IP: 10.10.10.84,
2. Utilizando o Owner JCGCOM ou JCGWEB, execute a Query a seguir:
---
     SELECT U.*, U.ROWID FROM JCGWEB.JCG_USUARIO U 
     WHERE U.USU_TX_NOME LIKE 'Exemplo'
---
4. Exemplo será o Nome de usuário que você inseriu.
5. Após executar a Query acima, você obterá esse resultado: 

<p><div align="center">
  <img src="../../assets/criar-usuario/4.png" alt="Resulatdo Query acima">
  <h6>Imagem 4: Resulatdo Query acima.</h6>
</div></p>

5. Clique no cadeado destacado na imagem e altere as 2 colunas demarcadas para o seguinte:
   - USU_TX_SENHA: ```á
Ü9IºY«¾VàWòˆ>```
   - USU_CH_AUT_WINDOWS: ```N```.

6. Após alterar, clique no ícone de "Check" destacado na imagem abaixo.
   <p><div align="center">
  <img src="../../assets/criar-usuario/5.png" alt="Postar Mudanças">
  <h6>Imagem 5: Postar Mudanças.</h6>
</div></p>

7. Agora, só commitar as mudançar no banco de dados.
   <p><div align="center">
  <img src="../../assets/criar-usuario/6.png" alt="Commit">
  <h6>Imagem 6: Commit.</h6>
</div></p>