.. _python-auto-move-files:

自动归档文件
==========================

:ref:`wechat`

一共三种文件：电影、图片、小说，

想要实现的效果是：当这些文件从浏览器下载到一个固定文件夹下面时，脚本能及时识别 并 自动归档到相应的电影、图片、小说的文件夹下面。

* 监视文件夹变化需要用到 `watchdog` 模块

* 移动文件需要用到 `shutil` 模块

步骤
------

1. 监视 downloads 文件夹的文件变化情况，类名：MyHandler, 继承自 watchdog.events.FileSystemEventHandler

2. 根据规则判断得到目标路径，函数名：get_des_folder, 参数是 filename(文件名)

3. 移动文件，函数名： move_multiple_times，参数是 file_src(原路径), file_des(目标路径)

.. _python-auto-move-files-config-json:

规则配置文件 config.json
--------------------------------

* 电影的关键字，前缀、后缀的列表、文件夹名字

.. code-block:: json

    {
        "movie": {
            "keywords": {
                "prefix": [
                    "movie"
                ],
                "suffix": [
                    "mp4",
                    "mkv",
                    "rmvb"
                ]
            },
            "folder": "movie"
        }
    }

keywords 中有前缀、后缀，逐一判断这些关键字，如果匹配，

取 folder 对应的 movie 来作为文件夹的名字，

图片、小说同理，具体的配置放在了最后面的 :ref:`python-auto-move-files-config-file`


具体的代码
-----------

.. code-block:: python

    import os
    import shutil
    import time

    from custom import file
    from watchdog.events import FileSystemEventHandler
    from watchdog.observers import Observer

    # root path
    path_root = r'C:\PycharmProjects\move_files'

    # folder monitored
    folder_to_track = r'C:\PycharmProjects\move_files\downloads'

    # configuration
    file_json = r'C:\PycharmProjects\move_files\config.json'


    def get_des_folder(filname):
        """
        get destination absolute path from file name
        :param file name
        :return: absolute path of destination file
        """
        data_dict = file.read_json(file_json)
        for category, keywords_folder_dict in data_dict.items():
            keywords_dict = keywords_folder_dict.get('keywords', {})
            prefix_list = keywords_dict.get('prefix', [])
            suffix_list = keywords_dict.get('suffix', [])
            folder = keywords_folder_dict.get('folder', '')

            if not keywords_dict:
                continue
            if not folder:
                continue

            if not prefix_list:
                continue
            if not suffix_list:
                continue

            # judge file name from prefix of file name
            for prefix in prefix_list:
                if str(filname).startswith(prefix):
                    folder_des = folder

            # judge file name from suffix of file name
            for suffix in suffix_list:
                if str(filname).endswith(suffix):
                    folder_des = folder

        # move to other folder by default if not hit any conditions
        try:
            return folder_des
        except UnboundLocalError:
            folder_des = data_dict.get('other', {}).get('folder', '')
            return folder_des


    def move_multiple_times(file_src, file_des):
        """
        file locked by download process when copy to download folder,
        then can not cut to other folder,
        move file by recursive using try except PermissionError util successfully,
        it is necessary to set `time.sleep(1)`, otherwise report error continuously,
        PS: except RecursionError will occur.

        :param file_src: absolute path of source file
        :param file_des: absolute of destination to move
        :return:
        """
        try:
            shutil.move(file_src, file_des)
        except PermissionError:
            time.sleep(1)
            move_multiple_times(file_src, file_des)


    class MyHandler(FileSystemEventHandler):
        def on_any_event(self, event):
            for filename in os.listdir(folder_to_track):
                file_src = os.path.join(folder_to_track, filename)

                folder = get_des_folder(filename)
                file_des = os.path.join(path_root, folder, filename)

                move_multiple_times(file_src, file_des)


    # monitor downloads folder every one seconds by monitor registered by `Observer`
    event_handler = MyHandler()
    observer = Observer()
    observer.schedule(event_handler, folder_to_track, recursive=True)

    observer.start()

    # keep monitor running, until end up scripts with `Ctrl + C`
    try:
        while True:
            time.sleep(1)
    except KeyboardInterrupt as e:
        observer.stop()
        observer.join()
        



.. _python-auto-move-files-config-file:

配置文件 
---------------------------------------------------------

回到 :ref:`python-auto-move-files-config-json` 标题


.. code-block:: json

    {
        "movie": {
            "keywords": {
                "prefix": [
                    "movie"
                ],
                "suffix": [
                    "mp4",
                    "mkv",
                    "rmvb"
                ]
            },
            "folder": "movie"
        },
        "picture": {
            "keywords": {
                "prefix": [
                    "pic"
                ],
                "suffix": [
                    "png",
                    "jpg"
                ]
            },
            "folder": "pic"
        },
        "novel": {
            "keywords": {
                "prefix": [
                    "novel"
                ],
                "suffix": [
                    "txt"
                ]
            },
            "folder": "novel"
        },
        "other": {
            "folder": "other"
        }
    }


