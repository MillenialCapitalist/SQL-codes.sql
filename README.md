# SQL-codes.sql
My early sql code

;//'SELECT id, account_id, occurred_at
FROM orders;

SELECT id, account_id, occurred_at
FROM orders;

SELECT id, account_id
FROM web_events;

SELECT id, name
FROM region;

SELECT id, name, website
FROM accounts;

SELECT id, account_id, occurred_at, standard_qty
FROM orders;

SELECT id, name
FROM region;

SELECT id, region_id
FROM sales_reps;

SELECT web_events, account_id, channel
FROM web_events;

SELECT id, occurred_at, total_amt_usd
  FROM orders
  ORDER BY occurred_at
  LIMIT 10;

SELECT id, account_id, total_amt_usd
	FROM orders
    ORDER BY total_amt_usd
    LIMIT 5;

SELECT id, account_id, total_amt_usd
	FROM orders
    ORDER BY account_id, total_amt_usd DESC;

SELECT id, account_id, total_amt_usd
	FROM orders
    ORDER BY total_amt_usd DESC, account_id;

SELECT id, account_id, total_amt_usd
	FROM orders
    ORDER BY total_amt_usd DESC
    LIMIT 20

SELECT *
	FROM orders
    WHERE gloss_amt_usd >= 1000
    LIMIT 5;

SELECT *
	FROM orders
    WHERE total_amt_usd < 500
    LIMIT 10;

SELECT name,website,primary_poc
	FROM accounts
	WHERE name = 'Exxon Mobil';

SELECT id, account_id, (standard_amt_usd/standard_qty) AS standard_unit_price
	FROM orders
    LIMIT 10;

SELECT id, account_id, poster_amt_usd/(standard_amt_usd+gloss_amt_usd+poster_amt_usd) * 100 AS poster_pct
	FROM orders
    LIMIT 10;

SELECT id, name
	FROM accounts
    WHERE name LIKE 'C%';

SELECT id, name
	FROM accounts
    WHERE name LIKE '%one%';

SELECT id, name
	FROM accounts
    WHERE name LIKE '%S'

SELECT name, primary_poc, sales_rep_id
	FROM accounts
    WHERE name IN ('Walmart','Target', 'Nordstrom')
    ORDER BY name;

SELECT *
	FROM web_events
    WHERE channel IN ('organic','adwords')
    ORDER BY channel;

SELECT  name, primary_poc, sales_rep_id
	FROM accounts
    WHERE name NOT IN ('Walmart','Target', 'Nordstrom')
    ORDER BY id;

SELECT *
FROM orders
WHERE standard_qty > 1000 AND poster_qty = 0 AND gloss_qty = 0;

SELECT name
FROM accounts
WHERE name NOT LIKE 'C%' AND name LIKE '%s';

SELECT occurred_at, gloss_qty
FROM orders
WHERE gloss_qty BETWEEN 24 AND 29;

SELECT *
FROM web_events
WHERE channel IN ('organic', 'adwords') AND occurred_at BETWEEN '2016-01-01' AND '2017-01-01'
ORDER BY occurred_at DESC;

SELECT id
  FROM orders
  WHERE gloss_qty>4000 OR poster_qty>4000;

SELECT id, standard_qty, gloss_qty, poster_qty
	FROM orders
    WHERE standard_qty=0 AND (gloss_qty>1000 OR poster_qty>1000);

SELECT name
	FROM accounts
    WHERE name LIKE 'C%' OR name LIKE 'W%' AND primary_poc LIKE '%ana%' OR primary_poc LIKE '%Ana%' AND primary_poc NOT LIKE '%eana%';

SELECT orders.*
	FROM orders
    JOIN accounts
    ON orders.account_id = accounts.id;

SELECT accounts.id,accounts.name, orders.account_id
	FROM accounts
    JOIN orders
    ON accounts.id = orders.account_id;

SELECT accounts.name, orders.id
	FROM accounts
    JOIN orders
    ON accounts.id = orders.account_id;

SELECT *
	FROM accounts
    JOIN orders
    ON accounts.id = orders.account_id
    LIMIT 20;

SELECT accounts.*, orders.*
	FROM accounts
    JOIN orders
    ON accounts.id = orders.account_id;

SELECT accounts.website, accounts.primary_poc, orders.standard_qty, orders.gloss_qty, orders.poster_qty
	FROM accounts
    JOIN orders
    ON accounts.id = orders.account_id;

SELECT *
	FROM web_events
	JOIN accounts
	ON web_events.account_id = accounts.id
	JOIN orders
	ON accounts.id = orders.account_id

