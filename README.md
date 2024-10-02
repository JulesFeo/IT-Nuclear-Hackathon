# Решение задачи от МТС Линк: "Использование ИИ в продукте" в рамках хакатона Nuclear IT Hack 2024
***Название команды: хихиteam***\
***Состав команды: Стародуб Анастасия Ивановна, Феофилактова Юлия Сергеевна, Майорова Анна Вячеславовна***\ 
## Описание проекта 
Данный проект выполняет следующие задачи:
1. **Предобработка текста:** включает очистку предложений от пунктуации и лишних символов, а также лемматизацию (приведение слов к их начальной форме) с использованием библиотеки pymorphy2.
2. **Кластеризация текста:** предложения из CSV-файла преобразуются в эмбеддинги с использованием модели Sentence Transformers, а затем кластеризуются с помощью метода KMeans.
3. **Визуализация результатов:** для каждого кластера создаются облака слов на основе наиболее часто встречающихся существительных, а также гистограммы частот этих слов.
## Установка и запуск
### Шаг 1: Установка зависимостей
Для корректной работы скрипта требуется установить следующие библиотеки Python. Выполните команду:
```
pip install nltk pymorphy2 scikit-learn sentence-transformers matplotlib numpy wordcloud
```
### Шаг 2: Загрузка ресурсов NLTK
В скрипте используется библиотека nltk для токенизации текста и получения стоп-слов. Перед запуском скрипта необходимо загрузить ресурсы NLTK:
```
import nltk
nltk.download('punkt')
nltk.download('stopwords')
```
### Шаг 3: Подготовка CSV-файла
Необходимо подготовить CSV-файл с текстовыми данными для анализа. В файле должен быть хотя бы один столбец с текстовыми предложениями, который будет обрабатываться. Убедитесь, что файл имеет корректную кодировку, например, UTF-8.

### Шаг 4: Запуск скрипта
Укажите путь к вашему CSV-файлу в переменной csv_file_path.
Запустите скрипт.\
Пример запуска:
```
csv_file_path = 'input.csv'
processed_sentences = process_csv(csv_file_path)
cluster_sentences_kmeans(processed_sentences, n_clusters=4)
```
Скрипт выполнит следующие действия:
- Прочитает CSV-файл.
- Очистит и лемматизирует текстовые данные.
- Создаст эмбеддинги предложений с помощью модели Sentence Transformers.
- Проведет кластеризацию методом KMeans на основе эмбеддингов.
- Визуализирует облака слов и гистограммы для каждого кластера.
## Основные функции
`clean_text(text)`   
Очищает текст от цифр, пунктуации и лишних символов. Приводит текст к нижнему регистру.   
   
`lemmatize(sentence)`   
Токенизирует текст и приводит каждое слово к его начальной форме (лемме) с использованием библиотеки pymorphy2. Стоп-слова исключаются из результата.  
   
`process_csv(file_path)`   
Читает CSV-файл и лемматизирует каждую строку текста.   
   
`get_sentence_embeddings(sentences)`   
Получает эмбеддинги предложений с помощью модели paraphrase-multilingual-MiniLM-L12-v2 из библиотеки Sentence Transformers.   
   
`cluster_sentences_kmeans(sentences, n_clusters)`   
Проводит кластеризацию методом KMeans на основе эмбеддингов предложений и выводит визуализацию кластеров (облака слов и гистограммы).
   
`extract_nouns(sentences)`   
Извлекает существительные из предложений для использования в облаках слов и гистограммах.   
   
`generate_wordclouds_and_histograms(sentences, labels)`   
Создает облака слов и гистограммы частот слов для каждого кластера.   
   
>[!NOTE]
>Вы можете вручную изменить количество кластеров, передавая нужное значение в функцию cluster_sentences_kmeans. Например, для 4 кластеров используется:   
> ```
>cluster_sentences_kmeans(processed_sentences, n_clusters=4)
> ```
    
Убедитесь, что в тексте нет пустых строк, так как это может вызвать ошибки при обработке данных.
