# Мета-репо для движения "создай своего бота"

## Боты для чата подкаста Радио-Т

- Каждый бот представляет из себя полностью законченный микросервис с единой точкой входа `/event`
- `/event` вызывается для любого сообщения через `POST` с телом `{text: сообщение, username: id пользователя, display_name: имя пользователя}` (json)
- Бот может на это реагировать 2мя способами:
 - вернуть 417 (Expectation Failed) если ему нечего сказать на сообщение
 - вернуть 201 и body `{text: сообщение, bot: имя/id бота}` (json). Техт может быть markdown. EOL должны быть представлены как строки `\n`
- Бот оформляется как контейнер с прилагаемым docker-compose.yml, для запуска которого должно хватить `git clone ... && docker-compose up -d`
- Бот (внутри контейнера) слушает на порту `8080`
- Бот может вызывать внешние сервисы, если есть такая необходимость.
- Нежелательно тянуть за собой внешние зависимости, типа баз данных, редисов и прочего.
- На запрос бот должен ответить за какое-то фиксированное время. Предлагаемый максимум 5 сек.
- Бот не получит след. сообщения пока не ответит на предыдущее.
- Бот можно писать на всем, чем хотите/умеете. Однако, результат должен быть разумен по размеру контейнера и используемым ресурсам.

### Идеи для полезных и забавных ботов
- ведение псевдо-разумной дискусси по варианту сири/алкесы/гугла
- ответы над узкие вопросы, типа "какая погода в Москве сегодня"
- функции поиска по подкасту (шоунотам и логам)
- все остальное, что можете придумать

### Зачем вам это надо?
- для развлечения
- для добавления в чат чего-то полезного
- для славы и почета :) Мы расскажем о каждом вашем боте который будет принят и поощрим авторов, как минимум добрым словом.

### Как в этом поучаствовать?
- посмотреть на то, что сделали другие
- почитать [что пишут](https://radio-t.com/p/2016/11/06/bot/)
- сделать PR со своим ботом в отдельном каталоге. Это хозяйство должно собираться и подниматься локально, через compose build + up
- в этом PR не забыть изменить рутовые `nginx.conf` и `docker-compose.yml` для вашего бота
