.. _python-auto-rename-files:

自动重命名电影名字
=========================

:ref:`wechat`

.. code-block::

    import glob
    import os
    import re


    def split_string(str_to_split, origin_str):
        return re.split('[%s]' % str_to_split, origin_str)


    def print_origin_filename(path_root):
        """
        直接打印目录下的所有文件，方便观察
        :param path_root: 目的文件夹
        """
        for i in os.listdir(path_root):
            print(i)


    def print_split_filename_list(path_root, str_to_split, suffix):
        """
        打印被分割的文件列表
        :param path_root: 目的文件夹
        :param str_to_split: 多个分隔符，例如：E.，这是两个字符，E和英文句号
        :param suffix: 后缀，例如：mp4或者mkv
        """
        suffix_re = '*.' + suffix

        os.chdir(path_root)
        for filename in glob.glob(suffix_re):
            item_list = split_string(str_to_split, filename)
            print(item_list)


    def get_episode(origin_str, str_to_split, ep_index):
        """
        获取集数
        :param origin_str: 文件名
        :param str_to_split: 多个分隔符，例如：E.，这是两个字符，E和英文句号
        :param ep_index: 集数对应的序号，从0开始
        :return: 返回集数对应的序号字符串
        """
        episodes = split_string(str_to_split, origin_str)
        episode_int = episodes[ep_index]
        episode = str(int(episode_int))
        return episode


    def run(path_root, string_split, ep_index, suffix):
        """
        重命名
        :param path_root: 目的文件夹
        :param string_split:  多个分隔符，例如：E.，这是两个字符，E和英文句号
        :param ep_index:  集数对应的序号，从0开始
        :param suffix:  后缀，例如：mp4或者mkv
        """
        suffix_re = '*.' + suffix

        os.chdir(path_root)
        for i in glob.glob(suffix_re):
            file_src = os.path.join(path_root, i)

            file_des = os.path.join(path_root,
                                    get_episode(
                                        i, string_split,
                                        ep_index) + '.' + suffix
                                    )
            os.rename(src=file_src, dst=file_des)
        print('恭喜你，批量重命名完毕！')


    def main():
        # 1. 原样输出目录下的文件名
        print('第1步：\n')
        print('输入你要批量修改名字的目录：')
        path_root = str(input()).strip()
        # 直接打印该文件夹下的所有文件名字
        print_origin_filename(path_root)
        print(
            '--------------------------------------------'
            '------------------------------------------------')

        # 2. 输入后缀和分割的多个字符
        print('第2步：\n')
        print('观察上面输出的电影、电视剧的名字')
        print('现在需要确定视频的后缀和作为分隔符的字母或字符')
        print('请输入视频的后缀，比如mp4, mkv：')
        suffix = str(input()).strip()
        print(
            '--------------------------------------------'
            '------------------------------------------------')

        print('第3步：\n')
        print('请输入需要分割的字符串， \n'
            '比如名字是 "国土安全.Homeland.S01E12.Chi_Eng.HR-HDTV", \n'
            '就需要输入 "E."， \n'
            '结果会输出: "[\'国土安全\', \'Homeland\', \'S01\', \'12\', '
            '\'Chi_\', \'ng\', \'HR-HDTV\']" \n')
        print('请输入需要分割的字符串（例如：E.）: \n')
        string_split = str(input()).strip()
        # 输入分割之后的列表，方便后面选择集数对应的序号
        print_split_filename_list(path_root, string_split, suffix)
        print(
            '--------------------------------------------'
            '------------------------------------------------')

        # 3. 输入集数所在的序号，从0开始
        print('第4步：\n')
        print('观察上面输出的列表，找出集数所在的序列号，从0开始  \n'
            '比如：'
            '"[\'国土安全\', \'Homeland\', \'S01\', \'12\', \'Chi_\', '
            '\'ng\', \'HR-HDTV\']" 这样的列表 \n '
            '集数在第4个，从0开始，输入3即可：\n')
        print('请输入集数（例如：3）：')
        ep_index = int(str(input()).strip())

        run(path_root, string_split, ep_index, suffix)


    if __name__ == '__main__':
        main()
    
