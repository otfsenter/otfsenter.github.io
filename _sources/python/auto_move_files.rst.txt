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

    # 根目录
    path_root = r'C:\PycharmProjects\move_files'

    # 被监视的文件夹
    folder_to_track = r'C:\PycharmProjects\move_files\downloads'

    # 规则配置文件
    file_json = r'C:\PycharmProjects\move_files\config.json'


    def get_des_folder(filname):
        """
        根据文件名判断出目标文件的绝对路径
        :param filname: 文件名
        :return: 目标文件的绝对路径
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

            # 根据文件名前缀判断
            for prefix in prefix_list:
                if str(filname).startswith(prefix):
                    folder_des = folder

            # 根据文件名后缀判断
            for suffix in suffix_list:
                if str(filname).endswith(suffix):
                    folder_des = folder

        # 如果前面都没有判断出目的文件的路径，默认放在 other 文件夹下
        try:
            return folder_des
        except UnboundLocalError:
            folder_des = data_dict.get('other', {}).get('folder', '')
            return folder_des


    def move_multiple_times(file_src, file_des):
        """
        文件刚刚被复制到 downloads 文件夹下面的时候，几秒之内可能被进程占用，
        导致无法剪切到其他目录，
        所以这里根据 PermissionError 使用递归重复剪切 直至移动文件成功，
        time.sleep(1)必须要，否则会继续报错, 另会报 RecursionError 错误。
        :param file_src: 文件原来所在的绝对路径
        :param file_des: 文件所要移动到的 目的 的绝对路径
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


    # 利用 Observer 注册一个监视器，时刻监视 downloads 文件夹的变化
    event_handler = MyHandler()
    observer = Observer()
    observer.schedule(event_handler, folder_to_track, recursive=True)

    # 启动监视器
    observer.start()

    # 监视器保持运行，直到按下 Ctrl + C 结束脚本
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


