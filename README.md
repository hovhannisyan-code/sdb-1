# Домашнее задание к занятию «Базы данных, их типы»2

Какие типы СУБД, на ваш взгляд, лучше всего подойдут для решения этих задач и почему? 
 
1.1. Бюджетирование проектов с дальнейшим формированием финансовых аналитических отчётов и прогнозирования рисков.

Ответ:

СУБД должна гарантировать целостность и чёткую структуру данных.
Лучше всего подойдёт Postgresql — надёжная реляционная СУБД с поддержкой транзакций и чёткой структуры данных.

___

1.1.* Хеширование стало занимать длительно время, какое API можно использовать для ускорения работы? 

Ответ:
На практике я использую bcrypt, так как он безопасный. Но если нужно ускорить процесс, можно кешировать аутентифицированных пользователей, чтобы не пересчитывать хеш каждый раз при проверке. Например, хранить данные в Redis и проверять токен/сессию, минуя повторную авторизацию.
___

1.2. Под каждый девелоперский проект создаётся отдельный лендинг, и все данные по лидам стекаются в CRM к 
маркетологам и менеджерам по продажам. Какой тип СУБД лучше использовать для лендингов и для CRM? 
СУБД должны быть гибкими и быстрыми.

Ответ: 
Для лендингов — MongoDB (гибкая схема). Для CRM — Postgresql.
___

1.2.* Можно ли эту задачу закрыть одной СУБД? И если да, то какой именно СУБД и какой реализацией?

Ответ: 
Да, можно. Я бы использовал Postgresql — у него есть тип данных jsonb, который хранится в бинарном виде и отлично подходит для гибких структур.

1.3. Отдел контроля качества решил создать базу по корпоративным нормам и правилам, обучающему материалу 
и так далее, сформированную согласно структуре компании. СУБД должна иметь простую и понятную структуру.

Ответ:
Sqlite, Mysql, Postgresql
___

1.3.* Можно ли под эту задачу использовать уже существующую СУБД из задач выше и если да, то как лучше это 
реализовать?

Ответ:
Да, можно — если выбрать Postgresql из CRM
___

1.4. Департамент логистики нуждается в решении задач по быстрому формированию маршрутов доставки материалов 
по объектам и распределению курьеров по маршрутам с доставкой документов. СУБД должна уметь быстро работать
со связями.

Ответ:
Neo4j, можно и Postgres там есть расширения PostGIS
___

1.4.* Можно ли к этой СУБД подключить отдел закупок или для них лучше сформировать свою СУБД в связке с СУБД 
логистов?

Ответ:
Можно Postgres


1.5.* Можно ли все перечисленные выше задачи решить, используя одну СУБД? Если да, то какую именно?

*Приведите ответ в свободной форме.*

Ответ: 
Всё можно реализовать на Postgresql — она универсальна: и для чёткой структуры, и для гибкости, и для работы с геоданными.
---

### Задание 2. Транзакции

2.1. Пользователь пополняет баланс счёта телефона, распишите пошагово, какие действия должны произойти для того, чтобы 
транзакция завершилась успешно. Ориентируйтесь на шесть действий.

Ответ: 
Пользователь вводит сумму и выбирает способ оплаты.
Система создаёт запрос на платёж и сохраняет его в базе.
Пользователь подтверждает платёж.
Платёжная система возвращает успешный статус.
Система проводит транзакцию — увеличивает баланс пользователя.
Финальный шаг — запись в журнал операций и уведомление пользовател

2.1.* Какие действия должны произойти, если пополнение счёта телефона происходило бы через автоплатёж?

*Приведите ответ в свободной форме.*

Ответ:
Система по расписанию проверяет условия автоплатежа и далее выполняет те же шаги, что и при обычном пополнении — формирует платёж, проверяет статус и зачисляет средства.
---

### Задание 3. SQL vs NoSQL

3.1. Напишите пять преимуществ SQL-систем по отношению к NoSQL. 

3.1.* Какие, на ваш взгляд, преимущества у NewSQL систем перед SQL и NoSQL.

*Приведите ответ в свободной форме.*

Ответ: 
Структура данных, поддержка транзакций (ACID), язык SQL, надёжность, аналитические возможности.
---

### Задание 4. Кластеры

Необходимо производить большое количество вычислений при работе с огромным количеством данных, под эту задачу 
выделено 1000 машин. 

На основе какого критерия будете выбирать тип СУБД и какая модель *распределённых вычислений* 
здесь справится лучше всего и почему?

*Приведите ответ в свободной форме.*

Ответ: 
Выбирать СУБД стоит по критерию масштабируемости и скорости распределённой обработки.
Лучше всего подойдёт колоночная база данных ClickHouse — она отлично справляется с аналитикой на больших объёмах.
