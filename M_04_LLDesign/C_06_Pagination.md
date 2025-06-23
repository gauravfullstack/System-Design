Awesome! Let’s now move on to the next important chapter in Low-Level Design (LLD):

---

# 📂 LLD Chapter 6: Pagination Component Design (System Design + Code)

---

## ✅ What is Pagination?

**Pagination** is a UI pattern that breaks up large data sets (like posts, products, comments) into smaller chunks (pages) that users can navigate through.

---

## 🧠 Functional Requirements

| Feature               | Description                                             |
| --------------------- | ------------------------------------------------------- |
| Page Navigation       | Buttons or links to move between pages (next, previous) |
| Page Size Control     | Option to change number of items per page (optional)    |
| Display Current Page  | Show active page clearly                                |
| Handle Loading State  | Show spinner/skeleton during data fetch                 |
| Accessible Navigation | Keyboard & screen reader support                        |

---

## 🔍 Non-Functional Requirements

* **Performance**: Efficient rendering even for 1000s of records
* **Responsiveness**: Mobile & desktop-friendly
* **Accessibility (a11y)**: Fully accessible pagination nav
* **SEO**: SSR support for paginated URLs (for blogs/products)
* **Scalability**: Easy to switch to infinite scroll or server-side pagination

---

## 📦 Component Structure

### Basic Usage

```tsx
<Pagination
  currentPage={1}
  totalPages={20}
  onPageChange={(page) => fetchData(page)}
/>
```

---

## 🧱 Frontend Architecture (Client Side)

```
/components/pagination
  Pagination.tsx
  usePagination.ts
  pagination.types.ts
```

---

### 🧾 TypeScript Types

```ts
export interface PaginationProps {
  currentPage: number;
  totalPages: number;
  onPageChange: (page: number) => void;
}
```

---

## ⚙️ Core Logic (Custom Hook)

### usePagination.ts

```ts
export const usePagination = (totalPages: number, currentPage: number) => {
  const pages = [];

  for (let i = 1; i <= totalPages; i++) {
    pages.push(i);
  }

  return pages;
};
```

---

## 🖼 Pagination UI (Component)

### Pagination.tsx

```tsx
export const Pagination = ({ currentPage, totalPages, onPageChange }: PaginationProps) => {
  const pages = usePagination(totalPages, currentPage);

  return (
    <div className="flex gap-2 items-center justify-center mt-4">
      <button
        disabled={currentPage === 1}
        onClick={() => onPageChange(currentPage - 1)}
        className="px-3 py-1 border rounded disabled:opacity-50"
      >
        Prev
      </button>

      {pages.map((page) => (
        <button
          key={page}
          onClick={() => onPageChange(page)}
          className={`px-3 py-1 border rounded ${currentPage === page ? 'bg-black text-white' : ''}`}
        >
          {page}
        </button>
      ))}

      <button
        disabled={currentPage === totalPages}
        onClick={() => onPageChange(currentPage + 1)}
        className="px-3 py-1 border rounded disabled:opacity-50"
      >
        Next
      </button>
    </div>
  );
};
```

---

## 🚀 Performance & Optimization

| Feature          | Tips                                                                         |
| ---------------- | ---------------------------------------------------------------------------- |
| SSR/SEO          | Use URL query param (`?page=2`) and SSR (Next.js) for SEO                    |
| Accessibility    | Use `aria-current`, `aria-label`, and keyboard focus trapping                |
| Skeleton Loading | Show shimmer placeholder while fetching new page data                        |
| Debounce         | Prevent multiple requests on fast clicks                                     |
| Chunk Rendering  | Only render visible items when items are heavy (combine with virtualization) |

---

## 🌐 Pagination Types

| Type                    | Use Case                                        |
| ----------------------- | ----------------------------------------------- |
| Client-side Pagination  | When entire dataset is loaded on frontend       |
| Server-side Pagination  | For large datasets, using query params          |
| Cursor-based Pagination | For APIs with dynamic data (e.g., Twitter feed) |

---

## 🔍 Interview Questions

* How to build pagination with dynamic data (e.g. filtered or sorted list)?
* How to maintain page state on route change?
* How to prefetch next page data?
* How would you implement infinite scroll in place of pagination?

---

## 🧪 Testing Considerations

* Should show correct number of page buttons
* Should call `onPageChange` with correct value
* Should disable "Prev" on page 1 and "Next" on last page
* Should highlight active page
* Should support keyboard navigation and focus management

---

## 🧠 Advanced Enhancements

| Feature           | Description                                |
| ----------------- | ------------------------------------------ |
| Page Jump         | Add input to jump to a specific page       |
| Responsive Layout | Collapse some pages on mobile view         |
| Smart Truncation  | Show only 3–5 page numbers + ellipsis (…)  |
| URL Sync          | Sync current page to URL query (`?page=2`) |

---

Would you like to:

* Add **server-side** pagination integration (e.g. with query params)?
* Learn how to switch this to **infinite scroll**?
* Or move to the next LLD chapter: **Search Bar**, **Modal**, or any topic you're ready for?

Let me know what's next!
