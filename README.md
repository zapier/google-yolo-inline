# google-yolo-inline

A [demo](https://zapier.github.io/google-yolo-inline/) showing how to seamlessly include [Google one tap sign-up](https://developers.google.com/identity/one-tap/web/overview) (a.k.a. Google Yolo) into your own sign up form.

![GIF of the Google account picker rendering inline with your own sign up form](https://cdn.zapier.com/storage/photos/b967f8451579c9de604e54ae3f18d19f.gif)

## Background

By default, Google one tap sign-up shows as a `position: fixed` popup that overlays your website. Having it detached from your standard sign up forms can lead to a confusing UX.

## Technical Details

Google one tap sign-up works by inserting an `<iframe>` into your document's `<body>` with `position: fixed` and `z-index: 9999` to overlay your website. Under the hood, Google one tap sign-up is based on [OpenYOLO-Web](https://github.com/openid/OpenYOLO-Web), which permits you to embed it within *another* `<iframe>` that you control. See [GoogleYoloIframed](https://github.com/TMSCH/GoogleYoloIframed) for a basic example.

This demo builds on GoogleYoloIframed by accounting for responsive design (so the Google account picker can be set to `width: 100%`) and expanding height (if the user clicks the `2 more accounts` button to reveal all their Google accounts).
