# ▣ Airgap·QR

**Camera-scanned file transfer that never touches a network.**

A single HTML file that turns any screen and camera into a file transfer link. One device displays a stream of animated QR codes, another device points its camera at the screen and reconstructs the file. No wifi, no Bluetooth, no server, no cloud in between, just light.

## How it works

- The file is split into small chunks and encoded as a looping sequence of QR codes.
- Each frame packs **three QR codes into one image**, one per color channel (red, green, blue), so a single scan pulls in three chunks instead of one.
- A header frame carries the filename, size, and a SHA-256 hash, so the receiving side can verify the file arrived intact.
- The sequence loops continuously. Start scanning whenever you like and missed frames just come back around.

## Using it

**Send**
1. Open the page, switch to **TX — Send**.
2. Drop in a file.
3. Hit **Start transmission** and hold the screen up to the receiving camera.

**Receive**
1. Switch to **RX — Receive** on the other device.
2. Hit **Start scanning** and point the camera at the sending screen, filling as much of the frame as you can.
3. Once every chunk arrives, the file is verified and offered as a download automatically.

Speed and density are both adjustable, trade a bit of reliability for throughput if your lighting and camera are steady.

> Best suited to small files, a few hundred KB up to a couple MB. QR-over-camera has real throughput limits no matter how it's colored.

## Running it

It's a static, dependency-free HTML file, so any static host works. The one thing to know: scanning needs camera access, and browsers only grant that over `https://` or `localhost`, not a bare local file.

The easiest option on GitHub:

1. Push this file to a repo (as `index.html` for the cleanest URL).
2. Enable **Settings → Pages → Deploy from branch**.
3. Open `https://<username>.github.io/<repo>/` on any device with a camera.

## Built with

- [qrcode-generator](https://github.com/kazuhikoarase/qrcode-generator) for encoding
- [jsQR](https://github.com/cozmo/jsQR) for decoding
- No build step, no framework, no backend

## License

MIT
