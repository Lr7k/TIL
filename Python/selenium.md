# seleniumのインストールから簡単な使い方

[selenium公式](http://phantomjs.org/download.html)

OSに合わせてphantomjsをインストールする

パスを通した後以下を確認する

```cmd
phantomjs
# phantomjs> 左のようになったらOK
```

pip でseleniumをインストールする
```pip
pip install selenium
```

## seleniumの使い方

selenium_python.py
```python
from selenium.webdriver.support.ui import WebDriverWait
from selenium import webdriver
from selenium.webdriver.support import expected_conditions
from selenium.webdriver.common.by import By

url = "対象サイトURL"
driver = webdriver.Phantomjs()
driver.get(url)
```

## 要素の取得
```selenium_python.py

# それぞれfind_elementsにしているが、要素がなかったときに
# エラーが発生しないようにしている。があまりよくない気がする。

# xpathで取得することが多い場合
driver.find_elements_by_xpath()

# classで取得する場合
driver.find_elements_by_class_name()

# 指定する要素が表示されるまで最大10秒待機する
# 今回はidを指定する
WebDriverWait(driver, 10).until(expected_conditions.presence_of_element_located(
	(By.ID, "")
)

# 指定する要素が非表示になるまで最大10秒待機する
# 今回はidを指定する
WebDriverWait(driver, 10).until(expected_conditions.invisibility_of_element_located(
	(By.ID, "")
)
```
