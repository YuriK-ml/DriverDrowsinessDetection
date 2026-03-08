# Drowsy Driver Detection System (English)

## Description
Neural network-based system for detecting drowsy drivers.  
Implements a full video pipeline: face detection → eye state classification → alert signal.  

**Approach:** classification on full face crops using **MobileNetV2** with pre-trained ImageNet weights.  
- Binary classification: `0` — eyes open, `1` — eyes closed  
- Base layers frozen to avoid overfitting  

The training data is based on an open dataset:  
[Roboflow Drowsiness Detection](https://universe.roboflow.com/buerp/drowsiness-detection-batyb)
The dataset contains annotated images of faces with different eye states and is suitable for detection and classification tasks.

**Note:**  
This prototype operates only with pre-recorded video files.  
For use in real-time systems, additional adaptation is required to process video streams from a live camera.

## Face Detection & Pipeline
- **OpenCV DNN (SSD + ResNet)** for face localization  
- Ensures input consistency and stable performance

## Tools
- TensorFlow / Keras — model training  
- OpenCV — video processing & visualization  
- Roboflow Drowsiness Detection Dataset — training & validation  
- Keras Callbacks, class weights — training control

## Key Findings
- Stable eye state classification  
- Balance between accuracy and computational efficiency  
- Temporal aggregation distinguishes blinks from drowsiness  

## Conclusion
Prototype demonstrates integration of computer vision and deep learning into practical driver monitoring solutions.

# Система распознавания засыпающего водителя (Русский)

## Описание прототипа
Представляет собой нейросетевую систему распознавания засыпающего водителя.  
Реализует полный пайплайн обработки видеопотока: от детекции лица до классификации состояния глаз и генерации тревожного сигнала.
Полученное решение может служить прототипом для дальнейшего внедрения в реальные системы мониторинга водителя.
В качестве обучающей базы используется открытый датасет:  
[Roboflow Drowsiness Detection](https://universe.roboflow.com/buerp/drowsiness-detection-batyb)
Датасет содержит размеченные изображения лиц с различными состояниями глаз и подходит для задач детекции и классификации.

**Примечание:**  
Данный прототип работает только с заранее записанным видеофайлом.  
Для использования в системах реального времени требуется дополнительная адаптация алгоритма для работы с видеопотоком камеры.

---

## Общий подход
- Классификация состояния глаз выполняется по **кропу лица целиком**.
- Используется архитектура **MobileNetV2** с предобученными весами ImageNet.
- Классификационная голова дообучена для бинарной классификации:
  - `0` — глаза открыты  
  - `1` — глаза закрыты
- Заморозка базовых слоёв MobileNetV2 предотвращает переобучение и фокусирует обучение на задаче распознавания состояния глаз.
- Для выделения области лица используется **DNN-детектор OpenCV (SSD + ResNet)**.

---

## Используемый инструментарий
- **TensorFlow / Keras** — построение и обучение модели.  
- **OpenCV** — обработка видеопотока, детекция лиц, визуализация.  
- **Roboflow Drowsiness Detection Dataset** — основная база для обучения и валидации.  
- **Keras Callbacks** (EarlyStopping, ModelCheckpoint) — контроль обучения.  
- **Class weights** — балансировка классов.  

---

## Результат работы прототипа
- Модель стабильно классифицирует состояние глаз по изображению лица.  
- Архитектура обеспечивает баланс между точностью распознавания и вычислительной эффективностью.  
- Временная агрегация предсказаний помогает различать кратковременные моргания и признаки сонливости.  

