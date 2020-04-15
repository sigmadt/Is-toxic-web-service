# Is the text toxic?

# **Introduction**

Данный сервис создан с целью определения токсичности того или иного высказывания (комментария). <br>
Данные для его создания были взяты с соревнования на kaggle.com "Jigsaw Unintended Bias in Toxicity Classification". <br>
Сервис способен принимать POST запрос со строкой в формате Json и возвращать 'Toxic' или 'Ok' также в формате Json. <br>

Для обработки слов (перевод в числовые значения) в строке я использовал статистику Tf-idf. Обученный на данных вокабуляр находится в файле "vectorize.pkl". <br>
Далее я обучил логистическую регрессию (auc_score ~0.9) и сохранил классификатор в файл "log_reg_model.pkl". Код с обработкой данных и обучением модели находится в файле "log_reg_model.py".

Ниже представлена интсрукция по запуску веб-сервиса. Для запуска сервиса на вашем компьютере вам нужен только Docker, все нужные файлы он установит самостоятельно.

# **Libraries**

Для создания данного веб-сервиса я использовал следующие Python библиотек: <br>
_ML_: pandas, numpy, scikit-learn. _Web_: Flask

# **Step 1**

Клонируем себе репозиторий.
Открываем docker, заходим в папку python_web_service_with_model: <br>

Запускаем команду в терминале: <br>
`$ docker-compose up --build`

Построили и открыли контейнер. Должен был образоваться локальный хост: http://localhost:5000/

Далее работаем с моим веб-сервисом.

# **Step 2**

В файле "service.py" находится функция, которая способна принимать POST запрос с Json (комментарием) и возвращать 'Toxic' или 'Ok' 
также в формате Json.

Есть два способа отправить данный POST запрос:
1. Используя curl
 
Для этого в терминале нужно вбить следующее: <br>
`curl --header "Content-Type: application/json" \
  --request POST \
  --data '{'Comment': 'comment text'}' \
  http://localhost:5000/is_toxic`
  
Здесь data - данные, которые мы хотим, чтобы наш сервис обработал.
На выходе мы получим токсичен комментарий или нет.

2. С помощью Postman

В этой программе нужно сделать POST запрос через адрес http://localhost:5000/is_toxic.
В `Headers` в `Key` добавить `Content-Type`, а в `Value` - `application/json`. Далее в `Body` нужно поставить галочку возле `raw`, 
в поле ниже вбить текст в формате JSON. <br>
Пример ниже:

![Alt text](//https://yadi.sk/d/62KEBt5xRGF5EQ/postman_example.png "Postman example")

