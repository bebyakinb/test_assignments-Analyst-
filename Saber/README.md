# Тестовое задание на должность Junior Analyst в компании Saber Interactive

## 1. Задание №1. SQL
Напишите запрос, который выведет, сколько времени в среднем задачи каждой группы находятся в статусе “Open” 
Условия:
Под группой подразумевается первый символ в ключе задачи. Например, для ключа “C-40460” группой будет “C”
Задача может переходить в один и тот же статус несколько раз.
Переведите время в часы с округлением до двух знаков после запятой.

### Решение:
```SQL I'm A tab
select
    substr(issue_key, 1, 1) as working_group,
    round(avg(avg_minutes)/60,2) as avg_hours
from
    (select 
        issue_key,
        sum(minutes_in_status) as avg_minutes
    from 
        history
    where
        status = 'Open'
    group by
        issue_key
     )
group by
    working_group
```
## 2. Задание №2. SQL
Напишите запрос, который выведет ключ задачи, последний статус и его время создания для задач, которые открыты на данный момент времени.
Условия:
Открытыми считаются задачи, у которых последний статус в момент времени не “Closed” и не “Resolved”
Задача может переходить в один и тот же статус несколько раз.
Оформите запрос таким образом, чтобы, изменив дату, его можно было использовать для поиска открытых задач в любой момент времени в прошлом
Переведите время в текстовое представление

### Решение:
```SQL I'm A tab
select 
    issue_key,
    status,
    strftime('%Y-%m-%d %H:%M:%S', started_at / 1000, 'unixepoch') as start_time
from
    history
where
    (julianday('now') - 2440587.5)*86400.0*1000.0 between started_at and ended_at
    and status <> "Closed"
    and status <> "Resolved"
```

## 3. Задание №3. Interactive app on Pyton using streamlit
Задачей был разработать инетрактивное приложение по макету

![image](https://github.com/bebyakinb/test_assignments_Analyst/tree/master/Saber/assets/maket.png)

[Код приложения](https://github.com/bebyakinb/test_assignments_Analyst/tree/master/Saber/Task_3_streamlit_app.py)

[Сайт приложения](https://35.91.83.221:8501)


