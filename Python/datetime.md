# datetimeオブジェクトから日付文字列を表示する
```python
from datetime import dateitme

now = datetime.now()
now = now.strftime("%Y-%m-%s %H:%M:%S")
print(now) # '2019-02-18 12:46:33'
```
