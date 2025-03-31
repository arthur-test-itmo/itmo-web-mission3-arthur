
# Mission 3
## SQL Queries

### Запрос 1
```
SELECT 
    username 
FROM 
    users;
```

### Запрос 2
```
SELECT 
    u.username,
    COUNT(m.id) AS "number of sent messages"
FROM 
    users u
LEFT JOIN 
    messages m ON u.id = m."from"
WHERE 
    u.id IN (1, 2)
GROUP BY 
    u.username;`
```    

### Запрос 3
```
SELECT 
    u.username,
    COUNT(m.id) AS "number of received messages"
FROM 
    users u
JOIN 
    messages m ON u.id = m."to"
GROUP BY 
    u.username
ORDER BY 
    COUNT(m.id) DESC
LIMIT 1;
```

### Запрос 4
```
    SELECT 
    AVG(message_count) AS "average messages per user"
FROM 
    (SELECT u.id,
        COUNT(m.id) AS message_count
    FROM 
        users u
    LEFT JOIN 
        messages m ON u.id = m."from"
    WHERE
        u.id IN (1, 2) 
    GROUP BY u.id
    ) 
AS 
    user_message_counts;   
```
