This is an H1 
=============
This is an H2
-------------
# This is a H1
## This is a H2
### This is a H3
#### This is a H4
##### This is a H5
###### This is a H6
> This is a first blockqute.
>	> This is a second blockqute.
>	>	> This is a third blockqute.
```
code
```
-------
Lnik:ex123
* test *
* 123

# Course 1
### Course 1 의 목적 : 파일생성 및 서버 접속
#### 파일생성
1. ```npm install -g pnpm``` 으로  node package manager(npm)를 install 한뒤
2. ``` npx create-next-app@latest nextjs-dashboard --example "설치경로" --use-pnpm``` 으로 해당 파일의 경로로 node package excute(npx)를 생성 할 수 있다
3. 설치 후 cd nextjs-dashboard 로 해당 파일을 확인해보면
   - /app: 애플리케이션의 몸든 orute, componenet, logic이 포함된 root폴더로 주로 이곳에서 작업을 한다
      + /app/lib : 유틸리티 함수나 데이터 패칭 함수 등 애플리케이션의 사용되는 함수들이 포함되어 있다
      + /app/ui : 애플리케이션의 모든 UI 컴포넌트가 포함되어 있다
      + /public : 이미지와 같은 애플리케이션의 정적 자산들이 포함되어 있다.
4. 파일이 정상적으로 작성되면 다음과 같이 폴더가 생성되어 있음을 확인할 수 있다
<img src="https://file.notion.so/f/f/649a15f1-a9e3-45d3-b23d-bb09016ffaf3/95e70520-f82a-470e-bf0e-4770b9c91f1b/image.png?table=block&id=11885d67-a342-80f0-9662-d0a46f483dba&spaceId=649a15f1-a9e3-45d3-b23d-bb09016ffaf3&expirationTimestamp=1729296000000&signature=bwlQb63FKo2e47Qv8TmVZvzKlCHUZo9Yq9UPrNR8oOY&downloadName=image.png" alt="img" style="width:15%; height:20%;">

#### TypeScript의 예시
<img src="https://file.notion.so/f/f/649a15f1-a9e3-45d3-b23d-bb09016ffaf3/9dd247d5-5b88-4f29-a133-6fc87da02be2/image.png?table=block&id=11885d67-a342-80e5-abb9-d8272203e9c5&spaceId=649a15f1-a9e3-45d3-b23d-bb09016ffaf3&expirationTimestamp=1729216800000&signature=lNq4azm-7fctfedvUNx3aWRPaDVs2EyBPHQCsX9yIno&downloadName=image.png" alt="Tscript" style="width:50%; height:30%;"> 
- TypeScript사용시 기존에는 const, var 등의 데이터만 가져오던 것을 위와 같이 해당 변수의 타입을 지정해서 사용할 수 있다

#### port 생성

change directory를 통해 nextjs-dashboard로 이동하고

1. Perpomant node package manager install (pnpm i) 로 node package를 install한뒤,

```jsx
pnpm i
```

1. Perpomant node package manager development 로 개발 모드에서 애플리케이션을 실행하면

```jsx
pnpm dev
```

