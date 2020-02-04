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
