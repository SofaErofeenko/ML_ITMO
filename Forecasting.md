**Формулировка задачи ML:**  обучить модель, которая будет прогнозировать стоимость объектов недвижимости на основе различных свойств, таких как общая площадь, количество комнат, этаж, тип объекта и т.д. Это задача регрессии, так как цена недвижимости (целевая переменная) - это непрерывная переменная.

**Определение и обоснование ML-метрик:** В данной задаче, важно измерить, насколько хорошо модель может предсказывать стоимость недвижимости. Используем метрику  MAE (средняя абсолютная ошибка). Она обеспечивает представление о том, насколько в среднем наши предсказания отклоняются от реального значения. Ее можно легко интерпретировать и она учитывает все ошибки, независимо от их направления. 
(Р^2 (коэффициент детерминации) также может быть полезен для оценки, какой процент изменчивости в данных может объяснить модель)

**Перейдем к закгрузке данных:** Импортируем нужные библиотеки (import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_absolute_error
from sklearn.preprocessing import OneHotEncoder) 
Данные можно загрузить с помощью pandas функции read_csv, так как у нас CSV-файл.

**Сдлеаем обзор данных:** Используя head(), info() и describe(), рассмотрим базовые характеристики набора данных. 

**Предварительно обработаем данные:** Сначала с помощью функции isnull().sum() опредлим, сколько пропущенных значений в каждом столбце. Далее, для заполненим пропуски в  количественных переменных - на медианы fillna(). А в столбце "Settlement" заменим пропуски в settlement и area на строку 'unknown'.

**Обработаем категориальные переменные:** Используем One-hot encoding, чтобы преобразовать категориальные данные в числовой формат с помощью функции get_dummies(). One-hot encoding создает бинарные столбцы для каждой категории и является хорошим выбором, когда количество уникальных значений конечно и не слишком велико.

**Обучение и валидация модели:** Данные случайным образом разделяем на тренировочную и тестовую выборки в пропорции 70/30 с помощью train_test_split(). Создаем датафрейм X из всех признаков, исключая цену, и y - только столбец с ценами. Сначала обучим базовую модель с помощью fit(), используем линейную регресию *Это дает понимание того, как исходные данные могут предсказывать цены на недвижимость без дополнительной обработки или сложных моделей.*  Затем проверим ее точность на тестовой выборке с помощью predict() и используем метрики оценки ошибок -  mean_absolute_error().
 
Если MAE равна 0, это означает, что модель идеально предсказывает стоимости объектов недвижимости. Чем больше значение MAE, тем хуже модель предсказывает целевую переменную, а именно это цена недвижимости.

**Применение более сложных моделей:** Из более сложных моделей я бы выбрала случайный лес или градиентный бустинг. С их помощью мы посмотрим улучшат ли они качество прогноза. Потому что эти модели  могут обрабатывать большее количество данных, и их работа постепенно улучшается по мере увеличения объема данных. Они также позволяют улавливать нелинейность между выборками. 
Также я бы использовала кросс-валидацию в процессе обучения и настройки моделей, чтобы убедиться, что результаты хорошо обобщаются на новые данные.
