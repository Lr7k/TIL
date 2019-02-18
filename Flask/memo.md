# Flaskであれとなったことを記載する

## render_template()した時に、指定したhtmlに変数が渡されていない

app.py
```flask
from flask import Flas
from flask import render_template

@app.route("/")
def index():
	message = "hello"
	return render_template("指定html", msg=message)
```

index.html
```index
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    {{ % msg % }}
</body>
</html>
```
注意:app.pyからhtmlへ渡されるのは、return render_template()の<strong>msg</strong>
