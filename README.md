# VK API
Установка VK API
```Bash
pip install vk_api
```
### Авторизация пользователя.

По логину и паролю
```python
import vk_api

vk_session = vk_api.VkApi('+71234567890', 'mypassword')
vk_session.auth()
```


По токену
```python
vk_session = vk_api.VkApi(token='*******')
```

### Работа с API

Берем данные API
```python
vk = vk_session.get_api()
```

Запить на стене
```python
vk.wall.post(message='Hello world!')
```
Проверка сообщения
```python
from vk_api.longpoll import VkLongPoll, VkEventType

longpoll = VkLongPoll(vk_session)

for event in longpoll.listen():
	if event.type == VkEventType.MESSAGE_NEW and event.to_me and event.text:
		if event.from_user:
			if event.text == "***":
				vk.messages.send(
          user_id=event.user_id,
          message="Текст сообщения",
          random_id=random.randint(1, 2147483647),
        )
```
