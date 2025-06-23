# 🧩 Low-Level Design: Component Design (LLD-01)

## ✅ What is Component Design?

> Designing **modular, reusable, testable, and performant UI units** in a scalable frontend codebase.

In **React** (or any component-based UI framework), this is **the foundation of system architecture** — just like microservices in backend.

---

## 🎯 Why It's Critical in System Design Interviews

Big tech interviewers want to evaluate:

| What They Check                                | Why                        |
| ---------------------------------------------- | -------------------------- |
| Component reusability & separation of concerns | Code scaling in large apps |
| Props & state management patterns              | Maintainability            |
| Configurability and composition                | Extensibility              |
| Performance awareness                          | UX at scale                |
| Testing + accessibility                        | Production readiness       |

---

## 🧱 1. Types of Components

### 1. **Atomic Design** Principle (Industry-standard)

| Level    | Example                   | Description          |
| -------- | ------------------------- | -------------------- |
| Atom     | `Button`, `Input`, `Icon` | Smallest UI elements |
| Molecule | `SearchBar`, `Card`       | Group of atoms       |
| Organism | `ProductList`, `Navbar`   | Complete UI section  |
| Template | `ProductPageLayout`       | Page layout          |
| Page     | `ProductDetailPage`       | Final rendered view  |

---

## ⚙️ 2. Standard Design Guidelines (Big Tech Level)

### 📁 Folder Structure

```
/src/components/
  /Button/
    Button.tsx
    Button.types.ts
    Button.stories.tsx
    Button.test.tsx
    index.ts
```

### 📦 Ideal Component Template

```tsx
// Button.tsx
import { ButtonProps } from './Button.types';

export const Button = ({ label, variant = "primary", ...props }: ButtonProps) => {
  return (
    <button className={`btn btn-${variant}`} {...props}>
      {label}
    </button>
  );
};
```

```ts
// Button.types.ts
export interface ButtonProps extends React.ButtonHTMLAttributes<HTMLButtonElement> {
  label: string;
  variant?: "primary" | "secondary" | "ghost";
}
```

---

## 💡 3. Design Principles to Follow

### ✅ a. Single Responsibility

* One component = one purpose.
* Separate `UI`, `logic`, and `data`.

### ✅ b. Props-Driven Design

* Design components to be **driven by configuration**.
* Avoid hardcoded logic.

```tsx
<ProductCard
  title="Running Shoes"
  price={1999}
  image="/shoe.jpg"
  onClick={...}
/>
```

### ✅ c. Composition > Inheritance

```tsx
<Card>
  <Card.Header />
  <Card.Body>
    <ProductInfo />
  </Card.Body>
</Card>
```

---

## 🧠 4. Frontend Design Patterns (Interview Goldmine)

| Pattern                    | What It Solves               |
| -------------------------- | ---------------------------- |
| Presentational & Container | UI separation from logic     |
| Controlled vs Uncontrolled | Form behavior control        |
| Compound Components        | Component composition        |
| Render Props / Hooks       | Sharing behavior across UIs  |
| Config-Driven UI           | Dynamic UI via JSON / schema |

---

## 🧪 5. Testing Strategy

### For every component:

* ✅ Unit test UI and behavior (`Jest`, `RTL`)
* ✅ Snapshot test
* ✅ Accessibility test

```tsx
test("Button renders correctly", () => {
  render(<Button label="Submit" />);
  expect(screen.getByText("Submit")).toBeInTheDocument();
});
```

---

## 🔒 6. Accessibility + UX

* Use semantic HTML: `<button>`, `<input>`, `<label>`
* ARIA roles when necessary
* Keyboard support
* Focus handling
* Color contrast

---

## 🧰 7. Tooling Best Practices

| Tool              | Why Use It                    |
| ----------------- | ----------------------------- |
| Storybook         | Component documentation + dev |
| Jest/RTL          | Testing                       |
| ESLint + Prettier | Code consistency              |
| Vite/Next         | Modern build tooling          |
| TypeScript        | Type safety                   |

---

## 📦 Component Checklist (Like a Pro)

Before finalizing any component, ask:

* [ ] Is it **configurable** via props?
* [ ] Does it **handle edge cases** gracefully?
* [ ] Can it be **unit tested**?
* [ ] Is it **reused** elsewhere?
* [ ] Does it follow **naming conventions**?
* [ ] Is it **accessible**?
* [ ] Is it **responsive**?

---

## 📍 Real-World Component Example (Interview Style)

**Component:** `ProductCard`

```tsx
<ProductCard
  title="Air Max 90"
  price={12999}
  discount={20}
  rating={4.2}
  onClick={() => openProductDetail()}
  image="/airmax.webp"
/>
```

### What Interviewer Might Ask:

* How will you make this card reusable?
* What happens on low network?
* How to make this lazy-load or SSR ready?
* What if rating is missing?
* How to write tests for this?

---

## 🧠 Interview Prompt Example

> "Design a reusable, accessible Button component for a design system that supports multiple variants, icons, loading state, and form submission."

This is **low-level design gold** — and often asked by companies like **Uber, Amazon, Flipkart, Swiggy**.

