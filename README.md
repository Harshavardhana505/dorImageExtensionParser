# DOR – Digital Output Raster

**DOR (Digital Output Raster)** is a minimalist, text-based image format designed for procedural art, real-time canvas rendering, and raw experimentation. It stores image data as base64-encoded RGB bytes, with a plain header defining dimensions.

This format was created for developers and creators who want full control over the pixel pipeline without relying on bloated standards, compression artifacts, or locked-down tools.

---

## Format Overview

A `.dor` file has two parts:

* `width`, `height`: dimensions of the image in pixels
* `BASE64DATA`: raw RGB data, encoded in base64 (3 bytes per pixel: R, G, B)

No alpha channel, no metadata, no compression. Just pixels.

### Example

```text
|h(4,4)|~QUJDREVGR0hJSktMTU5PUA==
```

---

## Key Features

* Fully human-readable
* Canvas-native — integrates directly with HTML5 `<canvas>`
* No dependencies — parse and draw in pure JS or any language
* Zero compression artifacts — perfect for pixel art or precise rendering
* Ideal for procedural art — simple to generate, mutate, and animate

---

## Intended Use Cases

* Pixel art editors
* Web-based drawing tools
* Procedural image generation
* Saving canvas data in editable text files
* Real-time image animation
* Minimalist game assets and sprite formats
* Education — teaching rendering without format complexity

---

## Advantages Over Traditional Formats

| PNG / JPEG / BMP            | `.dor`                        |
| --------------------------- | ----------------------------- |
| Binary, opaque              | Plain-text, readable          |
| Compressed                  | Raw RGB data                  |
| Metadata-heavy              | Zero metadata                 |
| Requires decoders           | Parse in < 10 lines of JS     |
| Not editable                | Editable in any text editor   |
| Hard to procedurally mutate | Built for procedural mutation |

---

## Basic Rendering (HTML Canvas Example)

```js
let base64 = "QUJDREVGR0hJSktMTU5PUA=="; // from file
let binary = atob(base64);
let imageData = ctx.createImageData(width, height);
let p = 0;

for (let i = 0; i < binary.length; i += 3) {
  imageData.data[p++] = binary.charCodeAt(i);     // R
  imageData.data[p++] = binary.charCodeAt(i + 1); // G
  imageData.data[p++] = binary.charCodeAt(i + 2); // B
  imageData.data[p++] = 255;                      // A (default)
}

ctx.putImageData(imageData, 0, 0);
```

---

## Known Limitations

* No alpha channel (transparency is not supported yet)
* No compression — base64 increases size \~33%
* No layers, blend modes, or metadata
* Not suitable for photographic media or color-rich photography

---

## Future Challenges & Expansion Goals

The `.dor` format is intentionally limited to invite experimentation. These are open technical challenges meant to guide extensions and inspire new formats or systems based on `.dor`.

### 1. Add Layer Support (Optional Format Extension)

**Challenge:** Define a clean, minimal way to support multiple layers, with optional opacity and blend modes, while keeping the format human-readable.

### 2. Procedural Animation with `.dor`

**Challenge:** Create an animation system using sequences of `.dor` files or a new `.dorseq` format. Handle timing, frame control, and memory efficiency.

Ideas:

* Fixed frame timing (e.g. 24 FPS)
* Frame metadata (delay, name, label)
* Loop control and palette cycling

### 3. Extend the Concept to Audio

**Challenge:** Design a `.dor-audio` format that mirrors `.dor`’s simplicity — raw, base64-encoded audio samples with optional headers.

Consider:

* Sample rate (e.g. 44100 Hz)
* Number of channels (stereo or mono)
* Format: 8-bit or 16-bit PCM
* Base64 for direct in-browser use

### 4. Extend the Concept to Video

**Challenge:** Build a basic `.dorvid` container that sequences `.dor` images + audio metadata. Should play in-browser using canvas and Web Audio APIs.

---

## Philosophy

DOR is not here to compete with PNG or JPEG.

It’s here for:

* Hackers
* Artists
* Indie tool builders
* Developers who want transparent, inspectable media formats

**Readable. Writable. Predictable. Portable.**
If you can parse a string, you can load a `.dor`.

---

## License

MIT — free to use, modify, fork, and break.

---

## Author

Developed by **Harshavardhana**, who wanted a format that puts control back in the hands of creators, not corporations or closed codecs.

---

## Contributions

Ideas, critiques, forks, tools, readers, and writers are welcome.
Post issues or pull requests if you're extending the format, building tools around it, or testing new encodings.