SELECT t_a.name, t_a.primary_poc, t_w.occurred_at, t_w.channel
	FROM accounts t_a
    JOIN web_events t_w
    ON t_a.id = t_w.account_id
    WHERE name = 'Walmart';

 SELECT t_r.name region_name, t_s.name sales_rep_name, t_a.name accounts
 	FROM region t_r
    JOIN sales_reps t_s
    ON t_r.id = t_s.region_id
    JOIN accounts t_a
    ON t_s.id = t_a.sales_rep_id
    ORDER BY t_a.name;

SELECT t_r.name region_name, t_a.name account_name, t_o.total_amt_usd/(total+0.01) unit_price
	FROM region t_r
    JOIN sales_reps t_s
    ON t_r.id = t_s.region_id
    JOIN accounts t_a
    ON t_s.id = t_a.sales_rep_id
    JOIN orders t_o
    ON t_a.id = t_o.account_id;

SELECT t_r.name region_name, t_s.name sales_rep_name, t_a.name account_name
	FROM region t_r
    LEFT JOIN sales_reps t_s
    ON t_r.id = t_s.region_id
    LEFT JOIN accounts t_a
    ON t_s.id = t_a.sales_rep_id
    WHERE t_r.name = 'Midwest'
    ORDER BY t_a.name;

SELECT t_r.name region_name, t_s.name sales_rep_name, t_a.name account_name
	FROM region t_r
    LEFT JOIN sales_reps t_s
    ON t_r.id = t_s.region_id
    LEFT JOIN accounts t_a
    ON t_s.id = t_a.sales_rep_id
    WHERE t_s.name LIKE 'S%' AND t_r.name = 'Midwest'
    ORDER BY t_a.name;

SELECT t_r.name region_name, t_s.name sales_rep_name, t_a.name account_name
	FROM region t_r
    LEFT JOIN sales_reps t_s
    ON t_r.id = t_s.region_id
    LEFT JOIN accounts t_a
    ON t_s.id = t_a.sales_rep_id
    WHERE t_s.name LIKE '% K%' AND t_r.name = 'Midwest'
    ORDER BY t_a.name;

SELECT t_r.name region_name, t_a.name account_name, t_o.total_amt_usd/(total + 0.01) unit_price
	FROM region t_r
    LEFT JOIN sales_reps t_s
    ON t_r.id = t_s.region_id
    LEFT JOIN accounts t_a
    ON t_s.id = t_a.sales_rep_id
    LEFT JOIN orders t_o
    ON t_a.id = t_o.account_id
    WHERE t_o.standard_qty > 100;

SELECT t_r.name region_name, t_a.name account_name, t_o.total_amt_usd/(total + 0.01) unit_price
	FROM region t_r
    LEFT JOIN sales_reps t_s
    ON t_r.id = t_s.region_id
    LEFT JOIN accounts t_a
    ON t_s.id = t_a.sales_rep_id
    LEFT JOIN orders t_o
    ON t_a.id = t_o.account_id
    WHERE t_o.standard_qty > 100 AND t_o.poster_qty > 50;

SELECT t_r.name region_name, t_a.name account_name, t_o.total_amt_usd/(total + 0.01) unit_price
	FROM region t_r
    LEFT JOIN sales_reps t_s
    ON t_r.id = t_s.region_id
    LEFT JOIN accounts t_a
    ON t_s.id = t_a.sales_rep_id
    LEFT JOIN orders t_o
    ON t_a.id = t_o.account_id
    WHERE t_o.standard_qty > 100 AND t_o.poster_qty > 50
    ORDER BY unit_price DESC;

SELECT t_a.id, t_w.channel
	FROM accounts t_a
	LEFT JOIN web_events t_w
	ON t_a.id = t_w.account_id
    WHERE t_w.account_id = 1001;

SELECT DISTINCT t_a.id, t_w.channel
	FROM accounts t_a
	LEFT JOIN web_events t_w
	ON t_a.id = t_w.account_id
    WHERE t_w.account_id = 1001;

SELECT t_o.occurred_at, t_a.name, t_o.total, t_o.total_amt_usd
	FROM orders t_o
	LEFT JOIN accounts t_a
	ON t_o.account_id = t_a.id
    WHERE t_o.occurred_at BETWEEN '2015-01-01' AND '2015-12-31'
    ORDER BY t_o.occurred_at DESC;


SSELECT COUNT (*)
	FROM accounts;

SELECT COUNT (*)
	FROM orders;

SELECT COUNT (*)
	FROM region;

