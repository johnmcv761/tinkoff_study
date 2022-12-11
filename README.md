**решение задач сайта тинькофф-обучение**

# Задача 1. Напишите запрос, который выведет пилотов, которые в качестве второго пилота в августе этого года трижды ездили в аэропорт Шереметьево.


select Пилоты.name 

from Пилоты 

left join Рейсы on Пилоты. pilot_id = Рейсы. second_pilot_id

where flight_dt between '2021-07-31' and '2021-09-01' 

and count(Рейсы.flight_id) = 3

and Рейсы.destination = “Шереметьево”


Задача 2. Выведите пилотов старше 45 лет, совершали полеты на самолетах с количеством пассажиров больше 30.


select Пилоты.name 

from Пилоты 

left join Рейсы on Пилоты. pilot_id = Рейсы. first_pilot_id

and Пилоты. pilot_id = Рейсы. second_pilot_id

inner join (select plane_id from Самолеты where cargo_flg = 0) Самолеты_пасс 

on Рейсы.plane_id = Самолеты_пасс.plane_id

where Пилоты.age > 45

and capacity > 30 


Задача 3. Выведите ТОП 10 пилотов-капитанов (first_pilot_id), которые совершили наибольшее число грузовых перелетов в этом году.


select top (10) Пилоты.name 

from Пилоты 

left join Рейсы on Пилоты. pilot_id = Рейсы. first_pilot_id 

inner join (select plane_id from Самолеты where cargo_flg = 1) Самолеты_груз

on Рейсы.plane_id = Самолеты_груз.plane_id

where extract(year from рейсы.flight_dt) = 2022

group by Пилоты.name 

order by count(flight_id) DESC 

