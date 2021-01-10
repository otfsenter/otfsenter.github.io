.. _python-auto-get-schedule:

用Python自动获取排班人员
==============================

:ref:`wechat`

总体思路是对比班次的开始时间和结束时间，

计算出当前的班次，

再根据班次得出当前的值班人员，

最后用while循环，实时刷新当前的值班人员，

当然也可以去个重，如果这个周期和上个周期的值班人员一样，不显示，如果不一样再显示出来也可以，更具有实用性

.. code-block::

    import time
    from datetime import datetime

    # 值班时间表，时间用字符串表示，看起来清晰一些
    # 中班分层两个key，是为了下面对比时间方便
    schedule_dict = {
        '早班': ['8:30', '16:30'],
        '中班-昨天': ["16:30", "00:00"],
        '中班-今天': ["00:00", "00:30"],
        '晚班': ["00:30", "8:30"]
    }

    # 值班人员表
    attendants_dict = {
        '早班': '张三',
        '中班-昨天': '李四',
        '中班-今天': '李四',
        '晚班': '王五'
    }

    # 自动计算好当前时间的年、月、日
    now_year = datetime.now().year
    now_month = datetime.now().month
    now_day = datetime.now().day


    # 从 schedule_dict 中的字符串提取出数字的小时、分钟
    def get_hour_minute(hour_minute_string):
        hour = int(str(hour_minute_string).split(':')[0])
        minute = int(str(hour_minute_string).split(':')[1])
        return hour, minute


    def run():
        # 值班人员列表初始化
        on_call_list = []
        
        # 遍历值班时间的表
        for k, v in schedule_dict.items():

            # 把 schedule_dict中的字符串弄成数字的小时、分钟
            time_begin_str, time_end_str = v
            hour_begin, minute_begin = get_hour_minute(time_begin_str)
            hour_end, minute_end = get_hour_minute(time_end_str)

            # 值班开始的时间
            time_begin = datetime(year=now_year, month=now_month, day=now_day,
                                hour=hour_begin, minute=minute_begin)

            # 值班结束的时间
            time_end = datetime(year=now_year, month=now_month, day=now_day,
                                hour=hour_end, minute=minute_end)
            
            # 现在的时间
            time_now = datetime.now()

            # 三个班次，会循环3次，对比现在的时间在哪个班次
            if time_begin <= time_now <= time_end:
                print('现在班次是：', k)
                on_call_person = attendants_dict.get(k)
                print('值班人员是：', on_call_person)
                on_call_list.append(on_call_person)

        no_on_call_list = list(set(attendants_dict.values()) - set(on_call_list))
        print('休息的人分别是：', '、'.join(no_on_call_list))
        print('-------------------------------------------------------------------')


    def main():
        while 1:
            run()
            # 这里可以30分钟刷一次，改成1800就行，
            # 这样就能实时获取当前值班的人，休息的人
            time.sleep(10)


    if __name__ == '__main__':
        main()

