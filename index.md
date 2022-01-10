## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/JJKEB/page_test/edit/gh-pages/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [Basic writing and formatting syntax](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/JJKEB/page_test/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.






깃헙 아이디 ( [https://github.com](https://github.com/) 회원가입 후 생성한다. )

새로운 저장소를 만들되 계정 생성시 작성한 **사용자이름** 을 붙여서
**사용자이름.github.io** 으로 적고
당연히 공개사이트 이기때문에 **Public** 로 설정되있는지 확인후
**Add a README fie** 정도 체크 하고
**Create repository** 버튼을 눌러 저장소를 생성한다.
※ **저장소의 첫 번째 부분이 사용자 이름과 일치하지 않으면 작동하지 않으니 주의 !**

![003.jpg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f818c82d-9418-4b50-91f3-7decf25dbd1e/003.jpg)

다음으로 상단 메뉴중 Settings → Pages 로 이동한다.

![002.jpg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3ce45b4e-ef00-4814-9e61-6a247cdcc706/002.jpg)

![004.jpg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e516127d-ac44-4cb5-bbbe-d6ba4df0e9ca/004.jpg)

보여지는 페이지에서 위의 사이트 주소를 클릭하면 해당 사이트로 접속할수 있고
Change theme 버튼을 클릭하면 테마를 선택하여 설치할수 있는 페이지로 갈수 있다.

![006.jpg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c2f19d0c-b66a-4a97-b683-fb2b8870bec9/006.jpg)

상단에서 디자인을 하나씩 클릭해보고
맘에드는 디자인이 있으면 **Select theme** 버튼을 클릭하면
해당 테마가 자동으로 본인의 깃헙 저장소에 적용된다.

설치된 테마는 [Jekyll](https://jekyllrb.com/) 이라는 정적 웹사이트 빌더의 테마이다.
운영은 Mark down 문법으로 페이지를 수정하거나 만들어서 올리면 되는데

다른 정적웹사이트와 달리 [Jekyll](https://jekyllrb.com/) 의 경우 GitHub Pages 에서 공식 지원중이기 때문에

저장소에 push 하면 Html 등의 파일로 자동 빌드되어 화면에 보여지게 된다.


2. 상품 리스트에서 상품 선택 order 상품 삭제 로직 만들기
    1. order 상태를 가지고 있어야 하기 때문에 전역상태를 설정해주기 위해서
    context 를 만들고 context 에 데이터를 주입하기 위해서 프로바이더 만들기
    2. src/contexts 폴더 생성
        1. AppStateContext.jsx 파일 생성후 React.createContext() 인스턴스 생성 하고
        export defalt 로 createContext 인스턴스인 **AppStateContext** 을 내보내 줍니다.
            
            ```jsx
            import React from 'react';
            
            const AppStateContext = React.createContext();
            export default AppStateContext;
            ```
            
    3. src/providers 폴더 생성
        1. AppStateProvider.jsx 파일 생성후 AppStateProvider 함수 생성하고
        contexts/AppStateContext.jsx 의 **AppStateContext** 을 받아 key 로 Provider 를 부여하고 리턴 합니다.
            
            ```jsx
            import { useState, useCallback } from 'react';
            import AppStateContext from '../contexts/AppStateContext';
            
            const AppStateProvider = ({ children }) => {
              const [prototypes] = useState([
                {
                  id: 'pp-01',
                  title: 'Kids-story',
                  artist: 'Thomas Buisson',
                  desc: 'This prototype was made with ProtoPie, the interactive prototyping tool for all digital products.',
                  thumbnail: 'https://prototype-shop.s3.ap-northeast-2.amazonaws.com/thumbnails/Kids-story_1.mp4',
                  price: 10,
                  pieUrl: 'https://cloud.protopie.io/p/8a6461ad85',
                },
            // ------------------------- 데이터 중간 생략 ------------------------------ //
                {
                  id: 'pp-12',
                  title: 'Voice Note',
                  artist: 'Haerin Song',
                  desc: `Made by Haerin Song
                          (Soda Design)`,
                  thumbnail: 'https://prototype-shop.s3.ap-northeast-2.amazonaws.com/thumbnails/Voice_note_with_sound_wave.mp4',
                  price: 90,
                  pieUrl: 'https://cloud.protopie.io/p/7a0d6567d2',
                },
              ]);
              const [orders, setOrders] = useState([]);
              const addToOrder = useCallback((id) => {}, []);
              const remove = useCallback((id) => {}, []);
              const removeAll = useCallback(() => {}, []);
            
              return (
                <AppStateContext.Provider     // <= **AppStateContext** 을 받아 key 로 Provider 를 부여
                  value={{                    // <= 데이터 값과, 필요 함수들을 value 로 넣어줍니다.
                    prototypes,
                    setOrders,
                    orders,
                    addToOrder,
                    remove,
                    removeAll,
                  }}
                >
                  {children}            // children 이건 뭘까...?
                </AppStateContext.Provider>
              );
            };
            
            export default AppStateProvider;
            ```
            
    4.
