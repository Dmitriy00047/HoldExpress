﻿# HoldExpress

#API
--Получение данных пользователя
GET /api/user
    request: {
        headers: {
            token
        }
    }

    response: {
        body: {
            name,
            record
        }
    }

--Добавление пользователя
POST /api/user
    request: {
        body: {
            uuid - ид устройства
        }
    }

    response: {
        token
    }

--Удаление пользователя
DELETE /api/user
    request: {
        headers: {
            token
        }
    }

    response: {}

--Сохранить выбранные настройки пользователя
PUT /api/settings
    request: {
        headers: {
            token
        },
        //Отправляешь что изменилось
        body: {
            sound - включен ли звук.Допустимые значения true или false
            vibrate - включена ли вибрация.Допустимые значения true или false
            name - имя пользователя
        }
    }

    response: {}

--Получить настройки пользователя
GET /api/settings
    request: {
        headers: {
            token
        }
    }
    //возвращаю что есть
    response: {
        body: {
            sound, - включен ли звук.Допустимые значения true или false
            vibrate, - включена ли вибрация.Допустимые значения true или false
            name - имя пользователя
        }
    }

--Получение результатов пользователя по принципу результаты до и после меня
GET /api/rating
    request: {
        headers: {
            token - сформированный токен, по которому будет происходить авторизация
        },
        body: {
            *не обязательно можно пустое тело: по-умолчанию буду присылать 4:4
            worse_count - кол - во результатов хуже, чем лучший у пользователя
            better_count - кол - во результатов лучше, чем лучший у пользователя
        }
    }

    response: {
        body: {
            worse[] - сформированный массив результатов.Каждый элемент массива - пара[имя пользователя, лучший результат]
            better[] - сформированный массив результатов.Каждый элемент массива - пара[имя пользователя, лучший результат]
        }
    }

--Добавление результата пользователя в копилку его результатов и если результат больше рекорда, то обновить рекорд
POST /api/results
    request: {
        headers: {
            token - сформированный токен, по которому будет происходить авторизация
        },
        body: {
            result: - результат пользователя
        }
    }

    response: {}

--Получение всех попыток пользователя.Служебная инфа для отладки, + покажет активность.
GET /api/results
    request: {
        headers: {
            token - сформированный токен, по которому будет происходить авторизация
        }
    }

    response: {
        body: {
            results[] - все результаты пользователя, массив чисел
        }
    }