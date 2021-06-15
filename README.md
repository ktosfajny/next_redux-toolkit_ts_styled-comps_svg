# Redux Toolkit TypeScript Example

This example shows how to integrate Next.js with [Redux Toolkit](https://redux-toolkit.js.org).

The **Redux Toolkit** is a standardized way to write Redux logic (create actions and reducers, setup the store with some default middlewares like redux devtools extension). This example demonstrates each of these features with Next.js

## Deploy your own

Deploy the example using [Vercel](https://vercel.com?utm_source=github&utm_medium=readme&utm_campaign=next-example):

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/git/external?repository-url=https://github.com/vercel/next.js/tree/canary/examples/with-redux-toolkit-typescript&project-name=with-redux-toolkit&repository-name=with-redux-toolkit)

## How to use

Execute [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app) with [npm](https://docs.npmjs.com/cli/init) or [Yarn](https://yarnpkg.com/lang/en/docs/cli/create/) to bootstrap the example:

```bash
npx create-next-app --example with-redux-toolkit-typescript with-redux-toolkit-app
# or
yarn create next-app --example with-redux-toolkit-typescript with-redux-toolkit-app
```

Deploy it to the cloud with [Vercel](https://vercel.com/new?utm_source=github&utm_medium=readme&utm_campaign=next-example) ([Documentation](https://nextjs.org/docs/deployment)).


---

# How to add svg as ReactComponent support:

1 - `yarn add @svgr/webpack --dev`
2 - `yarn add url-loader --dev`
3 - create `next.config.js` file in root dir and paste:
```
module.exports = {
  webpack(config) {
    config.module.rules.push({
      test: /\.svg$/,
      issuer: {
        test: /\.(js|ts)x?$/,
      },
      use: ["@svgr/webpack", "url-loader"],
    });

    return config;
  },
};
```

4 - create file with svg type declarations, for example: `types/svg.d.ts` and paste:
```
declare module "*.svg" {
  export const ReactComponent: React.FunctionComponent<
    React.SVGAttributes<SVGElement>
  >;
  const content: string;
  export default content;
}

```

5 - make sure that in `tsconfig.json` you have included that `next.config.ts` file like: `"include": ["next-env.d.ts", "**/*.ts", "**/*.tsx", "next.config.js"]`
6 - now you can use it just like in Create React App:
```
import LogoURL, { ReactComponent as LogoComp } from "assets/logo.svg";


<LogoComp width={150} />
 <img src={LogoURL} alt="" />
```

---

# how to add react hooks rules:

1 - `yarn add eslint -D`
2 - `yarn add eslint-plugin-react-hooks -D`
3 - `yarn add @typescript-eslint/parser -D`
4 - in root dir make `.eslintrc.json` file and pase:
```
{
  "parser": "@typescript-eslint/parser",
  "extends": ["plugin:react-hooks/recommended"],
  "rules": {
    // "react/react-in-jsx-scope": "off",
    "no-console": "warn",
    "no-unused-vars": "warn",
    "react-hooks/rules-of-hooks": "error", // Checks rules of Hooks
    "react-hooks/exhaustive-deps": "warn" // Checks effect dependencies
  }
}
```
5 - restart your Visual Studio Code and when you open it again it will show you that you're missing some depenencies in `useEffect` hook itd
