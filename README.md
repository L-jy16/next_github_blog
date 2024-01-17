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
## github 연동

1. github에 README.md 파일 없이 폴더 만들기
2. .gitignore에 "/dist/" 아래처럼 추가하기
```js
# next.js
/.next/
/out/
/dist/
```
3. github와 연동하여 파일이 올라왔는 지 확인
4. 해당 폴더의 github의 setting -> pages -> Build and deployment에 Source를 `GitHub Actions` 으로 변경하기
5. 변경 후 시간이 지나면 Next.js 박스 카드가 생기는데 거기의 Configure 버튼 클릭 후 파일이 생성 되면 저장 후 VScode로 돌아와서 `git pull` 해주기
6. .github 폴더에 nextjs.yml 파일에 job부분의 아랫 부분 쪽을 보면 아래와 같은 게 있는데 저 부분은 중복이므로 삭제
```js
- name: Static HTML export with Next.js
        run: ${{ steps.detect-package-manager.outputs.runner }} next export 
```
7. .github 폴더에 nextjs.yml 파일에 job부분의 아랫 부분 쪽을 보면 아래와 같은 게 있는데 아래와 같이 수정해 주기
```js
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./dist
```
8. git에 올리고 github 페이지로 가서 확인하기 build가 되었는 지 확인 하기
((이미지) L-jy16 2024.01.17 [표시되는 곳] 표시되는 곳을 동그라미가 있을 텐데 동그라미를 클릭하고 detail을 클릭하면 build하는 과정을 볼 수 있다.)