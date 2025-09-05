# Drag & Drop File Uploader (Vanilla JS)

A lightweight, dependency-free file uploader with drag & drop, queue management, per-file progress, validation, and image thumbnails. Works **with** or **without** a server (demo simulation included). Built for modern browsers with accessibility in mind.

---

## Features

- ✅ Drag & drop **and** click-to-browse  
- ✅ Multiple files, queue UI, per-file progress bars  
- ✅ Cancel, remove, retry  
- ✅ Validation: `maxFiles`, `maxFileSize`, `allowedTypes` (supports wildcards like `image/*`)  
- ✅ Image thumbnails + generic badge for non-images  
- ✅ Works offline in **simulation mode** (no server required)  
- ✅ Real uploads via `XMLHttpRequest` + `FormData`  
- ✅ i18n-ready UI texts  
- ✅ Accessible (keyboard & ARIA), responsive, no dependencies  

---

## Files

- `index.html` — Demo page and initialization  
- `uploader.css` — Styles for the uploader UI  
- `uploader.js` — The uploader class (ES5-compatible IIFE, global export)  
- `README.md` — This documentation  

---

## Quick Start

1. Copy files into your project and include CSS/JS:

```html
<link rel="stylesheet" href="uploader.css">
<script src="uploader.js"></script>
```

2. Add a container in your HTML:

```html
<div id="uploader"></div>
```

3. Initialize:

```html
<script>
const uploader = new DragDropUploader('#uploader', {
  uploadUrl: null, // keep null to simulate (no server). Set e.g. "/api/upload" for real uploads
  allowedTypes: ['image/*', 'application/pdf'],
  maxFileSize: 5 * 1024 * 1024,
  maxFiles: 20
});
</script>
```

---

## Options

| Option            | Type          | Default                 | Description |
|-------------------|---------------|-------------------------|-------------|
| `uploadUrl`       | string\|null  | `null`                  | Endpoint for real uploads. Keep `null` to simulate client-side progress (demo mode). |
| `method`          | string        | `POST`                  | HTTP method for uploads. |
| `fieldName`       | string        | `files[]`               | Form field name used in `FormData`. |
| `headers`         | object        | `{}`                    | Extra request headers. |
| `withCredentials` | boolean       | `false`                 | Send cookies/credentials with the request. |
| `multiple`        | boolean       | `true`                  | Allow multiple file selection. |
| `autoUpload`      | boolean       | `true`                  | Start uploading immediately after adding a file. |
| `maxFiles`        | number        | `20`                    | Max files in the queue. |
| `maxFileSize`     | number        | `5 * 1024 * 1024`       | Max file size in bytes. |
| `allowedTypes`    | string[]      | `['image/*']`           | Array of MIME types (supports wildcards like `image/*`). |
| `texts`           | object        | *(see source)*          | UI texts, override for localization. |

### Callbacks

- `onAdd(file)`  
- `onRemove(file)`  
- `onProgress(file, percent)`  
- `onSuccess(file, responseText)`  
- `onError(file, message)`  
- `onQueueComplete()`  

---

## Real Uploads (Server)

Set `uploadUrl` to your endpoint. The uploader sends a `multipart/form-data` request:

- Method: `POST` (configurable)  
- Body: `FormData` with `fieldName` (default `files[]`)  
- Include any custom headers via `headers`  
- Track progress with `xhr.upload.onprogress`  

**Example pseudo backend (Node/Express):**

```js
// npm i express multer
import express from 'express';
import multer from 'multer';
const app = express();
const upload = multer({ dest: 'uploads/' });

app.post('/api/upload', upload.array('files[]'), (req, res) => {
  // Files available at req.files
  res.json({ ok: true, count: req.files.length });
});

app.listen(3000);
```

---

## Styling

- All main elements are prefixed with `.uploader__*`.  
- Edit colors via CSS variables at the top of `uploader.css`.  
- Thumbnails are constrained to **48×48 px** by default.  

---

## Accessibility

- Dropzone is keyboard-activable (`Enter`/`Space`)  
- ARIA labels and live region for list updates  

---

## Browser Support

Modern evergreen browsers (Chromium, Firefox, Safari). Uses `FormData`, `XMLHttpRequest`, and `FileReader`.

---

## License

Sold under CodeCanyon (Regular/Extended) license terms.  

---

## Changelog

**1.0.0** — Initial release.