SELECT COUNT (*)
	FROM sales_reps;

SELECT COUNT (*)
	FROM web_events;

SELECT MIN (occurred_at) AS occured_at_first
	FROM orders;

SELECT id, occurred_at
	FROM orders
    ORDER BY occurred_at
    LIMIT 1;

SELECT MAX (occurred_at) AS occured_at_last
	FROM orders;

SELECT id, occurred_at
	FROM orders
    ORDER BY occurred_at DESC
    LIMIT 1;

SELECT AVG (standard_amt_usd) AS SAU_avg, AVG (gloss_amt_usd) AS GAU_avg, AVG (poster_amt_usd) AS PAU_avg, AVG (standard_qty) AS SQ_avg, AVG (gloss_qty) AS GQ_avg, AVG (poster_qty) AS PQ_avg

SELECT *
FROM (SELECT total_amt_usd
      FROM orders
      ORDER BY total_amt_usd
      LIMIT 3457) AS Table1
ORDER BY total_amt_usd DESC
LIMIT 2;


SELECT name, occurred_at
	FROM accounts
    JOIN orders
    ON accounts.id = orders.account_id
    ORDER BY name;

SELECT SUM(total_amt_usd) AS total_sales, accounts.name
	FROM orders
    JOIN accounts
    ON orders.account_id = accounts.id
    GROUP BY accounts.name
    ORDER BY accounts.name;

SELECT occurred_at, channel, accounts.name
	FROM web_events
    JOIN accounts
    ON web_events.account_id = accounts.id
    ORDER BY occurred_at DESC
    LIMIT 1;

SELECT channel, COUNT (channel) AS channel_total
	FROM web_events
    GROUP BY channel
    ORDER BY channel;

SELECT primary_poc, web_events.id, occurred_at
	FROM accounts
    JOIN web_events
    ON accounts.id = web_events.account_id
    ORDER BY occurred_at
    LIMIT 1;

SELECT COUNT (sales_reps.name) AS sales_reps_total, region.name
	FROM sales_reps
    JOIN region
    ON sales_reps.region_id = region.id
    GROUP BY region.name
    ORDER BY sales_reps_total;


SELECT account_id, AVG (standard_qty) AS mean_standard, AVG (gloss_qty) AS mean_gloss, AVG (poster_qty) AS mean_poster
	FROM orders
    GROUP BY account_id
    ORDER BY account_id;

SELECT account_id, AVG (standard_amt_usd) AS mean_standard_usd, AVG (gloss_amt_usd) AS mean_gloss_usd, AVG (poster_amt_usd) AS mean_poster_usd
    FROM orders
    GROUP BY account_id;

SELECT s.name, w.channel, COUNT(w.channel) AS channel_no
	FROM sales_reps s
    JOIN accounts a
    ON s.id = a.sales_rep_id
    JOIN web_events w
    ON a.id = w.account_id
    GROUP BY s.name, w.channel
    ORDER BY channel_no DESC;

SELECT r.name, w.channel, COUNT (w.channel) AS  no_channel
	FROM region r
    JOIN sales_reps s
    ON r.id = s.region_id
    JOIN accounts a
    ON s.id = a.sales_rep_id
    JOIN web_events w
    ON w.account_id = a.id
    GROUP BY r.name, w.channel
    ORDER BY no_channel DESC;

SELECT DISTINCT a.name, r.name AS region
	FROM accounts a
    JOIN sales_reps s
    ON a.sales_rep_id = s.id
    JOIN region r
    ON s.region_id = r.id
    ORDER BY a.name;

SELECT DISTINCT s.name AS sales_rep, a.name AS account
    	FROM accounts a
        JOIN sales_reps s
        ON a.sales_rep_id = s.id
        ORDER BY sales_rep;

SELECT s.id, s.name, COUNT(*) num_accounts
FROM accounts a
JOIN sales_reps s
ON s.id = a.sales_rep_id
GROUP BY s.id, s.name
HAVING COUNT(*) > 5
ORDER BY num_accounts;

SELECT COUNT(*) num_reps_above5
FROM(SELECT s.id, s.name, COUNT(*) num_accounts
     FROM accounts a
     JOIN sales_reps s
     ON s.id = a.sales_rep_id
     GROUP BY s.id, s.name
     HAVING COUNT(*) > 5
     ORDER BY num_accounts) AS Table1;

SELECT a.id, a.name, COUNT(*) num_orders
FROM accounts a
JOIN orders o
ON a.id = o.account_id
GROUP BY a.id, a.name
HAVING COUNT(*) > 20
ORDER BY num_orders;