다음과 같이 출력된다(Course 1에 나와있는 화면과는 조금 다르긴 하지만 해당 Typescript JavaScript XML (JSX)파일을 가져오는것을 확인할 수 있다

<img src="https://file.notion.so/f/f/649a15f1-a9e3-45d3-b23d-bb09016ffaf3/e8afb6b2-d906-4b79-92c7-398d5282dc3f/image.png?table=block&id=11885d67-a342-8003-bed7-c74fb605a79e&spaceId=649a15f1-a9e3-45d3-b23d-bb09016ffaf3&expirationTimestamp=1729216800000&signature=wwVUIW28pwlZfAYOWNbYF15CEIiYShmV6rCeF1SjMVI&downloadName=image.png" alt="Tscript" style="width:50%; height:30%;"> 

-------

# Course 2
### Course 2 의 목적 : Cascading Style Sheets 설정 

#### layout.tsx (TypeScript XML) 
- /app 경로에 존재하는 TypeScript 파일의 layout을 설정하는것으로 SpringToolSuite 와 다르게 별도의 Fragment화 없이 바로 적용되며 같은경로 or 상위경로에 있는 모든 TypeScriptXml파일에 적용된다
#### global.css/globals.css (Cascading Style Sheets)
- 스타일시트는 layout과 다르게
  ``` import ‘app/globals.css’; ``` 와 같이 import 한뒤, 해당 스타일을 불러오는 형식으로, 개별적으로 적용시킬 수 있다
  
  <img src="https://file.notion.so/f/f/649a15f1-a9e3-45d3-b23d-bb09016ffaf3/6cec1146-a590-47e0-a8e2-ab7462c6f085/image.png?table=block&id=11885d67-a342-80c2-8dc7-f93430a6f01d&spaceId=649a15f1-a9e3-45d3-b23d-bb09016ffaf3&expirationTimestamp=1729216800000&signature=hCC6hNXqUWGlzrqLmgjUzM2MeE_4133zA233IwJjmTY&downloadName=image.png" alt="img" style="width: 50%; height:50%">
  
#### TailWind
 + TailWind는 cascading style sheets의 FrameWork로 기존의 bootstrap과는 달리 사전에 정의된 유틸리티 클래스( 작은 CSS 클래스) 를 제공하기 때문에 완본품이 아닌 레고와 같이 사용자가 원하는 디자인을 적용시켜 만들 수 있다
 + tailwind.config.js를 통해 css를 사용자 정의할 수 있다

### 코드

```jsx
@tailwind base;
@tailwind components;
@tailwind utilities;

:root {
  --background: #f1becb;
  --foreground: #7278a8;
}

@media (prefers-color-scheme: dark) {
  :root {
    --background: #7278a8;
    --foreground: #ededed;
  }
}

body {
  color: var(--foreground);
  background: var(--background);
  font-family: Arial, Helvetica, sans-serif;
}

@layer utilities {
  .text-balance {
    text-wrap: balance;
  }
}

```

해당 코드에서 

```jsx
@tailwind base;
@tailwind components;
@tailwind utilities;
```

@tailwind어노테이션이 붙은 부분을 의미한다

TailWind는이런식으로 사용이 가능하다 (
```jsx
   <div
            className="relative w-0 h-0 border-l-[15px]
             border-r-[15px] border-b-[26px] 
             border-l-transparent
              border-r-transparent
               border-b-black"
        />
```
#### ModuleStyleSheet

+ 기존의 스타일 시트와 같이 localScope로 변수명을 지정하여 다른 스타일 시트의 변수명과 동일한 변수명을 사용할 수 있게한다
+ global.css 와 같이 css파일을 가져올 때 import {style} from "~~" 의 형식으로 가져오기 때문에 style.shpae , style2.shape와 같이 클래스명이 동일해도 서로 간섭되지 않는다
1. 스타일 시트 생성

```jsx
//여기에 @tailwind 등의 frameWork사용 가능
.shape{
   height: 0;
    width: 0;
    border-bottom: 13px solid black;
    border-left: 13px solid transparent;
    border-right: 13px solid transparent;

}
```

1. 스타일 시트 import

이때 해당 스타일 시트를 받는 파일은 

```jsx
import styles from "@/app/UI/home.module.css"
```

다음과 같이 import를 한뒤, style변수명을 선언하고

1. 해당 스타일 시트 사용

사용시에는 

```jsx
 <div className={styles.shape}></div>
```

와 같이 선언한 스타일시트의 변수명. 해당 스타일 클래스를 사용한다

#### clsx(classNames)

+ clsx는 Type의 값을 받아올 수 있는 TypeScript의 특징을 사용한 라이브러리로 적용시킬 부분의 condition에 따라 스타일을 조정해야할 때 (로그인 / 로그아웃 등) 이를 쉽게 조정할 수 있게 해준다

### 코드

```jsx
"use client";
import Image from "next/image";
import styles from "@/app/UI/home.module.css";
import clsx from 'clsx';
import {useState} from "react";

export default function Home({ initialStatus, initialStatus2,stat }: { initialStatus: string , initialStatus2 : string, stat : string}) {
    const [status, setStatus] = useState(initialStatus);
    const [status2, setStatus2] = useState(initialStatus2);
stat = 'paid';
    return (
        <div className="grid grid-rows-[20px_1fr_20px] items-center justify-items-center min-h-screen p-8 pb-20 gap-16 sm:p-20 font-[family-name:var(--font-geist-sans)]">
            <main className="flex flex-col gap-8 row-start-2 items-center sm:items-start">
                <Image
                    className="dark:invert"
                    src="https://nextjs.org/icons/next.svg"
                    alt="Next.js logo"
                    width={180}
                    height={38}
                    priority
                />
                <ol className="list-inside list-decimal text-sm text-center sm:text-left font-[family-name:var(--font-geist-mono)]">
                    <li className="mb-2">
                        Get started by editing{" "}
                        <code className="bg-black/[.05] dark:bg-white/[.06] px-1 py-0.5 rounded font-semibold">
                            app/page.tsx
                        </code>
                        .
                    </li>
                    <li>Save and see your changes instantly.</li>
                </ol>

                <div className="text-blue-300">파일출력확인 문구@@@</div>
                <a
                    className="flex items-center gap-2 hover:underline hover:underline-offset-4"
                    href="/nextjs-dashboard/app/test"
                    target="_blank"
                    rel="noopener noreferrer"
                >
                    test.tsx파일 링크d
                </a>
                <div>page이름의 TypeScript XML파일 가져오는 중</div>

                <div className="flex gap-4 items-center flex-col sm:flex-row">
                    <a
                        className="rounded-full border border-solid border-transparent transition-colors flex items-center justify-center bg-foreground text-background gap-2 hover:bg-[#383838] dark:hover:bg-[#ccc] text-sm sm:text-base h-10 sm:h-12 px-4 sm:px-5"
                        href="https://vercel.com/new?utm_source=create-next-app&utm_medium=appdir-template-tw&utm_campaign=create-next-app"
                        target="_blank"
                        rel="noopener noreferrer"
                    >
                        <Image
                            className="dark:invert"
                            src="https://nextjs.org/icons/vercel.svg"
                            alt="Vercel logomark"
                            width={20}
                            height={20}
                        />
                        Deploy now
                    </a>
                    <a
                        className="rounded-full border border-solid border-black/[.08] dark:border-white/[.145] transition-colors flex items-center justify-center hover:bg-[#f2f2f2] dark:hover:bg-[#1a1a1a] hover:border-transparent text-sm sm:text-base h-10 sm:h-12 px-4 sm:px-5 sm:min-w-44"
                        href="https://nextjs.org/docs?utm_source=create-next-app&utm_medium=appdir-template-tw&utm_campaign=create-next-app"
                        target="_blank"
                        rel="noopener noreferrer"
                    >
                        Read our docs
                    </a>
                </div>
            </main>
            <footer className="row-start-3 flex gap-6 flex-wrap items-center justify-center">
                <a
                    className="flex items-center gap-2 hover:underline hover:underline-offset-4"
                    href="https://nextjs.org/learn?utm_source=create-next-app&utm_medium=appdir-template-tw&utm_campaign=create-next-app"
                    target="_blank"
                    rel="noopener noreferrer"
                >
                    <Image
                        aria-hidden
                        src="https://nextjs.org/icons/file.svg"
                        alt="File icon"
                        width={16}
                        height={16}
                    />
                    Learn
                </a>
                <a
                    className="flex items-center gap-2 hover:underline hover:underline-offset-4"
                    href="https://vercel.com/templates?framework=next.js&utm_source=create-next-app&utm_medium=appdir-template-tw&utm_campaign=create-next-app"
                    target="_blank"
                    rel="noopener noreferrer"
                >
                    <Image
                        aria-hidden
                        src="https://nextjs.org/icons/window.svg"
                        alt="Window icon"
                        width={16}
                        height={16}
                    />
                    Examples
                </a>
                <a
                    className="flex items-center gap-2 hover:underline hover:underline-offset-4"
                    href="https://nextjs.org?utm_source=create-next-app&utm_medium=appdir-template-tw&utm_campaign=create-next-app"
                    target="_blank"
                    rel="noopener noreferrer"
                >
                    <Image
                        aria-hidden
                        src="https://nextjs.org/icons/globe.svg"
                        alt="Globe icon"
                        width={16}
                        height={16}
                    />
                    Go to nextjs.org →
                </a>
            </footer>
            <div className="relative w-0 h-0 border-l-[15px] border-r-[15px] border-b-[26px] border-l-transparent border-r-transparent border-b-black">
                TailWind테스트
            </div>

            <div className={styles.shape}></div>

            <span className={clsx(
                'inline-flex items-center rounded-full px-2 py-1 text-sm',
                {
                    'bg-gray-100 text-gray-500': stat === 'pending',
                    'bg-green-500 text-white': stat === 'paid',
                },
                )}>
{stat} 일때
            </span>
<div>
    <p>Status 1 == {status}</p>
    <p>Status 2 == {status2} </p>
    <button onClick={() => setStatus('paid')}>Mark Status 1 as Paid</button>
    <div></div>
    <button onClick={() => setStatus2('completed')}>Mark Status 2 as Completed</button>

</div>
        </div>
    );
}

//

```

먼저 clsx를 적용시키려면 기존의 코드인

```jsx
export default function Main(){ 에서

export default function Home({ initialStatus, initialStatus2,stat }: { initialStatus: string , initialStatus2 : string, stat : string}) {
    const [status, setStatus] = useState(initialStatus);
    const [status2, setStatus2] = useState(initialStatus2);
stat = 'paid'; 이 코드와 같이 
1. 초기값 2. 초기값의 타입(String 등) 3. 변경값(업데이트값을 받는 배열) 
```

로 변경해야한다

위와 같이 값을 받아올 변수명 : {변수타입} 을 설정하고

해당 값을 지정해주면 된다 위의 경우에는 status의 값을 setStauats로 지정하고, 그 값은 useState를 통해 받아온 (intialStatus)의 값으로 지정한다는 의미이다

따라서 

1. 버튼을 클릭시 setStatus로 지정된 값에 해당하는 ‘paid’ or ‘pending’이라는 문자열을 인식하고( TypeScript이므로) 
2.  status or statuss2에 해당 값을 전달한뒤
3. 다시 p태그에 해당되는 값을 출력한다

(아래 stat = ‘paid’와 같이 직접 지정해도 되지만  값이 fix가 되기 때문에 X)

### clsx미 사용시

```jsx

return{
    <span className={clsx(

  export default function InvoiceStatus({ status }: { status: string }) {
    let className = 'inline-flex items-center rounded-full px-2 py-1 text-sm';

    if (status === 'pending') {
        className += ' bg-gray-100 text-gray-500';
    } else if (status === 'paid') {
        className += ' bg-green-500 text-white';
    }

    return <span className={className}>{status}</span>;
}

    <p>Status 2 == {status2} </p>
    <button onClick={() => setStatus('paid')}>Mark Status 1 as Paid</button>
    <div></div>
    <button onClick={() => setStatus2('completed')}>Mark Status 2 as Completed</button>

</div>
}
```

### clsx를 사용했을 경우

```jsx
  <p className={clsx(
                'inline-flex items-center rounded-full px-2 py-1 text-sm',
            {
                'bg-red-100 text-red-500': status === '변경전',
                'bg-green-500 text-white': status === 'paid',
            }
            )}>
                status1 == {status}
            </p>
                <br/>
                <p className={clsx(
                    'inline-flex items-center rounded-full px-2 py-1 text-sm',
                    {
                        'bg-red-100 text-red-500': status2 === '변경전',
                        'bg-green-500 text-white': status2 === 'pending',
                    }
                )}>
                    status 2 == {status2}
            </p>
            <br/>
            <button onClick={() => setStatus('paid')}>paid</button>

            <br/>
            <button onClick={() => setStatus2('pending')}>pending</button>

위의 코드는 onclick이벤트 발생시 해당 status의 string값을 'paid' 로 바꾸고 값이 변경됨에 따라 해당 스타일이 적용된다
```

기존의 코드는 받아오는 값을 조건문 등을 통해 판독하고, 그에따라 값을 지정해 주기 때문에 조건문을 붙여야 한다는 단점이 있지만 

clsx를 사용하면 별도의 조건문없이 `<button onClick={() => setStatus('paid')}>paid</button>`등의 이벤트만으로  스타일,출력값을 조정할 수 있다

자바에서의 삼향연산자와 유사(”?”)한 개념이라 볼 수 있다

따라서
기존의 useState를 통해 받은값을, 조건문을 통해 결과값을 다르게 도출하던것에서 
useState를 통해 받은값을, 조건문이 아닌, clsx를 통해 결과값을 다르게 도출시키는것이 CLSX방식

---



# Course 3
### Course 3 의 목적 : 이미지 및 폰트 적용

#### Next/Font modules

font에 따라서 애플리케이션의 비율등이 변경되는것을 방지하기 위해 next/font 모듈을 사용하면 next.js에서 자동으로 font의 비율을 맞춰주어 레이아웃이 틀어지는것을 방지한다

사용방법

1. ui폴더 혹은 기존 폴더에 fonts.ts 파일 생성
2. 폰트 설정을 한다
    
    ```jsx
    import {Inter,Roboto, Noto_Sans_KR,Lusitana} from "next/font/google";
    
    export const inter = Inter({weight:'400', style:'italic', subsets:['latin']})
    export const notoSansKr = Noto_Sans_KR({
        // preload: true, 기본값
        subsets: ["latin"], // 또는 preload: false
        weight: ["100", "400", "700", "900"], // 가변 폰트가 아닌 경우, 사용할 fontWeight 배열
    });
    export const roboto = Roboto({weight:'400', style:'normal',subsets:['latin']});
    export const lusitana = Lusitana({weight:['400','700'], style:'normal',subsets:['latin']});
    ```
    
3. 해당 폰트를 import한 뒤 className을 통해 적용시킨다 
(이때 {’ ‘} 이 부분은 앞,뒤로 한칸 띄우는 react구문)
    
    ```jsx
    import {inter, notoSansKr, roboto, Roboto} from "@/app/UI/fonts";
    </div>
    <h1 className={***inter***.className}>구글 폰트 적용(latin font적용)</h1>
    <h1 className={***notoSansKr***.className}>구글 폰트 적용(notoSansKr 적용/ [100,400,700,900]의 크기)</h1>
    <h1 className={***roboto***.className}>폰트 적용 (Roboto 적용 / 200크기)</h1></div>
        <p
                    className={`${lusitana.className} text-xl text-gray-800 md:text-3xl md:leading-normal`}
                >
                    <strong>Welcome to Acme.</strong> This is the example for the{' '}
                    <a href="https://nextjs.org/learn/" className="text-blue-500">
                        Next.js Learn Course
                    </a>
                    , brought to you by Vercel.
                </p>
    ```

### public 폴더

이미지를 적용시키는 방법은 

1. CSS에서 이미지를 background형식으로 추가하는것과
2.  TypeScript파일에서 적용시키는 방법 2가지가 있다
- 이미지를 적용시키기 위해서는 최상위 폴더(app,node-modules등이 있는)에 public등의 폴더를 생성하여 가져오는 방식이 추천됨

### CSS에서 img를 사용하는 방식

기존의 html에서 사용하는 방법과 동일하게 

1.  css에 backgroun-image로 이미지 경로 추가(no-repeat)
2. 해당 css파일 import
3. className에 해당 클래스명 추가

```jsx
1. .doImg{
    height: 300px;
    width: 300px;
    /*background-image: url("public/image/do.jpg");*/
    background-image: url("../public/image/do.jpg");
    background-repeat: no-repeat;
  }
  
2.import styles from "@/app/UI/home.module.css";
  
3. <div className="doImg"></div>
```

### TypeScriptXML에서 img를 사용하는 방식

1. import Image from "next/image"; 로 모든 image에 대한 최적화 작업을 실시한 뒤
2. `<Image src="/image/do.jpg"/>` 와 같이 최상위 폴더에 있는 image파일을 연결시킨다

```jsx
1. import Image from "next/image"; (nextjs가 처리하는 모든 image의 최적화)

2.
<Image src="/image/do.jpg" alt="" width={200} height={100}/>
<Image src='/image/node.jpg' width={300} height={200}></Image>
```

### Course4
### 레이아웃 및 페이지 생성

- Create the `dashboard` routes using file-system routing.
- Understand the role of folders and files when creating new route segments.
- Create a nested layout that can be shared between multiple dashboard pages.
- Understand what colocation, partial rendering, and the root layout are.

### nested routing

- nextJS는 폴더 자체가 라우팅(주소)되며, 폴더가 중첩된 경로를 생성하며,
- URL주소에는 폴더가 중첩된 경로의 sagment(URL의 부분)를 보여준다
- 따라서 각각 라우팅된 폴더 구조가 URL구조와 매핑되며 , URL의 주소에는 라우팅된 파일의 폴더명이 출력된다 

<img src="https://file.notion.so/f/f/649a15f1-a9e3-45d3-b23d-bb09016ffaf3/76bd63ed-780e-49e2-a6ce-6c8e49b61042/image.png?table=block&id=11985d67-a342-80cf-ae33-e4bdc06f6113&spaceId=649a15f1-a9e3-45d3-b23d-bb09016ffaf3&expirationTimestamp=1729296000000&signature=mulnE421jpKceBkuk9QzSWjXdzgrj1BkRXju2q9ZjlQ&downloadName=image.png" alt="img" style="width: 50% height:30%">
위와 같이 dashboard폴더에 있는 page.tsx(TypeScriptXML), layout.tsx등이 보이는것이 아닌, 파일들이 들어있는 dashboard폴더 자체를 라우팅 하고 또 URL주소에 sagment(주소)가 저 폴더명, 즉 dashboard가 출력된다.

### Creating dashboard page

nextJS에서는 기존의 HTML파일 생성과는 다르게 nested routing의 규칙에 따라서 폴더 자체가 라우팅이 되기 때문에 단일 typescript파일로는 출력이 불가능하며, 폴더를 생성한 후에 그 폴더를 불러와야 해당 폴더에 있는 파일이 전부 불러와진다

1. 기본 페이지 app.tsx는 출력되는 이유 → app이라는 폴더에  속하는 폴더이므로 ‘/’경로로 접속이 가능하다
2. 어제 파일이 404가 뜨던 이유⇒ app폴더에 app.tsx파일이 존재했기 때문에 단독 파일의 생성만으로는 작동이 안되던것
3. 새로 생성된 폴더-tsx에 global.css가 적용되는 이유 → 루트폴더에 global.css에서
    
    ```jsx
    :root {  --background: #6f6f6f;  --foreground: #f1becb;}
    @media (prefers-color-scheme: dark) { 
    :root {    --background: #6f6f6f;    --foreground: #f1becb;  }}
    ```
    와 같이 root:로 선언했기 때문에

    
    이때 페이지 생성의 기준은
    
    1. 폴더를 생성한다
    2. page.tsx파일로 스크립트 파일을 생성한다 (그 외의 파일은 인식X)
    3. 다음과 같이 export defalut function page() 를 사용하여 export한다
    
    ```jsx
    
    import React from "react";
    
    export default function page (){
        return(
            <div>
                <p>
                    invoices page
                </p>
            </div>
        );
    };
    
    ```
    
    4. 해당 폴더의 이름으로 URL을 입력한다
    <img src="https://file.notion.so/f/f/649a15f1-a9e3-45d3-b23d-bb09016ffaf3/9a8bf978-89e4-4d93-88f9-2759a3b847a4/image.png?table=block&id=11985d67-a342-8059-836b-e25e33e7bb36&spaceId=649a15f1-a9e3-45d3-b23d-bb09016ffaf3&expirationTimestamp=1729216800000&signature=1fDXs4VzYXAOmhK9cCcB0Y3xpn-8e7ulFN68HYb8lGg&downloadName=image.png" alt="img" style="width: 50% height:30%">

### layout

globals.css와 같이 layout도 모든 파일에 적용시킬 수 있다

layout.tsx생성 후 

```jsx
import type { Metadata } from "next";
import localFont from "next/font/local";
import "./globals.css";

const geistSans = localFont({
  src: "./fonts/GeistVF.woff",
  variable: "--font-geist-sans",
  weight: "100 900",
});
const geistMono = localFont({
  src: "./fonts/GeistMonoVF.woff",
  variable: "--font-geist-mono",
  weight: "100 900",
});

export const metadata: Metadata = {
  title: "Create Next App",
  description: "Generated by create next app",
};

import '@/app/globals.css';

export default function RootLayout({
  children,
}: Readonly<{
  children: React.ReactNode;
}>) {
  return (
    <html lang="en">
      <body
        className={`${geistSans.variable} ${geistMono.variable} antialiased`}
      >
        {children}
      </body>
    </html>
  );
}

```

위와 같이 

1. local font 
2. layout html

등을 지정하여 global.css(root:가 적용된 cascading style sheets)를 layout에 적용시키면  전체페이지에 적용시킬 layout+css를 설정할 수 있다


# Course 5

### navigation 생성

먼저 navigaion과 같이 동적인 페이지를 사용하기 위해서는 

서버측에서 만들어진 HTML을 전달받는 서버 컴포넌트가 아니라 , 브라우저에서 렌더링 되는 클라이언트 컴포넌트를 사용해야 한다 ("use client" 사용)

(Component: 재사용 가능한 UI의 독립적인 구상)

### 서버 컴포넌트(Server Components) 와 클라이언트 컴포넌트(Client Components)

서버 컴포넌트

- 서버에서 랜더링 되어 서버에서 HTML생성 후 클라이언트로 전달한다
- 상태나 이벤트 처리가 불가능하다 (React의 useState, useEffect등)
- 서버 컴포넌트는 서버에서 실행되므로 DB나 API 호출을 서버에서 쉽게 처리할 수 있다
- 서버 컴포넌트는 클라이언트에 불필요한 자바스크립트가 적게 전달되어 성능향상이 가능하다

⇒서버에서 HTML을 만들고 전달하여 성능은 빠르지만 이미 만들어진 HTML을 전달하기 때문에 상호작용이 불가능함

클라이언트 컴포넌트

- HTML은 서버에서 제공받지만 브라우저에서 자바스크립트를 통해 랜더링 된다
- React에서 useState,useEffect,useContext와 같은 브라우저 전용 API를 사용할 수 있어 동적인 상호작용이 가능하다
- 사용자의 상호작용을 처리할 수 있어 상태관리에 용이하다(링크전송 or 페이지네이션 등등)
- 실시간 UI반응 또한 가능하다 (classNames[clsx]등의 사용이 가능)

⇒서버에서 HTML만 제공받고 자바스크립트를 통해 브라우저에서 렌더링 되기 때문에 상호작용이 가능하지만 성능의 저하가 생길 수 있다

 navigation은 CSS와 같이 navigation 파일을 생성한 뒤 

`import NavLinks from '../UI/dashboard/nav-lilnks'` 와 같이 해당 파일을 import하여 사용한다 

### 받는XML파일

```jsx
//import './globals.css'
import React from 'react';
import NavLinks from '../UI/dashboard/nav-lilnks'

export default function Page(){

return (
        <div>
            <h1>Text Page</h1>
            <p>여기에 내용을 추가하세요.</p>
            <p></p>
            <NavLinks/> {}
        </div>
    );
};

```

### navigation파일

1. 동적으로 rendering할 navigaion 파일에서는 ‘use client’를 선언하여 client components라는것을 명시해야 한다
2. import usePathname from "next/navigation"; 을 사용하여 현재 주소를 가져온다(현재 경로를 직접 입력할 필요가 없음)
3. links의 배열, 즉 pagination작업을 할 link와 href, icon 등을 나열한다
4. [links.map](http://links.map)((link))는 links배열에 map method를 사용하여 자동으로 반복문을 생성하고, 해당 반복문의 데이터는 return에 있는 정보를 넣는다
5. 따라서 key,href,p 의 데이터들을 위에서 생성한 배열을 map method를 사용하여 채우고
6. clsx를 사용하여 pathname === link.href, 일 경우, 즉 받아오는 주소값이 navigation링크의 주소값과 동일할 경우(현재페이지) 파란색으로 하이라이트 되게 한다

```jsx
return(
<>
            {links.map((link) => {

                return (
                    <Link
                        key={link.name}
                        href={link.href}
                        className={clsx("",
                            {
                                'bg-sky-100 text-blue-600': pathname === link.href,
                            },
                        )}
                    >

                        <p className="hidden md:block">{link.name}</p>
                    </Link>
                );
            })}
        </>
        )
```

```jsx
'use client';

import Link from "next/link";
import {usePathname} from "next/navigation";
import clsx from 'clsx';

export default function NavLinks(){
    const pathname = usePathname();
    const links = [
        {
            name:'home',
            href:'/'
/*            icon: 'exIcon'*/
        },
        {
            name:'Customers',
            href: '/dashboard/customers'

        },
        {
            name:'invocies',
            href:'/dashboard/invocies'

        },
        {
          name:'dashboard',
          href:'/dashboard'
        }
    ]
    return(
        <>
            {links.map((link) => {

                return (
                    <Link
                        key={link.name}
                        href={link.href}
                        className={clsx("",
                            {
                                'bg-sky-100 text-blue-600': pathname === link.href,
                            },
                        )}
                    >

                        <p className="hidden md:block">{link.name}</p>
                    </Link>
                );
            })}
        </>
    );
}
```

# Course 6

### DB생성 및 연결

+ vercel을 사용하려 했으나 학원 컴퓨터의 기존파일+버전문제 등등의 문제로 방법만 확인

+ vercel말고 일단 마리아DB or Oracle등 DB사용 한뒤 prisma 설치

# Course 7

Fetching Data는 여러 Application Programming Interface(API)를 이용하여 해당 API에서 필요한 정보를 fethcing하여 가져오고, 가공이 가능하다
 (intelliJ를 사용할 수 없는 상황이라 youtube 영상을 참고하였음)
<img src="" alt="img" style="width: 50% height:30%">
Link:https://www.youtube.com/watch?v=gSSsZReIFRk


<img src="https://file.notion.so/f/f/649a15f1-a9e3-45d3-b23d-bb09016ffaf3/d90bbc4f-0515-4618-bbe3-11a65b133d49/image.png?table=block&id=11985d67-a342-80d3-b208-ecbfb73c12f7&spaceId=649a15f1-a9e3-45d3-b23d-bb09016ffaf3&expirationTimestamp=1729216800000&signature=8Urz7Kt-z8gDGPRhZxECpLr_l1mcM6hn9gI5dsYytJc&downloadName=image.png" alt="img" style="width: 50% height:30%">

해당 page를 async(asynchronous / 비동기 방식)방식으로
fetch(’’)의 데이터를 await키워드를 이용해서 데이터를 다 받을때 까지 기다려서 res변수에 넣고,
다시 data에도 await키워드를 사용해서 위에서 변수res에 넣은 데이터를 JSON형식으로 넣은뒤
{data.id}로 해당 페이지의 JSON데이터중, id값에 해당하는 데이터를 출력한다
  <img src="https://file.notion.so/f/f/649a15f1-a9e3-45d3-b23d-bb09016ffaf3/dc441b4a-3d68-441a-95cc-c5fd4d04076a/image.png?table=block&id=11985d67-a342-80c9-b777-f93a4fbf68aa&spaceId=649a15f1-a9e3-45d3-b23d-bb09016ffaf3&expirationTimestamp=1729216800000&signature=AjDXGgRfjDY8DZYSUKavv53AbCUMBvNvsBwyIyzTvvM&downloadName=image.png" alt="img" style="width: 50% height:30%">  

또한 TypeScriptXML파일이므로 Repository로 해당 fetch값들의 이름,타입을 가져와서

<img src="https://file.notion.so/f/f/649a15f1-a9e3-45d3-b23d-bb09016ffaf3/253ba567-a80c-4c09-9507-adee9a418a59/image.png?table=block&id=11985d67-a342-8061-b82c-dfb2de236a68&spaceId=649a15f1-a9e3-45d3-b23d-bb09016ffaf3&expirationTimestamp=1729216800000&signature=hkx7_phFJq5SOtEBwVvYIn0qNfvSfOV_jrYupcaA-p4&downloadName=image.png" alt="img" style="width: 50% height:30%">

<img src="https://file.notion.so/f/f/649a15f1-a9e3-45d3-b23d-bb09016ffaf3/c8a752f7-16fa-4ad5-beab-1bef3e8ac03b/image.png?table=block&id=11985d67-a342-80a9-a327-eb1f80a1e9d6&spaceId=649a15f1-a9e3-45d3-b23d-bb09016ffaf3&expirationTimestamp=1729216800000&signature=qW5vcjxakcNhE-5vkx2rbnpZTsJhw7pXHz2Zdxs1eiI&downloadName=image.png" alt="img" style="width: 50% height:30%">

위와 같이 간단하게 관리할 수 있다

또한 layout에 추가하여 관리도 가능하다
<img src="https://file.notion.so/f/f/649a15f1-a9e3-45d3-b23d-bb09016ffaf3/261e59c0-2a81-4074-9740-10410908d147/image.png?table=block&id=11985d67-a342-80b8-8a54-cfac188f1cd7&spaceId=649a15f1-a9e3-45d3-b23d-bb09016ffaf3&expirationTimestamp=1729216800000&signature=GeFTlnuf8Uw9SL1hu6GZ2W9Bvt-XN8Lf7gYTjIgVwuw&downloadName=image.png" alt="img" style="width: 50% height:30%">

+시간도 관리 가능
이때 시간을 revalidate : 5 를 주어 5초마다 해당 데이터를 update시킬 수 있다
<img src="https://file.notion.so/f/f/649a15f1-a9e3-45d3-b23d-bb09016ffaf3/cdb1fa81-37b8-435f-9db7-7fb18b1a5e35/image.png?table=block&id=11985d67-a342-80d6-9565-f047f37f53b5&spaceId=649a15f1-a9e3-45d3-b23d-bb09016ffaf3&expirationTimestamp=1729216800000&signature=cSQRucZIofr9eaGxapcjIYJ_7J8XYY8th_4uvZC8OTw&downloadName=image.png" alt="img" style="width: 50% height:30%">

# Course 8 (Fetching Data)

+ 먼저 DB를 fetching해오기 위해서는 lib/data.ts 폴더에서 sql의 문법에 맞게 DB테이블을 생성해야 한다 이때 테이블의 데이터는 자동으로 가져오기 때문에 기존의 SQL문법만 숙지하고 있으면 테이블 생성시 이에 해당하는 데이터를 자동으로 채워준다

### 코드

```jsx
import { sql } from '@vercel/postgres';
import {
  CustomerField,
  CustomersTableType,
  InvoiceForm,
  InvoicesTable,
  LatestInvoiceRaw,
  Revenue,
} from './definitions';
import { formatCurrency } from './utils';

export async function fetchRevenue() {
  try {
    // Artificially delay a response for demo purposes.
    // Don't do this in production :)

    console.log('Fetching revenue data...');
    await new Promise((resolve) => setTimeout(resolve, 3000));

    const data = await sql<Revenue>`SELECT * FROM revenue`;

    console.log('Data fetch completed after 3 seconds.');

    return data.rows;
  } catch (error) {
    console.error('Database Error:', error);
    throw new Error('Failed to fetch revenue data.');
  }
}

export async function fetchLatestInvoices() {
  try {
    const data = await sql<LatestInvoiceRaw>`
      SELECT invoices.amount, customers.name, customers.image_url, customers.email, invoices.id
      FROM invoices
      JOIN customers ON invoices.customer_id = customers.id
      ORDER BY invoices.amount DESC
      LIMIT 10`;

    const latestInvoices = data.rows.map((invoice) => ({
      ...invoice,
      amount: formatCurrency(invoice.amount),
    }));
    return latestInvoices;
  } catch (error) {
    console.error('Database Error:', error);
    throw new Error('Failed to fetch the latest invoices.');
  }
}

export async function fetchCardData() {
  try {
    // You can probably combine these into a single SQL query
    // However, we are intentionally splitting them to demonstrate
    // how to initialize multiple queries in parallel with JS.
    const invoiceCountPromise = sql`SELECT COUNT(*) FROM invoices`;
    const customerCountPromise = sql`SELECT COUNT(*) FROM customers`;
    const invoiceStatusPromise = sql`SELECT
         SUM(CASE WHEN status = 'paid' THEN amount ELSE 0 END) AS "paid",
         SUM(CASE WHEN status = 'pending' THEN amount ELSE 0 END) AS "pending"
         FROM invoices`;

    const data = await Promise.all([
      invoiceCountPromise,
      customerCountPromise,
      invoiceStatusPromise,
    ]);

    const numberOfInvoices = Number(data[0].rows[0].count ?? '0');
    const numberOfCustomers = Number(data[1].rows[0].count ?? '0');
    const totalPaidInvoices = formatCurrency(data[2].rows[0].paid ?? '0');
    const totalPendingInvoices = formatCurrency(data[2].rows[0].pending ?? '0');

    return {
      numberOfCustomers,
      numberOfInvoices,
      totalPaidInvoices,
      totalPendingInvoices,
    };
  } catch (error) {
    console.error('Database Error:', error);
    throw new Error('Failed to fetch card data.');
  }
}

const ITEMS_PER_PAGE = 6;
export async function fetchFilteredInvoices(
  query: string,
  currentPage: number,
) {
  const offset = (currentPage - 1) * ITEMS_PER_PAGE;

  try {
    const invoices = await sql<InvoicesTable>`
      SELECT
        invoices.id,
        invoices.amount,
        invoices.date,
        invoices.status,
        customers.name,
        customers.email,
        customers.image_url
      FROM invoices
      JOIN customers ON invoices.customer_id = customers.id
      WHERE
        customers.name ILIKE ${`%${query}%`} OR
        customers.email ILIKE ${`%${query}%`} OR
        invoices.amount::text ILIKE ${`%${query}%`} OR
        invoices.date::text ILIKE ${`%${query}%`} OR
        invoices.status ILIKE ${`%${query}%`}
      ORDER BY invoices.date DESC
      LIMIT ${ITEMS_PER_PAGE} OFFSET ${offset}
    `;

    return invoices.rows;
  } catch (error) {
    console.error('Database Error:', error);
    throw new Error('Failed to fetch invoices.');
  }
}

export async function fetchInvoicesPages(query: string) {
  try {
    const count = await sql`SELECT COUNT(*)
    FROM invoices
    JOIN customers ON invoices.customer_id = customers.id
    WHERE
      customers.name ILIKE ${`%${query}%`} OR
      customers.email ILIKE ${`%${query}%`} OR
      invoices.amount::text ILIKE ${`%${query}%`} OR
      invoices.date::text ILIKE ${`%${query}%`} OR
      invoices.status ILIKE ${`%${query}%`}
  `;

    const totalPages = Math.ceil(Number(count.rows[0].count) / ITEMS_PER_PAGE);
    return totalPages;
  } catch (error) {
    console.error('Database Error:', error);
    throw new Error('Failed to fetch total number of invoices.');
  }
}

export async function fetchInvoiceById(id: string) {
  try {
    const data = await sql<InvoiceForm>`
      SELECT
        invoices.id,
        invoices.customer_id,
        invoices.amount,
        invoices.status
      FROM invoices
      WHERE invoices.id = ${id};
    `;

    const invoice = data.rows.map((invoice) => ({
      ...invoice,
      // Convert amount from cents to dollars
      amount: invoice.amount / 100,
    }));

    return invoice[0];
  } catch (error) {
    console.error('Database Error:', error);
    throw new Error('Failed to fetch invoice.');
  }
}

export async function fetchCustomers() {
  try {
    const data = await sql<CustomerField>`
      SELECT
        id,
        name
      FROM customers
      ORDER BY name ASC
    `;

    const customers = data.rows;
    return customers;
  } catch (err) {
    console.error('Database Error:', err);
    throw new Error('Failed to fetch all customers.');
  }
}

export async function fetchFilteredCustomers(query: string) {
  try {
    const data = await sql<CustomersTableType>`
		SELECT
		  customers.id,
		  customers.name,
		  customers.email,
		  customers.image_url,
		  COUNT(invoices.id) AS total_invoices,
		  SUM(CASE WHEN invoices.status = 'pending' THEN invoices.amount ELSE 0 END) AS total_pending,
		  SUM(CASE WHEN invoices.status = 'paid' THEN invoices.amount ELSE 0 END) AS total_paid
		FROM customers
		LEFT JOIN invoices ON customers.id = invoices.customer_id
		WHERE
		  customers.name ILIKE ${`%${query}%`} OR
        customers.email ILIKE ${`%${query}%`}
		GROUP BY customers.id, customers.name, customers.email, customers.image_url
		ORDER BY customers.name ASC
	  `;

    const customers = data.rows.map((customer) => ({
      ...customer,
      total_pending: formatCurrency(customer.total_pending),
      total_paid: formatCurrency(customer.total_paid),
    }));

    return customers;
  } catch (err) {
    console.error('Database Error:', err);
    throw new Error('Failed to fetch customer table.');
  }
}

```

page.tsx에서 사용시에는 `import { sql } from '@vercel/postgres';` 로 SQL을 import하고.

각각 데이터를 fetching시켜야 출력이 가능하다,

UI폴더에서 fetch시킬 데이터의 UI를 생성하고

page에서 값을 받아와 출력한다ㄴ

### page 코드

```jsx
import { Card } from '@/app/ui/dashboard/cards';
import RevenueChart from '@/app/ui/dashboard/revenue-chart';
import LatestInvoices from '@/app/ui/dashboard/latest-invoices';
import { lusitana } from '@/app/ui/fonts';
import {fetchLatestInvoices, fetchRevenue} from "@/app/lib/data";

export default async function Page() {
    const revenue = await fetchRevenue();
    const latestInvoices = await fetchLatestInvoices();
    return (
        <main>
            <h1 className={`${lusitana.className} mb-4 text-xl md:text-2xl`}>
                Dashboard
            </h1>
            <div className="grid gap-6 sm:grid-cols-2 lg:grid-cols-4">
                {/* <Card title="Collected" value={totalPaidInvoices} type="collected" /> */}
                {/* <Card title="Pending" value={totalPendingInvoices} type="pending" /> */}
                {/* <Card title="Total Invoices" value={numberOfInvoices} type="invoices" /> */}
                {/* <Card
          title="Total Customers"
          value={numberOfCustomers}
          type="customers"
        /> */}
            </div>
            <div className="mt-6 grid grid-cols-1 gap-6 md:grid-cols-4 lg:grid-cols-8">
                { <RevenueChart revenue={revenue}  /> }
                { <LatestInvoices latestInvoices={latestInvoices} /> }
            </div>
        </main>
    );
}
```

### revenue-chart

```jsx
import { generateYAxis } from '@/app/lib/utils';
import { CalendarIcon } from '@heroicons/react/24/outline';
import { lusitana } from '@/app/ui/fonts';
import { fetchRevenue } from '@/app/lib/data';

// This component is representational only.
// For data visualization UI, check out:
// https://www.tremor.so/
// https://www.chartjs.org/
// https://airbnb.io/visx/

export default async function RevenueChart() {
  const revenue = await fetchRevenue();

  const chartHeight = 350;
  // NOTE: Uncomment this code in Chapter 7

  const { yAxisLabels, topLabel } = generateYAxis(revenue);

  if (!revenue || revenue.length === 0) {
     return <p className="mt-4 text-gray-400">No data available.</p>;
   }

  return (
    <div className="w-full md:col-span-4">
      <h2 className={`${lusitana.className} mb-4 text-xl md:text-2xl`}>
        Recent Revenue
      </h2>

      {/* NOTE: Uncomment this code in Chapter 7 */}

      <div className="rounded-xl bg-gray-50 p-4">
        <div className="sm:grid-cols-13 mt-0 grid grid-cols-12 items-end gap-2 rounded-md bg-white p-4 md:gap-4">
          <div
            className="mb-6 hidden flex-col justify-between text-sm text-gray-400 sm:flex"
            style={{ height: `${chartHeight}px` }}
          >
            {yAxisLabels.map((label) => (
              <p key={label}>{label}</p>
            ))}
          </div>

          {revenue.map((month) => (
            <div key={month.month} className="flex flex-col items-center gap-2">
              <div
                className="w-full rounded-md bg-blue-300"
                style={{
                  height: `${(chartHeight / topLabel) * month.revenue}px`,
                }}
              ></div>
              <p className="-rotate-90 text-sm text-gray-400 sm:rotate-0">
                {month.month}
              </p>
            </div>
          ))}
        </div>
        <div className="flex items-center pb-2 pt-6">
          <CalendarIcon className="h-5 w-5 text-gray-500" />
          <h3 className="ml-2 text-sm text-gray-500 ">Last 12 months</h3>
        </div>
      </div>
    </div>
  );
}

```

### Card의 data.ts

select문으로 해당 데이터의 값을 가져온뒤 sum으로 계산을 하고

await Promise.all([])을 사용하여 parallel data fetching을 사용한다

```jsx

export async function fetchCardData() {
  try {
    // You can probably combine these into a single SQL query
    // However, we are intentionally splitting them to demonstrate
    // how to initialize multiple queries in parallel with JS.
    const invoiceCountPromise = sql`SELECT COUNT(*) FROM invoices`;
    const customerCountPromise = sql`SELECT COUNT(*) FROM customers`;
    const invoiceStatusPromise = sql`SELECT
         SUM(CASE WHEN status = 'paid' THEN amount ELSE 0 END) AS "paid",
         SUM(CASE WHEN status = 'pending' THEN amount ELSE 0 END) AS "pending"
         FROM invoices`;

    const data = await Promise.all([
      invoiceCountPromise,
      customerCountPromise,
      invoiceStatusPromise,
    ]);

    const numberOfInvoices = Number(data[0].rows[0].count ?? '0');
    const numberOfCustomers = Number(data[1].rows[0].count ?? '0');
    const totalPaidInvoices = formatCurrency(data[2].rows[0].paid ?? '0');
    const totalPendingInvoices = formatCurrency(data[2].rows[0].pending ?? '0');

    return {
      numberOfCustomers,
      numberOfInvoices,
      totalPaidInvoices,
      totalPendingInvoices,
    };
  } catch (error) {
    console.error('Database Error:', error);
    throw new Error('Failed to fetch card data.');
  }
}
```

### Card의 page.tsx

```jsx
import {fetchCardData, fetchLatestInvoices, fetchRevenue} from "@/app/lib/data";

const { numberOfCustomers,
        numberOfInvoices,
        totalPaidInvoices,
        totalPendingInvoices} = await fetchCardData();
return(
 <div className="grid gap-6 sm:grid-cols-2 lg:grid-cols-4">
                <Card title="Collected" value={totalPaidInvoices} type="collected" />
                <Card title ="pending" type="pending" value={totalPendingInvoices}></Card>
                <Card title="Total Invoices" value={numberOfInvoices} type="invoices" />
                <Card  title = "number of customers" value={numberOfCustomers} type={"customers"}></Card>
            </div>
            )
```

### Card의 cards.tsx

```jsx
import {
  BanknotesIcon,
  ClockIcon,
  UserGroupIcon,
  InboxIcon,
} from '@heroicons/react/24/outline';
import { fetchCardData } from "@/app/lib/data";
import { lusitana } from '@/app/ui/fonts';

const iconMap = {
  collected: BanknotesIcon,
  customers: UserGroupIcon,
  pending: ClockIcon,
  invoices: InboxIcon,
};

export default async function CardWrapper() {
  const {
    numberOfInvoices,
    numberOfCustomers,
    totalPaidInvoices,
    totalPendingInvoices,
  } = await fetchCardData();

  return (
    <>
      {/* NOTE: Uncomment this code in Chapter 9 */}

      <Card title="Collected" value={totalPaidInvoices} type="collected" />
      <Card title="Pending" value={totalPendingInvoices} type="pending" />
      <Card title="Total Invoices" value={numberOfInvoices} type="invoices" />
      <Card
        title="Total Customers"
        value={numberOfCustomers}
        type="customers"
      />
    </>
  );
}

export function Card({
  title,
  value,
  type,
}: {
  title: string;
  value: number | string;
  type: 'invoices' | 'customers' | 'pending' | 'collected';
}) {
  const Icon = iconMap[type];

  return (
    <div className="rounded-xl bg-gray-50 p-2 shadow-sm">
      <div className="flex p-4">
        {Icon ? <Icon className="h-5 w-5 text-gray-700" /> : null}
        <h3 className="ml-2 text-sm font-medium">{title}</h3>
      </div>
      <p
        className={`${lusitana.className}
          truncate rounded-xl bg-white px-4 py-8 text-center text-2xl`}
      >
        {value}
      </p>
    </div>
  );
}

```

# Course 9 (Randering)

- 정적(Static) vs 동적(Dynamic) Rendering
   + 정적 랜더링은 따로 데이터를 받아오는것 없이 그대로 출력되는 데이터를 의미(배경색 등등)
   + 동적 랜더링은 따로 데이터를 받아와 해당 값에 맞는 결과를 출력하는 데이터를 의미(현재 접속자 수 등등)
   + 이때 랜더링시 데이터가 전부 로드되지 않은경우에 로드되는 상황을 막기위해 java에서 time.sleep()과 같이  데이터가 로드될 수 있도록 setTimeout을 사용할 수 있다

```jsx
export async function fetchRevenue() {
  try {
    // Artificially delay a response for demo purposes.
    // Don't do this in production :)

    console.log('Fetching revenue data...');
    await new Promise((resolve) => setTimeout(resolve, 3000));
//3000ms, 즉 3초 지연
    const data = await sql<Revenue>`SELECT * FROM revenue`;

    console.log('Data fetch completed after 3 seconds.');

    return data.rows;
  } catch (error) {
    console.error('Database Error:', error);
    throw new Error('Failed to fetch revenue data.');
  }

```


# Course 10 (Streaming)

Straming은 페이지가 로딩될때 loading… 등과 같이 적절한 대체구문을 보여줄 수 있게한다

(Loading…출력됨)

loading.tsx는 일반적인 page.tsx들과는 달리 상위에 위치해야 하므로 해당 폴더들이 위치한 root에 (overview)라는 이름으로 폴더를 만들고, page.tsx파일을 해당 위치로 옮기면 사용자의 데이터를 불러오기 전까지 loading.tsx에 있는 대체문구/사진 등이 출력된다

```jsx
export default function Loading() {
  return <div>Loading...</div>;
}
```
<img src="https://file.notion.so/f/f/649a15f1-a9e3-45d3-b23d-bb09016ffaf3/bcfb21f0-4e93-4c7c-b19d-ef415ca18a22/image.png?table=block&id=11b85d67-a342-80bf-8928-c6e0e897f1dd&spaceId=649a15f1-a9e3-45d3-b23d-bb09016ffaf3&expirationTimestamp=1729296000000&signature=cSLQX_gJ_QNNZ9rDx2NiMvbC7HrPJ7mPvLHcB6x9lzg&downloadName=image.png" alt="" style="width:50% height: 50%">
![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/649a15f1-a9e3-45d3-b23d-bb09016ffaf3/bcfb21f0-4e93-4c7c-b19d-ef415ca18a22/image.png)

이때  단순히 텍스트로 대체하는 것이 아니라 빈 데이터를 가진 뼈대만 보여줄 수 있는데(Skleton) 

동일한 방법으로 loading.tsx파일에 return 부분에

```jsx
import DashboardSkeleton from "@/app/ui/skeletons";
export default function Loading(){
    /*return   <p>loadin.../</p>*/
return <DashboardSkeleton/>;
}
```

<DashboardSkleton/>을 사용하면  skelton이 적용된다 
<img src="https://file.notion.so/f/f/649a15f1-a9e3-45d3-b23d-bb09016ffaf3/053b0a51-a808-45a7-a78e-61df4c1a164f/image.png?table=block&id=11b85d67-a342-8050-bee3-e8293b714cca&spaceId=649a15f1-a9e3-45d3-b23d-bb09016ffaf3&expirationTimestamp=1729296000000&signature=f6KleImNTfDV39R2-AFyZhu3qEalaCKbpZXfD3vZ1Ik&downloadName=image.png" alt="" style="width:50% height: 50%">

### 개별로 skelton을 적용시키려면

1. `import {RevenueChartSkeleton,LatestInvoicesSkeleton,CardSkeleton} from "@/app/ui/skeletons";`
와 같이 미리 UI에서 만들어둔 skeletons를 불러온다
2. fallback으로 출력하려는 데이터를 스켈레튼으로 한번 감싸 출력하고자 하는 데이터가 출력되기 전에 스켈레톤이 먼저 출력되도록 한다 
3. 이떄 page에서는 기존의 출력문구가 필요 없으므로 생략한다
    
    ```jsx
     <div className="grid gap-6 sm:grid-cols-2 lg:grid-cols-4">
    {/*                <Card title="Collected" value={totalPaidInvoices} type="collected" />
                    <Card title ="pending" type="pending" value={totalPendingInvoices}></Card>
                    <Card title="Total Invoices" value={numberOfInvoices} type="invoices" />
                    <Card  title = "number of customers" value={numberOfCustomers} type={"customers"}></Card>*/}
                    <Suspense fallback={<CardSkeleton/>}>
                        <CardWrapper/>
                    </Suspense>
                </div>
    ```
    
    ### 전체코드
    
    ```jsx
    import { Card } from '@/app/ui/dashboard/cards';
    import RevenueChart from '@/app/ui/dashboard/revenue-chart';
    import LatestInvoices from '@/app/ui/dashboard/latest-invoices';
    import { lusitana } from '@/app/ui/fonts';
    import {fetchCardData} from "@/app/lib/data";
    import { Suspense } from "react";
    import {RevenueChartSkeleton,LatestInvoicesSkeleton,CardSkeleton} from "@/app/ui/skeletons";
    import CardWrapper from '@/app/ui/dashboard/cards'
    
    export default async function Page() {
        const { numberOfCustomers,
            numberOfInvoices,
            totalPaidInvoices,
            totalPendingInvoices} = await fetchCardData();
    
        return (
            <main>
                <h1 className={`${lusitana.className} mb-4 text-xl md:text-2xl`}>
                    Dashboard
                </h1>
    
                <div className="grid gap-6 sm:grid-cols-2 lg:grid-cols-4">
                    <Card title="Collected" value={totalPaidInvoices} type="collected" />
                    <Card title ="pending" type="pending" value={totalPendingInvoices}></Card>
                    <Card title="Total Invoices" value={numberOfInvoices} type="invoices" />
                    <Card  title = "number of customers" value={numberOfCustomers} type={"customers"}></Card>
                </div>
                <div className="mt-6 grid grid-cols-1 gap-6 md:grid-cols-4 lg:grid-cols-8">
                    <Suspense fallback={<CardSkeleton/>}>
                        <CardWrapper/>
                    </Suspense> 
                    
                    <Suspense fallback={<RevenueChartSkeleton />}>
                        <RevenueChart/>
                    </Suspense>
                    <Suspense fallback={<LatestInvoicesSkeleton />}>
                        <LatestInvoices />
                    </Suspense>
    
                </div>
            </main>
        );
    }
    ```
    
    ```jsx
    import { ArrowPathIcon } from '@heroicons/react/24/outline';
    import clsx from 'clsx';
    import Image from 'next/image';
    import { lusitana } from '@/app/ui/fonts';
    import { fetchLatestInvoices } from '@/app/lib/data';
    
    export default async function LatestInvoices(){
      const latestInvoices = await fetchLatestInvoices();
      return (
        <div className="flex w-full flex-col md:col-span-4">
          <h2 className={`${lusitana.className} mb-4 text-xl md:text-2xl`}>
            Latest Invoices
          </h2>
          <div className="flex grow flex-col justify-between rounded-xl bg-gray-50 p-4">
    
            <div className="bg-white px-6">
              {latestInvoices.map((invoice, i) => {
                return (
                  <div
                    key={invoice.id}
                    className={clsx(
                      'flex flex-row items-center justify-between py-4',
                      {
                        'border-t': i !== 0,
                      },
                    )}
                  >
                    <div className="flex items-center">
                      <Image
                        src={invoice.image_url}
                        alt={`${invoice.name}'s profile picture`}
                        className="mr-4 rounded-full"
                        width={32}
                        height={32}
                      />
                      <div className="min-w-0">
                        <p className="truncate text-sm font-semibold md:text-base">
                          {invoice.name}
                        </p>
                        <p className="hidden text-sm text-gray-500 sm:block">
                          {invoice.email}
                        </p>
                      </div>
                    </div>
                    <p
                      className={`${lusitana.className} truncate text-sm font-medium md:text-base`}
                    >
                      {invoice.amount}
                    </p>
                  </div>
                );
              })}
            </div>
            <div className="flex items-center pb-2 pt-6">
              <ArrowPathIcon className="h-5 w-5 text-gray-500" />
              <h3 className="ml-2 text-sm text-gray-500 ">Updated just now</h3>
            </div>
          </div>
        </div>
      );
    }
    
    ```
    
    ```jsx
    import {
      BanknotesIcon,
      ClockIcon,
      UserGroupIcon,
      InboxIcon,
    } from '@heroicons/react/24/outline';
    import {fetchCardData} from "@/app/lib/data";
    import { lusitana } from '@/app/ui/fonts';
    
    const iconMap = {
      collected: BanknotesIcon,
      customers: UserGroupIcon,
      pending: ClockIcon,
      invoices: InboxIcon,
    };
    
    export default async function CardWrapper() {
      const {
        numberOfInvoices,
        numberOfCustomers,
        totalPaidInvoices,
        totalPendingInvoices,
      } = await fetchCardData();
    
      return (
        <>
          {/* NOTE: Uncomment this code in Chapter 9 */}
    
          <Card title="Collected" value={totalPaidInvoices} type="collected" />
          <Card title="Pending" value={totalPendingInvoices} type="pending" />
          <Card title="Total Invoices" value={numberOfInvoices} type="invoices" />
          <Card
            title="Total Customers"
            value={numberOfCustomers}
            type="customers"
          />
        </>
      );
    }
    
    export function Card({
      title,
      value,
      type,
    }: {
      title: string;
      value: number | string;
      type: 'invoices' | 'customers' | 'pending' | 'collected';
    }) {
      const Icon = iconMap[type];
    
      return (
        <div className="rounded-xl bg-gray-50 p-2 shadow-sm">
          <div className="flex p-4">
            {Icon ? <Icon className="h-5 w-5 text-gray-700" /> : null}
            <h3 className="ml-2 text-sm font-medium">{title}</h3>
          </div>
          <p
            className={`${lusitana.className}
              truncate rounded-xl bg-white px-4 py-8 text-center text-2xl`}
          >
            {value}
          </p>
        </div>
      );
    }
    
    ```
 # Course 11 (Partial Prerendering)

- Partial Prerendering: 부분 사전 랜더링은
   + 장바구니에 상품추가, 인원수 추가 등등의 상황시에 모든 데이터를 동적으로 만들 필요가 없기 때문에 동적인 랜더링이 필요한 부분에만 Partial Prerendering을 사용할 수 있다
   + (아래와 같이 동적과 정적인 부분의 구분되어있을 경우에도 작동한다)
<img src="https://file.notion.so/f/f/649a15f1-a9e3-45d3-b23d-bb09016ffaf3/b23ea195-154c-4ac5-90d7-44cb02877d16/image.png?table=block&id=11b85d67-a342-80a0-bb62-d63dc4e1671d&spaceId=649a15f1-a9e3-45d3-b23d-bb09016ffaf3&expirationTimestamp=1729224000000&signature=aN8tXkdxZBHv66CbH8FEbNUeQ6MdQ4odHbrMNHhNOJ4&downloadName=image.png" alt="img" style="width:50% height:50%">

Partial Prerendering을 적용시키려면 

1. next.Config.mjs 에서  `experimental:{ppr: 'incremental',}` 을 추가한다
2. layout.tsx에서  `export const *experimental_ppr* = true;` 로 활성화 시킨다

```jsx
import '@/app/ui/global.css';
import {inter} from '@/app/ui/fonts';
export const experimental_ppr = true;
export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
      <html lang="en">
        <body className={`${inter.className} antialiased`}>{children}</body>
      </html>
  );

}

