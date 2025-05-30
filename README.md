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
      "platform": "all", // ios, android, web
      "versions": [
        {
          "version": "all", // all, номер версии
          "color": "#F3463B",
          "messageColor": "#FFFFFF",
          "icon": "https://status.ohmywishes.com/images/warning.svg",
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
      "platform": "android", // ios, android, web
      "versions": [
        {
          "version": "all", // all, номер версии
          "color": "#F3463B",
          "messageColor": "#FFFFFF",
          "icon": "https://status.ohmywishes.com/images/success.svg",
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
      "platform": "ios", // ios, android, web
      "versions": [
        {
          "version": "all", // all, номер версии
          "color": "#F3463B",
          "messageColor": "#FFFFFF",
          "icon": "https://status.ohmywishes.com/images/error.svg",
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
    },
    {
      "platform": "ios", // ios, android, web
      "versions": [
        {
          "version": ">1.5.0", // all, номер версии, не ниже определенной версии
          "color": "#F3463B",
          "messageColor": "#FFFFFF",
          "icon": "https://status.ohmywishes.com/images/error.svg",
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
    * `platforms.versions.version` – описание в разделе ниже
    * `platforms.versions.color` – цвет фона панели с уведомлением
    * `platforms.versions.messageColor` – цвет текста, который отображается на панели уведомления
    * `platforms.versions.icon` – иконка для панели уведомления, доступные варианты на текущий момент:
      * `https://status.ohmywishes.com/images/error.svg` – всё совсем плохо
      * `https://status.ohmywishes.com/images/warning.svg` – что-то может не работать
      * `https://status.ohmywishes.com/images/success.svg` – всё хорошо или что-то было решено и снова работает штатно
    * `platforms.versions.message` – список текстов сообщений на разных языках

#### Синтаксис поля version

Поле может содержать следующие значения:
* `all` – любые версии. Для платформы `web` возможно только это значение
* `(модификатор)(номер версии)` – модификатор указывать необязательно. Возможные варианты модификатора:
  * `<` – для всех версий ниже указанной
  * `<=` – для всех версий ниже указанной, а так же для указанной версии
  * `>` – для всех версий выше указанной
  * `>=` – для всех версий выше указанной, а так же для указанной версии

Примеры значений:
* `1.0.10` – только для версии `1.0.10`
* `<1.0.10` – для версий `1.0.9, 1.0.8, ...`
* `<=1.0.10` – для версий `1.0.10, 1.0.9, 1.0.8, ...`
* `>1.0.10` – для версий `1.0.11, ..., 1.1.0, ...`
* `>=1.0.10` – для версий `1.0.10, 1.0.11, ..., 1.1.0, ...`