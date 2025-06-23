# 📂 LLD Chapter 5: Accordion Component Design (System Design + Code)

---

## ✅ What is an Accordion?

An **Accordion** is a vertically stacked set of expandable items. Each item can be toggled open to reveal hidden content, while others may collapse.

Popular use cases:

* FAQ sections
* Product detail panels
* Sidebar filters

---

## 🧠 Functional Requirements

| Feature                 | Description                               |
| ----------------------- | ----------------------------------------- |
| Expand/Collapse         | Toggle sections open/closed               |
| Single vs Multiple Open | Configurable option (like FAQ vs sidebar) |
| Keyboard Accessibility  | Navigate using arrows, Enter, Space       |
| Animation Support       | Smooth open/close transitions             |

---

## 🛠 Component Structure

```tsx
<Accordion allowMultipleOpen>
  <AccordionItem title="Shipping Info">Content here</AccordionItem>
  <AccordionItem title="Returns Policy">More content</AccordionItem>
</Accordion>
```

---

## 🧱 System Design (Frontend)

### Folder Structure

```
/components/accordion
  Accordion.tsx
  AccordionItem.tsx
  useAccordion.ts
  accordion.types.ts
```

### TypeScript Types

```ts
export interface AccordionProps {
  children: ReactNode;
  allowMultipleOpen?: boolean;
}

export interface AccordionItemProps {
  title: string;
  children: ReactNode;
  index: number;
  isOpen: boolean;
  toggle: (index: number) => void;
}
```

---

## ⚙️ Component Logic (Custom Hook)

### useAccordion.ts

```ts
export const useAccordion = (count: number, allowMultiple: boolean) => {
  const [openIndexes, setOpenIndexes] = useState<number[]>([]);

  const toggle = (index: number) => {
    setOpenIndexes((prev) => {
      if (allowMultiple) {
        return prev.includes(index)
          ? prev.filter((i) => i !== index)
          : [...prev, index];
      } else {
        return prev.includes(index) ? [] : [index];
      }
    });
  };

  return { openIndexes, toggle };
};
```

---

## 📦 Component Files

### Accordion.tsx

```tsx
export const Accordion = ({ children, allowMultipleOpen = false }: AccordionProps) => {
  const count = React.Children.count(children);
  const { openIndexes, toggle } = useAccordion(count, allowMultipleOpen);

  return (
    <div className="rounded-xl shadow-md">
      {React.Children.map(children, (child, index) =>
        React.cloneElement(child as React.ReactElement<any>, {
          index,
          isOpen: openIndexes.includes(index),
          toggle,
        })
      )}
    </div>
  );
};
```

---

### AccordionItem.tsx

```tsx
export const AccordionItem = ({ title, children, index, isOpen, toggle }: AccordionItemProps) => {
  return (
    <div className="border-b">
      <button
        onClick={() => toggle(index)}
        className="w-full p-4 text-left font-medium"
        aria-expanded={isOpen}
      >
        {title}
      </button>
      {isOpen && <div className="p-4 bg-gray-100 transition-all">{children}</div>}
    </div>
  );
};
```

---

## ♿️ Accessibility Best Practices

| Feature         | Implementation                        |
| --------------- | ------------------------------------- |
| Keyboard nav    | Arrow key support to navigate items   |
| `aria-expanded` | Add to button for screen readers      |
| `role="region"` | Optional for expanded content section |

---

## 🎨 Optimization & UX

| Feature               | Tip                                     |
| --------------------- | --------------------------------------- |
| 🔁 Virtualization     | For huge FAQs, use `react-virtualized`  |
| 🎞 Smooth Animations  | Use CSS transitions or `framer-motion`  |
| 🔧 Server Side Render | Can hydrate static accordions for SEO   |
| 🧪 Unit Testing       | Test toggle logic, props, accessibility |

---

## 🔍 Common Interview Questions

* How would you handle deep nesting in an accordion?
* What if accordion content is fetched lazily?
* How to persist open state on route change?
* How to animate open/close content smoothly?

---

## 🚀 Advanced Enhancements

| Feature                     | Description                                  |
| --------------------------- | -------------------------------------------- |
| Async Content               | Fetch inner content on toggle (lazy loading) |
| Controlled vs Uncontrolled  | Prop-driven vs internal state                |
| Server-controlled Accordion | Toggle open sections via API                 |

---
