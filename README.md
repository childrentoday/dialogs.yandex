# Начало работы с Яндекс диалогом 

## Переходим в Панель разработчика
https://dialogs.yandex.ru/developer/



```php

<?php
    $data = file_get_contents('php://input'); //Получаем тело в виде json
    header('Content-Type: application/json');
    $data = json_decode($data, true); //Раскодируем json файл


    $text = $data['request']['command'];
    
    //Проверяем нужные поля
    if (!isset($data['request'], $data['session'])) {
        //Возвращаем ничего, т.к. нам не пришло необходимых полей


        exit(json_encode([]));
    }


    else {
        //В данном тестовом примере нам не нужен текст запроса и т.д.
        //Однако текст запроса можно найти в $data['request']['command']

        $response = json_encode([
            'version' => '1.0',
            'session' => [
                'session_id' => $data['session']['session_id'],
                'message_id' => $data['session']['message_id'],
                'user_id' => $data['session']['user_id']
            ],
            'response' => [
                'text' => 'Расписание уроков '.$text,
                //Ставим плюсики перед теми гласными, на которые ударение
                'tts' => 'В школе на сегодня нет занятий ',
                'buttons' => [
                    [
                    'title' => '2 Б',
                    'hide' => true
                 ],
                   [
                   'title' => '3 Б',
                   'hide' => true
                   ]
                ]


            ]
        ]);


        exit($response);
    }

```
