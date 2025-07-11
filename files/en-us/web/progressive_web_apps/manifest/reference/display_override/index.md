---
title: display_override
slug: Web/Progressive_web_apps/Manifest/Reference/display_override
page-type: web-manifest-member
status:
  - experimental
browser-compat: manifests.webapp.display_override
sidebar: pwasidebar
---

{{SeeCompatTable}}

The [`display`](/en-US/docs/Web/Progressive_web_apps/Manifest/Reference/display) member is used to determine the developer's preferred display mode for a website. It follows a process where the browser falls back to the next display mode if the requested one is not supported. In some advanced use cases, this fallback process might not be enough.

The `display_override` member solves this by letting the developer provide a sequence of display modes that the browser will consider before using the `display` member. Its value is an array of display modes that are considered in-order, and the first supported display mode is applied.

### Values

Display override objects are display-mode strings, the possible values are:

- `browser`
  - : The application opens in a conventional browser tab or new window, depending on the browser and platform.
    This is the default.

- `fullscreen`
  - : All of the available display area is used and no user agent {{Glossary("chrome")}} is shown.

- `minimal-ui`
  - : The application will look and feel like a standalone application with a minimal set of UI elements for controlling navigation.
    The elements will vary by browser.

- `standalone`
  - : The application will look and feel like a standalone application.
    This can include the application having a different window, its own icon in the application launcher, etc.
    In this mode, the user agent will exclude UI elements for controlling navigation, but can include other UI elements such as a status bar.

- `tabbed` {{experimental_inline}}
  - : The application can contain multiple application contexts inside a single OS-level window.
    Supporting browsers can choose how to display these contexts, but a common approach is to provide a tab bar to switch between them.

- `window-controls-overlay` {{experimental_inline}}
  - : This display mode only applies when the application is in a separate PWA window and on a desktop operating system.
    The application will opt-in to the Window Controls Overlay feature, where the full window surface area will be available for the app's web content and the window control buttons (maximize, minimize, close, and other PWA-specific buttons) will appear as an overlay above the web content.

## Examples

In the example below, the browser will consider the following display-mode fallback chain in this order: `fullscreen` → `minimal-ui` → `standalone`.

```json
{
  "display_override": ["fullscreen", "minimal-ui"],
  "display": "standalone"
}
```

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- [Preparing for the display modes of tomorrow](https://developer.chrome.com/docs/capabilities/display-override)
- [Customize the window controls overlay of your PWA's title bar](https://web.dev/articles/window-controls-overlay)
