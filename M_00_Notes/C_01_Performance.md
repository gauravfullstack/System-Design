
---

# 📘 Frontend System Design: **Performance Optimization Concepts**

---

## 🔷 1. **Above the Fold (Critical Rendering Path)**

### ✅ What is "Above the Fold"?

> The portion of the UI visible **without scrolling** when the page loads.

⚡ Users judge performance based on how fast they see above-the-fold content.

---

### 🧠 Key Optimization Strategies

| Technique    | What It Does                                                      |
| ------------ | ----------------------------------------------------------------- |
| **Defer**    | Loads JS *after* HTML is parsed. Doesn’t block rendering.         |
| **Async**    | Loads JS in parallel but executes as soon as it's downloaded.     |
| **Prefetch** | Tells browser to pre-download a resource (for future navigation). |

---

### 📌 Use in Practice (Next.js example):

```tsx
<script src="/analytics.js" defer></script>
<link rel="preload" href="/fonts/font.woff2" as="font" />
<link rel="prefetch" href="/about" />
```

✅ Prioritize rendering above-the-fold content
✅ Lazy-load everything else

---

## 🟩 2. **WebP Image Format**

### ✅ What is WebP?

> A modern image format developed by Google — **smaller** and **faster** than JPEG/PNG.

| Format   | Size (Typical)           | Support           |
| -------- | ------------------------ | ----------------- |
| PNG      | Large                    | ✅ All             |
| JPEG     | Medium                   | ✅ All             |
| **WebP** | Smallest (\~30% smaller) | ✅ Modern Browsers |

---

### 🔥 Benefits

* Faster load times
* Better Core Web Vitals
* Smaller CDN bandwidth

---

### 🛠 How to Use in React / Next.js:

```tsx
<Image
  src="/photo.webp"
  alt="Post"
  width={500}
  height={300}
  loading="lazy"
  priority
/>
```

✅ Bonus: Use `<picture>` + fallback for legacy browsers.

---

## 🌍 3. **CDN (Content Delivery Network) & Service Worker**

### ✅ What is a CDN?

> A geographically distributed set of servers that cache and deliver static files (HTML, JS, CSS, images).

| Benefit          | Why it Matters                   |
| ---------------- | -------------------------------- |
| Faster load time | Content served from nearest edge |
| Scalable         | Handles heavy traffic easily     |
| Secure           | Comes with SSL + DDoS protection |

---

### ✅ What is a Service Worker?

> JS file that runs in the background and **caches resources** offline or for faster access.

Used for:

* Offline support (PWA)
* Caching strategies (cache-first, network-first)
* Background sync

```ts
self.addEventListener('fetch', (event) => {
  event.respondWith(
    caches.match(event.request).then(res => res || fetch(event.request))
  );
});
```

---

## 🖼️ 4. **Image Priority (Critical Images First)**

### ✅ What is Image Priority?

> Tell browser which images are **critical** to load first — usually images **above the fold**.

In **Next.js**:

```tsx
<Image
  src="/hero.jpg"
  width={800}
  height={400}
  priority
/>
```

✅ Reduces **Largest Contentful Paint (LCP)**
✅ Improves Core Web Vitals

---

## 📱 5. **DPI (Dots Per Inch)**

### ✅ What is DPI?

> A measure of **screen pixel density**. Higher DPI = sharper image.

| DPI Level | Device Type             |
| --------- | ----------------------- |
| 72        | Low-end desktop         |
| 160+ (1x) | Standard mobile/desktop |
| 320+ (2x) | Retina, iPhones         |
| 480+ (3x) | Modern Android phones   |

---

### 🔧 Solution: Use `srcSet` or `<Image>` component to load right resolution

```html
<img
  src="img@1x.png"
  srcset="img@2x.png 2x, img@3x.png 3x"
  alt="Sharp Image"
/>
```

✅ Saves bandwidth on low-DPI screens
✅ Sharp rendering on high-DPI devices

---

## ⚙️ 6. **Adaptive Loading**

### ✅ What is Adaptive Loading?

> Load only what the user needs, based on **device, network speed, and CPU power**.

| Condition      | Action                          |
| -------------- | ------------------------------- |
| Slow network   | Serve compressed/low-res images |
| Low-end device | Reduce animation or FPS         |
| Background tab | Pause expensive JS tasks        |

---

### 🔍 Check Capabilities in JS:

```ts
if (navigator.connection.effectiveType === "2g") {
  // Load lighter assets
}
```

Or use libraries like [React Adaptive Loading](https://github.com/GoogleChromeLabs/react-adaptive-loading)

---

## 🚀 Summary Cheat Sheet

| Concept             | Use When                              |
| ------------------- | ------------------------------------- |
| Above the Fold      | Speed up perceived load               |
| WebP                | Optimize image size & quality         |
| CDN / ServiceWorker | Improve speed, scale, offline support |
| Image Priority      | Improve LCP                           |
| DPI & srcSet        | Optimize images per screen            |
| Adaptive Loading    | Adjust experience to device/network   |

---

