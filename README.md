# Спецификация протокола SSP

*Версия 1.2.4*

## Определения

*SSP (SimpleSmokeProtocol)* - простой протокол установления соглашения для
совместного похода до мест разрешенных для курения.

*Вызывающая сторона* - субъект инициирующий запрос

*Вызываемая сторона* - субъект принимающий запрос

## Описание команд протокола

`?` - запрос, инициирующий протокол. Соответствует фразе «Пойдем курить?»

`?X` - запрос, инициирующий протокол идти курить, но с отсрочкой на X минут. Соответствует фразе «Пойдем курить через X минут?» 

`!` - ответ на запрос инициирующий запрос, подразумевающий ответное желание идти
курить. Соответствует фразе «Да, пошли»

`+` - ответ на запрос инициирующий запрос, подразумевающий ответное желание идти
курить. Соответствует фразе «Да, пошли». Синоним предыдущего ответа.

`#` - ответ на запрос инициирующий запрос, подразумевающий отказ от похода курить.
Соответствует фразе «Нет, не хочу»

`#X` - ответ на запрос инициирующий запрос, подразумевающий отказ от похода курить.
Соответствует фразе «Нет, не хочу, X минут назад курил».
В случае, если точное время определить не представляется возможным, следует использовать 
знак `~` («тильда»), подразумевающий неопределённое, но небольшое (до 45 минут) время. 
В случае бо́льшего времени, возможно, следует использовать простой негативный 
ответ - `#` либо отвечать позитивным ответом - `!`.

`@X` - ответ на запрос инициирующий запрос, подразумевающий ответное желание
идти курить но с отсрочкой на X минут. В случае, если точное время определить 
не представляется возможным, следует использовать знак `~` («тильда»), подразумевающий 
неопределённое, но небольшое (до 15 минут) время. В случае бо́льшего
времени, следует использовать негативный ответ - `#`. Соответствует фразе «Пошли,
но через X минут.»

`>` - синхронизирующая команда, обозначающая начало исполнения протокола вызывающей стороной. Соответствует фразе «Выхожу!».

`>>` - синхронизирующая команда, обозначающая начало исполнения протокола вызываемой стороной. Соответствует фразе «Я тоже выхожу».

## Пример использования протокола

X - вызывающий
Y - вызываемый

### Пример 1

    X: ? («Пойдем курить?»)
    Y: ! («Да, пошли»)
    X: > («Выхожу!»)
    Y: >> («Я тоже выхожу.»)

### Пример 1.2

    X: ? («Пойдем курить?»)
    Y: + («Да, пошли»)
    X: > («Выхожу!»)
    Y: >> («Я тоже выхожу.»)

### Пример 2

    X: ? («Пойдем курить?»)
    Y: @5 («Пошли, но через 5 минут.»)
    Y: ! («Да, пошли»)
    X: > («Выхожу!»)
    Y: >> («Я тоже выхожу.»)

### Пример 3

    X: ? («Пойдем курить?»)
    Y: # («Нет, не хочу»)

### Пример 4

    X: ? («Пойдем курить?»)
    Y: #20 («Нет, не хочу, 20 минут назад курил»)

### Пример 5

    X: ? («Пойдем курить?»)
    Y: #~ («Нет, не хочу, только что курил»)

### Пример 6

    X: ?10 («Пойдем курить через 10 минут?»)
    Y: #2 («Нет, не хочу, 2 минуты назад курил»)
	