SELECT a.id, a.name, COUNT(*) num_orders
FROM accounts a
JOIN orders o
ON a.id = o.account_id
GROUP BY a.id, a.name
ORDER BY num_orders DESC
LIMIT 1;

SELECT a.id, a.name, SUM(o.total_amt_usd) total_spent
FROM accounts a
JOIN orders o
ON a.id = o.account_id
GROUP BY a.id, a.name
HAVING SUM(o.total_amt_usd) > 30000
ORDER BY total_spent;

SELECT a.id, a.name, SUM(o.total_amt_usd) total_spent
FROM accounts a
JOIN orders o
ON a.id = o.account_id
GROUP BY a.id, a.name
HAVING SUM(o.total_amt_usd) < 1000
ORDER BY total_spent;

SELECT a.id, a.name, SUM(o.total_amt_usd) total_spent
FROM accounts a
JOIN orders o
ON a.id = o.account_id
GROUP BY a.id, a.name
ORDER BY total_spent DESC
LIMIT 1;

SELECT a.id, a.name, SUM(o.total_amt_usd) total_spent
FROM accounts a
JOIN orders o
ON a.id = o.account_id
GROUP BY a.id, a.name
ORDER BY total_spent
LIMIT 1;

SELECT a.id, a.name, w.channel, COUNT(*) use_of_channel
FROM accounts a
JOIN web_events w
ON a.id = w.account_id
GROUP BY a.id, a.name, w.channel
HAVING COUNT(*) > 6 AND w.channel = 'facebook'
ORDER BY use_of_channel;

SELECT a.id, a.name, w.channel, COUNT(*) use_of_channel
FROM accounts a
JOIN web_events w
ON a.id = w.account_id
GROUP BY a.id, a.name, w.channel
ORDER BY use_of_channel DESC
LIMIT 10;

SELECT DATE_PART('year', occurred_at) ord_year,  SUM(total_amt_usd) total_spent
 FROM orders
 GROUP BY 1
 ORDER BY 2 DESC;

SELECT DATE_PART('month', occurred_at) ord_month, SUM(total_amt_usd) total_spent
FROM orders
WHERE occurred_at BETWEEN '2014-01-01' AND '2017-01-01'
GROUP BY 1
ORDER BY 2 DESC;

SELECT DATE_PART('year', occurred_at) ord_year,  COUNT(*) total_sales
FROM orders
GROUP BY 1
ORDER BY 2 DESC;

SELECT DATE_PART('month', occurred_at) ord_month, COUNT(*) total_sales
FROM orders
WHERE occurred_at BETWEEN '2014-01-01' AND '2017-01-01'
GROUP BY 1
ORDER BY 2 DESC;

SELECT DATE_TRUNC('month', o.occurred_at) ord_date, SUM(o.gloss_amt_usd) tot_spent
FROM orders o
JOIN accounts a
ON a.id = o.account_id
WHERE a.name = 'Walmart'
GROUP BY 1
ORDER BY 2 DESC
LIMIT 1;

SELECT id, account_id, standard_amt_usd/(standard_qty + 0.01) AS unit_price
FROM orders
LIMIT 10;

SELECT account_id, total_amt_usd, CASE WHEN total_amt_usd >= 3000 THEN 'Large' ELSE 'Small' END AS order_level
	FROM orders;

SELECT COUNT (total_amt_usd) AS no_of_orders, CASE WHEN total >= 2000 THEN 'over 2000' WHEN total > 1000 AND total < 2000 THEN '1000-2000' ELSE '1000 or under' END AS category
	FROM orders
    GROUP BY 2;

SELECT a.name, SUM (o.total_amt_usd) AS CLTV, CASE WHEN SUM (o.total_amt_usd) >= 200000 THEN 'high' WHEN SUM (o.total_amt_usd) >= 100000 THEN 'medium'  ELSE 'low' END AS level
	FROM orders o
  JOIN accounts a
  ON o.account_id = a.id
  GROUP BY 1
  ORDER BY 2 DESC;

SELECT a.name, SUM (o.total_amt_usd) AS CLTV, CASE WHEN SUM (o.total_amt_usd) >= 200000 THEN 'high' WHEN SUM (o.total_amt_usd) >= 100000 THEN 'medium'  ELSE 'low' END AS level
	FROM orders o
    JOIN accounts a
    ON o.account_id = a.id
    WHERE occurred_at BETWEEN '2016-01-01' AND '2017-12-31'
    GROUP BY 1
    ORDER BY 2 DESC;

