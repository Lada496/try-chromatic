# How to set up storybook and chromatic

## Set up storybook

1. run `npx storybook@latest init`
   ref: [Storybook for Next.js](https://storybook.js.org/docs/get-started/nextjs)

## Set up chromatic

### Install chromatic

1. [Sign up chromatic](https://www.chromatic.com/docs/storybook/setup/#sign-up)
2. run `npm install --save-dev chromatic`

### [Automate Chromatic](https://www.chromatic.com/docs/github-actions/)

1. Set up Workflow at `.github/workflows/chromatic.yml`

```
# .github/workflows/chromatic.yml

name: "Chromatic"

on: push

jobs:
  chromatic:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - name: Install dependencies
        run: npm ci

      - name: Run Chromatic
        uses: chromaui/action@latest
        with:
          # ⚠️ Make sure to configure a `CHROMATIC_PROJECT_TOKEN` repository secret
          projectToken: ${{ secrets.CHROMATIC_PROJECT_TOKEN }}

```

2. Get project token secret
   Go to your project on Chromatic.com. Manage > Configure > Project Token
3. Set up repository secret
   Go to the Github repogitory > Security > Secrets and variables > Actions > New repository secret.
   Then, set `CHROMATIC_PROJECT_TOKEN`` as the Name and paste the project token as the Secret.
4. [Enable UI Tests](https://www.chromatic.com/docs/storybook/test/#enable) on Chromatic.com.
