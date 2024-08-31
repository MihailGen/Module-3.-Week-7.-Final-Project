# Module-3.-Week-7.-Final-Project
```sql
-- Creating tables Artists, Albums, Songs, Users, Playlists, PlaylistSongs, Favorites
CREATE TABLE Artists (
    ID INTEGER PRIMARY KEY,
    Name TEXT NOT NULL
);

CREATE TABLE Albums (
    ID INTEGER PRIMARY KEY,
    Title TEXT NOT NULL,
    ReleaseDate DATE,
    ArtistID INTEGER,
    FOREIGN KEY (ArtistID) REFERENCES Artists(ID)
);

CREATE TABLE Songs (
    ID INTEGER PRIMARY KEY,
    Title TEXT NOT NULL,
    AlbumID INTEGER,
    ArtistID INTEGER,
    Duration INTEGER,
    FOREIGN KEY (AlbumID) REFERENCES Albums(ID),
    FOREIGN KEY (ArtistID) REFERENCES Artists(ID)
);

CREATE TABLE Users (
    ID INTEGER PRIMARY KEY,
    Username TEXT NOT NULL,
    Password TEXT NOT NULL,
    Email TEXT NOT NULL
);

CREATE TABLE Playlists (
    ID INTEGER PRIMARY KEY,
    Name TEXT NOT NULL,
    UserID INTEGER,
    FOREIGN KEY (UserID) REFERENCES Users(ID)
);

CREATE TABLE PlaylistSongs (
    PlaylistID INTEGER,
    SongID INTEGER,
    PRIMARY KEY (PlaylistID, SongID),
    FOREIGN KEY (PlaylistID) REFERENCES Playlists(ID),
    FOREIGN KEY (SongID) REFERENCES Songs(ID)
);

CREATE TABLE Favorites (
    UserID INTEGER,
    SongID INTEGER,
    AlbumID INTEGER,
    PRIMARY KEY (UserID, SongID, AlbumID),
    FOREIGN KEY (UserID) REFERENCES Users(ID),
    FOREIGN KEY (SongID) REFERENCES Songs(ID),
    FOREIGN KEY (AlbumID) REFERENCES Albums(ID)
);


-- 1. Creating tables Subscriptions and implementation of functionality for subscriptions to performers
CREATE TABLE Subscriptions (
    UserID INTEGER,
    ArtistID INTEGER,
    PRIMARY KEY (UserID, ArtistID),
    FOREIGN KEY (UserID) REFERENCES Users(ID),
    FOREIGN KEY (ArtistID) REFERENCES Artists(ID)
);

-- Filling out the "Artists" table
INSERT INTO Artists (ID, name) VALUES 
(1, 'Григорий Лепс'),
(2, 'Шаман'),
(3, 'Филипп Киркоров'),
(4, 'Николай Басков'),
(5, 'Полина Гагарина');

-- Filling out the "Albums" table
INSERT INTO Albums (ID, Title, ReleaseDate, ArtistID) VALUES 
(1, 'Завтра', '2023-07-07', 1),
(2, 'Сделано в России', '2023-09-08', 2),
(3, 'Романы, Часть 1', '2020-01-01', 3),
(4, 'Романы, Часть 2', '2020-04-30', 3),
(5, 'За тебя', '2020-05-21', 4),
(6, 'Солнце взойдёт', '2023-04-28', 5);


-- Filling out the "Songs" table
INSERT INTO Songs (ID, Title, AlbumID, ArtistID, duration) VALUES 
-- Григорий Лепс "Завтра"
(1, 'Завтра', 1, 1, 210),
(2, 'Мне не нужна', 1, 1, 342),
(3, 'Параноик', 1, 1, 211),
(4, 'Бейби', 1, 1, 248),
(5, 'Я буду с тобой', 1, 1, 197),
(6, 'Московские пробки', 1, 1, 152),
(7, 'Пока', 1, 1, 183),
(8, 'Я не узнал бы о любви', 1, 1, 186),
(9, 'Весна', 1, 1, 195),
(10, 'Один на один', 1, 1, 269),
(11, 'Зпасной аэродром', 1, 1, 259),
(12, 'Я оставляю', 1, 1, 235),
(13, 'Да', 1, 1, 247),
(14, 'Предатель', 1, 1, 221),
(15, 'Падший ангел', 1, 1, 287),
(16, 'Музыка в сердце', 1, 1, 238),
(17, 'Всё, что было важно', 1, 1, 259),

-- Шаман "Сделано в России"
(18, 'Моя Россия', 2, 2, 156),
(19, 'Дай жару', 2, 2, 231),
(20, 'Да', 2, 2, 210),
(21, 'Мы', 2, 2, 192),
(22, 'Самый русский хит', 2, 2, 201),
(23, 'Исповедь', 2, 2, 155),
(24, 'Мой бой', 2, 2, 145),
(25, 'Встанем', 2, 2, 244),
(26, 'Я русский', 2, 2, 211),
(27, 'Гимн России', 2, 2, 210),
(28, 'За тобой', 2, 2, 195),
(29, 'Теряем мы любовь', 2, 2, 185),
(30, 'Улетай', 2, 2, 131),
(31, 'До самого неба', 2, 2, 180),
(32, 'Грешная любовь', 2, 2, 215),
(33, 'Ты моя', 2, 2, 204),
(34, 'Родная', 2, 2, 202),
(35, 'Мёд', 2, 2, 235),
(36, 'Сердце плачет и болит', 2, 2, 195),
(37, 'Спасибо', 2, 2, 276),

-- Филипп Киркоров "Романы. Часть 1"
(38, 'Романы', 3, 3, 244),
(39, 'Это была любовь', 3, 3, 231),
(40, 'Любимые люди', 3, 3, 200),
(41, 'Улети', 3, 3, 231),
(42, 'Гореть на ветру', 3, 3, 257),
(43, 'Позволь', 3, 3, 249),
(44, 'Скажи любовь', 3, 3, 245),
(45, 'Молодой ангел', 3, 3, 273),
(46, 'Ты прости мне', 3, 3, 206),
(47, 'Сладкая да горькая', 3, 3, 235),
(48, 'Прости', 3, 3, 213),
(49, 'Ты у меня в крови', 3, 3, 233),
(50, 'Ты не веришь', 3, 3, 199),
(51, 'Я найду тебя', 3, 3, 192),
(52, 'Я тебя выдумал', 3, 3, 222),
(53, 'Не верю я', 3, 3, 233),

-- Филипп Киркоров "Романы. Часть 2"
(54, 'Цвет настроения синий', 4, 3, 202),
(55, 'Ты', 4, 3, 238),
(56, 'Никогда', 4, 3, 227),
(57, 'За горизонты', 4, 3, 211),
(58, 'Нет любви на расстоянии', 4, 3, 232),
(59, 'Народная артистка', 4, 3, 289),
(60, 'Сердце львицы', 4, 3, 231),
(61, 'Переплачем-перетерпим', 4, 3, 249),
(62, 'Верить', 4, 3, 222),
(63, 'Вокруг тебя', 4, 3, 192),
(64, 'Химера', 4, 3, 194),
(65, 'Не кричи', 4, 3, 188),
(66, 'Каждый день с тобой', 4, 3, 235),
(67, 'Я больше не буду петь о нас', 4, 3, 248),
(68, 'Сквозняки', 4, 3, 229),
(69, 'Незнакомка', 4, 3, 195),
(70, 'Как золото', 4, 3, 216),
(71, 'Включаем радость', 4, 3, 194),
(72, 'Ещё, ещё', 4, 3, 253),
(73, 'Главное верить!', 4, 3, 201),

-- Николай Басков "За тебя!"
(74, 'Давай дружить', 5, 4, 223),
(75, 'День рождения', 5, 4, 213),
(76, 'Жить красиво', 5, 4, 223),
(77, 'Принц на белом коне', 5, 4, 245),
(78, 'Всё сбудется', 5, 4, 191),
(79, 'Несравненная', 5, 4, 227),
(80, 'Небо на двоих', 5, 4, 258),
(81, 'За тебя', 5, 4, 218),
(82, 'Улыбка', 5, 4, 212),
(83, 'На берегу моей любви', 5, 4, 215),
(84, 'Судьба морская', 5, 4, 198),
(85, 'Шарманка', 5, 4, 258),

-- Полина Гагарина "Вдох"
(86, 'Бабочки', 6, 5, 188),
(87, 'Вдох', 6, 5, 179),
(88, 'Тени', 6, 5, 216),
(89, 'Плакали', 6, 5, 190),
(90, 'Вода', 6, 5, 186),
(91, 'Не мое кино', 6, 5, 206),
(92, 'Безотносительно', 6, 5, 213),
(93, 'Последний ноябрь', 6, 5, 171),
(94, 'Мировой океан', 6, 5, 209);

-- SQL query to add a user
INSERT INTO Users (ID, username, password, email) VALUES (1, 'Михаил', '1', 'genziks@inbox.lv');

-- SQL query to add a user's subscription to an artist
INSERT INTO Subscriptions (UserID, ArtistID) VALUES (1, 1);

-- SQL query to delete a user's subscription to an artist
DELETE FROM Subscriptions WHERE UserID = 1 AND ArtistID = 1;


-- SQL query to get a list of subscriptions for a specific user
SELECT Artists.Name
FROM Subscriptions
JOIN Artists ON Subscriptions.ArtistID = Artists.ID
WHERE Subscriptions.UserID = 1;


-- 2. Creating the SongRecommendations table and implementing song recommendation functionality
CREATE TABLE SongRecommendations (
    UserID INTEGER,
    SongID INTEGER,
    PRIMARY KEY (UserID, SongID),
    FOREIGN KEY (UserID) REFERENCES Users(ID),
    FOREIGN KEY (SongID) REFERENCES Songs(ID)
);


-- SQL-query to add song recommendation for user
INSERT INTO SongRecommendations (UserID, SongID) VALUES (1, 1);

-- SQL-query to get a list of recommended songs for a specific user
SELECT Songs.Title, Songs.Duration
FROM SongRecommendations
JOIN Songs ON SongRecommendations.SongID = Songs.ID
WHERE SongRecommendations.UserID = 1;


-- 3. Adding a Rating field to the Songs table and implementing a ratings system

-- Creating a temporary table with the Rating field
CREATE TABLE TempSongs AS
SELECT *, 0.0 AS Rating FROM Songs;
ALTER TABLE TempSongs ADD PRIMARY KEY (id);
ALTER TABLE TempSongs ADD FOREIGN KEY (AlbumID) REFERENCES Albums(ID);
ALTER TABLE TempSongs ADD FOREIGN KEY (ArtistID) REFERENCES Artists(ID);

-- Deleting the current Songs table
DROP TABLE Songs;

-- Renaming the temporary table in Songs
ALTER TABLE TempSongs RENAME TO Songs;


-- Creating a SongReviews table to store user ratings of songs
CREATE TABLE IF NOT EXISTS SongReviews (
    UserID INTEGER,
    SongID INTEGER,
    Rating FLOAT,
    PRIMARY KEY (UserID, SongID),
    FOREIGN KEY (UserID) REFERENCES Users(ID),
    FOREIGN KEY (SongID) REFERENCES Songs(ID)
);

-- SQL-query to add a user rating for a song
INSERT INTO SongReviews (UserID, SongID, Rating) VALUES (1, 1, 4.5);


-- SQL-query to calculate the average song rating and update the Rating field
SET Rating = (SELECT AVG(Rating) FROM SongReviews WHERE SongID = 1)
WHERE ID = 1;


SELECT AVG(Rating) FROM SongReviews WHERE SongID = 1;

```
