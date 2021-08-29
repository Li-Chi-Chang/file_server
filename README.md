# file_server

LiChi

## Result Presentation

## Building structure steps

ref page [here](https://developer.mozilla.org/zh-TW/docs/Learn/Server-side/Django/development_environment)

1. start project

    ```cmd
    django-admin startproject file_server
    ```

2. check default setting

    ```cmd
    python manage.py runserver
    ```

    ![check pic](./doc/1.1.png)

3. move your secret key in settings.py to secrets.py(if you need to public your code online like github, or skip)

    ```cmd
    # in the proj folder:
    cd file_server
    touch secrets.py # or create file in win
    ```

    ```py
    SECRET_KEY = 'd*************************************************'
    def getSecret():
        return SECRET_KEY
    ```

    add this secrets.py into gitignore

4. add an app

   ```cmd
   python manage.py startapp dirtravel
   ```

   in file_server\settings.py:

   ```py
   INSTALLED_APPS = [
        ...,
        'dirtravel.apps.DirtravelConfig',# you can find the class name in /appname/apps.py
    ]
   ```

5. set url to your app, in this case, this app will be redirected to website.com/dirtravel

    in file_server\urls.py:

    ```py
    # Use include() to add paths from the dirtravel application
    from django.conf.urls import include
    from django.urls import path

    urlpatterns += [
        path('dirtravel/', include('dirtravel.urls')),
    ]
    ```

    create dirtravel/urls.py file

    ```py
    from django.urls import path
    from . import views
    urlpatterns = [
    ]
    ```

6. add static path

    ```py
    # Use static() to add url mapping to serve static files during development (only)
    from django.conf import settings
    from django.conf.urls.static import static

    urlpatterns += static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
    ```

7. now, it is done for all setting. you can try the command below. There is an error(page not found) is very normal(we didn't create page for it)

   ```cmd
   python manage.py runserver
   ```

## TODO
