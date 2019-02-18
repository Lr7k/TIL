# configparseの使い方

設定ファイルを用意する

conf.ini
```conf
[setting]
url:xxxxx
```

設定ファイルを読み込む
read_conf.py
```
import configparser

config = configparser.ConfigParser()
config.read("conf.ini")

print(config["setting"]["url"])
# "XXXXX"
```
