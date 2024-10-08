# Estudo de SQL com MySQL e Banco de Dados Sakila

Este repositório contém uma série de consultas SQL e exercícios projetados para aprimorar o entendimento e a proficiência em MySQL, utilizando o banco de dados Sakila como conjunto de dados principal.

## Sumário
- [Introdução](#introdução)
- [Pré-requisitos](#pré-requisitos)
- [Configuração](#configuração)
- [Exercícios](#exercícios)
  - [Consultas Básicas](#consultas-básicas)
  - [Joins](#joins)
  - [Subconsultas](#subconsultas)
  - [Views](#views)
  - [Procedures Armazenadas](#procedures-armazenadas)
- [Conclusão](#conclusão)
- [Recursos](#recursos)

## Introdução
O banco de dados Sakila é um conhecido exemplo de banco de dados MySQL que fornece um bom conjunto de dados para o aprendizado de SQL. Ele contém dados sobre uma locadora de DVDs, incluindo informações sobre filmes, atores, clientes, locações e pagamentos. Este projeto é destinado a quem deseja praticar consultas SQL e entender como funcionam os bancos de dados relacionais.

## Pré-requisitos
- **Docker**: Confira se tem o docker instalado em sua maquina.

## Configuração
1. Clone este repositório:
   ```bash
   git clone https://github.com/juliofilizzola/SQL_QUERY.git
   cd SQL_QUERY
   ```
2. Importe o banco de dados Sakila no MySQL:
   ```bash
   docker-compose up -d
   ```
3. Teste a instalação do banco de dados:
   ```sql
   USE sakila;
   SHOW TABLES;
   ```

## Exercícios

### Consultas Básicas
Comece com instruções SELECT simples para se familiarizar com a estrutura do banco de dados Sakila.

Exemplo:
```sql
SELECT * FROM actor LIMIT 10;
```

### Joins
Pratique a escrita de diferentes tipos de JOIN para combinar dados de várias tabelas.

Exemplo:
```sql
SELECT f.title, a.first_name, a.last_name 
FROM film f
JOIN film_actor fa ON f.film_id = fa.film_id
JOIN actor a ON fa.actor_id = a.actor_id
LIMIT 10;
```

### Subconsultas
Aprenda a escrever subconsultas para realizar recuperações de dados mais complexas.

Exemplo:
```sql
SELECT title
FROM film
WHERE film_id IN (
    SELECT film_id
    FROM inventory
    WHERE store_id = 1
);
```

### Views
Crie e utilize views para simplificar consultas complexas.

Exemplo:
```sql
CREATE VIEW actor_info AS
SELECT a.actor_id, a.first_name, a.last_name, COUNT(fa.film_id) AS film_count
FROM actor a
JOIN film_actor fa ON a.actor_id = fa.actor_id
GROUP BY a.actor_id;
```

### Procedures Armazenadas
Implemente procedures armazenadas para encapsular a lógica SQL reutilizável.

Exemplo:
```sql
DELIMITER $$
CREATE PROCEDURE get_film_by_actor(IN actor_name VARCHAR(100))
BEGIN
    SELECT f.title
    FROM film f
    JOIN film_actor fa ON f.film_id = fa.film_id
    JOIN actor a ON fa.actor_id = a.actor_id
    WHERE CONCAT(a.first_name, ' ', a.last_name) = actor_name;
END$$
DELIMITER ;
```

## Conclusão
Ao trabalhar nesses exercícios, você deve ter uma compreensão sólida dos fundamentos de SQL e de como usar o MySQL de forma eficaz. O banco de dados Sakila fornece um conjunto de dados rico para aprimorar suas habilidades em recuperação, manipulação e análise de dados.

## Recursos
- [Documentação do MySQL](https://dev.mysql.com/doc/)
- [Banco de Dados de Exemplo Sakila](https://dev.mysql.com/doc/sakila/en/)
- [Tutorial de SQL](https://www.w3schools.com/sql/)
- [Problemas de SQL no LeetCode](https://leetcode.com/problemset/database/)

---

Sinta-se à vontade para personalizar o conteúdo para melhor se adequar ao seu projeto ou foco de estudo!