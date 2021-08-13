
# Командное задание на летней школе МТС Тета


## 1. Выбор проекта

Проект будет реализован в области ритейла. В бизнесе с огромными оборотами всегда крайне остро стоят вопросы оптимизации. Благодаря эффективной обработке накопленных данных о поведении покупателей и их предпочтениях розничные торговые сети вполне способны получить конкурентные преимущества при минимальных затратах. «Умные» программы повышения лояльности клиентов, исключающие заведомо ненужные предложения или взаимодействие с незаинтересованной аудиторией, влияют на рост товарооборота и снижение потерь.

Наше решение позволит компании снизить средства на маркетинговую компанию, а также исключить взаимодействие с пользователями, которые могут негативно воспринять взаимодействие с ним.

Зная параметры клиентов мы сможем создать сервис, который будет автоматически определять, стоит ли компании как-либо взаимодействовать с клиентом.

## 2. Бизнес и математическая постановка задачи

Цель проекта - Нам необходимо разработать сервис, который предсказывает, следует ли отправлять текстовое сообщение клиенту.

Успешность внедрения проекта мы сможем оценить по уменьшенному оттоку клиентов и по уменьшенным затратам на отправку сообщений клиентам.

В качестве бизнес метрики мы будем использовать:

$$Revenue = \text{\it Number of customers} \times \text{\it Average Bill}$$


Оценивать бизнес метрику мы будем на всех клиентах



Для решения поставленой задачи мы построим uplift модель.

<img src="https://hsto.org/r/w1560/webt/mb/ed/iw/mbediw3l1dh76tk6_0-zgaxz-ss.jpeg" alt="drawing" width="200"/>

Принято выделять 4 типа клиентов реакции на коммункацию:
+ Не беспокоить — человек, который будет реагировать негативно, если с ним прокоммуницировать.
+ Потерянный — человек, который никогда не совершит целевое действие, вне зависимости от коммуникаций. Взаимодействие с такими клиентами не приносит дополнительного дохода, но создает дополнительные затраты.
+ Лояльный — человек, который будет реагировать положительно, несмотря ни на что. Это самый лояльный вид клиентов. По аналогии с предыдущим пунктом, такие клиенты также расходуют бюджет.
+ Убеждаемый — это человек, который положительно реагирует на предложение, но при его отсутствии не выполнил бы целевого действия. Это те люди, которых мы хотели бы определить нашей моделью, чтобы с ними прокоммуницировать.

Мы будем использовать uplift модель для того, чтобы выделить только убеждаемых клиентов.

В нашей задаче мы будем использовать метрику uplift@k, которая представляет собой размер uplift на топ k процентах выборки.
Значение k будет зависеть от бюджета, который есть для коммуникации с клиентами.

Таким образом мы сформулировали бизнес и математическую задачу, определили необходимые метрики для каждой из них.

## 3. Выбор набора данных

В этом проекте используются данные, предоставленные платформой ods.ai: [X5 Retail Hero: Uplift Modeling for Promotional Campaign](https://ods.ai/competitions/x5-retailhero-uplift-modeling), с помощью которых предсказывается, насколько можно увеличить вероятность покупки в результате отправки рекламного SMS. 

В данных содержится информация о клиентах и история покупок клиентов до коммуникации. 

Информация о клиентах: пол, возраст, first_redeem_date, first_issue_date

История покупок: дата покупки, id магазина, список купленных товаров, стоимость каждого товара, количество начисленных и потраченных бонусных баллов


## 4. Валидация данных и оценка потенциала

Исследование данных и построение baseline модели приведено в ноутбуке [uplift_eda.ipynb](https://github.com/flashlight101/teta_summer_school_uplift_x5/blob/main/uplift_eda.ipynb), ссылка для удобного просмотра в браузере: [nbviewer](https://nbviewer.jupyter.org/github/flashlight101/teta_summer_school_uplift_x5/blob/main/uplift_eda.ipynb)

Чтобы оценить качество модели, мы сделали отложенную выборку (hold-out) в 30%. Так как данных у нас много, кросс-валидация вычислительно дорогостоящий метод, поэтому использовать его нецелесообразно.

Мы исследовали данные и построили baseline модель, поэтому можем переходить к оценке экономического эффекта

## 5. Оценка экономического эффекта

Для визуализации оценки экономического эффекта составим таблицу:

Сценарий | Расходы | Доход | Прибыль |
---------|:-------:|------:|--------:|
Никак не взаимодействовать с клиентами     |  :arrow_right: | :arrow_right: | :arrow_right:
Провзаимодействовать со всеми клиентами     |  :arrow_upper_right: | :arrow_right: | :arrow_lower_right:
Взаимодействовать только с убеждаемыми клиентами     | :arrow_lower_right:  | :arrow_upper_right: | :arrow_upper_right:


Логично, что при улучшении качества нашей модели, расходы снизятся. Алгоритм все лучше и лучше будет ранжировать убеждаемых клиентов, на которых мы хотим сосредоточиться. За счет этого, прибыль с маркетинговой компании увеличится.




## Установка

```
git clone https://github.com/flashlight101/teta_summer_school_uplift_x5.git
cd teta_summer_school_uplift_x5
pip install -r requirements.txt
```
## Команда
+ Безмен Евгений
+ Евгений Туров
+ Петрик Ярослав
+ Шаймухаметов Ильяс