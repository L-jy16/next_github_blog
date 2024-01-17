# Github blog site
## vercel에서 templates 다운
1. vercel site -> templates -> Blog Starter Kit -> `npx create-next-app --example blog-starter blog-starter-app` 터미널에 입력 후 `npm run dev`

## server로 옮기기
1. next.js 사이트 -> Static Exports 검색 -> next.config.js 파일 만들기
```js
/**
 * @type {import('next').NextConfig}
 */
const nextConfig = {
    output: 'export',
    distDir: 'dist',
    images: {
        unoptimized: true,
    }
}

module.exports = nextConfig
```
붙여넣기
2. `npm run build` 터미널에 입력
3. `npx serve ./dist` 터미널에 입력 => 로컬에서 실행 시킨 것임(아래처럼 나오면 성공)
```js
PS C:\Users\line\Desktop\blog\blog-starter-app> npx serve ./dist
Need to install the following packages:
serve@14.2.1
Ok to proceed? (y) y

   ┌───────────────────────────────────────────┐
   │                                           │
   │   Serving!                                │
   │                                           │
   │   - Local:    http://localhost:3000       │
   │   - Network:  http://192.168.0.147:3000   │
   │                                           │
   │   Copied local address to clipboard!      │
   │                                           │
   └───────────────────────────────────────────┘
```
4. 