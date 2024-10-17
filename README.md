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
