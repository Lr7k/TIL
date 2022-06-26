# Securityについて  

## CORS(Cross-origin-resource-sharing)  

origin = scheme + hostname + port   
scheme: ex https, http  
hostname: ex yahoo.co.jp  
port: ex 80, 443  

origin毎のアクセス制御可能(while list使用)  
リクエストは可能だがレスポンスが受け取れない  

## XSS(Cross Site Scripting)攻撃  

- 不正サイトに誘導される(リンクを踏む)  
- 不正なjavascriptが実行されブラウザのcookieを読み取られる(document.cookieなどを読み込まれる)、外部に送信  

対策: cookieの性質でhttpOnlyというものがあり、これを設定することでjavascriptからcookieを読み取れなくする  

## CSRF(Cross-site request forgeries)攻撃  

- ユーザーが正規サイトからログイン(jwtのcookieをリクエスト)  
- サーバーサイドがレスポンス(jwt cookieを付与)  
- クライアントはリクエストヘッダーにそのjwt cookieを付与(アクセス)  
- 不正サイトに誘導→アクセス、その際jwt cookieも付与するため不正なDB操作が行われる可能性  

対策: 正規サイトからのリクエストか判断する仕組み　→ CSRF Token  

- 正規サイトからのアクセス時にサーバサイドからCSRF Tokenの発行  
- DB操作リクエストの際に、headerにCSRF Tokenを付与し、サーバサイドが正規リクエストかバリデーションを行う  
- 外部サイトおよび不正サイトからのCSRF Token付与済みリクエストがあっても、CORS(while listに入っていない)によってレスポンスを読み取れない  

## SameSite  

Cross domain(originが異なる)間通信時のcookieの扱いの違い  

SameSite = lax(default)
- POST methodでログイン認証してもcookieがsetされない(googleのCSRF対策)  

対策: SPAではSameSiteをnoneにするとCookieの送受信が可能  
- その際、secureをtrueすること。httpsで暗号化された通信のみcookie使用可能にするため。