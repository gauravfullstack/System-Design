# 🔁 LLD Chapter 4: Infinite Scroll (Frontend System Design)

---

## 🔍 What is Infinite Scroll?

**Infinite Scroll** is a UX pattern where **content loads automatically as the user scrolls down**, without needing to click a “Next” or “Load More” button.

Popular in:

* Instagram, Twitter (Feed)
* YouTube (Videos)
* Flipkart, Amazon (Products)

---

## 🚫 Traditional Pagination vs 🔁 Infinite Scroll

| Pagination            | Infinite Scroll                   |
| --------------------- | --------------------------------- |
| User clicks buttons   | Content loads automatically       |
| Slower UX             | Seamless, fast content experience |
| SEO friendly          | Harder to manage SEO              |
| Easy state management | Complex scroll/event handling     |

---

## 🎯 Why Use Infinite Scroll?

| Benefit                  | Description                               |
| ------------------------ | ----------------------------------------- |
| 🔄 Seamless UX           | Feels continuous, no clicks               |
| ⚡️ Perceived Performance | User always sees fresh content            |
| 📱 Ideal for Mobile Apps | Less interaction needed                   |
| 💰 Improves Engagement   | Users scroll more = more time on platform |

---

## 🧱 Core Building Blocks

1. **Data Source (Paginated API)**
   API should support:

   ```http
   GET /posts?page=2&limit=10
   ```

2. **Scroll Trigger**
   Detect when user reaches **near bottom** of the list.

3. **Fetch More**
   Load next batch & append to existing list.

4. **Loading Indicator / Shimmer**

5. **End of List Handling**

---

## ⚙️ Implementation Plan (React + TS)

### 1. Define API Function

```ts
const fetchPosts = async (page: number) => {
  const res = await fetch(`/api/posts?page=${page}&limit=10`);
  return res.json();
};
```

---

### 2. Component with Scroll Hook (IntersectionObserver)

```tsx
import { useEffect, useRef, useState } from "react";

export const InfiniteFeed = () => {
  const [page, setPage] = useState(1);
  const [posts, setPosts] = useState([]);
  const [loading, setLoading] = useState(false);
  const loaderRef = useRef(null);

  useEffect(() => {
    const loadPosts = async () => {
      setLoading(true);
      const data = await fetchPosts(page);
      setPosts((prev) => [...prev, ...data]);
      setLoading(false);
    };
    loadPosts();
  }, [page]);

  useEffect(() => {
    const observer = new IntersectionObserver(
      (entries) => {
        if (entries[0].isIntersecting && !loading) {
          setPage((prev) => prev + 1);
        }
      },
      { threshold: 1 }
    );
    if (loaderRef.current) observer.observe(loaderRef.current);
    return () => observer.disconnect();
  }, [loading]);

  return (
    <div>
      {posts.map((post) => (
        <PostCard key={post.id} {...post} />
      ))}
      <div ref={loaderRef}>{loading && <SkeletonPost />}</div>
    </div>
  );
};
```

---

## 🧠 Key Interview Concepts

| System Design Angle   | Explanation                                                         |
| --------------------- | ------------------------------------------------------------------- |
| Scroll-based triggers | Use `IntersectionObserver`, not scroll events                       |
| API rate-limiting     | Avoid flooding server with fetches                                  |
| UX fallback           | Add “Load More” for devices that don’t support IntersectionObserver |
| SSR + hydration       | First page SSR, rest via infinite scroll                            |
| Debounce + Throttle   | Prevent rapid fetches while scrolling                               |
| Shimmer UI            | Add for better perceived performance                                |

---

## 🔍 Optimization Techniques

| Optimization         | How?                                     |
| -------------------- | ---------------------------------------- |
| 🧠 Memoized Lists    | Use `React.memo`, `key` prop properly    |
| 🪄 Virtualization    | Use `react-window` / `react-virtualized` |
| 🎯 Lazy Load Images  | `loading="lazy"`, use `srcset`, CDN      |
| 🛑 End of List Check | Use `hasMore` flag from backend          |

---

## 📦 Libraries You Can Use

| Library                       | Purpose                       |
| ----------------------------- | ----------------------------- |
| `react-intersection-observer` | Scroll detection              |
| `react-query` / `tanstack`    | Data fetching + caching       |
| `react-window`                | Virtual scroll for huge lists |

---

## 🧪 Testing Strategy

| Test Type   | What to test                    |
| ----------- | ------------------------------- |
| Unit        | Intersection logic, fetch logic |
| Integration | Posts append properly on scroll |
| Edge Case   | Show “No More Posts” at end     |
| Performance | Ensure no layout thrashing      |

---

## 📍 Real-World Use Case Breakdown

| App       | API Param Used        | Scroll Strategy        |
| --------- | --------------------- | ---------------------- |
| Instagram | `cursor` (pagination) | `IntersectionObserver` |
| YouTube   | `nextPageToken`       | Infinite Feed          |
| Flipkart  | `offset`              | Infinite Product Load  |

---
