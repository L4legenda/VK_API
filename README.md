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
   # Проверка сообщения
   if event.text == "***":
			
    #Отправка сообщения
    vk.messages.send(
     user_id=event.user_id, # Пользователь получатель
     message="Текст сообщения", # Текст сообщения
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

Отправка URL изображения
```python
session = requests.Session()
from vk_api import VkUpload 
upload = VkUpload(vk_session)

image_url = 'Ссылка на картинку'
image = session.get(image_url, stream=True)
photo = upload.photo_messages(photos=image.raw)[0]

vk.messages.send(
    user_id=event.user_id,
    attachment='photo{}_{}'.format(photo['owner_id'], photo['id']),
    message='Ваш текст'
)
```
Несколько изображений
```python
imgs = []
photo1 = upload.photo_messages(photos="123.jpg")[0]
photo2 = upload.photo_messages(photos="bot.jpg")[0]

imgs.append('photo{}_{}'.format(photo1['owner_id'], photo1['id']))
imgs.append('photo{}_{}'.format(photo2['owner_id'], photo2['id']))
# photos - пусть к изображению

vk.messages.send(
    user_id=event.user_id,
    message="Текст сообщения",
    # Атрибут отправки изображения
    attachment=','.join(imgs),
    random_id=random.randint(1, 2147483647),
)
```
