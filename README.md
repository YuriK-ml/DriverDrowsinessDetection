# Drowsy Driver Detection System (English)

## Description
Neural network-based system for detecting drowsy drivers.  
Implements a full video pipeline: face detection → eye state classification → alert signal.  
Serves as a prototype for real driver monitoring systems using computer vision and deep learning.

## Experiments
- **Full frames:** trained on entire video frames — low accuracy, sensitive to background.  
- **Eye crops:** trained on eye regions — high accuracy on static images, unstable on real video (lighting, head rotation, partial occlusion).  

**Final approach:** classification on full face crops using **MobileNetV2** with pre-trained ImageNet weights.  
- Binary classification: `0` — eyes open, `1` — eyes closed  
- Base layers frozen to avoid overfitting  

## Face Detection & Pipeline
- **OpenCV DNN (SSD + ResNet)** for face localization  
- Same detector used for training and real-time video  
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
- Real-time eye detection not required due to instability

## Conclusion
Prototype demonstrates integration of computer vision and deep learning into practical driver monitoring solutions.

# Система распознавания засыпающего водителя (Русский)

## Описание проекта
Проект представляет собой нейросетевую систему распознавания засыпающего водителя.  
Система реализует полный пайплайн обработки видеопотока: от детекции лица до классификации состояния глаз и генерации тревожного сигнала.

Проект направлен на практическое применение методов компьютерного зрения и глубокого обучения для обеспечения безопасности дорожного движения. Полученное решение может служить прототипом для дальнейшего внедрения в реальные системы мониторинга водителя.

---

## Этапы экспериментов

### Эксперимент 1: Обучение на полных кадрах видео
- Модель обучалась на изображениях полного видеокадра без выделения лица или глаз.
- Результаты: низкая точность классификации, чувствительность к фону и салону автомобиля.

### Эксперимент 2: Обучение на кропах глаз
- Модель обучалась на областях глаз.
- Высокая точность на статических изображениях, но нестабильность при реальном видео (изменение освещения, повороты головы, частичное перекрытие лица).
- Требовался дополнительный этап детекции глаз в реальном времени.

### Итоговый подход
- Классификация состояния глаз выполняется по **кропу лица целиком**.
- Используется архитектура **MobileNetV2** с предобученными весами ImageNet.
- Классификационная голова дообучена для бинарной классификации:
  - `0` — глаза открыты  
  - `1` — глаза закрыты
- Заморозка базовых слоёв MobileNetV2 предотвращает переобучение и фокусирует обучение на задаче распознавания состояния глаз.

---

## Детекция лица и видеопайплайн
- Для выделения области лица используется **DNN-детектор OpenCV (SSD + ResNet)**.
- Один и тот же детектор применяется на этапе подготовки данных и в реальном видеопотоке.
- Обеспечивается согласованность входных данных и стабильность работы системы.

---

## Используемый инструментарий
- **TensorFlow / Keras** — построение и обучение модели.  
- **OpenCV** — обработка видеопотока, детекция лиц, визуализация.  
- **Roboflow Drowsiness Detection Dataset** — основная база для обучения и валидации.  
- **Keras Callbacks** (EarlyStopping, ModelCheckpoint) — контроль обучения.  
- **Class weights** — балансировка классов.  

---

## Основные выводы
- Модель стабильно классифицирует состояние глаз по изображению лица.  
- Архитектура обеспечивает баланс между точностью распознавания и вычислительной эффективностью.  
- Временная агрегация предсказаний помогает различать кратковременные моргания и признаки сонливости.  
- Отказ от детекции глаз в реальном времени оправдан из-за нестабильности предыдущего подхода.

---

## Заключение
Данный проект создает основу для разработки систем мониторинга водителя.  
Прототип позволяет интегрировать методы компьютерного зрения и глубокого обучения в реальные системы обеспечения безопасности дорожного движения.