SELECT s.name, COUNT(*) num_ords,
   CASE WHEN COUNT(*) > 200 THEN 'top'
   ELSE 'not' END AS sales_rep_level
   FROM orders o
   JOIN accounts a
   ON o.account_id = a.id
   JOIN sales_reps s
   ON s.id = a.sales_rep_id
   GROUP BY s.name
   ORDER BY 2 DESC;

SELECT s.name, COUNT(*) num_ords, SUM (total_amt_usd) AS total_sales, CASE WHEN COUNT(*) > 200 OR SUM (total_amt_usd) > 750000 THEN 'top' WHEN COUNT (*) > 150 OR SUM (total_amt_usd) > 500000 THEN 'middle' ELSE 'low' END AS sales_rep_level
FROM orders o
JOIN accounts a
ON o.account_id = a.id
JOIN sales_reps s
ON s.id = a.sales_rep_id
GROUP BY 1
ORDER BY 3 DESC;

SELECT channel, AVG(events_number) AS events_number_average
	FROM
	(SELECT DATE_TRUNC('day', occurred_at) AS day, channel, COUNT (*) AS events_number
	FROM web_events
    GROUP BY 1, 2
    ) sub
    GROUP BY 1
    ORDER BY 2 DESC;

SELECT DATE_TRUNC('day', occurred_at) AS day, channel, COUNT (*) AS events_number
	FROM web_events
    GROUP BY 1, 2
    ORDER BY 3 DESC;

SELECT account_id, total_amt_usd, CASE WHEN total_amt_usd >= 3000 THEN 'Large' ELSE 'Small' END AS order_level
  FROM orders;

SELECT COUNT (total_amt_usd) AS no_of_orders, CASE WHEN total >= 2000 THEN 'over 2000' WHEN total > 1000 AND total < 2000 THEN '1000-2000' ELSE '1000 or under' END AS category
	FROM orders
  GROUP BY 2;

SELECT a.name, SUM (o.total_amt_usd) AS CLTV, CASE WHEN SUM (o.total_amt_usd) >= 200000 THEN 'high' WHEN SUM (o.total_amt_usd) >= 100000 THEN 'medium'  ELSE 'low' END AS level
	FROM orders o
  JOIN accounts a
  ON o.account_id = a.id
  GROUP BY 1
  ORDER BY 2 DESC;

SELECT a.name, SUM (o.total_amt_usd) AS CLTV, CASE WHEN SUM (o.total_amt_usd) >= 200000 THEN 'high' WHEN SUM (o.total_amt_usd) >= 100000 THEN 'medium'  ELSE 'low' END AS level
	FROM orders o
  JOIN accounts a
  ON o.account_id = a.id
  WHERE occurred_at BETWEEN '2016-01-01' AND '2017-12-31'
  GROUP BY 1
  ORDER BY 2 DESC;

SELECT s.name, COUNT(*) num_ords,
CASE WHEN COUNT(*) > 200 THEN 'top'
ELSE 'not' END AS sales_rep_level
  FROM orders o
  JOIN accounts a
  ON o.account_id = a.id
  JOIN sales_reps s
  ON s.id = a.sales_rep_id
  GROUP BY s.name
  ORDER BY 2 DESC;

SELECT s.name, COUNT(*) num_ords, SUM (total_amt_usd) AS total_sales, CASE WHEN COUNT(*) > 200 OR SUM (total_amt_usd) > 750000 THEN 'top' WHEN COUNT (*) > 150 OR SUM (total_amt_usd) > 500000 THEN 'middle' ELSE 'low' END AS sales_rep_level
    FROM orders o
    JOIN accounts a
    ON o.account_id = a.id
    JOIN sales_reps s
    ON s.id = a.sales_rep_id
    GROUP BY 1
    ORDER BY 3 DESC;

SELECT DATE_TRUNC('day',occurred_at) AS day,
channel, COUNT(*) as events
    FROM web_events
    GROUP BY 1,2
    ORDER BY 3 DESC;

SELECT *
  FROM (SELECT DATE_TRUNC('day',occurred_at) AS day,
               channel, COUNT(*) as events
        FROM web_events
        GROUP BY 1,2
        ORDER BY 3 DESC) sub;

SELECT channel, AVG(events) AS average_events
 FROM (SELECT DATE_TRUNC('day',occurred_at) AS day,
          channel, COUNT(*) as events
      FROM web_events
      GROUP BY 1,2) sub
      GROUP BY channel
      ORDER BY 2 DESC;

