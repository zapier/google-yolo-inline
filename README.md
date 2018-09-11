# Inline Google One-tap Sign Up

To run the demo, clone the repo then start a server:

```
python -m SimpleHTTPServer 8080
```

[`index.html`](index.html) shows how to include [Google One-tap sign up](https://developers.google.com/identity/one-tap/web/overview) (a.k.a. Google Yolo) into your own sign up form, or wherever it makes sense for your website, to help your sign up conversion rate 🚀

## Problems With Google One-Tap

By default, Google One-tap sign-up shows as a `position: fixed` popup that overlays your website. This can frustrate your users if it occludes important information or navigation. Users may also be confused if this is the first time they've seen Google One-tap sign-up, since most ["Sign in with Google"](https://developers.google.com/identity/branding-guidelines) experiences today are along side a traditional sign up form, not isolated in their own popup.

![Screenshot of hipmunk.com with Google One-tap sign-up overlayed](https://user-images.githubusercontent.com/709153/39146066-87996ae0-46ea-11e8-9276-51f980588673.png)
*Example from hipmunk.com showing Google One-tap's out-of-the-box experience.*

## Solution

We recommend wrapping Google One-tap in an `<iframe>` so you can include it inline with your own sign up form, or wherever makes sense for your website.

![GIF of the Google account picker rendering inline with your own sign up form](https://user-images.githubusercontent.com/709153/39495663-0fbc51b0-4d50-11e8-9f3e-0471f5eaf8b9.gif)

## Technical Details

Google One-tap sign-up works by inserting an `<iframe>` into your document's `<body>` with `position: fixed` and `z-index: 9999` to overlay your website. Under the hood, Google One-tap sign-up is based on [OpenYOLO-Web](https://github.com/openid/OpenYOLO-Web), which fortunately permits you to embed it within *another* `<iframe>` that you control. See [GoogleYoloIframed](https://github.com/TMSCH/GoogleYoloIframed) for a basic example.

This demo builds on GoogleYoloIframed by accounting for responsive design (so the Google account picker can be set to `width: 100%`) and expanding height (if the user clicks the `2 more accounts` button to reveal all their Google accounts).

This behavior is mostly implemented by [`google-yolo-iframe.html`](google-yolo-iframe.html). It's used like:

```
<iframe id="google-iframe" src="google-yolo-iframe.html"></iframe>
```

In the place of the standard `onGoogleYoloLoad` [callback handlers](https://developers.google.com/identity/one-tap/web/retrieve-hints#handle_the_hint_request_result), you'll instead register for `window.addEventListener('message', () => { /* handler here */ })`, which catches events from `google-yolo-iframe.html`.

When `event.data.type === 'height'` is caught, this means GoogleYolo's iframe has changed height. Be sure to update `google-iframe`'s height.
