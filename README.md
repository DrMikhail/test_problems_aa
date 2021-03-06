## Объяснения по задачам
### Journey to Springfield
В рассматриваемой задаче данных относительно немного, поэтому чтобы компенсировать нехватку данных для обучения слоев, выделяющих общие паттерны, используем предобученную модель Inception v3 с последующем дообучением, заменив слои для классификации на нужное число классов (auxiliary output и final output). Также данные сильно несбалансированы, поэтому примерно уравняем число объектов в каждом классе, размножив объекты в кажом классе до значения как в классе с максимальным числом объектов. Засчет рандомности аугментаций в каком-то смысле так раскопированные объекты можно считать как новые изображения. Будем использовать только отражения и повороты. Так как изображения взяты из мультфильма (не реальные снимки), то они не страдают тенями, нехваткой освещенности, шумами, поэтому не будем добавлять аугментации цвета, шума, контрастности, яркости и т.д., чтобы не путать модель. Более того цвета в данной задаче более менее стабильны в датасете, поэтому они как раз могу быть важны и характерны для определения принадлежности к классу конкретного персонажа. Обучение организуем в три этапа: сначала замораживаем модель кроме слоя классификатора, чтобы получить некоторое предварительное распределение; затем обучим модель на несбалансированных данных; после на сбалансированных. Второй шаг обусловлен тем, что модель на сбалансированных данных учиться долго (потому что их просто больше).

В данной задаче уже с такой подготовкой данных получается достаточно высокий скор по метрике f1 на тесте: 0.99787.

Вообще был такой прогресс: без ребалансировки c Resnet18: 0.99043 -> c ребалансировкой c Resnet18: 0.99574 -> c ребалансировкой c Inception v3: 0.99787

Предсказания в submission.csv

### Flower Segmentation

Использовалась модель DeepLab V3+, непредобученная, но с backbone из Resnet 50. Если все верно понял, то backbone использовать можно, что также сказано и в baseline в конкурсе. Использование backbone оправдано, так как данных мало. В аугментациях использовал отражения, повороты и кропы (из исходного изображения сразу кропы нужного размера). Также добавлял дилатацию и эрозию (но не особо принципиально в данном случае).

Модель дает скор 0.85825

Предсказания в submission.csv
