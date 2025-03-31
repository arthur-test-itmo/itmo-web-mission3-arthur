
# Mission 3
## SQL Queries

### Запрос 1 - получить список юзернеймов пользователей
```
SELECT 
    username 
FROM 
    users;
```

### Запрос 2 - получить кол-во отправленных сообщений каждым пользователем:
    
    username - number of sent messages
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

### Запрос 3 - получить пользователя с самым большим кол-вом полученных сообщений и само количество
    
    username - number of received messages
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

### Запрос 4 - получить среднее кол-во сообщений, отправленное каждым пользователем
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
