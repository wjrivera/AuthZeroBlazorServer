# Auth0 Blazor Server

Basic Blazor Server app that uses Auth0 for authentication and authorization.

## Installation

```c#
dotnet build
```

## Required Dependencies

[Microsoft.AspNetCore.Authentication.OpenIdConnect](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.OpenIdConnect)

## Auth0

After following the setup linked below on References, do the following:

* Roles

  * Add new rule under **Auth Pipeline** on Auth0 dashboard

  * Name it what you want and add the following:

  * ```javascript
    function (user, context, callback) {
      context.idToken['https://schemas.quickstarts.com/roles'] = user.app_metadata.authorization.roles;
      context.idToken['https://schemas.quickstarts.com/groups'] = user.app_metadata.authorization.groups;
      context.idToken['https://schemas.quickstarts.com/permissions'] = user.app_metadata.authorization.permissions;
      return callback(null, user, context);
    }
    ```

  * Under **Roles** on Auth0 dashboard, create two new roles (**admin.user** and **normal.user**)

* Users

  * Add new user either thru app or under **User Management** on Auth dashboard

  * Name it what you want and add the following under **app_metadata**

  * ```json
    {
      "authorization": {
        "groups": [
          "admin.group",
          "normal.group"
        ],
        "roles": [
          "admin.user",
          "normal.user"
        ],
        "permissions": [
          "read.user",
          "write.user"
        ]
      }
    }
    ```

  * Don't forget to hit **Save**

## License

[MIT](https://choosealicense.com/licenses/mit/)

## References

[Auth0 Official Website](https://auth0.com/)

[Auth0 Blazor Setup](https://auth0.com/blog/what-is-blazor-tutorial-on-building-webapp-with-authentication/#What-is-Blazor-)

