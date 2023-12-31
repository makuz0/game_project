# game_project
В настоящем проекте принимаю роль аналитика в компании, разрабатывающей мобильный игры.


#### **Предстоит решить три вопроса:**

1. Написание функции по подсчету Retention игроков
**Имеющиеся данные:**
reg_data - df о времени регистрации
auth_data - df о времени захода пользователей в игру
data - df в котором смерджены reg_data и auth_data по "uid"

2. Имеются два различных набора предложений (a_group и b_group).
- ARPU в тестовой группе(b_group) выше на 5%, чем в контрольной(a_group);
- В контрольной группе(a_group) 1928 игроков из 202103 платящие (~0.95%);
- В тестовой(b_group) группе 1805 из 202667 платящие (~0.89%).

**Объявляем гипотезы:**
- H0 – никакого различия между группами a & b нет
- H1 – группы a & b значимо различаются

Требуется выявить лучший набор предложений.

3. Необходимо определить набор метрик оценки результат согласно следующему условию:
_В игре Plants & Gardens каждый месяц проводятся тематические события, ограниченные по времени. В них игроки могут получить уникальные предметы для сада и персонажей, дополнительные монеты или бонусы. 
Для получения награды требуется пройти ряд уровней за определенное время. С помощью каких метрик можно оценить результаты последнего прошедшего события?
Предположим, в другом событии мы усложнили механику событий так, что при каждой неудачной попытке выполнения уровня игрок будет откатываться на несколько уровней назад. Изменится ли набор метрик оценки результата? Если да, то как?_


#### **Используемый стек:**
* Python
- numpy 
- pandas 
- scipy.stats
- matplotlib.pyplot
- tqdm.auto
- seaborn 
- datetime
* Tableau


### **Итоги:**
1. Написана функция по расчету Retention с возможностью указания индивидуальных параметров отбора (указание временного промежутка для расчета Retention или выбор всего периода словом "all", выбор требуемых uid или выбор всех, указание требуемого диапазона дней удержания).
Также, для примера, выбран период 2017-01-01 по 2017-01-10 по которому подготовлена визуализация для бОльшего удобства в Tableau - https://public.tableau.com/app/profile/maksim.kuzmin/viz/Final_project_v1_Retention/Sheet2?publish=yes

2.  Принимая во внимание проведенный тест бутстрап, очистку данных(удаление 'нулевых значений') и анализ графиков, считаю абсолютно обоснованным отклонить H0 гипотезу и заключить, что b_group(тестовая группа) значимо отличается от a_group(контрольная группа) 
и приносит бОльшую прибыль компании, а значит наборы акционных предложений b_group работают корректно и стоит распространить их(наборы акционных предложений b_group) на всех пользователей для увеличения прибыли компании.
P.S. в идеале отобрать новые выборки согласно методологии и еще раз провести наш анализ:

- Выборка должна быть репрезентативной (отражать разнообразие ГС)
- Размер выборки должен быть достаточным для обнаружения различий
- Выборка должна быть случайной 
- Постараться исключить из выборки выбросы
- Учесть специфические факторы, влияющие на выборки.

3.  Так как тематические события проводятся ограниченное кол-во времени в месяц, то они должны вызывать повышенный интерес у игроков, т.к. это даёт возможность получить дополнительные и уникальные предметы/бонусы/монеты для персонажа или сада, что в свою очередь улучшит их игровые показатели, 
даст  преимущество перед другими игроками(по меньшей мере моральное удовольствие), которые не участвуют в тематических событиях и не получают уникальные предметы/бонусы/монеты, а значит их сад и персонажи развиваются чуть медленнее. Также устанавливается условие по времени прохождения уровней, 
что усложняет задачу игрокам, а значит надо принимать участие в тематическом событии как можно раньше после его старта. Принимая во внимание вышеизложенное, считаю желательным набором для оценки результатов следующие метрики:

**ОХВАТ(общее кол-во игроков)** - оценить до начала тематического события 
и вовремя его проведения, путем подсчета уникальных ID игроков участвующих в событии, это позволит оценить заинтересованность и качество самого события;

**ДЛИТЕЛЬНОСТЬ СЕАНСА** - измерить продолжительность игровой сессии игроков в обычное время (без событий) и во время их проведения, также можно подсчитать кол-во входов в игру. 
Если события увлекательны и интересны игрокам, то время, проведенное в игре и кол-во входов будет больше.

**RETENTION RATE(коэффициент удержания)** - измерить процент пользователей, которые возвращаются в игру после их первого входа. Если процент удержания падает, 
то подумать над введением дополнительных наград игрокам в случае участия в каждом событии или выполнения минимального задания.

**CHURN RATE(коэффициент оттока)** - отследить изменения процента игроков, которые перестали пользоваться игрой. Вряд ли данные события могут отрицательно повлиять на эту метрику, 
но в случае однотипности событий или снижения мотивации игроков, эта метрика покажет отток, и в этом случае необходимо пересмотреть формат событий.

**ПРОГРЕСС ПРОХОЖДЕНИЯ** - важно измерить средний процент прохождения каждого уровня игроками (например, всего 5 уровней, где 1 уровень это - легко, а 5 - очень сложно, 
условно 1 уровень проходит 90% игроков, 2 уровень 75% игроков, ... 5 уровень 20% игроков), это позволит отслеживать корректность сложности составления уровней и на сколько интересно\сложно они составлены для игроков, а также кол-во игроков прошедших каждый из этапов из месяца в месяц.

**КОЛ-ВО ОБРАЩЕНИЙ В ПОДДЕРЖКУ / ОТЗЫВЫ** - позволит оценить качество проработки событий и работы поддержки. Можно высчитать среднее кол-во обращений по каждому событию (позитивное / негативное), например за три месяца проведения событий и использовать как ориентир. 
В случае превышения среднего значения по негативным отзывам/обращениям скорректировать последующие события с учетом полученных замечаний.

**РЕГИСТРАЦИЯ НОВЫХ ПОЛЬЗОВАТЕЛЕЙ** - сравнить с обычным периодом (без событий) среднее кол-во новых игроков и во время начала события. Позволит выяснить увеличивают ли события приток новых игроков.

**МОНЕТИЗАЦИЯ** - в случае наличия в игре возможности приобретать доп. бонусы/преимущества, надо сравнить средний чек в период без событий и вовремя. Это позволит узнать тратят ли игроки больше денег на игровой процесс во время событий. 
Также можем рассчитать такие метрики как ARPU(средний доход на одного пользователя), ARPPU(средний доход на одного платящего пользователя). 


В данном случае более важными метриками могут стать:

**CHURN RATE** - важно следить за оттоком игроков, так как усложнение игрового процесса в качестве отката, может снизить заинтересованность игроков.

**RETENTION RATE(коэффициент удержания)** - также будет являться важной метрикой, так как создавая откат в уровнях, игроки могут начать терять интерес и перестанут участвовать в событиях.

**ПРОГРЕСС ПРОХОЖДЕНИЯ** - данная метрика однозначно будет отличаться от версии без откатов, так как психологически некоторые игроки будут "нервничать" во время откатов (особенно на последних уровнях) и переставать участвовать в событиях. 

Надо внимательно следить за этой метрикой и в случае сильного снижения прохождения определенных уровней корректировать их сложность или повышать ценность наград за их прохождение, что бы сохранить интерес и мотивацию игроков.

Также будет полезно отслеживать отзывы/обращения в поддержку, будет представление о реакции игроков и может указать на технические сложности в прохождении или процессе откатов.
