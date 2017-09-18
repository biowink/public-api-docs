## Authentication
  * Clue supports standard server-side OAuth2 flow
  * Register an oauth client (for now, we create these for you)
  * Start the oauth flow by opening a the authorization url in a browser
    * Authorization domain: `auth.helloclue.com`
    * Authorization url: `/oauth2/authorize`
    * HTTP Verb: `GET`
    * Params:
      * `response_type`: only valid value, for now, is `code`
      * `client_id`: the oauth2 app key
      * `scope`: comma seperated list of scopes to be authorized
      * `redirect_uri`: callback url to redirect to at the end of the UI flow (validation not done yet)
      * `state`: security text to prevent --->LOOKUP<--- attack
    * On a successful authorization, the callback url recieves
      * `code`: a unique one-time code, that can be exchanged for an access_token & a refresh-token
      * `state`: same value as the state param sent in the authorization flow
  * Exchange the code for a token (standard OAuth2 code exchange)
    * Api Domain: `api.helloclue.com`
    * Token url: `/oauth2/token`
    * HTTP Verb: `POST`
    * Params:
      * `grant_type`: only valid value is `authorization_code`
      * `client_id`: the oauth2 app key
      * `client_secret`: the oauth2 app secret
      * `code`: the code recieved via the callback url
    * On a successful code-exchange, the api returns a json object with the following properties
      * `access_token`: a Bearer token that can be used to talk to the api
      * `refresh_token`: OAuth refresh token to generate a new access_tokens, preferably when the old one about to be expired, or expired already
      * `expires_in`: number of seconds for which the token is valid (7 days for now)
  * When an access_token expires, it can be refreshed (Standard OAuth2 token refresh call)
    * Api Domain: `api.helloclue.com`
    * Token url: `/oauth2/token`
    * HTTP Verb: `POST`
    * Params:
      * `grant_type`: only valid value is `refresh_token`
      * `refresh_token`: a valid refresh token
    * On a successful token refresh, the api returns a json object with the following properties
      * `access_token`: a Bearer token that can be used to talk to the api
      * `expires_in`: number of seconds for which the token is valid (7 days for now)
