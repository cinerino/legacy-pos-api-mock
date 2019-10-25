# Group OAuth

## Issue an access token [/token]

### アクセストークン発行 [POST]
[OAuth2](https://tools.ietf.org/html/rfc6749) に準拠したトークンエンドポイントです。

::: note
エンドポイントは、

`https://ttts-development.auth.ap-northeast-1.amazoncognito.com/token`

となります。
:::

**利用可能な認可タイプ**

+ `client_credentials`

~~認証時には必要なスコープを必ず指定してください。~~

スコープ指定が非必須となりました。

::: note
返却値には、`access_token`と`expires_in`が含まれます。

アプリケーション側でアクセストークンの有効期間を管理し、適宜再取得してください。
:::

+ Request クライアント認証 (application/x-www-form-urlencoded)
    +  Headers
        Authorization: Basic ABC123
    + Attributes
        + `grant_type`: `client_credencials` (string, required) - 認証タイプ(固定値)
        + `state`: `state123456789` (string, required)
            クライアント状態(クライアント側で現在のユーザー状態を表す文字列を送信してください。例えばセッションIDなどです)
        + `scopes` (array, fixed-type) - 未指定であれば、必要なスコープがセットされます。
            + `https://ttts-api-development-azurewebsites.net/transactions` (string)
            + `https://ttts-api-development-azurewebsites.net/performances.read-only` (string)

+ Response 200 (application/json)
    + Attributes
        + access_token: `JWT` (string, required) - アクセストークン
        + token_type: `Bearer` (string, required) - 発行されたトークンタイプ
        + expires_in: 1800 (number, required) - アクセストークンの有効期間

<!-- include(../response/400.md) -->
