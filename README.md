# Поиск одинаковых товаров (Хакатон ЛЦТ 2023, задача от компании OZON)
Проект завершён в мае 2023

## В ходе проекта:
- **Отработаны навыки командной работы**
- **Были изучены и активно использовались разреженные матрицы, что позволило значительно увеличить скорость и сократить потребление памяти**
- **Отлично прокачаны навыки оптимизации алгоритмов – разработаны и реализованы технические решения, позволяющие значительно сократить время выполнения операций и потребляемую память: использование множеств, применение векторизованных операций над массивами, использование разреженных матриц, обработка и заполнение данных батчами и т.п.**

<br>

## Описание
OZON – одна из крупнейших интернет-компаний в России. На данный момент более 90% ассортимента компании формируют её партнеры, в некоторых случаях предлагающие одинаковые товары по разной стоимости и с разными сроками доставки. Необходимо разработать ML-модель, способную определять идентичность товаров по названиям, атрибутам и изображениям. Это поможет Ozon усовершенствовать алгоритм определения одинаковых товаров, чтобы клиенты лучше ориентировались в предложениях продавцов

В распоряжении:
- Тренировочная выборка: пары одинаковых и различных товаров
- Тестовая выборка: пары товаров без разметки
- Дополнительные данные: названия, атрибуты, векторные представления картинок (эмбеддинги) товаров

Во время подготовки к хакатону мы уже отработали навыки командной работы, поэтому, так же, как и в прошлый раз, мы сразу распределили задачи среди участников. Моей зоной ответственности были атрибуты товаров

## Цели
Построить модель машинного обучения, позволяющую определять одинаковые товары в паре на основании их атрибутов

## Результаты и выводы
Разработанная модель, определяющая одинаковые товары в паре на основании их атрибутов, показала неплохие результаты, была включена в общую модель команды, а также попала в тройку лучших сабмитов команды

Реализация проведена в рамках двух основных этапов: подготовки признаков из атрибутов товаров и непосредственно процесса обучения модели на них и получения предиктов. Подробнее:

#### 1. Подготовка признаков
При обработке столбца с атрибутами товаров из обучающей выборки всего было получено 1447 уникальных атрибута. Значения атрибутов представляют собой списки строковых данных, в большинстве случаев состоящие из одного элемента-атрибута, реже – из нескольких элементов в списке

В качестве признаков используются совпадения, несовпадения и частичные совпадения в векторе из 1447 атрибутов, которые обозначаются определенными числовыми значениями, например, 1, 0.1, 0.5. Частичное совпадение имеет место, когда хотя бы у одного из товаров список значений для конкретного рассматриваемого атрибута состоит из 2 или более элементов и они пересекаются со значениями в списке атрибута второго товара в паре. В случаях, когда конкретного атрибута нет у сравниваемых товаров, или у одного товара есть, а у другого нет, в векторе признаков проставляются нули

#### 2. Обучение и предикты модели
Чтобы помочь модели разделять классы, для каждого признака рассчитывается "коэффициент значимости", который "подсвечивает" для модели случаи, на которые нужно обратить внимание. Например, в нулевом классе несовпадения атрибутов являются очень важным фактором, а совпадения атрибутов – наоборот, незначительным, на который не стоит обращать внимание (как впрочем в какой-то мере и совпадения атрибутов в первом классе). Таким образом, для каждой пары товаров исходный вектор признаков умножается на factor – вектор коэффициентов для каждого признака, подобранный в результате исследования и анализа их влияния на модель

Первичный исследовательский анализ показал, что разные категории товаров довольно сильно различаются по множеству параметров, в том числе и по атрибутам, характерным для данной категории. Для того чтобы модель более прицельно могла классифицировать пары товаров, она обучалась отдельно на каждой категории. Далее предикты каждой категории объединялись в единый вектор предиктов. В качестве моделей для каждой категории была применена модель градиентного бустинга LightGBM

## Стек
python, pandas, numpy, matplotlib, scipy, sklearn, lightgbm

<br><br>

Код 1-й части проекта: [attr04_1_get_features.ipynb](https://github.com/petrochenkovp/leaders2023/blob/main/attr04_1_get_features.ipynb)

Код 2-й части проекта: [attr04_2_model.ipynb](https://github.com/petrochenkovp/leaders2023/blob/main/attr04_2_model.ipynb)

Другие мои проекты: [Портфолио](https://github.com/petrochenkovp/portfolio)

<br><br>