WITH t1 AS (
        SELECT s.name rep_name, r.name region_name, SUM(o.total_amt_usd) total_amt
         FROM sales_reps s
         JOIN accounts a
         ON a.sales_rep_id = s.id
         JOIN orders o
         ON o.account_id = a.id
         JOIN region r
         ON r.id = s.region_id
         GROUP BY 1,2
         ORDER BY 3 DESC),
      t2 AS (
         SELECT region_name, MAX(total_amt) total_amt
         FROM t1
         GROUP BY 1)
      SELECT t1.rep_name, t1.region_name, t1.total_amt
      FROM t1
      JOIN t2
      ON t1.region_name = t2.region_name AND t1.total_amt = t2.total_amt;

WITH t1 AS (
        SELECT r.name region_name, SUM(o.total_amt_usd) total_amt
         FROM sales_reps s
         JOIN accounts a
         ON a.sales_rep_id = s.id
         JOIN orders o
         ON o.account_id = a.id
         JOIN region r
         ON r.id = s.region_id
         GROUP BY r.name),
      t2 AS (
         SELECT MAX(total_amt)
         FROM t1)
      SELECT r.name, COUNT(o.total) total_orders
      FROM sales_reps s
      JOIN accounts a
      ON a.sales_rep_id = s.id
      JOIN orders o
      ON o.account_id = a.id
      JOIN region r
      ON r.id = s.region_id
      GROUP BY r.name
      HAVING SUM(o.total_amt_usd) = (SELECT * FROM t2);

      WITH t1 AS (
        SELECT a.name account_name, SUM(o.standard_qty) total_std, SUM(o.total) total
        FROM accounts a
        JOIN orders o
        ON o.account_id = a.id
        GROUP BY 1
        ORDER BY 2 DESC
        LIMIT 1),
      t2 AS (
        SELECT a.name
        FROM orders o
        JOIN accounts a
        ON a.id = o.account_id
        GROUP BY 1
        HAVING SUM(o.total) > (SELECT total FROM t1))
      SELECT COUNT(*)
      FROM t2;
      For the customer that spent the most (in total over their lifetime as a customer) total_amt_usd, how many web_events did they have for each channel?

      WITH t1 AS (
         SELECT a.id, a.name, SUM(o.total_amt_usd) tot_spent
         FROM orders o
         JOIN accounts a
         ON a.id = o.account_id
         GROUP BY a.id, a.name
         ORDER BY 3 DESC
         LIMIT 1)
      SELECT a.name, w.channel, COUNT(*)
      FROM accounts a
      JOIN web_events w
      ON a.id = w.account_id AND a.id =  (SELECT id FROM t1)
      GROUP BY 1, 2
      ORDER BY 3 DESC;

WITH t1 AS (
         SELECT a.id, a.name, SUM(o.total_amt_usd) tot_spent
         FROM orders o
         JOIN accounts a
         ON a.id = o.account_id
         GROUP BY a.id, a.name
         ORDER BY 3 DESC
         LIMIT 10)
      SELECT AVG(tot_spent)
      FROM t1;

WITH t1 AS (
         SELECT AVG(o.total_amt_usd) avg_all
         FROM orders o
         JOIN accounts a
         ON a.id = o.account_id),
      t2 AS (
         SELECT o.account_id, AVG(o.total_amt_usd) avg_amt
         FROM orders o
         GROUP BY 1
         HAVING AVG(o.total_amt_usd) > (SELECT * FROM t1))
      SELECT AVG(avg_amt)
      FROM t2;

SELECT RIGHT(website, 3) AS domain, COUNT(*) num_companies
      FROM accounts
      GROUP BY 1
      ORDER BY 2 DESC;
SELECT LEFT(UPPER(name), 1) AS first_letter, COUNT(*) num_companies
      FROM accounts
      GROUP BY 1
      ORDER BY 2 DESC;

SELECT SUM(num) nums, SUM(letter) letters
  FROM (SELECT name, CASE WHEN LEFT(UPPER(name), 1) IN ('0','1','2','3','4','5','6','7','8','9')
                             THEN 1 ELSE 0 END AS num,
               CASE WHEN LEFT(UPPER(name), 1) IN ('0','1','2','3','4','5','6','7','8','9')
                             THEN 0 ELSE 1 END AS letter
            FROM accounts) t1;

SELECT SUM(vowels) vowels, SUM(other) other
  FROM (SELECT name, CASE WHEN LEFT(UPPER(name), 1) IN ('A','E','I','O','U')
                                    THEN 1 ELSE 0 END AS vowels,
        CASE WHEN LEFT(UPPER(name), 1) IN ('A','E','I','O','U')
       THEN 0 ELSE 1 END AS other
       FROM accounts) t1;

