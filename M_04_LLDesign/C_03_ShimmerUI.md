# ✨ LLD Chapter 3: Shimmer UI (Skeleton Loading)

---

## 🔍 What is Shimmer UI?

**Shimmer UI**, also called **Skeleton Loading**, is a design pattern used to show a **placeholder (UI skeleton)** while the real content is loading.

Instead of showing a blank screen or a spinner, we display greyed-out blocks that **mimic the layout of actual content**, creating a **perceived performance boost**.

---

## 🎯 Why Use Shimmer UI?

| 🚫 Problem Without Shimmer       | ✅ Benefit With Shimmer UI              |
| -------------------------------- | -------------------------------------- |
| Spinner shows no content context | Mimics actual layout, improves UX      |
| User sees blank screen           | Keeps user engaged, content feels fast |
| Poor perceived performance       | Looks like app is responsive           |

---

## 📱 Real-World Examples

| App           | Shimmer Usage Example              |
| ------------- | ---------------------------------- |
| Facebook      | Loading posts (skeleton cards)     |
| LinkedIn      | Profile preview shimmer            |
| Instagram     | Grid/feed skeleton boxes           |
| YouTube       | Video card shimmers before loading |
| Zomato/Swiggy | Restaurant or item skeletons       |

---

## 🧱 Core Components of Shimmer UI

1. **Skeleton Layout**

   * A placeholder UI matching the shape of actual content.
   * Use rectangles/circles for images, lines for text.

2. **Shimmer Animation**

   * Horizontal light sweep animation gives loading effect.

3. **Conditional Rendering**

   * Show shimmer if `loading === true`, else show actual UI.

---

## ⚙️ Implementation in React (Basic)

### 1. Skeleton UI (No Animation)

```tsx
export const SkeletonCard = () => (
  <div className="w-full p-4 border rounded-md animate-pulse">
    <div className="h-48 bg-gray-300 rounded-md" />
    <div className="mt-4 h-4 bg-gray-300 rounded" />
    <div className="mt-2 h-4 bg-gray-300 rounded w-3/4" />
  </div>
);
```

### 2. Use With Conditional Rendering

```tsx
{
  isLoading
    ? <SkeletonCard />
    : <ActualCard data={data} />
}
```

---

## 💡 Tips for Production-Grade Shimmer

| ✅ Best Practice                          | 🧠 Reason                              |
| ---------------------------------------- | -------------------------------------- |
| Match actual layout closely              | Improves illusion of performance       |
| Animate (e.g., shimmer sweep)            | More dynamic and modern UX             |
| Avoid heavy layout shifts                | Minimize CLS (Cumulative Layout Shift) |
| Keep it lightweight                      | Don’t overuse gradients, CSS load      |
| Group skeletons into reusable components | Reuse across feed/grid/list screens    |

---

## ✨ CSS Shimmer Animation (Optional)

```css
.shimmer {
  background: linear-gradient(
    to right,
    #eeeeee 0%,
    #dddddd 50%,
    #eeeeee 100%
  );
  background-size: 200% 100%;
  animation: shimmer 1.5s infinite;
}

@keyframes shimmer {
  0% { background-position: -200% 0; }
  100% { background-position: 200% 0; }
}
```

Apply this class to skeleton elements.

---

## 🧪 Testing Best Practices

* Snapshot testing of loading state
* Write separate tests for loading, success, and error states

---

## 🎯 Frontend System Design Interview Angle

**Question**: *“How would you handle loading states in a feed UI with high perceived performance?”*

**Expected Answer**:

> I’d use **Shimmer UI (skeleton screens)** that closely match the real feed card layout, possibly with a shimmer animation. This gives users a fast and consistent visual experience.

---

## 🛠️ Component Design Reusability

```tsx
<SkeletonLoader
  type="card"
  lines={3}
  image={true}
/>
```

Make a generic `<SkeletonLoader />` component that can be configured for various use cases (card, list, profile).

---

## 🧠 Extra Credit

* Use libraries like `react-content-loader` for SVG skeletons
* SSR Consideration: preload shimmer UI for fast Time-to-First-Paint
* Use **React Suspense + Lazy + Fallback** for async boundaries

---
