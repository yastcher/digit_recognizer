# Digit Recognizer

Kaggle Competition: [Digit Recognizer](https://www.kaggle.com/competitions/digit-recognizer)

Классификация рукописных цифр MNIST с использованием CNN (PyTorch).

## Результаты

| Модель | Public Score | Описание |
|--------|-----------|----------|
| CNN + BatchNorm | 0.99264 | Baseline: 3 conv блока с BatchNorm и Dropout |
| CNN + Polar | 0.99067 | Эксперимент: добавление полярных координат как второго канала |
| CNN + Augmentation | 0.99421 | Data Augmentation: rotation, shift, scale |

## Структура проекта

```
digit_recognizer/
├── data/
│   ├── train.csv
│   ├── test.csv
│   └── sample_submission.csv
├── digit_recognizer_baseline.ipynb    # Baseline решение
├── digit_recognizer_polar.ipynb       # Эксперимент с полярными координатами
├── digit_recognizer_augmentation.ipynb # Data Augmentation
├── pyproject.toml
├── submission.csv
└── README.md
```

## Архитектура модели

```
CNN(
  (conv1): Conv2d(1, 32, kernel_size=3, padding=1)
  (conv2): Conv2d(32, 64, kernel_size=3, padding=1)
  (conv3): Conv2d(64, 128, kernel_size=3, padding=1)
  (bn1-3): BatchNorm2d
  (pool): MaxPool2d(2, 2)
  (dropout1): Dropout(0.25)
  (dropout2): Dropout(0.5)
  (fc1): Linear(128*3*3, 256)
  (fc2): Linear(256, 10)
)
```

## Запуск

1. Загрузить notebook на [Kaggle](https://www.kaggle.com/competitions/digit-recognizer/code)
2. Включить GPU: Settings → Accelerator → GPU
3. Запустить все ячейки
4. Скачать `submission.csv` и отправить

## Эксперименты

### Baseline
Стандартная CNN с BatchNorm — достаточно для ~99.3%.

### Polar Coordinates (неудачный)
Гипотеза: полярное представление изображения может выделить радиальные паттерны цифр.
Результат: ухудшение на 0.2%. CNN справляется лучше с исходными данными.

### Data Augmentation
- RandomRotation(±10°)
- RandomAffine: translate(±10%), scale(90-110%)
- Без горизонтального отражения (цифры станут нечитаемыми)

## Зависимости

- Python 3.13+
- PyTorch
- torchvision
- pandas
- numpy
- matplotlib
- scikit-learn