SELECT LEFT(primary_poc, STRPOS(primary_poc, ' ') -1 ) first_name,
        RIGHT(primary_poc, LENGTH(primary_poc) - STRPOS(primary_poc, ' ')) last_name
 FROM accounts;

 SELECT LEFT(name, STRPOS(name, ' ') -1 ) first_name,
        RIGHT(name, LENGTH(name) - STRPOS(name, ' ')) last_name
 FROM sales_reps;

WITH t1 AS (
  SELECT LEFT(primary_poc,     STRPOS(primary_poc, ' ') -1 ) first_name,  RIGHT(primary_poc, LENGTH(primary_poc) - STRPOS(primary_poc, ' ')) last_name, name
  FROM accounts)
 SELECT first_name, last_name, CONCAT(first_name, '.', last_name, '@', name, '.com')
 FROM t1;

WITH t1 AS (
  SELECT LEFT(primary_poc,     STRPOS(primary_poc, ' ') -1 ) first_name,  RIGHT(primary_poc, LENGTH(primary_poc) - STRPOS(primary_poc, ' ')) last_name, name
  FROM accounts)
 SELECT first_name, last_name, CONCAT(first_name, '.', last_name, '@', REPLACE(name, ' ', ''), '.com')
 FROM  t1;

WITH t1 AS (
  SELECT LEFT(primary_poc,     STRPOS(primary_poc, ' ') -1 ) first_name,  RIGHT(primary_poc, LENGTH(primary_poc) - STRPOS(primary_poc, ' ')) last_name, name
  FROM accounts)
 SELECT first_name, last_name, CONCAT(first_name, '.', last_name, '@', name, '.com'), LEFT(LOWER(first_name), 1) || RIGHT(LOWER(first_name), 1) || LEFT(LOWER(last_name), 1) || RIGHT(LOWER(last_name), 1) || LENGTH(first_name) || LENGTH(last_name) || REPLACE(UPPER(name), ' ', '')
 FROM t1;

SELECT *
 FROM sf_crime_data
 LIMIT 10;
 yyyy-mm-dd

SELECT date orig_date, (SUBSTR(date, 7, 4) || '-' || LEFT(date, 2) || '-' || SUBSTR(date, 4, 2)) new_date
 FROM sf_crime_data;

SELECT date orig_date, (SUBSTR(date, 7, 4) || '-' || LEFT(date, 2) || '-' || SUBSTR(date, 4, 2))::DATE new_date
 FROM sf_crime_data;

SELECT *
 FROM accounts a
 LEFT JOIN orders o
 ON a.id = o.account_id
 WHERE o.total IS NULL;

SELECT COALESCE(a.id, a.id) filled_id, a.name, a.website, a.lat, a.long, a.primary_poc, a.sales_rep_id, o.*
 FROM accounts a
 LEFT JOIN orders o
 ON a.id = o.account_id
 WHERE o.total IS NULL;

SELECT COALESCE(a.id, a.id) filled_id, a.name, a.website, a.lat, a.long, a.primary_poc, a.sales_rep_id, COALESCE(o.account_id, a.id) account_id, o.occurred_at, o.standard_qty, o.gloss_qty, o.poster_qty, o.total, o.standard_amt_usd, o.gloss_amt_usd, o.poster_amt_usd, o.total_amt_usd
 FROM accounts a
 LEFT JOIN orders o
 ON a.id = o.account_id
 WHERE o.total IS NULL;

SELECT COALESCE(a.id, a.id) filled_id, a.name, a.website, a.lat, a.long, a.primary_poc, a.sales_rep_id, COALESCE(o.account_id, a.id) account_id, o.occurred_at, COALESCE(o.standard_qty, 0) standard_qty, COALESCE(o.gloss_qty,0) gloss_qty, COALESCE(o.poster_qty,0) poster_qty, COALESCE(o.total,0) total, COALESCE(o.standard_amt_usd,0) standard_amt_usd, COALESCE(o.gloss_amt_usd,0) gloss_amt_usd, COALESCE(o.poster_amt_usd,0) poster_amt_usd, COALESCE(o.total_amt_usd,0) total_amt_usd
 FROM accounts a
 LEFT JOIN orders o
 ON a.id = o.account_id
 WHERE o.total IS NULL;

SELECT COUNT(*)
 FROM accounts a
 LEFT JOIN orders o
 ON a.id = o.account_id;

