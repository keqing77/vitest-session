---
# You can also start simply with 'default'
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: Unit-Testing with Vitest
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
---

# Unit-Testing with Vitest

Next Generation Testing Framework

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space for next page <carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
  <a href="https://vitest.dev/" target="_blank" alt="GitHub" title="Open in GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

---

# What is Vitest?

a blazing-fast unit testing framework built on Vite

- 📝 **Fast** - Vitest is faster than Jest and most api are similar
- 🎨 **UI mode** - Simple and easy-to-use interface for running tests
- 🧑‍💻 **Developer Friendly** - hot module replacement (HMR), EMS support.

  <br>
  <br>

Read more about [Why Vitest?](https://vitest.dev/guide/why.html)

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# Command

check test scripts in `package.json`

```sh
# Run all tests
npm run test

# Generate html coverage report
npm run test:coverage

# pass --watch flag to enable watch mode
npm run test:watch

# use vitest ui to run tests and check coverage
npm run test:ui

# Run single test file
npm run test <test_file_path>
```

---

# Vitest example

````md magic-move {lines: true}
```ts {*|6|*}
// Simple test
import { expect, test } from "vitest";
import { sum } from "./sum.js";

test("adds 1 + 2 to equal 3", () => {
  expect(sum(1, 2)).toBe(3);
});
```

```ts {*|1-4|6-18|19-21,24}
// Test Components with HTTP requests
import { setupServer } from "msw/node";
import { rest } from "msw";
import { test, expect, beforeAll, afterEach, afterAll } from "vitest";

export const restHandlers = [
  rest.get("https://api.agify.io/", (req, res, ctx) => {
    return res(
      ctx.status(200),
      ctx.json([
        {
          age: 55,
          name: "tope",
        },
      ])
    );
  }),
];
const server = setupServer(...restHandlers);
// Start server before all tests
beforeAll(() => server.listen({ onUnhandledRequest: "error" }));

//  Close server after all tests
afterAll(() => server.close());

// Reset handlers after each test `important for test isolation`
afterEach(() => server.resetHandlers());
```

```ts {*|8|10|12}
// Testing custom hooks
describe("useCounter", () => {
  //…
  it("should increment the initial value once", () => {
    const initialValue = 1;
    const { result } = renderHook(() => useCounter(initialValue));

    expect(result.current.value).toBe(initialValue);

    act(() => result.current.increment());

    expect(result.current.value).toEqual(2);
  });
});
```
````

---

# Thanks all!

[Documentation](https://sli.dev) · [GitHub](https://github.com/slidevjs/slidev) · [Showcases](https://sli.dev/showcases.html)

<PoweredBySlidev mt-10 />
````
