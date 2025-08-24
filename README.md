# Chrome Offline T‑Rex Game — Farcaster Miniapp

This project packages the classic Chrome “No Internet” T‑Rex game as a Farcaster miniapp. It runs entirely client‑side, includes all assets encoded inline, and signals readiness to the Farcaster SDK to enable miniapp controls.

## Features

- 🎮 Play the familiar T‑Rex runner without an internet connection.
- ✅ Integrates with Farcaster via the `fc:miniapp` `<meta>` tag.
- 📱 Calls `sdk.actions.ready()` once the DOM is loaded, ensuring the miniapp is flagged as ready.
- 🖼️ All images and sounds embedded via Base64, so there are no external dependencies.
- 💅 Responsive layout with mobile support.

## File Structure

```
index.html     # Main HTML file containing the game and Farcaster metadata
script.js      # Full T‑Rex game logic (includes the sdk.actions.ready call)
style.css      # Styles for the game and miniapp
```

## Quick Start

To host or test the miniapp locally:

1. Place `index.html`, `script.js`, and `style.css` in the same directory.
2. Open `index.html` in a modern browser (Chrome/Edge/Firefox).
3. The game should start immediately. Use the **Space** bar to jump and the **Down Arrow** to duck.

If you deploy these files via a web server (e.g. GitHub Pages, Vercel, Netlify), Farcaster will be able to embed your miniapp. Make sure the base URL matches the `url` specified in the `fc:miniapp` metadata.

## Farcaster Integration Details

The `<meta name="fc:miniapp">` tag in `index.html` defines how the miniapp appears in Farcaster clients. Here’s an example:

```html
<meta name="fc:miniapp" content='{
  "version": "1",
  "imageUrl": "https://chrome-offline-game.vercel.app/image.GIF",
  "button": {
    "title": "Play Now",
    "action": {
      "type": "launch_frame",
      "name": "T-rex Game",
      "url": "https://chrome-offline-game.vercel.app",
      "splashImageUrl": "https://chrome-offline-game.vercel.app/splash.png",
      "splashBackgroundColor": "#111111"
    }
  }
}'> 
```

- **version**: The Farcaster miniapp version (currently `"1"`).
- **imageUrl**: A 1:1 ratio thumbnail that represents your app.
- **button.title**: The label on the miniapp call‑to‑action button.
- **button.action**: Describes how to launch the miniapp:
  - `type`: Always `"launch_frame"`.
  - `name`: Display name in the launch frame.
  - `url`: The URL of your hosted miniapp.
  - `splashImageUrl`: (Optional) Splash screen image.
  - `splashBackgroundColor`: Background color of the splash screen.

### Signalling Readiness

In `script.js`, call Farcaster’s `sdk.actions.ready()` after the game initializes:

```javascript
import { sdk } from 'https://esm.sh/@farcaster/miniapp-sdk';

window.addEventListener('DOMContentLoaded', () => {
  new Runner('.interstitial-wrapper');         // Start the game
  sdk.actions.ready({ disableNativeGestures: true }); // Notify Farcaster
});
```

This tells Farcaster your app is loaded and ready for user interaction.

## Customizing

- **Change Images**: Update the Base64 strings in `index.html` with your own assets (be sure to keep the IDs the same).
- **Meta Button**: Adjust the `fc:miniapp` metadata as needed; for example, change the `title` or the target `url`.
- **Disable Native Gestures**: Pass `disableNativeGestures: false` in the `ready()` call if you want Farcaster’s default gestures to remain active.

## Contributing

Pull requests are welcome! If you spot a bug or want to add a feature, please open an issue first to discuss what you would like to change.

## License

This miniapp is provided for educational purposes. You are free to modify and use it in your own projects. This repository is not affiliated with Google or Farcaster.
