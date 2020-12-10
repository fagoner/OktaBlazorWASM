## Blazor Okta WASM

Simple Blazor app to login with Okta

### Credits / Source

- [Build Auth FAST for Blazor WebAssembly in .NET](https://www.youtube.com/watch?v=qN1vSk8lPtU)

### Requeriments
- [x] Okta account
- [x] Dotnet Core 3.1

### Settings

#### Okta Setting  `wwwroot/appsettings.json`

```
{
  "Okta": {
    "Authority": "https://dev.okta.com",
    "ClientId": "clientId"
  }
}
```
Authority can be find on: `Api/Authorization Servers/Settings/Issuer`

#### OidcAuthentication Setting  `Program.cs`
```
....

builder.Services.AddOidcAuthentication(options =>
{
    ...
    builder.Configuration.Bind("Okta", options.ProviderOptions);
    options.ProviderOptions.ResponseType = "code";
    options.ProviderOptions.DefaultScopes.Add("profile");
    options.ProviderOptions.DefaultScopes.Add("address");
});
```

#### Authorized views
See Authorized Components on `Pages/Claims.razor`

#### Authorized link
Add to `Shared/NavMenu.razor` the following path
```
<li class="nav-item px-3">
    <NavLink class="nav-link" href="claims">
        <span class="oi oi-list-rich" aria-hidden="true"></span>
        claims
    </NavLink>
</li>
```


#### Okta settings

|Setting|Value|
|-|-|
|Login redirect URIs |https://localhost:5001/authentication/login-callback|
| Logout redirect URIs |https://localhost:5001/authentication/logout-callback	|
|Login initiated by  App Only Initiate login URI |https://localhost:5001|
|Application type |Single Page App (SPA) |
|Allowed grant types / Client acting on behalf of a user | Authorization Code|

