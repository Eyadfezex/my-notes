# Intro to TS (TypeScript)

TypeScript is a statically-typed programming language that is a superset of JavaScript. It was developed and is maintained by Microsoft. TypeScript was created to address the challenges of building large-scale JavaScript applications and adds optional type annotations, classes, interfaces, and other features to the language.

---

TS and JS are both for web development, but with a key difference: typing. TypeScript (TS) is stricter (static typing), catching errors early. JavaScript (JS) is more flexible (dynamic typing), but error-prone.

- TS: Better for large projects with complex code.
- JS: Better for small projects or quick prototyping.

Think of TS as a powerful tool with training wheels, JS as a simpler tool for faster use.

---

TS and JS work together seamlessly. Since TS is a superset of JS, your existing JS code works in TS projects, and compiled TS code runs in any JS environment.

- Use JS libraries directly in TS or with type definitions (.d.ts files) for better editor support.
- Compile TS code to JS using `tsc` and include the generated .js file in your JS project.

This makes switching between TS and JS or using both together very flexible.

---

To set up TypeScript (TS):

1. **Install:** Make sure you have Node.js and install TS with `npm install typescript --save-dev`.

2. **Configure:** Run `npx tsc --init` to create a `tsconfig.json` (configuration file). You can customize options here (optional).

Once set up, write TS files (`.ts` extension) and compile them to JS using `tsc`.

For details, refer to online guides.

---
