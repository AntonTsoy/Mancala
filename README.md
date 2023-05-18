# Mancala-2023
  Репозиторий для учебного проекта. Реализация игры Mancala с помощью Logisim и академической версии языка Ассемблера. Создатели: 
  Ветров Вясеслав, Козолий Михаил, Цой Антон

## Разделение на руководителей:
- Цой Антон - CDM-8/Логика
- Козолий Михаил - Logisim/Интерфейс
- Ветров Вячеслав - Документация/Защита

## Правила игры:
- Первоначально от 4 до 8 камней помещаются в каждую лунку. Всего получается 48 - 96. Игроки по очереди делают ход. 
- Ход состоит в том, чтобы взять все камни из одной из непустых лунок, принадлежащих игроку, и разбросать их против часовой стрелки. 
Один камень опускается в каждую лунку или манкалу игрока по пути, но при этом манкала противника обходится стороной.
- [Правило захвата/Capture rule] Если последний камень падает в собственную пустую лунку, а противоположная лунка не пуста, то этот камень
и все камни из противоположной лунки захватываются и переносятся в манкалу игрока.
- [Правило повтора/Repeat rule] Если последний камень в конце хода падает в манкалу игрока, игрок делает еще один ход. Игра останавливается,
если у одного из игроков нет семян/он не может сделать ход. Если в их манкалах семян поровну, то это ничья, больше - победа, меньше - поражение.

## Роли ячеек RAM памяти:
##### 0x00: выбор пользователя начального кол-ва камней
##### 0x01-0x07: лунки пользователя
##### 0x08: выбор пользователя, кто будет ходить первым
##### 0x09-0x0F: лунки ИИ

##### 0x10: предикат инициализации памяти 
##### 0x11: номер банка памяти 
##### 0x12: ячейка для спец. сообщений (Error, Computing, Waiting user и т.д)
##### 0x13: значение (1 или 2) - чья-очередь хода 
##### 0x14: номер лунки, которую выбрал AI
##### 0x15: номер лунки, которую выбрал пользователь
##### 0x16: предикат пустоты лунок AI
##### 0x17: предикат пустоты лунок пользователя
### *далее идут ячейки для временных вычислений Deep Purple:
##### 0x19: предикат того, должно ли хотя бы на одной лунке работать правило Capture
##### 0x1A: предикат того, нужно ли ходить сейчас из лунки для срабатывания Repeat
##### 0x1B: текущее максимальное значение, на которое может увеличено число в манкале
##### 0x1C: номер лунки, из которой было получено текущее максимальное значение
##### 0x1D: текущее увеличение в манкале 


## Подробное описание ячейки 0x12 по битам:
#### 0b0000.0000
#### 0 - Error!
#### 1 - Clear button register
#### 2 - Please, choose settings
#### 3 - Wait user move
#### 4 - Deep Purple deciding...
#### 5 - Making move
#### 6 - Game over!
#### 7 - *пока не используется
