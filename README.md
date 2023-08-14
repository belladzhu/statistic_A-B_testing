В ходе тестирования некоторой гипотезы целевой группе была предложена новая механика оплаты услуг на сайте, у контрольной группы оставалась базовая механика.
Необходимо проанализировать итоги эксперимента и сделать вывод, стоит ли запускать новую механику оплаты на всех пользователей.


## Предварительный анализ данных
Был проведен предварительный анализ данных и построение графиков распределения оплат.
Распределение оплат активных пользователей: \
![распределение оплат](https://github.com/belladzhu/statistic_A-B_testing/assets/101130608/e37d641e-ede2-4125-8554-e4d7f97bed72) \
Выбросы по оплатам:
![боксплот по чеку](https://github.com/belladzhu/statistic_A-B_testing/assets/101130608/788ac2c1-4173-42d5-a0bc-36a837ca39c4)

## Определение метрик
Так как целевой группе была предложена новая механика оплаты услуг на сайте, то в первую очередь это повлияет на **CR в покупку**. Также проверим степень воздействия новой механики оплаты на среднее значение суммы оплаты (**ARPPU**). Ещё посчитаю **ARPU** вместе с ARPPU для просмотра степени воздействия на всех активных пользователей. \
Таким образом:
* CR в оплату (сonversion rate) — отношение количества платящих пользователей к общему количеству пользователей.\
Переход в оплату услуги. CR будет выше в том варианте, где пользователю проще проивзести оплату.

* ARPU - отношение всей выручки на количество активных пользователей.

* ARPPU - отношение выручки на количество активных оплативших пользователей.

## A/B - тест
* H0 - Новая механика оплаты услуг на сайте в группе B не отличается от базовой механики котрольной группы A.
* H1 - Новая механика оплаты услуг на сайте в группе B имеет значимые различия в сравнении с базовой механикой в группе A.

### Bootstrap CR в покупку
Гипотеза:
Н0: CR в покупку в двух группах не отличается
Н1: CR в покупку в двух группах отличается
![бутстрап CR](https://github.com/belladzhu/statistic_A-B_testing/assets/101130608/c59bab7b-6eaf-4bde-be3a-24bbdda79a1d)

### Bootstrap ARPU
Гипотеза:
Н0: ARPU в двух группах не отличается
Н1: ARPU в двух группах отличается
![бутстрап ARPU](https://github.com/belladzhu/statistic_A-B_testing/assets/101130608/5edb5257-2c4f-4cfd-b578-98756aebbbc6)

### Bootstrap ARPPU
Гипотеза:
Н0: ARPPU в двух группах не отличается
Н1: ARPPU в двух группах отличается
![бутстрап ARPPU](https://github.com/belladzhu/statistic_A-B_testing/assets/101130608/e050aff9-e9f2-42f4-960d-42ed6660be15)

## Вывод
Выводы по тестам:
* Бутстрап по CR показал pvalue > 0.05. Это не дало нам основания отвергнуть нулевую гипотезу.
* Бутстрап по ARPU показал pvalue < 0.05. Есть основания отвергнуть нулевую гипотезу.
* Бутстрап по ARPPU показал pvalue < 0.05. Это дает нам основания отвергнуть нулевую гипотезу.

Таким образом, согласно проведенным тестам новая механика оплаты даёт статистически значимый прирост в метриках ARPU и ARPPU. Имеет смысл применить новую механику оплаты услуг на всех пользователей. При этом в дальнейшем следить за метриками. Особенно за коэффициентом конверсии перехода к оплате. \
Однако стоит еще отметить, что так как система сплитования делит пользователей на группы неравномерно, в результате мы тестируем изменения на 85% наших активных пользователей. В будущем неудачный эксперимент в таком объеме может привести к значительному падению выручки. \
В идеале нужно было выделить больше пользователей для группы А, потому что из-за малого количества уникальных пользователей в группе А мы можем столкнуться с ситуацией, когда тесты показали статистически значимые различия, а в генеральной совокупности эти различий может не оказаться, либо различия будут в пользу базовой механики оплаты услуг на сайте.

### Дополнительно были рассчитаны метрики, с использованием SQL и реализована функция на языке python для автоматической подгрузки дополнительного файла и функция для построения графиков
Графики:
![графики метрик](https://github.com/belladzhu/statistic_A-B_testing/assets/101130608/fc091638-7517-4368-8179-ca4f562bd96c)



