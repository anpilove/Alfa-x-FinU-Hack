# Alfa x FinU Hack

## Команда Бета Банк

1. Karim Kuserbaev - руководитель, data scientist, бизнес-аналитик
2. Anpilov Kirill - data scientist
3. Dmitry Kondrashov - Аналитик данных
4. Artem Petrikov - data Scientist
5. Aidar Farkhutdinov - Бизнес-аналитик

==============================

### Стек технологий

`Python 3.10` `Pandas` `Numpy` `Catboost` `scikit-learn`

### Инструкция по запуску

Клонировать репозиторий

`git clone https://github.com/anpilove/Alfa-x-FinU-Hack.git`

`cd Alfa-x-FinU-Hack`

Установить виртуальное окружение

`python3 -m venv venv`

Запустить виртуальное окружение

`своя команда`

Установить все зависимости

`pip install -r requirements.txt`

Для обучения также требуется `GPU`

`CatBoostClassifier(task_type="GPU")`

==============================

## Организация проекта

    ├── AFH_Финал_Бета_Банк.ipynb         <- Основной файл-решение!
    ├── README.md                         <- Основной README для разработчиков, использующих этот проект.
    ├── data
    │   ├── test_data.pqt                 <- Оригинальный train.
    │   └── test_data.pqt                 <- Оригинальный test.
    │
    ├── submissions                       <- Лучшие сабмиты, top_1 public, top_1_all(на всем).
    │
    ├── models                            <- Обученные модели.
    │   ├── catboost_model_start_cluster.json   <- Модель catboost для восстановления start_cluster.
    │   └── catboost_model_end_cluster.json     <- Модель catboost для end_cluster.
    │
    ├── notebooks                         <- Jupyter ноутбуки. Со всеми нашими этапами и попытками.
    │
    └── requirements.txt                  <- Файл с требованиями для воспроизведения окружения анализа.

==============================

## Итог

Наша задача заключалась в создании модели CLTV, способной предсказывать вероятности перехода клиентов в каждый из 17 продуктовых кластеров в течение 12 месяцев.

Для этого мы использовали данные, предоставленные Альфа-Банком:

- Тренировочный датасет `train_data.pqt`, содержащий информацию о 200 000 клиентах банка и их целевых переменных за три последовательных месяца (month_1, month_2, month_3).
- Тестовый датасет `test_data.pqt`, включающий записи о 100 000 клиентах за 3 последовательных месяца (month_4, month_5, month_6).
- Для каждого клиента указан продуктовый кластер, в который он, предположительно, будет принадлежать через год (`end_cluster`). Наша задача - предсказать вероятности перехода клиентов в эти продуктовые кластеры для последнего месяца (month_6).

В результате анализа данных мы обнаружили следующие закономерности:

- Клиент остаётся в том же кластере с 2 по 3 месяц: 93.3%
- Данные имели пропуски с определенной закономерностью

Мы создали новые признаки со средними значениями из комбинации других столбцов. Также мы объединили данные об одном клиенте в единую строку.

Качество модели оценивалось по метрике **ROC-AUC**.

Лучший результат по качеству и скорости показала модель градиентного бустинга **CatBoost**. <br>
Полученный результат: ROC-AUC = **0.9039141107**, на всей выборке. <br>
Полученный результат: ROC-AUC = **0.896941145**, на публичной выборке (1 место).
