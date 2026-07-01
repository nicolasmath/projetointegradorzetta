# Aplicação Java Web — Deploy com Tomcat e MySQL

[← Home](Home)

**Data:** 27 e 28 de maio de 2026  
**Responsáveis:** Gabriel M. e Sara  
**Stack:** Eclipse IDE + Apache Tomcat + MySQL Workbench + Servidor Debian (MySQL)

---

## Fluxo geral do processo

```
Copiar o projeto Agenda para o workspace
      ↓
Importar no Eclipse (perspectiva Java EE)
      ↓
Configurar IP e credenciais do banco em DAO.java
      ↓
Exportar como arquivo .war
      ↓
Criar o banco de dados no MySQL Workbench
      ↓
Restaurar o dump do banco (Data Import/Restore)
      ↓
Fazer o deploy do .war no Apache Tomcat
      ↓
Testar o acesso via navegador
```

---

## Parte 1 — Eclipse IDE

### 1. Copiar o projeto para o workspace

No Windows, navegar até:

```
C:\Usuários\<seu usuário>\workspace
```

Colar a pasta `Agenda` dentro do diretório `workspace`.

### 2. Abrir a perspectiva Java EE

```
Window → Perspective → Open Perspective → Other → Java EE
```

### 3. Importar o projeto

```
File → Import → General → Existing Projects into Workspace
→ Browse → selecionar a pasta "workspace"
→ Marcar o projeto Agenda
→ Finish
```

### 4. Configurar a conexão com o banco de dados

No projeto Agenda, acessar:

```
Java Resources → model → DAO.java
```

Localizar o trecho de conexão e alterar:

```java
// Exemplo do que deve ser ajustado em DAO.java
String url  = "jdbc:mysql://192.168.20.40:3306/agenda?useTimezone=true&serverTimezone=UTC";
String user = "dba";
String pass = "123@Senac";
```

> Substituir o IP pelo endereço real do servidor MySQL no ambiente. Salvar com **Ctrl+Shift+S** (Save All).

![DAO.java configurado no Eclipse IDE](Imagens/agenda-dao-eclipse.png)

### 5. Exportar como arquivo WAR

```
Botão direito no projeto Agenda
→ Export → WAR File
→ Destination: agenda.war
→ Finish
```

---

## Parte 2 — MySQL Workbench (banco de dados)

### Pré-requisito

Ter o MySQL instalado no servidor Debian e acessível remotamente na porta 3306. Verificar a conexão no Workbench — se o IP não estiver correto:

```
Botão direito na conexão → Edit Connection → alterar o IP
```

### 1. Criar o banco de dados

Na aba **Query 1**, executar:

```sql
show databases;
create database agenda;
show databases;
use agenda;
```

![Banco agenda criado — Schemas e Query 1](Imagens/agenda-schemas-query.png)

### 2. Restaurar o dump (Data Import/Restore)

```
Administration → Data Import/Restore
→ Import from Self-Contained File
→ [...] → selecionar: Dump20260527.sql
   (localizado dentro da pasta agenda)
→ Start Import
```

![Tela de Data Import/Restore com dump selecionado](Imagens/agenda-data-import.png)

Após a importação, clicar em **Refresh** nos Schemas para confirmar que o banco `agenda` apareceu com as tabelas restauradas.

### 3. Verificar os dados importados

```sql
use agenda;
show tables;
select * from contato;
```

---

## Parte 3 — Apache Tomcat (deploy)

### 1. Acessar o painel do Tomcat

```
http://192.168.20.20:8080
```

> O Tomcat está instalado no Srv-APP-01 (192.168.20.20), mesmo servidor do GLPI e WordPress.

### 2. Fazer o deploy do arquivo WAR

```
Manager App → Deploy
→ WAR file to deploy → escolher arquivo: agenda.war
→ Deploy
```

O Tomcat descompacta e publica a aplicação automaticamente.

### 3. Testar o acesso

```
http://192.168.20.20:8080/agenda
```

A interface web da aplicação Agenda deve carregar no navegador.

---

## Exportar dump do banco (backup)

Para exportar o banco após popular com dados:

```
Administration → Data Export
→ Selecionar schema: agenda
→ Export to Self-Contained File
→ Start Export
```

O arquivo `.sql` gerado serve como backup e pode ser reimportado em outro ambiente.

---

## Nota

Durante a aula de 27/28 de maio, ocorreram erros no processo que impediram o funcionamento da aplicação `agenda.war`. O problema foi identificado e resolvido: **a tabela `contatos` não existia no banco de dados**, causando falha na aplicação ao tentar acessá-la.

### Solução aplicada

No MySQL Workbench, com o banco `agenda` selecionado, executar o comando abaixo para criar a tabela manualmente:

```sql
CREATE TABLE contatos (
    idcon  INT          NOT NULL AUTO_INCREMENT,
    nome   VARCHAR(100) NOT NULL,
    fone   VARCHAR(30)  NOT NULL,
    email  VARCHAR(150),
    PRIMARY KEY (idcon)
);
```

Após executar o comando, verificar se a tabela foi criada:

```sql
show tables;
```

Com a tabela criada, refazer o deploy do `agenda.war` no Tomcat e acessar novamente:

```
http://192.168.20.20:8080/agenda
```

A aplicação passou a funcionar corretamente após a criação da tabela.

---

## Evidências obrigatórias

- Screenshot do projeto Agenda importado no Eclipse com DAO.java configurado
- Screenshot do banco `agenda` criado e schemas atualizados no MySQL Workbench
- Screenshot do deploy do `agenda.war` no painel do Tomcat
- Screenshot da aplicação acessível em `http://192.168.20.20:8080/agenda`
- Screenshot do `select * from contato;` retornando dados
