---
title: "Partitioned: All third-party storage access requests"
slug: Web/Privacy/Guides/Storage_Access_Policy/Errors/CookiePartitionedForeign
page-type: guide
sidebar: privacy
---

A request to access cookies or storage was _partitioned_ because it came from a third-party (a different origin) and [dynamic state partitioning](/en-US/docs/Web/Privacy/Guides/State_Partitioning#dynamic_partitioning) is enabled.

## Message

Firefox:

```plain
CookiePartitionedForeign=Partitioned cookie
or storage access was provided to "<URL>" because it is loaded in the
third-party context and storage partitioning is enabled.
```

## What can be done

With Dynamic State Partitioning enabled, Firefox provides embedded resources with a separate storage bucket for every top-level website. Embedded third-parties may request access to the top-level storage bucket via the [Storage Access API](/en-US/docs/Web/Privacy/Guides/State_Partitioning#storage_access_api). You can also [disable Dynamic State Partitioning](/en-US/docs/Web/Privacy/Guides/State_Partitioning#disable_dynamic_state_partitioning) with the `network.cookie.cookieBehavior` pref.

## See also

- [State Partitioning](/en-US/docs/Web/Privacy/Guides/State_Partitioning)