SELECT COALESCE(a.id, a.id) filled_id, a.name, a.website, a.lat, a.long, a.primary_poc, a.sales_rep_id, COALESCE(o.account_id, a.id) account_id, o.occurred_at, COALESCE(o.standard_qty, 0) standard_qty, COALESCE(o.gloss_qty,0) gloss_qty, COALESCE(o.poster_qty,0) poster_qty, COALESCE(o.total,0) total, COALESCE(o.standard_amt_usd,0) standard_amt_usd, COALESCE(o.gloss_amt_usd,0) gloss_amt_usd, COALESCE(o.poster_amt_usd,0) poster_amt_usd, COALESCE(o.total_amt_usd,0) total_amt_usd
 FROM accounts a
 LEFT JOIN orders o
 ON a.id = o.account_id;

SELECT standard_qty. SUM(standard_qty) OVER (ORDER BY occurred_at) AS running_total
  FROM orders

SELECT standard_qty, DATE_TRUNC('month', occurred_at) AS month,
SUM(standard_qty) OVER (PARTITION BY DATE_TRUNC('month', occurred_at) ORDER BY occurred_at) AS running_total
  FROM orders

SELECT id, account_id, occurred_at, ROW_NUMBER() OVER (ORDER BY id) AS ROW_NUMBER
  FROM orders

SELECT id, account_id, occurred_at, ROW_NUMBER() OVER (ORDER BY occurred_at) AS ROW_NUMBER
  FROM orders

SELECT id, account_id, occurred_at, ROW_NUMBER() OVER (PARTITION BY account_id ORDER BY occurred_at) AS ROW_NUMBER

SELECT id, account_id, occurred_at, ROW_NUMBER() OVER (PARTITION BY account_id ORDER BY DATE_TRUNC('month', occurred_at)) AS row_num
  FROM orders
  FROM orders

SELECT id, account_id, occurred_at,
      ROW_NUMBER() OVER (ORDER BY occurred_at) AS row_num
  FROM orders

SELECT id, account_id, occurred_at,
      RANK() OVER (PARTITION BY account_id ORDER BY occurred_at) AS row_num
  FROM orders

SELECT id, account_id, occurred_at,
      RANK() OVER (PARTITION BY account_id ORDER BY occurred_at) AS row_num
  FROM orders

SELECT id, account_id, DATE_TRUNC('month', occurred_at) AS month,
      RANK() OVER (PARTITION BY account_id ORDER BY DATE_TRUNC('month', occurred_at)) AS row_num
  FROM orders

SELECT id, account_id, DATE_TRUNC('month', occurred_at) AS month,
      DENSE_RANK() OVER (PARTITION BY account_id ORDER BY DATE_TRUNC('month', occurred_at)) AS row_num
  FROM orders

SELECT id, account_id, total,
  		RANK() OVER (PARTITION BY account_id ORDER BY total DESC) AS total_rank
  FROM orders

SELECT id, account_id, standard_qty,
      DATE_TRUNC('month', occurred_at) AS month,
      DENSE_RANK() OVER (PARTITION BY account_id ORDER BY DATE_TRUNC('month', occurred_at)) AS dense_rank,
      SUM(standard_qty) OVER (PARTITION BY account_id ORDER BY DATE_TRUNC('month', occurred_at)) AS sum_standard_qty,
      COUNT(standard_qty) OVER (PARTITION BY account_id ORDER BY DATE_TRUNC('month', occurred_at)) AS count_standard_qty,
      AVG(standard_qty) OVER (PARTITION BY account_id ORDER BY DATE_TRUNC('month', occurred_at)) AS avg_standard_qty,
      MIN(standard_qty) OVER (PARTITION BY account_id ORDER BY DATE_TRUNC('month', occurred_at)) AS min_standard_qty,
      MAX(standard_qty) OVER (PARTITION BY account_id ORDER BY DATE_TRUNC('month', occurred_at)) AS max_standard_qty
  FROM orders

SELECT id, account_id, standard_qty,
        DATE_TRUNC('month', occurred_at) AS month,
        DENSE_RANK() OVER main_window AS dense_rank,
        SUM(standard_qty) OVER main_window AS sum_standard_qty,
        COUNT(standard_qty) OVER main_window AS count_standard_qty,
        AVG(standard_qty) OVER main_window AS avg_standard_qty,
        MIN(standard_qty) OVER main_window AS min_standard_qty,
        MAX(standard_qty) OVER main_window AS max_standard_qty
  FROM orders
  WINDOW main_window AS (PARTITION BY account_id ORDER BY DATE_TRUNC('month', occurred_at))
