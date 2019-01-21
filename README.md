/* Write a query to print all prime numbers less than or equal to . 
Print your result on a single line, and use the ampersand () character as your separator (instead of a space).
*/
SELECT LISTAGG(PRIME_NUMBER,'&') WITHIN GROUP (ORDER BY PRIME_NUMBER)
FROM(
SELECT L PRIME_NUMBER
FROM(
SELECT LEVEL L
FROM DUAL
CONNECT BY LEVEL <= 1000),
(SELECT LEVEL M FROM DUAL CONNECT BY LEVEL <= 1000)
WHERE M <= L
GROUP BY L
HAVING COUNT(CASE WHEN L/M = TRUNC(L/M) THEN 'Y' END) = 2
ORDER BY L);
