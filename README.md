# Garpix Favourites


User Favourites module for Django/DRF projects. Part of GarpixCMS.

## Quickstart

Install with pip 

    $ pip install garpix_favorite

Add the `garpix_favourite` to your INSTALLED_APPS:

```python
# settings.py

INSTALLED_APPS = [
    # ...
    'garpix_favourite',
]
```

Make migrations and migrate database:

    $ ./manage.py makemigrations
    $ ./manage.py migrate

Add to `urls.py`:

```
urlpatterns = [
    # ...
    path('', include('garpix_favourite.urls'))
]
```
Add models that can be added to favorites in `settings.py`:

```
ACCEPTED_FAVORITE_MODELS = [
    'YourModel',
]
```

Also inherit them from `FavoriteMixin` and override `get_absolute_url()` method:
```
# models.py

from django.db import models
from garpix_favourite.utils import FavoriteMixin


class YourModel(FavoriteMixin, models.Model):
    ...

    def get_absolute_url(self) -> str:
        return reverse('view-detail', args=[self.id])
```

Inherit your serializer from `FavoriteSerializerMixin`:
```
# serializers.py

from rest_framework import serializers
from garpix_favourite.utils import FavoriteMixin


class YourModelSerializer(FavoriteMixin, serializers.ModelSerializer):
    ...
```

---

Developed by Garpix / [https://garpix.com](https://garpix.com)