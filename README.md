# 📁 Projeto de Transações, Procedures, Backup e Recovery

## 🎯 Objetivo

### Este projeto visa demonstrar o uso de transações no MySQL, o desenvolvimento de uma procedure com controle de transações e o processo de backup e recuperação de bancos de dados utilizando o mysqldump.

## 🛠️ Estrutura do Projeto

O projeto é dividido em três partes principais:

### 1️⃣ 🔄 Transações Simples

Descrição: Nesta etapa, são realizadas transações sem o uso de procedures.

```sql
-- Desabilitar o autocommit
SET autocommit = 0;

-- Iniciar a transação
START TRANSACTION;

-- Exemplo de modificação na base de dados
UPDATE produtos SET preco = preco * 1.1 WHERE categoria = 'Eletrônicos';

-- Confirma a transação
COMMIT;

-- Em caso de erro, reverter a transação
-- ROLLBACK;
```

### 2️⃣ 🚦 Transações com Procedure

Descrição: Esta etapa envolve a criação de uma procedure com controle de transações e tratamento de erros.

```sql
DELIMITER $$

CREATE PROCEDURE AtualizaPrecoEletronicos()
BEGIN
    DECLARE EXIT HANDLER FOR SQLEXCEPTION
    BEGIN
        -- Rollback em caso de erro
        ROLLBACK;
    END;

    -- Inicia a transação
    START TRANSACTION;
    
    -- Exemplo de atualização com controle de erros
    UPDATE produtos SET preco = preco * 1.1 WHERE categoria = 'Eletrônicos';

    -- Confirma a transação
    COMMIT;
END $$

DELIMITER ;

-- Executar a procedure
CALL AtualizaPrecoEletronicos();
```

### 3️⃣ 💾 Backup e Recovery

Descrição: Realização do backup e recuperação do banco de dados utilizando o mysqldump.

```sql
# Backup do banco de dados
dump -u usuario -p e_commerce > backup_e_commerce.sql

# Recovery do banco de dados
mysql -u usuario -p e_commerce < backup_e_commerce.sql

# Backup de múltiplos bancos de dados
mysqldump -u usuario -p --databases db1 db2 db3 > backup_multibancos.sql

# Incluir procedures, eventos e outros
mysqldump -u usuario -p --routines --events e_commerce > backup_completo.sql
```


## 📝 Conclusão

Este projeto abrange desde o uso básico de transações até o controle avançado com procedures e a segurança oferecida pelo backup e recovery do banco de dados. 
É uma base sólida para qualquer aplicação que necessite de integridade e resiliência de dados.