```

```jsx
/** @type {import('next').NextConfig} */

const nextConfig = {
    experimental:{
        ppr: 'incremental',
    },
};

export default nextConfig;

```

# Course 12 (pagination)

타임리프에서 사용하는 방식과 같이 url주소에 따라 출력하는 방식을 사용하며

1. 특정 페이지에 북마크가 가능하다
2. serve rside Randering방식이다
3. 쉽게 추적이 가능하다 
4. 검색버튼의 클릭없이 바로 검색이 가능하게 만들 수 있다

의 특징이 있다

• **`useSearchParams`**- Allows you to access the parameters of the current URL. For example, the search params for this URL `/dashboard/invoices?page=1&query=pending` would look like this: `{page: '1', query: 'pending'}`.
- serachparams를 사용하면 위와 같이 URL이 나오고 해당 정보를 가져와서 출력한다

## 검색 작동순서

1. Capture the user's input.

input에 입력된 값을 String 타입으로 가져와서 해당값을 캡쳐한다

```jsx
  function handleSearch(term: string) {
    console.log(term);
  }
  return (
        onChange={(e) => {
          handleSearch(e.target.value);
  );
}
```

1. Update the URL with the search params.
`useSearchParams`에서 후크 를 가져와 `'next/navigation'`변수에 할당한뒤,

 `const params = new URLSearchParams(searchParams);` 에서 새로운 변수로  할당한다 
(URLSearchParams의 변수로 할당하면 ?page=1&query=a 과 같이 출력됨)

현재 검색창은 별도의 검색버튼 없이 검색값 입력시 바로 출력되므로 
검색창의 데이터 유뮤를 받아와서 term(입력값)이 있는경우에는 해당 결과값으로 검색될 수 있게 replace메서드를 사용하여 검색값으로 유지되게 하고
검색값이 없을경우 초기값이 출력되게 만든다

```tsx
'use client';
 
import { MagnifyingGlassIcon } from '@heroicons/react/24/outline';
import { useSearchParams, usePathname, useRouter } from 'next/navigation';
 
export default function Search() {
  const searchParams = useSearchParams();
  const pathname = usePathname();
  const { replace } = useRouter();
 
  function handleSearch(term: string) {
    const params = new URLSearchParams(searchParams);
    if (term) {
      params.set('query', term);
    } else {
      params.delete('query');
    }
    replace(`${pathname}?${params.toString()}`);
  }
}
```

여기서 pathname은 파일의 pathname을 의미하고

params.toString()는 사용자가 입력한 값으로 해당 값을 받아와서  URL의 주소를 업데이트 한다
<img src="https://file.notion.so/f/f/649a15f1-a9e3-45d3-b23d-bb09016ffaf3/b23ea195-154c-4ac5-90d7-44cb02877d16/image.png?table=block&id=11b85d67-a342-80a0-bb62-d63dc4e1671d&spaceId=649a15f1-a9e3-45d3-b23d-bb09016ffaf3&expirationTimestamp=1729224000000&signature=aN8tXkdxZBHv66CbH8FEbNUeQ6MdQ4odHbrMNHhNOJ4&downloadName=image.png" alt="img" style="width:50% height:50%">
1. (https://nextjs.org/learn/dashboard-app/adding-search-and-pagination#3-keeping-the-url-and-input-in-sync)
value 속성: 입력된 값을 설정하는 value값
dafaultvalue 속성: 초기값을 설정하는 value값
이떄 defaultvalue를 사용하는 이유는 혹시모를 오류방지를 위해 아무것도 검색되지 않은 상태에서는 value(현재 상태에서는 검색값이 없으므로 “”)로 지정하고
사용자가 값을 입력했을 경우에는** handleSearch(e.target.value);로 해당값을 받아와서 value의 값으로 지정한다
    
    ```tsx
    <input
    className="peer block w-full rounded-md border border-gray-200 py-[9px] pl-10 text-sm outline-2 placeholder:text-gray-500"
    placeholder={placeholder}
    onChange={(e) => {
    handleSearch(e.target.value);
    }}
    defaultValue={searchParams.get('query')?.toString()}
    />
    ```
    
2. Update the table to reflect the search query.
Table에서 검색 쿼리를 반영하기 위해 삼향연산자를 사용하여 입력된 값과 , 변수타입을 지정하여 검색한다
    
    ```tsx
    export default async function Page({
      searchParams,
    }: {
      searchParams?: {
        query?: string;
        page?: string;
      };
    }) {
      const query = searchParams?.query || '';
      const currentPage = Number(searchParams?.page) || 1;
    
    ```
    

### Debouncing

이때 검색창을 클릭해서 검색을 하는것이 아니기 때문에 “Dean”을 검색하려고 했을경우 “D”,”De”,”Dea”,”Dean”이렇게 4가지가 반복해서 검색되어 속도의 저하가 발생할 수 있다

따라서 디바운스를 주어 특정시간 (300ms등)이 지난후에 코드가 실행되도록 할 수 있다

1. pnpm i use-debounce로 설치
2. import, useDebouncedCallback((term) 사용 및

replace(`${pathname}?${params.toString()}`);
}, 300);  검색어/URL이 replace되는 검색값 뒤에 delay시간을 주어 300ms가 지난후에 코드가 실행되도록 할 수 있다

```tsx
import { useDebouncedCallback} from "use-debounce";

const handleSearch = useDebouncedCallback((term) => { 

  replace(`${pathname}?${params.toString()}`);
}, 300);
```

### pagination

아래의 코드로 페이지를 import한뒤, totalpage를 가져온다(페이지네이션 계산은 data.xml에서 실시함) 

이때 

```tsx
import { fetchInvoicesPages } from '@/app/lib/data';

 const totalPages = await fetchInvoicesPages(query);
 
```

pagination 컴포넌트가 작동하면 클라이언트 구성요소임을 확인할 수 있는데 이때 클라이언트에서 데이터를 가져오면 DB 테이블이 노출되므로 서버에서 데이터를 가져와서 전달시킬 수 있다(자바에서 DTO?)

작동 방식은
1. 
사용자가 페이지네이션 클릭시 pagination및 hook를 가져와, usePathname, useSearchParams를 사용하여 현제페이지와 새 페이지를 설정한다(+-2페이지 )

```jsx
import { usePathname, useSearchParams } from 'next/navigation';
 
export default function Pagination({ totalPages }: { totalPages: number }) {
  const pathname = usePathname();
  const searchParams = useSearchParams();
  const currentPage = Number(searchParams.get('page')) || 1;
 
```

2. 
Componenet내부에 createPageURL이라는 함수를 만들고, 검색에서 사용하는 함수와 비슷하게 URLSearchParams를 사용하여 새 페이지에 할당한

```jsx
  const createPageURL = (pageNumber: number | string) => {
    const params = new URLSearchParams(searchParams);
    params.set('page', pageNumber.toString());
    return `${pathname}?${params.toString()}`;
  };
```

1. 
createPageURL이 현재 검색 매개변수의 인스턴스를 생성한뒤, page매개변수를 선택된 페이지 번호로 업데이트하면 페이지 네이션이 작동한다(검색시 input에 있는 DefaultValue값을 사용자가 입력한 value값으로 업데이트 하는것과 같이 사용자가 선택한 page의 값을 현재 page의 값으로 업데이트)

```jsx
'use client';
 
import { MagnifyingGlassIcon } from '@heroicons/react/24/outline';
import { usePathname, useRouter, useSearchParams } from 'next/navigation';
import { useDebouncedCallback } from 'use-debounce';
 
export default function Search({ placeholder }: { placeholder: string }) {
  const searchParams = useSearchParams();
  const { replace } = useRouter();
  const pathname = usePathname();
 
  const handleSearch = useDebouncedCallback((term) => {
    const params = new URLSearchParams(searchParams);
    params.set('page', '1');
    if (term) {
      params.set('query', term);
    } else {
      params.delete('query');
    }
    replace(`${pathname}?${params.toString()}`);
  }, 300);
 
```

# Course 13 (Mutating Data)

여기서는 invocie를 예시로 form데이터 Create,Read,Update,Delete(CRUD)를 설명함

- What React Server Actions are and how to use them to mutate data.
- How to work with forms and Server Components. (양식 및 서버 구성요소)
- Best practices for working with the native `formData` object, including type validation.(validation 검사)
- How to revalidate the client cache using the `revalidatePath` API.(revalidatPath API사용법)
- How to create dynamic route segments with specific IDs. (특정 ID로 동적 route 구간을 만드는법)

### 예시 코드

```jsx

// Server Component
export default function Page() {
  // Action
  async function create(formData: FormData) {
    'use server';
 
    // Logic to mutate data...
  }
 
  // Invoke the action using the "action" attribute
  return <form action={create}>...</form>;
}

```

위 코드는 form태그를 async방식, 즉 비동기 방식으로 생성한 것으로  formData Type으로 받은 FormData를 async방식의 create메서드로 만들고, 이를 반환한다
이떄 비동기 방식이 사용된 이유는 formdata가 전송될때 Synchronous방식으로 전송되면 UI가 멈추는등이 발생하므로 Asynchronous방식으로 전송한다

### 사용예시 (invoice 생성)

1. invoice를 출력할 페이지를 만든다
    <img src="https://file.notion.so/f/f/649a15f1-a9e3-45d3-b23d-bb09016ffaf3/cdd7acc3-5088-474a-b9da-770fd1d40029/image.png?table=block&id=11e85d67-a342-80fd-9e28-fefba0447821&spaceId=649a15f1-a9e3-45d3-b23d-bb09016ffaf3&expirationTimestamp=1729296000000&signature=SJBSgKqg3gHOiuAVwDcX-IxZCdG4m_CfQcyVGGbtg7c&downloadName=image.png" alt="img" style="width:50%; height:50%">

2. 해당 page의 코드로는 아래와 같이 작성한다
    
    ```jsx
    (/dashboard/invoices/create/page.tsx)
    import Form from '@/app/ui/invoices/create-form';
    import Breadcrumbs from '@/app/ui/invoices/breadcrumbs';
    import { fetchCustomers } from '@/app/lib/data';
     
    export default async function Page() {
      const customers = await fetchCustomers();
     
      return (
        <main>
          <Breadcrumbs
            breadcrumbs={[
              { label: 'Invoices', href: '/dashboard/invoices' },
              {
                label: 'Create Invoice',
                href: '/dashboard/invoices/create',
                active: true,
              },
            ]}
          />
          <Form customers={customers} />
        </main>
      );
    }
    ```
    <img src="https://file.notion.so/f/f/649a15f1-a9e3-45d3-b23d-bb09016ffaf3/a4988e68-9a1d-451e-9d49-83d662d8c62f/image.png?table=block&id=11e85d67-a342-807e-bbf4-d38e0d2f57ac&spaceId=649a15f1-a9e3-45d3-b23d-bb09016ffaf3&expirationTimestamp=1729224000000&signature=wvFBkzJKCp0OWNuEbkppZ_QteGRUqEK0kRhtzMyOqeA&downloadName=image.png" alt="img" style="width:50%; height:50%">
    
    
3. 양식이 제출될 때 호출되는 서버를 작성한다
    1.  /app/lib에 action.ts파일을 생성하고,
    2.  ‘use server’를 사용하여 
    해당 코드가 서버에서 작동하는 코드임을 명시한다
    3. createInvoice 과 Buttons를 가져와서 꾸민다
        
        ```jsx
        (/app/ui/invoices/create-form.tsx)
        import { customerField } from '@/app/lib/definitions';
        import Link from 'next/link';
        import {
        CheckIcon,
        ClockIcon,
        CurrencyDollarIcon,
        UserCircleIcon,
        } from '@heroicons/react/24/outline';
        import { Button } from '@/app/ui/button';
        import { createInvoice } from '@/app/lib/actions';
        export default function Form({
        customers,
        }: {
        customers: customerField[];
        }) {
        return (
        <form action={createInvoice}>
        // ...
        )
        }
        ```
        
    
    4 . forData에서 get방식으로 데이터를 추출한다⭐⭐⭐
    
    1. formData.get으로 form에 입력된 값을 가져온뒤, 사용시에는 
        
        **import { Invoice } from '@/app/lib/definitions';로 사용한다**
        
    
    ```jsx
    (/app/lib/actions.ts)
    'use server';
     
    export async function createInvoice(formData: FormData) {
      const rawFormData = {
        customerId: formData.get('customerId'),
        amount: formData.get('amount'),
        status: formData.get('status'),
      };
      // Test it out:
      console.log(rawFormData);
    }
    ```
    
    1. 단위,날짜 등등의 양식을 변경한다(필수X) 그 후 sql에 입력하는 구문을 작성한다 
    2. revalidatePath를 사용하여 insert된 데이터 캐쉬를 update한다
    3. redirect를 통해 해당 페이지를 reload한다
    
    ```jsx
    (/app/lib/actions.ts)
    'use server';
    
    import { z } from 'zod';
    import { sql } from '@vercel/postgres';
     import { revalidatePath } from 'next/cache';
    import { redirect } from 'next/navigation';
    // ...
     
    export async function createInvoice(formData: FormData) {
      const { customerId, amount, status } = CreateInvoice.parse({
        customerId: formData.get('customerId'),
        amount: formData.get('amount'),
        status: formData.get('status'),
      });
      const amountInCents = amount * 100;
      const date = new Date().toISOString().split('T')[0];
     
      await sql`
        INSERT INTO invoices (customer_id, amount, status, date)
        VALUES (${customerId}, ${amountInCents}, ${status}, ${date})
      `;
    }
    ```
    

### 사용예시2 (invocie 업데이트)

1. Create a new dynamic route segment with the invoice `id`.
2. Read the invoice `id` from the page params. (해당 id의 정보를 읽음)
3. Fetch the specific invoice from your database. (DB에서 해당 id의 데이터를 가져옴)
4. Pre-populate the form with the invoice data. (데이터를 채움)
5. Update the invoice data in your database. (DB를 업데이트(변경된 값으로 덮어쓰기))

1. table과 button의 경로를 설정한다 
    
    ```jsx
    (/app/ui/invoices/table.tsx)
     <UpdateInvoice id={[invoice.id](http://invoice.id/)} />
    
    (/app/ui/invoices/buttons.tsx)
    <Link
    href={/dashboard/invoices/${id}/edit}
    className="rounded-md border p-2 hover:bg-gray-100"
    >
    ```
    
2. edit을 가져오는 page를 만든다
이때 id값을 가져와야 하므로
    1. export default async function Page({ params }: { params: {id: String } }) { 와 const id = [params.id](http://params.id) 를 사용하여 id값을 받는다
    2.  fetchInvoiceById 와 fetchCustomers 로 /app/lib/data에 있는 고객 id와 이름을 가져온다
    3. Promis.all을 사용하여 해당 Id에 해당하는 invoice와  고객의 데이터를 모두 가져온다
    
    ```jsx
    import Form from '@/app/ui/invoices/edit-form';
    import Breadcrumbs from '@/app/ui/invoices/breadcrumbs';
    import { fetchCustomers } from '@/app/lib/data';
    import { fetchInvoiceById, fetchCustomers } from '@/app/lib/data';
     
    export default async function Page({ params }: { params: {id: String } }) {
    const id = params.id;
      const [invoice, customers] = await Promise.all([
        fetchInvoiceById(id),
        fetchCustomers(),
      ]);
      return (
        <main>
          <Breadcrumbs
            breadcrumbs={[
              { label: 'Invoices', href: '/dashboard/invoices' },
              {
                label: 'Edit Invoice',
                href: `/dashboard/invoices/${id}/edit`,
                active: true,
              },
            ]}
          />
          <Form invoice={invoice} customers={customers} />
        </main>
      );
    }
    
    ```
   <img src="https://file.notion.so/f/f/649a15f1-a9e3-45d3-b23d-bb09016ffaf3/ccbc18ce-240e-4ac0-90cf-ff268db517bb/image.png?table=block&id=11e85d67-a342-80ed-bcc1-e06d64336c7f&spaceId=649a15f1-a9e3-45d3-b23d-bb09016ffaf3&expirationTimestamp=1729224000000&signature=KsFTE7KvmYDQYU3ybdvzsj8ZNtKTqurJ4OMm2mUkLBw&downloadName=image.png" alt="img" style="width:50%; height:50%">
    
3. eidt-form에서 해당 form의 value로 가져온 데이터를 채운다
    
    ```jsx
    // ...
    import { updateInvoice } from '@/app/lib/actions';
     
    export default function EditInvoiceForm({
      invoice,
      customers,
    }: {
      invoice: InvoiceForm;
      customers: CustomerField[];
    }) {
      const updateInvoiceWithId = updateInvoice.bind(null, invoice.id);
     
      return (
        <form action={updateInvoiceWithId}>
          <input type="hidden" name="id" value={invoice.id} />
        </form>
      );
    }
    ```
    
    이후 lib/action.ts에 UpdateInvoice라는 작업을 만든다 (update쿼리문 사용)
    
    ```jsx
    // Use Zod to update the expected types
    const UpdateInvoice = FormSchema.omit({ id: true, date: true });
     
    // ...
     
    export async function updateInvoice(id: string, formData: FormData) {
      const { customerId, amount, status } = UpdateInvoice.parse({
        customerId: formData.get('customerId'),
        amount: formData.get('amount'),
        status: formData.get('status'),
      });
     
      const amountInCents = amount * 100;
     
      await sql`
        UPDATE invoices
        SET customer_id = ${customerId}, amount = ${amountInCents}, status = ${status}
        WHERE id = ${id}
      `;
     
      revalidatePath('/dashboard/invoices');
      redirect('/dashboard/invoices');
    }
    ```
    

### 사용예시3 (invocie 삭제)

invoice삭제는 간단하다 Button.tsx→action.ts로 가서 delete구문만 실행되면 삭제가 된다

1. button
    
    ```jsx
    import { deleteInvoice } from '@/app/lib/actions';
     
    // ...
     
    export function DeleteInvoice({ id }: { id: string }) {
      const deleteInvoiceWithId = deleteInvoice.bind(null, id);
     
      return (
        <form action={deleteInvoiceWithId}>
          <button type="submit" className="rounded-md border p-2 hover:bg-gray-100">
            <span className="sr-only">Delete</span>
            <TrashIcon className="w-4" />
          </button>
        </form>
      );
    }
    ```
    
2. action
    
    ```jsx
    export async function deleteInvoice(id: string) {
      await sql`DELETE FROM invoices WHERE id = ${id}`;
      revalidatePath('/dashboard/invoices');
    }
    ```



    # Course 14 (Handling Data)

Spring에서 try-catch,throw를 사용하여 개발단계에서 에러가 발생하는 부분을 확인하거나,

 에러 페이지를 핸들링 하는것처럼 next에서도 핸들링이 가능하다 이떄 에러페이지는 error.tsx파일을 사용한다

### try-catch

```jsx
(기존코드)
export async function deleteInvoice(id: string) {
  await sql`DELETE FROM invoices WHERE id = ${id}`;
  revalidatePath('/dashboard/invoices');
}
(try-catch 사용코드)
try{
export async function deleteInvoice(id: string) {
  await sql`DELETE FROM invoices WHERE id = ${id}`;
 } catch (error) {
		 return{
			 message: "error! error!"
		 }
 }
  revalidatePath('/dashboard/invoices');
}
```

try-catch를 사용할 구문에 

```jsx
catch(error){
		return{
			message: ""
		}
}
```

를 사용하여 error발생시 출력한 구문을 입력한다

### throw

아래와 같이 해당 메서드가 실행중 오류가 났을경우 Error구문이 출력되어 어느 메서드에서 문제가 발생중인지 개발단계에서 확인이 가능하다

```jsx
export async function deleteInvoice(id: string) {
  throw new Error('Failed to Delete Invoice');
 
  // Unreachable code block
  try {
    await sql`DELETE FROM invoices WHERE id = ${id}`;
    revalidatePath('/dashboard/invoices');
    return { message: 'Deleted Invoice' };
  } catch (error) {
    return { message: 'Database Error: Failed to Delete Invoice' };
  }
}
```

### Handling

1. ‘use client’를 사용하여 해당 처리가 웹페이지에서만 이루어지도록 적용시키고,
2. error와 reset2가지를 만들어 error가 발생하면 아래 error문구가 출력되도록 하고, reset버튼(Try again)을 만들어 사용자가 다시 실행할 수 있도록 유도한다

```jsx
'use client';
 
import { useEffect } from 'react';
 
export default function Error({
  error,
  reset,
}: {
  error: Error & { digest?: string };
  reset: () => void;
}) {
  useEffect(() => {
    // Optionally log the error to an error reporting service
    console.error(error);
  }, [error]);
 
  return (
    <main className="flex h-full flex-col items-center justify-center">
      <h2 className="text-center">Something went wrong!</h2>
      <button
        className="mt-4 rounded-md bg-blue-500 px-4 py-2 text-sm text-white transition-colors hover:bg-blue-400"
        onClick={
          // Attempt to recover by trying to re-render the invoices route
          () => reset()
        }
      >
        Try again
      </button>
    </main>
  );
}
```
<img src="https://file.notion.so/f/f/649a15f1-a9e3-45d3-b23d-bb09016ffaf3/79e456a0-4683-4614-a54c-f0962fa062c7/image.png?table=block&id=11e85d67-a342-80d8-bf97-c24272322ad1&spaceId=649a15f1-a9e3-45d3-b23d-bb09016ffaf3&expirationTimestamp=1729224000000&signature=1zzk9DHAun9qXBwz5pcdbqj91pFAKs6kyxUBPBppOvc&downloadName=image.png" alt="img" style="width:50%; height:50%">
### 404

존재하지않는 UUID, 페이지 등을 사용자가 접근하려고 하면 해당 페이지(404)로 보낼 수 있다

page.tsx에서 !invoice인 경우, 즉 invocie혹은 customer의 데이터가 없는 경우 import { notFound } from 'next/navigation'를 실행시켜 404페이지를 호출한다(next에서 기본적으로 제공됨)

이때 not-found.tsx의 이름으로 페이지를 만들경우 404페이지를 커스텀할 수 있다
( 404페이지 호출 따로, 404페이지 커스텀 따로)

```jsx
import { fetchInvoiceById, fetchCustomers } from '@/app/lib/data';
import { updateInvoice } from '@/app/lib/actions';
import { notFound } from 'next/navigation';
 
export default async function Page({ params }: { params: { id: string } }) {
  const id = params.id;
  const [invoice, customers] = await Promise.all([
    fetchInvoiceById(id),
    fetchCustomers(),
  ]);
 
  if (!invoice) {
    notFound();
  }
 
  // ...
}
```

```jsx
import Link from 'next/link';
import { FaceFrownIcon } from '@heroicons/react/24/outline';
 
export default function NotFound() {
  return (
    <main className="flex h-full flex-col items-center justify-center gap-2">
      <FaceFrownIcon className="w-10 text-gray-400" />
      <h2 className="text-xl font-semibold">404 Not Found</h2>
      <p>Could not find the requested invoice.</p>
      <Link
        href="/dashboard/invoices"
        className="mt-4 rounded-md bg-blue-500 px-4 py-2 text-sm text-white transition-colors hover:bg-blue-400"
      >
        Go Back
      </Link>
    </main>
  );
}
```
<img src="https://file.notion.so/f/f/649a15f1-a9e3-45d3-b23d-bb09016ffaf3/1aac64b3-2e44-4d0d-a9ee-b12e9e90b2fd/image.png?table=block&id=11e85d67-a342-8036-932e-ec1bbb78bd10&spaceId=649a15f1-a9e3-45d3-b23d-bb09016ffaf3&expirationTimestamp=1729224000000&signature=OKF3RWpm65nejr0hnn1u236bauwO8zGaiFBb9sWDMz4&downloadName=image.png " alt="img" style="width:50%; height:50%">


# Course 15 (Improving Accessibility)

- How to use `eslint-plugin-jsx-a11y` with Next.js to implement accessibility best practices.
- How to implement server-side form validation.
- How to use the React `useActionState` hook to handle form errors, and display them to the user.

### 코드 오류 검사

[`eslint-plugin-jsx-a11y`](https://www.npmjs.com/package/eslint-plugin-jsx-a11y) 플러그인을 사용하여 

1. package.json에 해당 구문 입력
    
    ```jsx
    (/package.json) 
    "scripts": {
        "build": "next build",
        "dev": "next dev",
        "start": "next start",
        "lint": "next lint"
    },
    ```
    
2. 이미지 태그에서 image를 삭제
    
    ```jsx
    <Image
      src={invoice.image_url}
      className="rounded-full"
      width={28}
      height={28}
      alt={`${invoice.name}'s profile picture`} // Delete this line
    />
    ```
    
3. cmd에 pnpm lint 로 lint를 실행하면 
오류가 없는 경우에는
`✔ No ESLint warnings or errors` 가 출력되며
오류가 있는 경우에는 
    
    ```jsx
    ./app/ui/invoices/table.tsx
    45:25  Warning: Image elements must have an alt prop,
    either with meaningful text, or an empty string for decorative images. jsx-a11y/alt-text
    ```
    
    가 출력되어 수정위치를 확인할 수 있다
    

### 양식 검증

### 클라이언트 측

클라이언트 측 양식 검증은 form에 필수값 등에 사용할 수 있다

```jsx
<input
  id="amount"
  name="amount"
  type="number"
  placeholder="Enter USD amount"
  className="peer block w-full rounded-md border border-gray-200 py-2 pl-10 text-sm outline-2 placeholder:text-gray-500"
  required
/>
```

위와 같이 required를 붙여주면 해당 input은 필수값이 된다

### 서버측

```jsx
(/app/ui/invoices/create-form.tsx)
'use client';
 
// ...
import { useActionState } from 'react';
```

# Course 16 (Adding Authentication)

### login 페이지 생성

### page.tsx코드

```tsx
import AcmeLogo from '@/app/ui/acme-logo';
import LoginForm from '@/app/ui/login-form';
 
export default function LoginPage() {
  return (
    <main className="flex items-center justify-center md:h-screen">
      <div className="relative mx-auto flex w-full max-w-[400px] flex-col space-y-2.5 p-4 md:-mt-32">
        <div className="flex h-20 w-full items-end rounded-lg bg-blue-500 p-3 md:h-36">
          <div className="w-32 text-white md:w-36">
            <AcmeLogo />
          </div>
        </div>
        <LoginForm />
      </div>
    </main>
  );
}
```

nextjs에서 인증을 사용하려면 NextAuth.js를 사용해야한다

1. pnpm i next-auth@beta 설치
2. openssl rand -base64 32 (실행안됨)
3. .env에 AUTH_SECRET=your-secret-key  로 key설정

### 또한 위에서 만든 login페이지의 option또한 설정해야 한다

1. next-auth를 import하고 login 사용시 nextAuthConfig를 충족하는지 확인한다
    
    ```tsx
    (/auth.config.ts)
    import type { NextAuthConfig } from 'next-auth';
     
    export const authConfig = {
      pages: {
        signIn: '/login',
      },
    } satisfies NextAuthConfig;
    ```
    
2. callback함수를 이용해서 권한이 필요한 페이지에 접근했을 경우, 해당 session에 저장된 정보와 request한 정보가 일치하는지 확인한뒤 데이터가 일치하는 경우 해당 데이터를 받아온다
또한 providers 배열을 이용해서 다른 로그인 옵션을 추가할 수 있다
    
    ```tsx
    (/auth.config.ts)
    import type { NextAuthConfig } from 'next-auth';
     
    export const authConfig = {
      pages: {
        signIn: '/login',
      },
      callbacks: {
        authorized({ auth, request: { nextUrl } }) {
          const isLoggedIn = !!auth?.user;
          const isOnDashboard = nextUrl.pathname.startsWith('/dashboard');
          if (isOnDashboard) {
            if (isLoggedIn) return true;
            return false; // Redirect unauthenticated users to login page
          } else if (isLoggedIn) {
            return Response.redirect(new URL('/dashboard', nextUrl));
          }
          return true;
        },
      },
      providers: [], // Add providers with an empty array for now
    } satisfies NextAuthConfig;
    ```
    
3. root폴더에 middleware.ts파일을 만들고 object타입으로 데이터를 전송한다 
auth또한 matcher-middleware의 속성을 사용하여 데이터를 전송한다
    
    ```tsx
    (/middleware.ts)
    import NextAuth from 'next-auth';
    import { authConfig } from './auth.config';
     
    export default NextAuth(authConfig).auth;
     
    export const config = {
      // https://nextjs.org/docs/app/building-your-application/routing/middleware#matcher
      matcher: ['/((?!api|_next/static|_next/image|.*\\.png$).*)'],
    };
    ```
    
4. password hashing
    
    사용자의 암호를 저장할 때는 암호를 bcrypt등을 사용하여 hasing(무작위로 변환)하여 저장하는 것이 좋다
    또한 providers에 로그인 방식 추가 할 수 있다(google , github등)
    
    ```tsx
    (/auth.ts)
    import NextAuth from 'next-auth';
    import { authConfig } from './auth.config';
    import Credentials from 'next-auth/providers/credentials';
     
    export const { auth, signIn, signOut } = NextAuth({
      ...authConfig,
      providers: [Credentials({})],
    });
    ```
    
5. 로그인 추가
zod를 사용하여 email: z.String().email() 와 password: z.String().min(6) 를 사용하여 email(id)와 password의 입력된 값이 있는지 유효성 검사를 한번 거친다.
이후 sql문으로 해당 users의 email(id)이 있는지 확인 후
`await bcrypt.compare(password, user.password);` 로 입력된 password값이 해당 email이 가지고 있는 password값과 동일한지 비동기 방식으로 확인한다
    
    ```jsx
    (/auth.ts)
    import NextAuth from 'next-auth';
    import Credentials from 'next-auth/providers/credentials';
    import { authConfig } from './auth.config';
    import { z } from 'zod';
    import { sql } from '@vercel/postgres';
    import type { User } from '@/app/lib/definitions';
    import bcrypt from 'bcrypt';
     
    async function getUser(email: string): Promise<User | undefined> {
      try {
        const user = await sql<User>`SELECT * FROM users WHERE email=${email}`;
        return user.rows[0];
      } catch (error) {
        console.error('Failed to fetch user:', error);
        throw new Error('Failed to fetch user.');
      }
    }
     
    export const { auth, signIn, signOut } = NextAuth({
      ...authConfig,
      providers: [
        Credentials({
          async authorize(credentials) {
            const parsedCredentials = z
              .object({ email: z.string().email(), password: z.string().min(6) })
              .safeParse(credentials);
     
            if (parsedCredentials.success) {
              const { email, password } = parsedCredentials.data;
              const user = await getUser(email);
              if (!user) return null;
               const passwordsMatch = await bcrypt.compare(password, user.password);
     
              if (passwordsMatch) return user;
            }
     
            return null;
          },
        }),
      ],
    });
    ```
    
    1. 로그인 페이지와 로직 연결
    action.ts 파일을 만들고
    `signIn` `auth` 두가지 인증 함수를 가져와 오류가 있는경우 CredentialsSignin의 메시지를 출력하고 login-form에서 호출한다
    
    ```jsx
    (/app/lib/action.ts)
    'use server';
     
    import { signIn } from '@/auth';
    import { AuthError } from 'next-auth';
     
    // ...
     
    export async function authenticate(
      prevState: string | undefined,
      formData: FormData,
    ) {
      try {
        await signIn('credentials', formData);
      } catch (error) {
        if (error instanceof AuthError) {
          switch (error.type) {
            case 'CredentialsSignin':
              return 'Invalid credentials.';
            default:
              return 'Something went wrong.';
          }
        }
        throw error;
      }
    }
    ```
    
    ```jsx
    (/app/ui/login-form.tsx)
    'use client';
     
    import { lusitana } from '@/app/ui/fonts';
    import {
      AtSymbolIcon,
      KeyIcon,
      ExclamationCircleIcon,
    } from '@heroicons/react/24/outline';
    import { ArrowRightIcon } from '@heroicons/react/20/solid';
    import { Button } from '@/app/ui/button';
    import { useActionState } from 'react';
    import { authenticate } from '@/app/lib/actions';
     
    export default function LoginForm() {
      const [errorMessage, formAction, isPending] = useActionState(
        authenticate,
        undefined,
      );
     
      return (
        <form action={formAction} className="space-y-3">
          <div className="flex-1 rounded-lg bg-gray-50 px-6 pb-4 pt-8">
            <h1 className={`${lusitana.className} mb-3 text-2xl`}>
              Please log in to continue.
            </h1>
            <div className="w-full">
              <div>
                <label
                  className="mb-3 mt-5 block text-xs font-medium text-gray-900"
                  htmlFor="email"
                >
                  Email
                </label>
                <div className="relative">
                  <input
                    className="peer block w-full rounded-md border border-gray-200 py-[9px] pl-10 text-sm outline-2 placeholder:text-gray-500"
                    id="email"
                    type="email"
                    name="email"
                    placeholder="Enter your email address"
                    required
                  />
                  <AtSymbolIcon className="pointer-events-none absolute left-3 top-1/2 h-[18px] w-[18px] -translate-y-1/2 text-gray-500 peer-focus:text-gray-900" />
                </div>
              </div>
              <div className="mt-4">
                <label
                  className="mb-3 mt-5 block text-xs font-medium text-gray-900"
                  htmlFor="password"
                >
                  Password
                </label>
                <div className="relative">
                  <input
                    className="peer block w-full rounded-md border border-gray-200 py-[9px] pl-10 text-sm outline-2 placeholder:text-gray-500"
                    id="password"
                    type="password"
                    name="password"
                    placeholder="Enter password"
                    required
                    minLength={6}
                  />
                  <KeyIcon className="pointer-events-none absolute left-3 top-1/2 h-[18px] w-[18px] -translate-y-1/2 text-gray-500 peer-focus:text-gray-900" />
                </div>
              </div>
            </div>
            <Button className="mt-4 w-full" aria-disabled={isPending}>
              Log in <ArrowRightIcon className="ml-auto h-5 w-5 text-gray-50" />
            </Button>
            <div
              className="flex h-8 items-end space-x-1"
              aria-live="polite"
              aria-atomic="true"
            >
              {errorMessage && (
                <>
                  <ExclamationCircleIcon className="h-5 w-5 text-red-500" />
                  <p className="text-sm text-red-500">{errorMessage}</p>
                </>
              )}
            </div>
          </div>
        </form>
      );
    }
    ```
    
    ### 로그아웃 기능
    
    로그아웃 기능은 간단하게 signOut메서드를 사용하면 된다
    아래코드와 같이 @/auth에서 signOut메서드를 호출하고 해당 form / button등에 await방식으로 연결하면 된다
    
    ```jsx
    import Link from 'next/link';
    import NavLinks from '@/app/ui/dashboard/nav-links';
    import AcmeLogo from '@/app/ui/acme-logo';
    import { PowerIcon } from '@heroicons/react/24/outline';
    import { signOut } from '@/auth';
     
    export default function SideNav() {
      return (
        <div className="flex h-full flex-col px-3 py-4 md:px-2">
          // ...
          <div className="flex grow flex-row justify-between space-x-2 md:flex-col md:space-x-0 md:space-y-2">
            <NavLinks />
            <div className="hidden h-auto w-full grow rounded-md bg-gray-50 md:block"></div>
            <form
              action={async () => {
                'use server';
                await signOut();
              }}
            >
              <button className="flex h-[48px] grow items-center justify-center gap-2 rounded-md bg-gray-50 p-3 text-sm font-medium hover:bg-sky-100 hover:text-blue-600 md:flex-none md:justify-start md:p-2 md:px-3">
                <PowerIcon className="w-6" />
                <div className="hidden md:block">Sign Out</div>
              </button>
            </form>
          </div>
        </div>
      );
    }
    ```
    

# Course 17 (Adding MetaData)

MeataData는 해당 페이지를 설명하는 부분으로

아래와 같이 해당 문서가 어떤 내용인지 와 어떻게 작성되었는지 설명하는 코드이다
