# Adapter

🌏 [한국어](README.md)

## 🚩 Table of Contents

* [Overview](#overview)
* [Specification](#specification)
* [AdapterTool](#-adaptertool)
* [API](#-api)

## Overview

IdPs, such as Facebook or Google, provide Unity SDK to apply IdP functions faster and more easily in applications under development for Unity. However, as each IdP has different API, sufficient learning and time is required to implement each and every IdP function. 
Adapter provides a common interface so as to easily apply different IdP fuctions.

## Specification

### Unity support version

* 2018.4.0 or higher

### Support IdP

Each IdP SDK must be downloaded and installed manually.

* Google Play Games plugin for Unity
    * [Download](https://github.com/playgameservices/play-games-plugin-for-unity)
    * Tested version
        * 0.9.56
        * 0.9.57
        * 0.9.63
        * 0.9.64
        * 0.10.09
* Facebook SDK for Unity
    * [Download](https://developers.facebook.com/docs/unity/downloads)
    * Tested version
        * 7.15.0
        * 7.15.1
        * 7.16.0
        * 7.16.1
        * 7.17.0
        * 7.17.1
        * 7.17.2
        * 7.18.0
        * 7.18.1
        * 7.19.0
        * 7.19.1
        * 7.19.2

## 🔧 AdapterTool

Error occurs as below unless IdP SDK exists as supported by Adapter.

```cs
error CS0103: The name 'FB' does not exist in the current context
```

Adapter must be set depending on the IdP.

![GPMAdapterSettingTool](./images/TOASTKitAdapterSettingTool_001.png)

### Usage

1. Menu > Tools > GPM > Adapter > Settings
2. Select or deselect depending on the service use.
3. Click Set to complete the setting.

> [`Caution`]
>
> Do not change the folder structure of Adpater.
> Do not delete the code and files of Adpater.


## 🔨 API

### IsSuccess

Use AdapterError object to see if it is successful. 
For more information regarding AdapterErrorCode, see the ErrorCode itmes as below.

#### API

```cs
static bool IsSuccess(AdapterError error)
```

#### Example

```cs
private void SampleIsSucces(AdapterError error)
{
    if (GpmAdapter.IsSuccess(error) == true)
    {
        Debug.Log("success");
    }
    else
    {
        Debug.Log(string.Format("failure. error:{0}", error));
    }
}
```

### Login

Try login to IdP, by using IdP name and additional information.
The IdP names supported by Adapter are provided via the GpmAdapterType.Idp class. 

> [Note]
> To login to Facebook SDK, Facebook authority information is required, which can be configured at additional information by using the `facebook_permissions` key. If Facebook authority information is not configured, the default value `[public_profile, email]` is configured. For more details, see Example as below. 

#### API

```cs
static void Login(string idpName, Dictionary<string, object> additionalInfo, Action<AdapterError> callback)
```

#### Example

```cs
private void SampleLogin(string idpName)
{
    Dictionary<string, object> additionalInfo;
    
    switch (idpName)
    {
        case GpmAdapterType.Idp.FACEBOOK:
        {
            var facebookPermissionList = new List<string> { "public_profile", "email" };
            additionalInfo = new Dictionary<string, object>();
            additionalInfo.Add("facebook_permissions", facebookPermissionList);
            break;
        }
        case GpmAdapterType.Idp.GPGS:
        default:
        {
            additionalInfo = null;
            break;
        }
    }
    
    GpmAdapter.Idp.Login(GpmAdapterType.Idp.FACEBOOK, additionalInfo, (error) => 
    {
        if (GpmAdapter.IsSuccess(error) == true)
        {
            Debug.Log("success");
        }
        else
        {
            Debug.Log(string.Format("failure. error:{0}", error));
        }
    });
}
```

### Logout

Try logout of IdP.

#### API

```cs
static void Logout(string idpName, Action<AdapterError> callback)
```

#### Example

```cs
private void SampleLogout()
{
    GpmAdapter.Idp.Logout(GpmAdapterType.Idp.FACEBOOK, (error) => 
    {
        if (GpmAdapter.IsSuccess(error) == true)
        {
            Debug.Log("success");
        }
        else
        {
            Debug.Log(string.Format("failure. error:{0}", error));
        }
    });
}
```

### LogoutAll

Try logout of all IdPs.
If an error occurs before all IdPs are logged-out, stop processing logouts and return the error.

#### API

```cs
static void LogoutAll(Action<AdapterError> callback)
```

#### Example

```cs
private void SampleLogoutAll()
{
    GpmAdapter.Idp.LogoutAll((error) =>
    {
        if (GpmAdapter.IsSuccess(error) == true)
        {
            Debug.Log("success");
        }
        else
        {
            Debug.Log(string.Format("failure. error:{0}", error));
        }
    });
}
```

### GetAuthInfo

Query authentication information of IdP. 
Return AccessToken for Facebook, and return ServerAuthCode for Google. 
When authentication information is empty, enable DebugLogEnabled and check logs.

#### API

```cs
static void GetAuthInfo(string idpName, Action<string> callback)
```

#### Example

```cs
private void SampleGetAuthInfo()
{
    GpmAdapter.Idp.GetAuthInfo(GpmAdapterType.Idp.FACEBOOK, (facebookAuthInfo) => 
    {
        Debug.Log(string.Format("authInfo:{0}", facebookAuthInfo));
    });
}
```

### GetProfile

Query profile information of IdP.
Basic profile information is as follows.

* id
* name
* email


#### API

```cs
static void GetProfile(string idpName, Action<Dictionary<string, object>> callback)
```

#### Example

```cs
private void SampleGetProfile()
{
    GpmAdapter.Idp.GetProfile(GpmAdapterType.Idp.FACEBOOK, (facebookProfile) =>
    {
        if (facebookProfile == null)
        {
            Debug.Log("Facebook profile is null.");
        }
        else
        {
            foreach (KeyValuePair<string, object>kvp in facebookProfile)
            {
                Debug.Log(string.Format("{0}:{1}\n", kvp.Key, kvp.Value));
            }
        }
    });
}
```

### GetLoggedInIdpList

Query all logged-in IdP names.

#### API

```cs
static List<string> GetLoggedInIdpList()
```

#### Example

```cs
private void SampleGetLoggedInIdpList()
{
    var loggedInIdpList = GpmAdapter.Idp.GetLoggedInIdpList();
    foreach (var loggedInIdp in loggedInIdpList)
    {
        Debug.Log(string.Format("loggedInIdp:{0}", loggedInIdp));
    }
}
```

### GetUserId

Query UserId information of IdP.

#### API

```cs
static string GetUserId(string idpName)
```

#### Example

```cs
private void SampleGetUserId()
{
    var facebookUserId = GpmAdapter.Idp.GetUserId(GpmAdapterType.Idp.FACEBOOK);
    Debug.Log(string.Format("facebookUserId:{0}", facebookUserId));
}
```

### ErrorCode

| Error | Error Code | Description |
| --- | --- | --- |
| SUCCESS | 0 | Success. |
| ADAPTER_NOT_FOUND | 1 | Cannot find adapter. Configure an adapter. |
| NOT_LOGGED_IN | 2 | Not logged-in. Log in first to call API. |
| USER_CANCELED | 3 | Cancelled by user. |
| EXTERNAL_LIBRARY_ERROR | 4 | Error in external library. |