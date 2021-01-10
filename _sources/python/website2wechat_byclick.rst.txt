.. _website2wechage-by-click:

自动发布文章到微信公众号-doing
=======================================

:ref:`wechat`


* 还没完成的列表

.. csv-table::
    :header: 序号, 项

    1, send png auto
    2, 声明原创
    3, 自动添加文章列表

.. code-block:: python

    import time

    from pymouse import PyMouse
    from pykeyboard import PyKeyboard
    import win32clipboard
    import win32con

    m = PyMouse()
    k = PyKeyboard()

    author = 'otfsenter'
    position_title_end = [732, 239]
    position_article_end = [416, 858]


    def send_to_clip(input_string):
        win32clipboard.OpenClipboard()
        win32clipboard.EmptyClipboard()
        win32clipboard.SetClipboardData(win32con.CF_UNICODETEXT, input_string)
        win32clipboard.CloseClipboard()


    def click_first_page():
        m.click(146, 28)
        time.sleep(1)


    def click_second_page():
        m.click(369, 31)
        time.sleep(1)


    def click_second_page_article():
        m.click(330, 485, 1)
        time.sleep(1)


    def click_second_page_title():
        m.click(203, 308, 1)
        time.sleep(1)


    def click_second_page_author():
        m.click(226, 345)
        time.sleep(1)


    def press_title_start():
        m.press(349, 233, 1)
        time.sleep(1)


    def move_title_end():
        m.move(
            position_title_end[0],
            position_title_end[1]
        )
        time.sleep(1)


    def release_title_end():
        m.release(
            position_title_end[0],
            position_title_end[1]
        )
        time.sleep(1)


    def press_article_start():
        m.press(353, 288, 1)
        time.sleep(1)


    def move_article_end():
        m.move(
            position_article_end[0],
            position_article_end[1]
        )
        time.sleep(1)


    def release_article_end():
        m.release(
            position_article_end[0],
            position_article_end[1]
        )
        time.sleep(1)


    def ctrl_c():
        k.press_keys([k.control_l_key, 'c'])
        time.sleep(1)


    def ctrl_a():
        k.press_keys([k.control_l_key, 'a'])
        time.sleep(1)


    def ctrl_v():
        k.press_keys([k.control_l_key, 'v'])
        time.sleep(1)


    def input_author():
        k.type_string(author)
        time.sleep(1)


    def delete():
        k.press_key(k.backspace_key)
        time.sleep(1)


    def run():
        # copy title
        click_first_page()
        press_title_start()
        move_title_end()
        release_title_end()
        ctrl_c()
        click_second_page()
        click_second_page_title()
        ctrl_a()
        ctrl_v()

        # copy author
        click_second_page_author()
        ctrl_a()
        delete()
        input_author()

        # copy article
        click_first_page()
        press_article_start()
        move_article_end()
        release_article_end()
        ctrl_c()
        click_second_page()
        click_second_page_article()
        ctrl_a()
        ctrl_v()


    def main():
        run()


    if __name__ == '__main__':
        main()
    
