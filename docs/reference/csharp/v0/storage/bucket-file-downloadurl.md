---
title: bucket.file.getDownloadUrl()
description: Get a download url for a file from a bucket.
---

Create a download url for a file within a bucket.

```C#
using Nitric.Sdk;
using Nitric.Sdk.Storage;

var assets = Nitric.Bucket('assets').With(BucketPermission.Reading);

var logo = assets.File('images/logo.png');

// Create a read-only signed url reference for downloading
var downloadUrl = logo.GetDownloadUrl();
```

## Parameters

---

**expiry** `int`

Seconds until link expiry. Defaults to `600`, Maximum of `604800` (7 days)

---

## Examples

### Create a readable link that is valid for the next 5 minutes

```C#
using Nitric.Sdk;
using Nitric.Sdk.Storage;

var assets = Nitric.Bucket('assets').With(BucketPermission.Reading);

var logo = assets.File('images/logo.png');

// Create a read-only signed url reference for downloading
var downloadUrl = logo.GetDownloadUrl(300);
```

### Redirect response to an image url

```C#
using Nitric.Sdk;
using Nitric.Sdk.Storage;

var images = Nitric.Bucket('images').With(BucketPermission.Reading);
var mainApi = Nitric.Api("main");

mainApi.Get("/images/:id", context => {
    var id = context.Req.PathParams["id"];
    var signedUrl = images.File(id).GetDownloadUrl();

    context.Res.Status = 303;
    context.Res.Headers["Location"] = new string[] { signedUrl };

    return context;
});
```