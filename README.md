# !Ссылка на задание 2: https://drive.google.com/file/d/1JEJdcb7YJF1UsPOyq30Ha8y8ZKYAuX8T/view?usp=sharing


# Разделение монолитного фронтенда на микрофронтенды

## Выбор технологии

Я выбирал между Single SPA и Module Federation, потому что остальные способы не особо популярны и не являются в полном смысле этого слова микрофронтендами (например, [Yarn Worskpaces](https://yarnpkg.com/features/workspaces))

Поскольку я не был знаком ни с одной из технологий (я работаю бэкенд-разработчиком), то сначала решил попробовать обе. На этапе настройки Single SPA сразу возникли проблемы. Документация показалось недостаточно понятной, так что я решил воспользоваться примером https://github.com/microsoft/micro-frontend-react. Во время выполнения [туториала](https://www.youtube.com/watch?v=vjjcuIxqIzY&list=PLLUD8RtHvsAOhtHnyGx57EYXoaNsxGrTU&index=5&ab_channel=JoelDenning), в котором было показано, как в режиме разработчика подменить путь до микрофронендов прямо в браузере, кнопка, которую должен быть добавить тег **import-map-overrides-full**, не появилась. Не помогало убрать show-when-local-storage, localStorage.setItem('devtools', true), или сменить браузер. На этом я решил закончить изучение Single SPA.

С другой стороны, [туториал](https://www.youtube.com/watch?v=s_Fs4AXsTnA) для Module Federation сработал отлично, и мне даже удалось настроить встраивание микрофронтенда на solid-js в host на React (достаточно было предварительно его отрендерить). На этом этапе я решил, что Module Federation подоходит для использования.

## Планирование изменений

- Сначала я решил создать host, полностью дублирующий монолитный фронтенд, но при этом использующий webpack и позволяющий подключить к нему микрофронтенды
- После этого я решил выделять микрофронтенды по одному: auth - для авторизации, photos - для просмотра/загрузки фотографий и лайков, profile - для редактирования и отображения профиля

Компоненты, которые должны быть в auth:
- [Login](frontend/src/components/Login.js)
- [InfoTooltip](frontend/src/components/InfoTooltip.js)
- [Register](frontend/src/components/Register.js)
- [InfoTooltip](frontend/src/components/InfoTooltip.js)
Компоненты, которые должны быть в photos:
- [Card](frontend/src/components/Card.js)
- [PopupWithForm](frontend/src/components/PopupWithForm.js)
- [ImagePopup](frontend/src/components/ImagePopup.js)
В profile:
- [ImagePopup](frontend/src/components/ImagePopup.js)
- [EditAvatarPopup](frontend/src/components/EditAvatarPopup.js)
- [EditProfilePopup](frontend/src/components/EditProfilePopup.js)

Я наметил, какие функции api нужны каждому из микрофронтендов (перенёс auth.json в auth, но до остальных добраться не успел).
Основная сложность - информация о том, вошёл ли пользователь в систему, и если да, то под кем, нужна другим микрофронтедам. Для этого я решил использовать глобальное состояние с помощью Redux.   

Я готов доделать эту работу на следующей неделе, сейчас отправил потому что подходит дедлайн, и надо отправить хотя бы что-то. Я начал проходить курс вчера утром.