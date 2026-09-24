# GeeUISetting

Robot settings screens.

## Cloud URL

This app does not define `https://yourservice.com` and it has no Kotlin type for that host. Every screen passes the path `"your interface url"` to `GeeUiNetManager.get` or `GeeUiNetManager.post`.

The host is hardcoded in GeeUIComponents, class `GeeUINetworkUtil`:

```text
https://yourservice.com + uri + ?sn=<serial>&ts=<timestamp>
```

`uri` must be a path such as `/robot_api/v1/...`. Replacing `"your interface url"` with `http://10.0.2.2:8080` builds `https://yourservice.comhttp://10.0.2.2:8080`, which is not a valid URL. The named path constants are `GeeUINetworkConsts` in the GeeUIComponents repository; these screens do not use them. The full list is `docs/NETWORK.md` in that repository.
