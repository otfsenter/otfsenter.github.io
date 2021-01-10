.. _en-python-auto-get-schedule:

Get schedule person automatically with python
=====================================================

:ref:`wechat`

Compare start time and end time,

Calculate current schedule plan,

Get schedule person by plan,

Refresh current schedule persion with while loop

Repeat data, we can do not display schedule person which the same as last loop until different with last loop.


.. code-block::

    import time
    from datetime import datetime

    schedule_dict = {
        'morning': ['8:30', '16:30'],
        'noon-yesterday': ["16:30", "00:00"],
        'noon-today': ["00:00", "00:30"],
        'night': ["00:30", "8:30"]
    }

    # schedule person table
    attendants_dict = {
        'morning': 'Mike',
        'noon-yesterday': 'John',
        'noon-today': 'John',
        'night': 'Stone'
    }

    now_year = datetime.now().year
    now_month = datetime.now().month
    now_day = datetime.now().day


    def get_hour_minute(hour_minute_string):
        hour = int(str(hour_minute_string).split(':')[0])
        minute = int(str(hour_minute_string).split(':')[1])
        return hour, minute


    def run():
        on_call_list = []
        
        for k, v in schedule_dict.items():

            time_begin_str, time_end_str = v
            hour_begin, minute_begin = get_hour_minute(time_begin_str)
            hour_end, minute_end = get_hour_minute(time_end_str)

            time_begin = datetime(year=now_year, month=now_month, day=now_day,
                                hour=hour_begin, minute=minute_begin)

                                hour=hour_end, minute=minute_end)
            
            time_now = datetime.now()

            if time_begin <= time_now <= time_end:
                print('now ：', k)
                on_call_person = attendants_dict.get(k)
                print('right person: ', on_call_person)
                on_call_list.append(on_call_person)

        no_on_call_list = list(set(attendants_dict.values()) - set(on_call_list))
        print('person in holiday: ', ', '.join(no_on_call_list))
        print('-------------------------------------------------------------------')


    def main():
        while 1:
            run()
            time.sleep(10)


    if __name__ == '__main__':
        main()

