.. _cannnot_find_media_files_in_debug:


Cannot find media files like mp4 when debug is True in Django
=================================================================


:ref:`wechat`

add configuration in main urls.py

.. code-block::

    from django.conf import settings
    from django.conf.urls.static import static

    if settings.DEBUG:
        urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)

We cannot find media files just because do not configure urls for media!
