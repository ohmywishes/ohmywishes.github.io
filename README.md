## Спецификация файлика "status.json"

Для обновления структуры файла его необходимо: 
* обновить в `./api/status.json`
* запушить изменения в github

После этих действий в github запустится процесс публикации изменений.
В течение минуты обновлённая версия файла появится по адресу https://status.ohmywishes.com/api/status.json

### Описание структуры файла

Рядом сполем, где возможно ограниченное кол-во значений после 
`//` указан список возможных вариантов.

```json5
{
  "isEnabled": true, // true, false
  "platforms": [
    {
      "name": "all", // ios, android, web
      "versions": [
        {
          "name": "all", // all, номер версии
          "color": "#F3463B",
          "messageColor": "#FFFFFF",
          "icon": "https://static.ohmywishes.com/status/warning.svg",
          "message": [
            { 
              "lang": "default", // default, ISO 639-1 код языка (2 символа в нижнем регистре)
              "text": "Нам очень жаль, но сервис временно недоступен. Мы уже работаем над решением проблемы и скоро всё исправим!" },
            { 
              "lang": "ru", // default, ISO 639-1 код языка (2 символа в нижнем регистре)
              "text": "Нам очень жаль, но сервис временно недоступен. Мы уже работаем над решением проблемы и скоро всё исправим!"
            }
          ]
        }
      ]
    },
    {
      "name": "android", // ios, android, web
      "versions": [
        {
          "name": "all", // all, номер версии
          "color": "#F3463B",
          "messageColor": "#FFFFFF",
          "icon": "https://static.ohmywishes.com/status/success.svg",
          "message": [
            { 
              "lang": "default", 
              "text": "Нам очень жаль, но сервис временно недоступен. Мы уже работаем над решением проблемы и скоро всё исправим!"
            }
          ]
        }
      ]
    },
    {
      "name": "ios", // ios, android, web
      "versions": [
        {
          "name": "all", // all, номер версии
          "color": "#F3463B",
          "messageColor": "#FFFFFF",
          "icon": "https://static.ohmywishes.com/status/error.svg",
          "message": [
            {  
              "lang": "default", 
              "text": "We're really sorry, but the service is temporarily unavailable. We're already working on a fix and will be back soon!"
            },
            { 
              "lang": "en", 
              "text": "We're really sorry, but the service is temporarily unavailable. We're already working on a fix and will be back soon!"
            }
          ]
        }
      ]
    }
  ]
}

```

### Описание полей файла

* `isEnabled` – показывать или нет сообщение в приложениях (ios, android, web). Если `false`, остальная структура файла игнорируется
* `platforms` – список платформ, на которых нужно показать сообщение
  * `platforms.versions` – список версий приложения на конкретной платформе, на которых показать сообщение
    * `platforms.versions.name` – для `web` возможно только `all`, для остальных может содержать номер версии
    * `platforms.versions.color` – цвет фона панели с уведомлением
    * `platforms.versions.messageColor` – цвет текста, который отображается на панели уведомления
    * `platforms.versions.icon` – иконка для панели уведомления, доступные варианты на текущий момент:
      * `https://static.ohmywishes.com/status/error.svg` – всё совсем плохо
      * `https://static.ohmywishes.com/status/warning.svg` – что-то может не работать
      * `https://static.ohmywishes.com/status/success.svg` – всё хорошо или что-то было решено и снова работает штатно
    * `platforms.versions.message` – список текстов сообщений на разных языках