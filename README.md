# Smart Road AI – Mobile Pothole Reporting Prototype

## What this prototype does
- Captures a road photo using an Android phone camera or image picker.
- Requests GPS coordinates with accuracy information.
- Stores pothole reports locally in the browser.
- Classifies severity using a user-selected category, optionally suggested from AI bounding-box area.
- Shows GPS-tagged reports on an OpenStreetMap map.
- Provides a dashboard, status updates, deletion, and CSV export.
- Supports optional Roboflow hosted object-detection inference.

## Important AI note
The app does NOT contain trained model weights. Real automatic pothole detection requires a trained pothole object-detection model. In AI Setup, configure a compatible Roboflow model ID (for example `your-project/1`) and API key. The model must return predictions with bounding boxes. If you do not configure a model, camera/GPS/report/map features still work, but detection is manual and must not be presented as AI output.

The bounding-box area severity suggestion is only a rough visual proxy. It does not measure pothole depth or establish engineering safety.

## Run on Android
1. Extract the ZIP.
2. Host the `smart_road_ai` folder on an HTTPS static host such as GitHub Pages or Netlify. Camera and GPS permissions generally require HTTPS (or localhost).
3. Open the HTTPS URL in Chrome on Android.
4. Allow camera/photo and location permissions.
5. Use **Open camera**, then **Get GPS**, choose severity, and submit.
6. Open **Map** and **Dashboard** to inspect reports.

You can also run a local development server from a computer:
`python -m http.server 8000`
Then open `http://<computer-LAN-IP>:8000` on the phone. Note: non-HTTPS LAN URLs may block camera/geolocation; use an HTTPS host for reliable phone testing.

## Configure AI inference
1. Create or select a pothole object-detection project in Roboflow.
2. Upload and annotate pothole images; train a model.
3. Deploy the model using a compatible hosted inference endpoint.
4. In the app, open **AI Setup** and enter the model ID and API key.
5. Test with a road photo and verify the predictions.

Security: the API key is stored in local browser storage and sent from the phone. This is acceptable only for a private demonstration device. For a public deployment, create a small backend proxy and keep the API key on the server. Check the provider's current endpoint, authentication, CORS, and pricing documentation.

## Limitations
- Data is stored only on the current phone/browser; there is no shared cloud database.
- Reports do not automatically reach municipal authorities.
- GPS can be inaccurate in dense urban areas.
- Severity is not a certified measurement.
- Internet is required for map tiles and hosted AI inference.
