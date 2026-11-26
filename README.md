This is a [Next.js](https://nextjs.org) project bootstrapped with [`create-next-app`](https://nextjs.org/docs/app/api-reference/cli/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `app/page.tsx`. The page auto-updates as you edit the file.

This project uses [`next/font`](https://nextjs.org/docs/app/building-your-application/optimizing/fonts) to automatically optimize and load [Geist](https://vercel.com/font), a new font family for Vercel.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js) - your feedback and contributions are welcome!

## Architectural Overview
This project is structured using the Next.js framework, which provides a powerful and flexible architecture for building web applications. The main components of the architecture include:
- **Pages**: The `app` directory contains the main page components, such as `page.tsx`, which serves as the entry point for the application. Each file in this directory corresponds to a route in the application.
- **Components**: Reusable UI components can be created and stored in a separate `components` directory. This promotes modularity and code reusability across different pages.

## Shared front logic

This repository is only a scaffold for creating a new front. The logic shared by every front
(session refresh, logout and resume, proxy guard, CSP, theme, instance context) ships with the
published `@mairie360/lib-components` package since MAIR-126. Import it from its subpaths, never
from the root entry, so the client build only carries what the front uses:

| Subpath | Content |
| --- | --- |
| `@mairie360/lib-components/next` | Server session cookies, BFF proxy, refresh, logout and resume handlers |
| `@mairie360/lib-components/guard` | Middleware auth guard with Content Security Policy |
| `@mairie360/lib-components/browser` | `sessionFetch`, which renews the session once on a 401 |
| `@mairie360/lib-components/shared` | CSP builder, JWT display role, instance time zone, public front URLs |
| `@mairie360/lib-components/react` | `InstanceProvider`, role and time zone hooks, modal focus scope |
| `@mairie360/lib-components/theme` | Appearance cookie and confirmed theme |

Pin the same exact `@mairie360/lib-components` version as the other fronts, and copy
`tests/bundle/client-bundle.test.cjs` from an existing front to check the client bundle.
