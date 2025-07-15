USE library;

-- Join to test performance so far-- 

SELECT b.book_id,
	   g.genre_id,
       g.genre_name,
       b.title,
       a.author_name,
       b.available_to_rent
FROM genres AS g
JOIN books AS b ON g.genre_id = b.genre_id
JOIN authors AS a ON b.author_id = a.author_id;

-- Total number of books per author --

SELECT a.author_id,
	   a.author_name,
       COUNT(b.book_id) AS books_available,
       g.genre_name
FROM authors AS a
JOIN 
books AS b ON a.author_id = b.author_id
JOIN 
genres AS g ON b.genre_id = g.genre_id
GROUP BY a.author_name,g.genre_name,a.author_id
ORDER BY author_name;


-- how many books per genre--

SELECT g.genre_name,
       COUNT(b.book_id) AS number_of_books
FROM books AS b
JOIN
genres AS g ON b.genre_id = g.genre_id
GROUP BY g.genre_name;

-- Number of active vs inactive members -- 

SELECT membership_status,
COUNT(member_id) AS total_members
FROM members
GROUP BY membership_status;

-- most popular genre--

SELECT g.genre_name ,
	   COUNT(bw.book_id) AS total_borrowed
FROM borrowings AS bw
JOIN 
books AS b ON b.book_id = bw.book_id
JOIN 
genres AS g ON b.genre_id = g.genre_id
GROUP BY g.genre_name
ORDER BY total_borrowed DESC;


-- genres per author -- 

SELECT a.author_name,
       COUNT(DISTINCT g.genre_id) AS total_genres
FROM authors AS a
JOIN 
books AS b ON a.author_id = b.author_id
JOIN 
genres AS g ON b.genre_id = g.genre_id
GROUP BY a.author_name;


-- Members who borrow the most books -- 

SELECT member_id,
       COUNT(borrowing_id) AS number_of_borrows
FROM borrowings
GROUP BY member_id
ORDER BY number_of_borrows DESC;

-- Popular renting months 2023--
	
SELECT YEAR(borrowing_date) AS year_booked,
       MONTH(borrowing_date) AS month_booked,
       COUNT(borrowing_date)AS total_borrows
FROM borrowings
WHERE YEAR(borrowing_date) = 2023
GROUP BY year_booked,month_booked
ORDER BY year_booked,month_booked;

-- Popular renting months 2024--


SELECT YEAR(borrowing_date) AS year_booked,
       MONTH(borrowing_date) AS month_booked,
       COUNT(borrowing_date)AS total_borrows
FROM borrowings
WHERE YEAR(borrowing_date) = 2024
GROUP BY year_booked,month_booked
ORDER BY year_booked,month_booked;

-- Most borrowed book--

SELECT bw.book_id,
       b.title,
       COUNT(bw.borrowing_id) AS times_borrowed
FROM borrowings AS bw
JOIN 
books AS b ON bw.book_id = b.book_id
GROUP BY b.book_id
ORDER BY times_borrowed DESC
LIMIT 1;
       
