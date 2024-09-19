<h1 id="english" align="center">Resumo - Estudos SQL</h1>

> <p align="center"> Material elaborado para revisão de estudos sobre SQL realizados no site https://sqlbolt.com/ (SQLBolt) </p>

<details>
  <summary>Sumário</summary>
  <ul>
    <li><a href="#select">SELECT</a></li>
    <li><a href="#where">WHERE</a></li>
    <li><a href="#distinct">DISTINCT</a></li>
    <li><a href="#group_by">GROUP BY</a></li>
    <li><a href="#order_by">ORDER BY</a></li>
    <li><a href="#limit_offset">LIMIT & OFFSET</a></li>
    <li><a href="#pratica">Praticando</a></li>
  </ul>
</details>

<h2 id="select">1. SELECT </h2>

### Descrição Geral:

- O SELECT resulta em uma seleção específica do que o usuário busca ao final da sua consulta em um banco relacional SQL;
- Ao final da seleção, deve-se colocar o ponto e vírgula (;).

### Exemplos:

**Selecionar coluna(s) específica(s)**
```
SELECT column, another_column, …
FROM mytable;
```

**Selecionar todas colunas**
```
SELECT *
FROM mytable;
```

<h2 id="where">2. WHERE </h2>

### Descrição Geral:

- Funciona como um filtro;
- É onde o usuário especifica o que busca.

| Operadores  | Condicional | SQL  |
| ------------- | ------------- | ------------- |
| =, !=, <, <=, >, >= | Operadores padrão | col_name != 4 |
| BETWEEN x AND y | Intervalo de valor | col_name BETWEEN 1.5 AND 10.5 |
| NOT BETWEEN x AND y | Não estpa no intervalo de valor  | col_name NOT BETWEEN 1.5 AND 10.5 |
| IN (…) | Condição está na lista | col_name IN (2, 4, 6) |
| NOT IN (…) | Condição não está na lista | col_name NOT IN ("A", "B", "C") |
| LIKE | Busca valores de um determinado padrão | col_name LIKE "ABC" (funciona como operador "=") |
| NOT LIKE | Número não está na lista | col_name NOT LIKE "ABC" (funciona como operador "!=") |
| % | Representa qualquer sequência de caracteres (incluindo nenhuma) | col_name LIKE "%AT%" (igual a "AT", "ATTIC", "CAT", "BATS", etc) |
| _ | Representa exatamente um único caractere | col_name LIKE "AN_" (igual a "AND", mas não "AN") |

### Exemplos:

**Tabela de Consulta**

| id  | title                | director       | year | length_minutes |
| --- | -------------------- | -------------- | ---- | -------------- |
| 1   | Toy Story            | John Lasseter  | 1995 | 81             |
| 2   | A Bug's Life         | John Lasseter  | 1998 | 95             |
| 3   | Toy Story 2          | John Lasseter  | 1999 | 93             |
| 4   | Monsters, Inc.       | Pete Docter    | 2001 | 92             |
| 5   | Finding Nemo         | Andrew Stanton | 2003 | 107            |
| 6   | The Incredibles      | Brad Bird      | 2004 | 116            |
| 7   | Cars                 | John Lasseter  | 2006 | 117            |
| 8   | Ratatouille          | Brad Bird      | 2007 | 115            |
| 9   | WALL-E               | Andrew Stanton | 2008 | 104            |
| 10  | Up                   | Pete Docter    | 2009 | 101            |
| 11  | Toy Story 3          | Lee Unkrich    | 2010 | 103            |
| 12  | Cars 2               | John Lasseter  | 2011 | 120            |
| 13  | Brave                | Brenda Chapman | 2012 | 102            |
| 14  | Monsters University  | Dan Scanlon    | 2013 | 110            |


**Find the movie with a row id of 6**
```
SELECT * 
FROM movies
WHERE id = 6;
```
**Find the movies released in the years between 2000 and 2010**
```
SELECT * 
FROM movies
WHERE year BETWEEN 2000 AND 2010;
```
**Find the movies not released in the years between 2000 and 2010**
```
SELECT * 
FROM movies
WHERE year NOT BETWEEN 2000 AND 2010;
```
**Find the first 5 Pixar movies and their release year**
```
SELECT title, year
FROM movies
LIMIT 5;
```
**Find all the Toy Story movies**
```
SELECT * 
FROM movies
WHERE title LIKE "Toy Story%";
```
**Find all the movies directed by John Lasseter**
```
SELECT * 
FROM movies
WHERE director LIKE "John Lasseter";
```
**Find all the movies (and director) not directed by John Lasseter**
```
SELECT title, director
FROM movies
WHERE director NOT LIKE "John Lasseter";
```
**Find all the WALL- movies**
```
SELECT *
FROM movies
WHERE title LIKE "WALL-%";
```

