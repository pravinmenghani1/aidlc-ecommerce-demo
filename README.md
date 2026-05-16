# AI-DLC E-Commerce Demo — 30-Minute Walkthrough

## Pre-Setup (5 minutes before demo)

```bash
# 1. Create project directory
mkdir aidlc-ecommerce-demo && cd aidlc-ecommerce-demo
git init

# 2. Install AI-DLC rules for Kiro
curl -sL https://api.github.com/repos/pravinmenghani1/aidlc-workflows/releases/latest \
  | grep -o '"browser_download_url": *"[^"]*"' \
  | head -1 | cut -d'"' -f4 \
  | xargs -I {} curl -sL {} -o /tmp/aidlc.zip
unzip -o /tmp/aidlc.zip -d /tmp/aidlc-release
mkdir -p .kiro/steering
cp -R /tmp/aidlc-release/aidlc-rules/aws-aidlc-rules .kiro/steering/
cp -R /tmp/aidlc-release/aidlc-rules/aws-aidlc-rule-details .kiro/
rm -rf /tmp/aidlc.zip /tmp/aidlc-release

# 3. Verify setup
# Run kiro-cli, then: /context show
# Confirm entries for .kiro/steering/aws-aidlc-rules
```

---

## ⏱️ MINUTE 0-2: Kick Off AI-DLC

### Prompt to paste in Kiro:

```
Using AI-DLC, I want to build a simple e-commerce product catalog website with the following requirements:

- Tech stack: Next.js 14 (App Router) + TypeScript + Tailwind CSS
- Pages: Home (product grid), Product Detail, Cart, Checkout
- Data: Mock product data (10 products with name, price, image, description)
- Features: Add to cart, remove from cart, quantity update, cart total
- State management: React Context (no external libraries)
- No backend needed — all client-side with mock data
- Must be deployable locally with `npm run dev`

This is a demo project to showcase AI-DLC workflow.
```

### What AI-DLC Does:
- Recognizes AI-DLC invocation
- Asks structured questions about complexity and preferences
- Classifies as MEDIUM complexity
- Begins Inception Phase

---

## ⏱️ MINUTE 2-10: 🔵 INCEPTION PHASE

### What the Agent Produces:

```
aidlc-docs/
└── inception/
    ├── requirements.md
    ├── user-stories.md
    ├── application-design.md
    ├── units-of-work.md
    └── risk-assessment.md
```

### Expected Questions from Agent:

```
Q1: What is the primary purpose of this application?
(a) Production e-commerce store
(b) Demo/prototype for showcasing workflow  ← SELECT THIS
(c) Learning exercise
(d) MVP for customer validation

Q2: Authentication requirements?
(a) Full auth with login/signup
(b) Guest checkout only  ← SELECT THIS
(c) No auth needed
(d) OAuth integration

Q3: Styling approach?
(a) Custom design system
(b) Tailwind utility classes  ← SELECT THIS
(c) Component library (shadcn/ui)
(d) Minimal/no styling
```

### 🎯 Demo Talking Points:
- "Notice how AI-DLC asks structured questions BEFORE writing code"
- "This prevents the agent from guessing and building the wrong thing"
- "The specs it generates become the source of truth"
- "If all code is deleted, we can regenerate from these docs"

---

## ⏱️ MINUTE 10-25: 🟢 CONSTRUCTION PHASE

### What the Agent Builds:

```
aidlc-ecommerce-demo/
├── .kiro/steering/aws-aidlc-rules/
├── aidlc-docs/
│   ├── inception/
│   └── construction/
│       ├── component-design.md
│       ├── implementation-plan.md
│       └── test-strategy.md
├── src/
│   ├── app/
│   │   ├── layout.tsx
│   │   ├── page.tsx
│   │   ├── products/[id]/page.tsx
│   │   ├── cart/page.tsx
│   │   └── checkout/page.tsx
│   ├── components/
│   │   ├── ProductCard.tsx
│   │   ├── ProductGrid.tsx
│   │   ├── CartItem.tsx
│   │   ├── CartSummary.tsx
│   │   ├── Header.tsx
│   │   └── Footer.tsx
│   ├── context/CartContext.tsx
│   ├── data/products.ts
│   └── types/index.ts
├── package.json
├── tsconfig.json
├── tailwind.config.ts
└── next.config.js
```

### 🎯 Demo Talking Points:
- "Notice the agent creates documentation ALONGSIDE code"
- "Each component has a clear spec it's implementing against"
- "The agent runs its own validation — checking code matches spec"
- "Watch how it handles the cart state — it follows the design doc"

