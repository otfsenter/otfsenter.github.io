.. _python-merge_lines_with_regular:

*************
合并多行
*************


.. code-block:: python

  import re

  data = open("1.txt").readlines()
  for n, line in enumerate(data):
      a = re.match('^\d{4}-\d{2}-\d{2}\s+\d{2}:\d{2}:\d{2},\d{3}', line)
      if a:
          data[n] = "\n" + line.strip()
      else:
          data[n] = line.strip()
  print ' '.join(data)