<h2 id="distinct">3. DISTINCT </h2>

### Descrição Geral:

- Usado para retornar apenas valores únicos em uma consulta, eliminando linhas duplicatas.

### Exemplos:

**Selecionar com valores únicos como resultado**
```
SELECT DISTINCT column, another_column, …
FROM mytable
WHERE condition(s);
```

<h2 id="group_by">4. GROUP BY</h2>

### Descrição Geral:

- Usado para retornar apenas valores únicos em uma consulta, eliminando colunas duplicatas.

### Exemplos:

**Selecionar com valores únicos como resultado**
```
SELECT column_name, COUNT(*)
FROM mytable
WHERE condition(s)
GROUP BY column_name
ORDER BY COUNT(*) DESC;
```

<h2 id="order_by">5. ORDER BY</h2>

### Descrição Geral:

- Uma maneira de classificar seus resultados por uma determinada coluna em ordem crescente ou decrescente.

### Exemplos:

**Selecionar com valores ordenados**
```
SELECT column, another_column, …
FROM mytable
WHERE condition(s)
ORDER BY column ASC/DESC;
```

<h2 id="limit_offset">6. LIMIT & OFFSET</h2>

### Descrição Geral:

- Usado para controlar o número de registros que uma consulta retorna, o que é útil para paginação ou para limitar a quantidade de dados exibidos;
- O OFFSET é usado junto com o LIMIT para pular um determinado número de registros antes de começar a retornar os resultados;

***Se LIMIT = 5 e OFFSET = 10, pesquisa retorna 5 registros começando a partir do 11º registro (ou seja, ignora os primeiros 10).***

### Exemplos:

**Selecionar com linhas limitadas**
```
SELECT column, another_column, …
FROM mytable
WHERE condition(s)
ORDER BY column ASC/DESC
LIMIT num_limit OFFSET num_offset;
```

<h2 id="pratica">Praticando</h2>

### Tabela de Consulta 1:

| City                  | Country       | Population | Latitude  | Longitude   |
|-----------------------|---------------|------------|-----------|-------------|
| Guadalajara           | Mexico        | 1,500,800  | 20.659699 | -103.349609 |
| Toronto               | Canada        | 2,795,060  | 43.653226 | -79.383184  |
| Houston               | United States | 2,195,914  | 29.760427 | -95.369803  |
| New York              | United States | 8,405,837  | 40.712784 | -74.005941  |
| Philadelphia          | United States | 1,553,165  | 39.952584 | -75.165222  |
| Havana                | Cuba          | 2,106,146  | 23.054070 | -82.345189  |
| Mexico City           | Mexico        | 8,555,500  | 19.432608 | -99.133208  |
| Phoenix               | United States | 1,513,367  | 33.448377 | -112.074037 |
| Los Angeles           | United States | 3,884,307  | 34.052234 | -118.243685 |
| Ecatepec de Morelos   | Mexico        | 1,742,000  | 19.601841 | -99.050674  |
| Montreal              | Canada        | 1,717,767  | 45.501689 | -73.567256  |
| Chicago               | United States | 2,718,782  | 41.878114 | -87.629798  |

---
**1) List all the Canadian cities and their populations**
```
SELECT City, Population
FROM north_american_cities
WHERE Country = "Canada";
```
**2) Order all the cities in the United States by their latitude from north to south**
```
SELECT City
FROM north_american_cities
WHERE Country = "United States"
ORDER BY Latitude DESC;
```
**3) List all the cities west of Chicago, ordered from west to east**
```
SELECT City
FROM north_american_cities
WHERE Longitude < -87.629798
ORDER BY Longitude;
```
**4) List the two largest cities in Mexico (by population)**
```
SELECT City
FROM north_american_cities
WHERE Country = "Mexico"
ORDER BY Population DESC
LIMIT 2;
```
**5) List the third and fourth largest cities (by population) in the United States and their population**
```
SELECT City, Population
FROM north_american_cities
WHERE Country = "United States"
ORDER BY Population DESC
LIMIT 2 OFFSET 2;
```
