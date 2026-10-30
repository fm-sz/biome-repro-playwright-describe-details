# Biome repro: `usePlaywrightValidDescribeCallback` and `describe` details

Reproduction for [biomejs/biome#12766](https://github.com/biomejs/biome/issues/12766).

Playwright supports `test.describe(title, details, callback)`, where `details` holds `tag`, `annotation` or `lock`
([docs](https://playwright.dev/docs/api/class-test#test-describe)). Since Biome 2.6.2 the recommended rule
`usePlaywrightValidDescribeCallback` treats the second argument as the callback and reports this valid call:

```ts
test.describe("suite", { tag: "@smoke" }, () => {
	test("a", async () => {});
});
```

```
src/index.ts:11:1 lint/correctness/usePlaywrightValidDescribeCallback
  × Describe callback must be a function.
  i The second argument to describe must be a function, not a string, number, object, or other type.
```

The rule is only active because `@playwright/test` is a dependency in `package.json`.

## Run it

```sh
npm ci
npx biome lint
```

The [Lint workflow](https://github.com/fm-sz/biome-repro-playwright-describe-details/actions/workflows/lint.yml) runs the same check on every push.

Generated with Claude Code · Claude Opus 5.5
