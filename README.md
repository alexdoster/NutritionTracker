# Macros

A photo based calorie and macro tracker that runs entirely in the browser. Snap a photo of your meal, the Anthropic API estimates calories, protein, carbs, and fat, and progress bars show how you are tracking against your daily targets. Everything is stored on your phone. There is no server and no account.

## How it works

1. First launch asks for your Anthropic API key and your stats (age, weight, height, activity, goal).
2. It calculates daily targets using the Mifflin St Jeor formula. You can edit any number before saving.
3. Tap "Snap a meal", take a photo, and review the estimate before adding it to your day.
4. Four progress bars track calories, protein, carbs, and fat. They reset automatically each day.
5. Prefer typing? Tap "Quick add", type a food name, and tap "Look up" to pull calories and macros from the USDA FoodData Central database. No photo and no Anthropic API call needed.

Your API key, targets, and food log live in the browser's local storage on your phone. Nothing leaves the device except the meal photo, which goes directly to the Anthropic API.

## Testing on your Mac

From this folder, run:

```
python3 -m http.server 8000
```

Then open http://localhost:8000 in a browser. You can test everything except the camera, which uses the file picker on desktop.

## Putting it on your iPhone

The easiest path is GitHub Pages, the same hosting as your portfolio site.

1. Create a new GitHub repository, for example `macros`.
2. Upload the four files in this folder (index.html, manifest.json, apple-touch-icon.png, README.md).
3. In the repo, go to Settings, then Pages, and set the source to the main branch.
4. Open the published URL in Safari on your iPhone.
5. Tap the Share button, then "Add to Home Screen". It will launch full screen like a native app.

## Notes on the API key

- Create a dedicated key for this app at console.anthropic.com and set a low monthly spend limit on it. If the phone is ever lost, revoke that one key.
- The key is stored in the browser's local storage on your device. Do not commit the key to the GitHub repo. The repo only contains the app files, which are safe to publish.
- Each photo analysis is one API call to claude-opus-4-8. Typical cost is a few cents per meal.

## Notes on food lookup

- The "Look up" button on Quick add calls the USDA FoodData Central API, a free public nutrition database. It's separate from the Anthropic API and costs nothing.
- Works out of the box on a shared, low free tier. If it gets rate limited, grab a free key at fdc.nal.usda.gov/api-key-signup and paste it into Settings under "USDA food lookup key" for a much higher personal limit.
- It fills calories, protein, carbs, and fat for a typical serving (like "1 large" for an egg). Adjust the numbers if your portion is different.

## Files

- `index.html` is the entire app (layout, styles, and logic in one file)
- `manifest.json` tells iOS to run it as a standalone app
- `apple-touch-icon.png` is the home screen icon
