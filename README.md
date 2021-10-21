# Set up MFA in .NET with Blazor Server-Side

This repository shows you how to use Okta in a Blazor server side application with Multi Factor Authentication. Please read [Set up MFA in .NET with Blazor Server-Side][blog] to see how it was created.

**Prerequisites:**

- [.NET 5](https://dotnet.microsoft.com/download/dotnet/5.0)
- [Okta CLI](https://cli.okta.com)

> [Okta](https://developer.okta.com/) has Authentication and User Management APIs that reduce development time with instant-on, scalable user infrastructure. Okta's intuitive API and expert support make it easy for developers to authenticate, manage and secure users and roles in any application.

* [Getting Started](#getting-started)
* [Links](#links)
* [Help](#help)
* [License](#license)

## Getting Started

To run this example, run the following commands:

```bash
git clone https://github.com/nickolasfisher/Okta_BlazorServer.git
cd Okta_RoutingDemo
```

### Create an OIDC Application in Okta

Create a free developer account with the following command using the [Okta CLI](https://cli.okta.com):

```shell
okta register
```

If you already have a developer account, use `okta login` to integrate it with the Okta CLI. 

Provide the required information. Once you register, create a client application in Okta with the following command:

```shell
okta apps create
```

You will be prompted to select the following options:
- Type of Application: **1: Web**
- Framework of Application: **Other**
- Redirect URI: `https://localhost:44378/callback`
- Post Logout Redirect URI: `https://localhost:44378/signout/callback`

The application configuration will be printed to `.okta.env`.

```dotenv
export OKTA_OAUTH2_ISSUER="{yourOktaDomain}/oauth2/default"
export OKTA_OAUTH2_CLIENT_SECRET="{yourClientSecret}"
export OKTA_OAUTH2_CLIENT_ID="{yourClientId}"
```

Open the file `appsettings.Development.json` and update the code.

```json
{
  "DetailedErrors": true,
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning",
      "Microsoft.Hosting.Lifetime": "Information"
    }
  },
  "Okta": {
    "Domain": "{yourOktaDomain}",
    "ClientId": "{yourClientId}",
    "ClientSecret": "{yourClientSecret}"
  }
}
```

### Enable MFA in your Application

Navigate to your Okta admin console.

Select the application you just made under the **Applications** tab.

Click on the **Sign On** tab.

Under *Sign on Policy* click **Add Rule**.

Name you Rule *MFA* and under the *Access* section: 
   > Click **MultiFactor Settings**
   > Click **SMS Authentication**
   > Set the drop down to *Active* if it hasn't already been done.
   > Return to the Rule page.
   > Select *Prompt for factor* then *Every Sign on*.  

Press **Save**.

Start the Application.

Open `https://localhost:44378` in your favorite browser and you should be able to see the home page.

## Links

This example uses the following open source libraries from Okta:

* [Okta ASPNet SDK](https://github.com/okta/okta-aspnet)
* [Okta CLI](https://github.com/okta/okta-cli)

## Help

Please post any questions as comments on the [blog post][blog], or visit our [Okta Developer Forums](https://devforum.okta.com/).

## License

Apache 2.0, see [LICENSE](LICENSE).

[blog]: https://developer.okta.com/blog/2021/xyz
