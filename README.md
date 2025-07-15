# Data Exploration
Full sql code can be found above as a file (Insights.sql)

## Important Table of Contents

- [Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda) 📊
- [SQL scripts written to gain insights](#sql-scripts-written-to-gain-insights) 💻
- [Recommendations](#recommendations) 💡
- [Excel Interactive Dashboard](#excel-interactive-dashboard) 📊📉📈

### Project Overview

The aim of this project is to see what valuable insights can be gained from the library database. I seek to identify trends that can be used to help improve the library's operations.

### Data sources

For the purpose of this project, my main source of data is an online library database that I accessed for analysis.

## Tools

- Microsoft SQL Server

## Exploratory Data Analysis (EDA)

EDA used to answer the following key questions:

- What is the most borrowed book?
- What was the most popular renting month for 2023 and then for 2024?
- What member borrowed the most books?
- How many genres are there per author?
- What is the most popular genre?
- What is the number of active vs inactive library memberships?
- How many books are there per genre?
- What is the total number of books per author?

## SQL scripts written to gain insights

```sql
-- Most borrowed book --

SELECT bw.book_id,
       b.title,
       COUNT(bw.borrowing_id) AS times_borrowed
FROM borrowings AS bw
JOIN
books AS b ON bw.book_id = b.book_id
GROUP BY b.book_id
ORDER BY times_borrowed DESC
LIMIT 1;
```

<img width="445" height="56" alt="327984054-15e7ff3e-de75-4763-9de9-b529d369b9d7" src="https://github.com/user-attachments/assets/2b50f93b-570c-4197-a280-c2bf6f2332df" />

```sql
-- Most popular renting months in 2023 --

SELECT YEAR(borrowing_date) AS year_booked,
       MONTH(borrowing_date) AS month_booked,
       COUNT(borrowing_date) AS total_borrows
FROM borrowings
WHERE YEAR(borrowing_date) = 2023
GROUP BY year_booked, month_booked
ORDER BY year_booked, month_booked;
```

<img width="301" height="213" alt="327911438-97308f46-2033-4f4b-b81e-b9435889903d" src="https://github.com/user-attachments/assets/d8205efb-f6fb-4f92-a145-8eb6408e943f" />

```sql
-- Most popular renting months in 2024 --

SELECT YEAR(borrowing_date) AS year_booked,
       MONTH(borrowing_date) AS month_booked,
       COUNT(borrowing_date) AS total_borrows
FROM borrowings
WHERE YEAR(borrowing_date) = 2024
GROUP BY year_booked, month_booked
ORDER BY year_booked, month_booked;
```

<img width="301" height="110" alt="327911595-984f4dc1-acd9-429b-9cad-6d3814770e4d" src="https://github.com/user-attachments/assets/7290836b-0e0e-4629-86c8-32810910e49f" />

```sql
-- Members who borrow the most books--

SELECT member_id,
       COUNT(borrowing_id) AS number_of_borrows
FROM borrowings
GROUP BY member_id
ORDER BY number_of_borrows DESC;
```

<img width="243" height="381" alt="327911753-f4bf3317-fc07-493d-bea3-7337d9d0c94e" src="https://github.com/user-attachments/assets/1820bb66-de5d-4091-b946-504d48e1ae10" />

```sql
-- genres per author--

SELECT a.author_name,
       COUNT(DISTINCT g.genre_id) AS total_genres
FROM authors AS a
JOIN
books AS b ON b.genre_id = g.genre_id
GROUP BY a.author_name;
```

<img width="213" height="365" alt="327911904-74b3b531-b32b-419f-bec1-a3cc2892952b" src="https://github.com/user-attachments/assets/ff241d94-6c75-4cac-ac48-ac2f6b53dcab" />

```sql
-- Most popular genre--

SELECT g.genre_name,
       COUNT(bw.book_id) AS total_borrowed
FROM borrowings AS bw
JOIN
books AS b ON b.book_id = bw.book_id
JOIN
genres AS g ON b.genre_id = g.genre_id
GROUP BY g.genre_name
ORDER BY total_borrowed DESC;
```

<img width="252" height="245" alt="327912589-5e8ff8db-724e-44ac-b475-0ac5c4a900d3" src="https://github.com/user-attachments/assets/5d1f4d9f-36dd-412a-b6fe-07beeb413e31" />

```sql
-- Number of active vs inactive memberships--

SELECT membership_status
COUNT(member_id) AS total_members
FROM members
GROUP BY membership_status;
```

<img width="265" height="62" alt="327912907-02153fec-60fe-4e3d-b4db-0c7652cc882a" src="https://github.com/user-attachments/assets/70622395-b6ba-458f-be6d-39d6b05a563a" />

```sql
-- How many books per genre--

SELECT g.genre_name,
       COUNT(b.book_id) AS number_of_books
FROM books AS b
JOIN
genres AS g ON b.genre_id = g.genre_id
GROUP BY g.genre_name;
```

<img width="254" height="274" alt="327913039-1301c1ac-94f3-4785-94ed-51d559b85cc5" src="https://github.com/user-attachments/assets/2bd76600-3271-403c-a266-d022bbc28842" />

```sql
-- Total books per author--

SELECT a.author_name,
       COUNT(b.book_id) AS books_available,
       g.genre_name
FROM authors AS a
JOIN
books AS b ON a.author_id = b.author_id
JOIN
genres AS g ON b.genre_id = g.genre_id
GROUP BY a.author_name,g.genre_name
ORDER BY author_name;
```

<img width="389" height="546" alt="327913274-3f65c389-c47d-47a2-b244-bf870e1c704e" src="https://github.com/user-attachments/assets/d61dfd5f-6b6f-4b4e-8000-41c42d7e6d20" />

### Recommendations

The results and recommendations are summarised as follows: [Download here](https://github.com/faray003/Library-Database-Exploratory-Analysis/blob/main/Data.exploration.findings.pdf)

### Excel Interactive Dashboard

Please click the download link to access the Microsoft Excel interactive dashboard I created for viewers to have a better understanding of some of my insights. [Download here](https://github.com/faray003/Library-Database-Exploratory-Analysis/blob/main/Library.Management.Dashboard.finalised.xlsx)
