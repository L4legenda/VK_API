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
