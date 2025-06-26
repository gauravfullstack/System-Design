# 🔍 LLD Chapter 7: **Autosuggest Search Bar**

> A core component in modern UIs (e.g, Amazon, Google, YouTube) that provides instant suggestions as the user types.

----

## ✅ Functional Requirements

| Feature                 | Description                          |
| ----------------------- | ------------------------------------ |
| Live Suggestion List    | Fetch suggestions as the user types  |
| Debounced API Calls     | Avoid API calls on every keystroke   |
| Keyboard Navigation     | Navigate suggestions with ↑ ↓ keys   |
| Mouse Selection         | Click on a suggestion to select      |
| Highlight Matching Text | Bold or highlight matched part       |
| Loading & Error States  | Show spinner or error messages       |
| Empty State             | Show message if no suggestions found |

---

## 🔐 Non-Functional Requirements

| Concern        | Strategy                                                |
| -------------- | ------------------------------------------------------- |
| Performance    | Debouncing, caching, min character limit                |
| UX             | Instant feedback, accessibility, graceful fallback      |
| Accessibility  | `aria` tags, keyboard support, focus management         |
| Reusability    | Generic `<AutoSuggest />` component with flexible props |
| Mobile Support | Full touch interaction, compact suggestion dropdown     |

---

## 🧱 Folder Structure

```
/components/autosuggest
  AutoSuggest.tsx
  useAutoSuggest.ts
  autosuggest.types.ts
```

---

## 🧾 TypeScript Types

```ts
export interface AutoSuggestProps {
  fetchSuggestions: (query: string) => Promise<string[]>;
  placeholder?: string;
  onSelect?: (value: string) => void;
  minChar?: number;
}
```

---

## ⚙️ Debounced Fetch Logic (Custom Hook)

```ts
import { useState, useEffect } from 'react';

export const useAutoSuggest = (query: string, fetchFn: (query: string) => Promise<string[]>, delay = 300) => {
  const [suggestions, setSuggestions] = useState<string[]>([]);
  const [loading, setLoading] = useState(false);

  useEffect(() => {
    if (query.length < 2) return;

    const timeout = setTimeout(() => {
      setLoading(true);
      fetchFn(query)
        .then((data) => setSuggestions(data))
        .catch(() => setSuggestions([]))
        .finally(() => setLoading(false));
    }, delay);

    return () => clearTimeout(timeout);
  }, [query]);

  return { suggestions, loading };
};
```

---

## 🖼 UI Component

```tsx
import React, { useState } from 'react';
import { useAutoSuggest } from './useAutoSuggest';

export const AutoSuggest = ({ fetchSuggestions, placeholder = "Search...", onSelect }: AutoSuggestProps) => {
  const [query, setQuery] = useState("");
  const { suggestions, loading } = useAutoSuggest(query, fetchSuggestions);

  return (
    <div className="relative w-full max-w-md mx-auto">
      <input
        type="text"
        placeholder={placeholder}
        value={query}
        onChange={(e) => setQuery(e.target.value)}
        className="w-full border px-4 py-2 rounded shadow"
      />
      {loading && <div className="absolute right-4 top-2">⏳</div>}

      {suggestions.length > 0 && (
        <ul className="absolute bg-white shadow w-full mt-1 border rounded max-h-60 overflow-auto z-10">
          {suggestions.map((item, i) => (
            <li
              key={i}
              onClick={() => {
                setQuery(item);
                onSelect?.(item);
              }}
              className="p-2 hover:bg-gray-200 cursor-pointer"
            >
              {item}
            </li>
          ))}
        </ul>
      )}
    </div>
  );
};
```

---

## 🚀 Optimizations

| Feature                 | How to Achieve                                                           |
| ----------------------- | ------------------------------------------------------------------------ |
| **Debounce**            | Avoid calling API on every keystroke                                     |
| **Min Characters**      | Skip API calls if query is under 2 chars                                 |
| **Caching**             | Store previous queries in memory to reduce API hits                      |
| **Keyboard Navigation** | Support ↑ ↓ arrow keys to navigate suggestions                           |
| **SSR / SEO**           | SSR not needed for search UI; important for search **results page** only |
| **Loading States**      | Add shimmer or loader while fetching                                     |

---

## 🧠 Interview Tips

* How would you make this component reusable across app?
* What happens if 3rd API fails or is slow?
* How would you show personalized suggestions?
* Can you optimize network requests further (like aborting prev calls)?
* How would you integrate this with GraphQL search?

---

## 🧪 Testing Checklist

* ✅ Renders input and calls fetch on typing
* ✅ Debounces API calls
* ✅ Shows suggestions
* ✅ Supports click selection
* ✅ Shows loading and error state
* ✅ Keyboard support (up/down/enter)
* ✅ Edge case: empty result, slow response

---