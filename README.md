# 📁 Projeto de Transações, Procedures, Backup e Recovery

## 🎯 Objetivo

Este projeto visa demonstrar o uso de transações no MySQL, o desenvolvimento de uma procedure com controle de transações e o processo de backup e recuperação de bancos de dados utilizando o mysqldump.

## 🛠️ Estrutura do Projeto

O projeto é dividido em três partes principais:

1. 🔄 Transações Simples

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