### Agent Self-Validation:
1. Generates code for each unit of work
2. Validates against the spec
3. Runs `npm run build` to check for TypeScript errors
4. Self-corrects any issues

### If Agent Gets Stuck:
```
Skip detailed testing for now. Focus on getting a working build.
Prioritize: Home page with product grid + Cart functionality.
```

---

## ⏱️ MINUTE 25-28: 🟡 VERIFY & RUN

```bash
npm install
npm run dev
```

### Quick Verification Checklist:
- [ ] Home page shows product grid (10 products)
- [ ] Clicking a product shows detail page
- [ ] "Add to Cart" button works
- [ ] Cart page shows items with quantities
- [ ] Cart total calculates correctly
- [ ] Remove from cart works

### 🎯 Demo Talking Points:
- "From English spec to working app in ~20 minutes"
- "All decisions are documented in aidlc-docs/"
- "If we delete all code, we can regenerate from specs"

---

## ⏱️ MINUTE 28-30: 🎯 WRAP-UP

```bash
tree aidlc-docs/
```

### Key Metrics:
| Metric | Value |
|--------|-------|
| Time to working app | ~25 minutes |
| Lines of code generated | ~800-1200 |
| Documentation pages | 5-7 |
| Human decisions made | 3-5 |
| Human code written | 0 lines |

> "AI-DLC isn't about replacing developers — it's about elevating them
> from writing code to making decisions. In 30 minutes, we went from
> an idea to a working application with full documentation, and the
> human was in control at every decision point."

---

## 🚨 TROUBLESHOOTING

| Issue | Quick Fix |
|-------|-----------|
| Agent takes too long on Inception | "Keep it simple, this is a demo. Skip risk assessment." |
| Agent asks too many questions | "Use sensible defaults for remaining questions." |
| Build fails | "Fix the TypeScript errors and try again." |
| Agent goes off-track | "Stop. Let's focus only on the product grid and cart." |
| Running out of time | "Skip checkout page. Just deliver Home + Cart." |

---

## 🎁 BONUS: If You Have Extra Time

### Security Extension:
```
Now add the security extension. Run a security review on the code we just generated.
```

### Add a Feature:
```
Using AI-DLC, add a search/filter feature to the product grid.
Allow filtering by category and sorting by price.
```

---

## 🔑 PROMPT VARIATIONS

### For Executives:
```
Using AI-DLC, build me a product showcase website with
a shopping cart. Use React and make it look professional.
```

### For Developers:
```
Using AI-DLC, build an e-commerce SPA with:
- Next.js 14 App Router + TypeScript + Tailwind
- Product CRUD with mock JSON data
- Cart with Context API + useReducer pattern
- Responsive grid layout
- Client-side search with debounce
```

### For Security-Focused Audience:
```
Using AI-DLC with security extension enabled, build a secure
e-commerce checkout flow. Focus on input validation, XSS prevention,
and CSRF protection in the cart/checkout pages.
```

---

## 📋 QUICK REFERENCE TIMELINE

| Time | Phase | What's Happening | Human Action |
|------|-------|-----------------|--------------|
| 0:00-2:00 | Setup | Paste prompt, AI-DLC activates | Type initial prompt |
| 2:00-5:00 | 🔵 Inception | Agent asks questions | Answer 3-5 questions |
| 5:00-10:00 | 🔵 Inception | Agent creates specs & design | Review & approve |
| 10:00-20:00 | 🟢 Construction | Agent generates code | Watch & narrate |
| 20:00-25:00 | 🟢 Construction | Agent validates & fixes | Approve stages |
| 25:00-28:00 | 🟡 Verify | Run app, test features | Click through app |
| 28:00-30:00 | Wrap-up | Show docs, share metrics | Present takeaways |

---

## 📋 FACILITATOR NOTES

### For Workshop Setting:

1. **Pre-provision**: Have participants clone your repo for AI-DLC rules:
   ```bash
   # Participants run this to get rules without manual setup
   curl -sL https://api.github.com/repos/pravinmenghani1/aidlc-workflows/releases/latest \
     | grep -o '"browser_download_url": *"[^"]*"' \
     | head -1 | cut -d'"' -f4 \
     | xargs -I {} curl -sL {} -o /tmp/aidlc.zip
   ```

2. **Fallback**: If Kiro is slow, have a pre-recorded video of the flow

3. **Parallel tracks**:
   - Fast participants → Add bonus features
   - Slow participants → Focus on Inception only, show pre-built Construction

4. **Key observation for audience**:
   - Count how many times the human typed code (should be 0)
   - Count how many decisions the human made (should be 3-5)
