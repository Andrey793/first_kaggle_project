# first_kaggle_project

Выполнял вот это задание: https://www.kaggle.com/competitions/leaf-classification/overview
Задача: дан датасет с черно белыми фотографими растений 99 видов и некоторыми извлеченными табличными данными. Нужно обучить модель, которая будет предсказывать по этим данным вид растения. Ошибка измерятеся при помощи logloss.

Для извлечения дополнительных признаков из фотографий взял предобученную модель resnet18. Здесь и в остальных сетях использовал алгоритм оптимизации adam. И дообучил ее последние 2 слоя на имеющихся данных. Эта модель предсказывает класс только по фотографии. На валидационной выборке получил logloss ~ 0.4 и acc ~ 0.955. На тестовых данных ошибка гораздо выше logloss ~ 9.
Полученные предсказания по картинкам добавил к имеющимся табличным данным и обучил на них catboost classifier. Ошибка на валидационной выборке logloss ~ 0.09. На тестовых ~ 6.5.

Потом решил заменить модель градиентного бустинга нейронной сетью. Сначала создал из 3 слоев, после первых двух функция relu и после второго dropout с вероятностю 0.3. На валидации acc ~ 0.98 и logloss ~ 0.1, на тесте ошибка занчительно больше - 15. 

После взял сеть TabNet при обучении использовал lr_scheduler для коректировки learning rate. Модель обучалась медленно, удалось добиться на валидации acc ~ 0.86 и logloss ~ 0.7. На тестовой выборке ошибка самая большая ~ 25. 

В итоге выбранные нейронные сети показали себя хуже в работе с табличными данными, чем методы градиентного бустинга. Приблизить ошибку на тестовой выборке к ошибке на валидационной не удалось. 
