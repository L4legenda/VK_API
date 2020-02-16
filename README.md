# VK API
Установка VK API
```Bash
pip install vk_api
```
### Авторизация пользователя.

По токену
```python
import vk_api

vk_session = vk_api.VkApi(token='*******')
```

### Работа с API

Берем данные API
```python
vk = vk_session.get_api()
```

Проверка сообщения
```python

from vk_api.longpoll import VkLongPoll, VkEventType
import random

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

Отправка изображений
```python
from vk_api import VkUpload 
upload = VkUpload(vk_session)

photo = upload.photo_messages(photos="img.jpg")[0]
# photos - пусть к изображению

vk.messages.send(
  user_id=event.user_id,
  message="Текст сообщения",
	# Атрибут отправки изображения
  attachment='photo{}_{}'.format(photo['owner_id'], photo['id']),
  random_id=random.randint(1, 2147483647),
)
```
