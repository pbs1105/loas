# 법무사 홈페이지 기능 및 플랜 논의
_Exported on 11/17/2025 at 21:28:33 GMT+9 from Cursor (2.0.77)_

---

**User**

법무사 홈페이지에 들어가는 기능들

메인페이지(홈화면)
홍보 
1)서비스 : 좌측 목차, 중앙 컨텐츠 우측 법령, 비용 등
               중앙 컨텐츠를 강조조
2)블로그 : 카드 형식, FAQ, 주제별 사안정리, 중요판례
             클릭하면 상세 페이지로 이동
컨택트(상담/위임)
1)상담/위임 버턴
2) 클릭시 상담폼이 고객에게 전달_>고객이 상담폼 제출하면 N8N의 트리거작용하여 NOTION 저장
3) 위임버턴에서 업무위임 클릭하면 위임폼 양식 : 이후 N8N과 동일한 시스템

관리자 
법무사가 관리자가 되어
서비스/블로그 글 추가/수정/삭제
삭제시 일정기간 경과 후 완전 삭제
5. JSON 형식 사용 : 데이터를 별도의 서버에 저장하지 않고, 로컬스토리지에 저장

5. 네비게이션바 : 법무사/부동산등기/법인등기/민사소송/민사집행/상속/신탁  블로그/상담/업무위임
개별 00클릭하면 각 페이지로 이동
상담과 엄무위임은 네비바와 푸터의 우측에 고정하여 쉽게 찾을 수 있도록
푸터는 스크롤을 해도 고정되도록 함
6. 디자인
홈페이지의 가독성을 가장 중시
파란색 많이 사용
기타 법무사 홈페이지의 가동성 등을 고려한 글꼴, 색상, 여백 등을 중시 배치
7. 확장성 : 본 홈페이지와 N8N 업무자동화, NOTION를 연동하여 구축할 계획임을 전제로 해줘


나는 이러한 기능들이 포함된 법무사 홈페이지르 만들고 싶어. 이를 위한 플랜을 짜줘.

---

**Cursor**

요구사항 확인을 위해 몇 가지 질문이 있습니다:


프로젝트가 비어 있어 초기 설정이 필요합니다. 계획 수립 전에 다음을 확인해 주세요:

1. **프론트엔드 프레임워크 선택**
   - a) React (권장 - 확장성 좋음)
   - b) Vanilla JavaScript (HTML/CSS/JS)
   - c) Vue.js

2. **데이터 저장 방식**
   - a) 로컬스토리지만 사용 (N8N 연동은 폼 제출 시 웹훅으로만)
   - b) 로컬스토리지 + 간단한 백엔드 API (관리자 기능용)

3. **관리자 인증 방식**
   - a) 간단한 비밀번호 입력 (프론트엔드만)
   - b) 별도 로그인 페이지

답변 주시면 구체적인 플랜을 제시하겠습니다.

---

**User**

1. a, 2. a 3. a로 해줘

---

**Cursor**

선택하신 옵션을 반영해 플랜을 작성 중입니다.


---

**User**

Implement the plan as specified, it is attached for your reference. Do NOT edit the plan file itself.

To-do's from the plan have already been created. Do not create them again. Mark them as in_progress as you work, starting with the first one. Don't stop until you have completed all the to-dos.

---

**Cursor**

프로젝트 구조 확인 후 플랜에 따라 구현을 시작합니다.


Vite + React 프로젝트 초기 설정부터 진행합니다.


npm이 없어 보입니다. 프로젝트 구조를 직접 생성합니다.


```json
{
  "name": "lawyer-website",
  "private": true,
  "version": "0.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  },
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-router-dom": "^6.20.0"
  },
  "devDependencies": {
    "@types/react": "^18.2.43",
    "@types/react-dom": "^18.2.17",
    "@vitejs/plugin-react": "^4.2.1",
    "vite": "^5.0.8"
  }
}

```

```javascript
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
})

```

```html
<!doctype html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/vite.svg" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>법무사 홈페이지</title>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.jsx"></script>
  </body>
</html>

```

```ignore
# Logs
logs
*.log
npm-debug.log*
yarn-debug.log*
yarn-error.log*
pnpm-debug.log*
lerna-debug.log*

node_modules
dist
dist-ssr
*.local

# Editor directories and files
.vscode/*
!.vscode/extensions.json
.idea
.DS_Store
*.suo
*.ntvs*
*.njsproj
*.sln
*.sw?

```

```javascriptreact
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.jsx'
import './styles/global.css'

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
)

```

```css
:root {
  --color-primary: #007bff;
  --color-text-dark: #333;
  --color-text-darker: #444;
  --color-text-black: #000;
  --color-bg-light: #f5f5f5;
  --color-bg-white: #ffffff;
  --font-main: '맑은고딕', 'Malgun Gothic', sans-serif;
  --font-size-body: 18px;
  --line-height-body: 1.6;
  --spacing-small: 10px;
  --spacing-medium: 20px;
  --spacing-large: 30px;
  --spacing-xlarge: 40px;
}

```

```css
@import './variables.css';

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: var(--font-main);
  font-size: var(--font-size-body);
  line-height: var(--line-height-body);
  color: var(--color-text-black);
  background-color: var(--color-bg-light);
  text-shadow: 0.5px 0.5px 1px rgba(0, 0, 0, 0.1);
}

h1, h2, h3 {
  color: var(--color-text-dark);
  margin-bottom: var(--spacing-medium);
  font-weight: bold;
}

h1 {
  font-size: 32px;
  color: var(--color-text-darker);
}

h2 {
  font-size: 28px;
  color: var(--color-text-dark);
}

h3 {
  font-size: 24px;
  color: var(--color-text-dark);
}

h4 {
  font-size: var(--font-size-body);
  color: var(--color-text-black);
}

p {
  font-size: var(--font-size-body);
  margin-bottom: var(--spacing-medium);
  color: var(--color-text-black);
}

a {
  color: var(--color-primary);
  text-decoration: none;
}

a:hover {
  text-decoration: underline;
}

ul {
  list-style: none;
  padding-left: 0;
}

ul li {
  position: relative;
  padding-left: var(--spacing-medium);
  margin-bottom: var(--spacing-small);
  font-size: var(--font-size-body);
}

ul li::before {
  content: '•';
  position: absolute;
  left: 0;
  color: var(--color-text-black);
}

ol {
  padding-left: var(--spacing-medium);
  margin-bottom: var(--spacing-medium);
}

ol li {
  font-size: var(--font-size-body);
  margin-bottom: var(--spacing-small);
}

strong {
  font-weight: bold;
  color: var(--color-text-dark);
}

button {
  font-family: var(--font-main);
  font-size: var(--font-size-body);
  cursor: pointer;
  border: none;
  padding: var(--spacing-small) var(--spacing-medium);
  border-radius: 4px;
  transition: all 0.3s ease;
}

input, textarea, select {
  font-family: var(--font-main);
  font-size: var(--font-size-body);
  padding: var(--spacing-small);
  border: 1px solid #ddd;
  border-radius: 4px;
  width: 100%;
}

input:focus, textarea:focus, select:focus {
  outline: none;
  border-color: var(--color-primary);
}

```

```javascript
// localStorage 관리 유틸리티

const STORAGE_KEY = 'lawyer_website_data';

// 초기 데이터 구조
const getInitialData = () => ({
  services: [],
  blogPosts: [],
  adminPassword: null, // 나중에 해시된 비밀번호 저장
});

// 데이터 로드
export const loadData = () => {
  try {
    const stored = localStorage.getItem(STORAGE_KEY);
    if (stored) {
      return JSON.parse(stored);
    }
    return getInitialData();
  } catch (error) {
    console.error('데이터 로드 실패:', error);
    return getInitialData();
  }
};

// 데이터 저장
export const saveData = (data) => {
  try {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(data));
    return true;
  } catch (error) {
    console.error('데이터 저장 실패:', error);
    return false;
  }
};

// 서비스 관련 함수
export const getServices = () => {
  const data = loadData();
  return data.services || [];
};

export const getServiceById = (id) => {
  const services = getServices();
  return services.find(service => service.id === id);
};

export const saveService = (service) => {
  const data = loadData();
  const existingIndex = data.services.findIndex(s => s.id === service.id);
  
  if (existingIndex >= 0) {
    data.services[existingIndex] = { ...service, updatedAt: new Date().toISOString() };
  } else {
    data.services.push({ ...service, createdAt: new Date().toISOString() });
  }
  
  return saveData(data);
};

export const deleteService = (id) => {
  const data = loadData();
  data.services = data.services.filter(s => s.id !== id);
  return saveData(data);
};

// 블로그 관련 함수
export const getBlogPosts = (includeDeleted = false) => {
  const data = loadData();
  let posts = data.blogPosts || [];
  
  if (!includeDeleted) {
    posts = posts.filter(post => !post.deletedAt);
  }
  
  return posts.sort((a, b) => {
    const dateA = new Date(a.createdAt || 0);
    const dateB = new Date(b.createdAt || 0);
    return dateB - dateA;
  });
};

export const getBlogPostById = (id) => {
  const data = loadData();
  return data.blogPosts.find(post => post.id === id);
};

export const getBlogPostsByCategory = (category) => {
  const posts = getBlogPosts();
  return posts.filter(post => post.category === category);
};

export const saveBlogPost = (post) => {
  const data = loadData();
  const existingIndex = data.blogPosts.findIndex(p => p.id === post.id);
  
  if (existingIndex >= 0) {
    data.blogPosts[existingIndex] = { ...post, updatedAt: new Date().toISOString() };
  } else {
    data.blogPosts.push({ ...post, createdAt: new Date().toISOString() });
  }
  
  return saveData(data);
};

export const deleteBlogPost = (id) => {
  const data = loadData();
  const postIndex = data.blogPosts.findIndex(p => p.id === id);
  
  if (postIndex >= 0) {
    // 삭제 시 deletedAt 타임스탬프 기록
    data.blogPosts[postIndex].deletedAt = new Date().toISOString();
    return saveData(data);
  }
  
  return false;
};

export const permanentlyDeleteBlogPost = (id) => {
  const data = loadData();
  data.blogPosts = data.blogPosts.filter(p => p.id !== id);
  return saveData(data);
};

// 삭제된 항목 정리 (30일 경과 후 완전 삭제)
export const cleanupDeletedItems = () => {
  const data = loadData();
  const thirtyDaysAgo = new Date();
  thirtyDaysAgo.setDate(thirtyDaysAgo.getDate() - 30);
  
  const initialCount = data.blogPosts.length;
  data.blogPosts = data.blogPosts.filter(post => {
    if (post.deletedAt) {
      const deletedDate = new Date(post.deletedAt);
      return deletedDate > thirtyDaysAgo;
    }
    return true;
  });
  
  const deletedCount = initialCount - data.blogPosts.length;
  saveData(data);
  
  return deletedCount;
};

// 관리자 비밀번호 관련
export const setAdminPassword = (password) => {
  const data = loadData();
  // 간단한 해시 (실제로는 더 안전한 방법 사용 권장)
  data.adminPassword = btoa(password);
  return saveData(data);
};

export const verifyAdminPassword = (password) => {
  const data = loadData();
  if (!data.adminPassword) {
    return false;
  }
  return btoa(password) === data.adminPassword;
};

```

```javascript
// N8N 웹훅 호출 함수

// N8N 웹훅 URL (환경 변수나 설정 파일에서 가져올 수 있음)
const N8N_CONSULTATION_WEBHOOK_URL = process.env.VITE_N8N_CONSULTATION_WEBHOOK_URL || '';
const N8N_COMMISSION_WEBHOOK_URL = process.env.VITE_N8N_COMMISSION_WEBHOOK_URL || '';

// 상담 폼 제출
export const submitConsultationForm = async (formData) => {
  if (!N8N_CONSULTATION_WEBHOOK_URL) {
    console.warn('N8N 상담 웹훅 URL이 설정되지 않았습니다.');
    return { success: false, message: '웹훅 URL이 설정되지 않았습니다.' };
  }

  try {
    const response = await fetch(N8N_CONSULTATION_WEBHOOK_URL, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({
        type: 'consultation',
        ...formData,
        submittedAt: new Date().toISOString(),
      }),
    });

    if (response.ok) {
      return { success: true, message: '상담 신청이 완료되었습니다.' };
    } else {
      return { success: false, message: '상담 신청 중 오류가 발생했습니다.' };
    }
  } catch (error) {
    console.error('N8N 웹훅 호출 실패:', error);
    return { success: false, message: '네트워크 오류가 발생했습니다.' };
  }
};

// 위임 폼 제출
export const submitCommissionForm = async (formData) => {
  if (!N8N_COMMISSION_WEBHOOK_URL) {
    console.warn('N8N 위임 웹훅 URL이 설정되지 않았습니다.');
    return { success: false, message: '웹훅 URL이 설정되지 않았습니다.' };
  }

  try {
    const response = await fetch(N8N_COMMISSION_WEBHOOK_URL, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({
        type: 'commission',
        ...formData,
        submittedAt: new Date().toISOString(),
      }),
    });

    if (response.ok) {
      return { success: true, message: '위임 신청이 완료되었습니다.' };
    } else {
      return { success: false, message: '위임 신청 중 오류가 발생했습니다.' };
    }
  } catch (error) {
    console.error('N8N 웹훅 호출 실패:', error);
    return { success: false, message: '네트워크 오류가 발생했습니다.' };
  }
};

```

```javascript
// 관리자 인증 유틸리티

const ADMIN_SESSION_KEY = 'lawyer_admin_session';

// 관리자 세션 확인
export const isAdminLoggedIn = () => {
  const session = sessionStorage.getItem(ADMIN_SESSION_KEY);
  if (!session) return false;
  
  try {
    const sessionData = JSON.parse(session);
    const expiresAt = new Date(sessionData.expiresAt);
    return expiresAt > new Date();
  } catch {
    return false;
  }
};

// 관리자 로그인
export const loginAdmin = () => {
  const expiresAt = new Date();
  expiresAt.setHours(expiresAt.getHours() + 2); // 2시간 유효
  
  sessionStorage.setItem(ADMIN_SESSION_KEY, JSON.stringify({
    loggedIn: true,
    expiresAt: expiresAt.toISOString(),
  }));
};

// 관리자 로그아웃
export const logoutAdmin = () => {
  sessionStorage.removeItem(ADMIN_SESSION_KEY);
};

```

```javascript
// 초기 데이터 구조 및 샘플 데이터

export const initialServices = [
  {
    id: 'real-estate',
    title: '부동산등기',
    content: `
      <h2>부동산등기 서비스</h2>
      <p>부동산등기는 부동산의 권리관계를 명확히 하고 거래의 안전을 보장하기 위한 중요한 제도입니다.</p>
      <h3>주요 서비스 내용</h3>
      <ul>
        <li>소유권 이전등기</li>
        <li>저당권 설정등기</li>
        <li>전세권 설정등기</li>
        <li>지상권 설정등기</li>
      </ul>
    `,
    laws: [
      '부동산등기법',
      '민법',
      '부동산 실권리자명의 등기에 관한 법률'
    ],
    costs: '비용은 <a href="/costs">비용 안내 페이지</a>를 참고하시기 바랍니다.'
  },
  {
    id: 'corporate-registration',
    title: '법인등기',
    content: `
      <h2>법인등기 서비스</h2>
      <p>법인등기는 법인의 설립, 변경, 해산 등 법인의 중요한 사항을 공시하는 제도입니다.</p>
      <h3>주요 서비스 내용</h3>
      <ul>
        <li>법인 설립등기</li>
        <li>법인 변경등기</li>
        <li>법인 해산등기</li>
        <li>법인 청산등기</li>
      </ul>
    `,
    laws: [
      '상법',
      '법인세법',
      '부가가치세법'
    ],
    costs: '비용은 <a href="/costs">비용 안내 페이지</a>를 참고하시기 바랍니다.'
  },
  {
    id: 'civil-litigation',
    title: '민사소송',
    content: `
      <h2>민사소송 서비스</h2>
      <p>민사소송은 개인 간의 권리관계에 관한 분쟁을 법원을 통해 해결하는 절차입니다.</p>
      <h3>주요 서비스 내용</h3>
      <ul>
        <li>소장 작성 및 제출</li>
        <li>변론 준비 및 대리</li>
        <li>화해 및 조정</li>
        <li>항소 및 상고</li>
      </ul>
    `,
    laws: [
      '민사소송법',
      '민법',
      '소송촉진 등에 관한 특례법'
    ],
    costs: '비용은 <a href="/costs">비용 안내 페이지</a>를 참고하시기 바랍니다.'
  },
  {
    id: 'civil-execution',
    title: '민사집행',
    content: `
      <h2>민사집행 서비스</h2>
      <p>민사집행은 확정된 채권을 실현하기 위한 강제집행 절차입니다.</p>
      <h3>주요 서비스 내용</h3>
      <ul>
        <li>부동산 강제경매</li>
        <li>동산 압류 및 매각</li>
        <li>채권 압류 및 추심</li>
        <li>가압류 및 가처분</li>
      </ul>
    `,
    laws: [
      '민사집행법',
      '민법',
      '채권자회생 및 파산에 관한 법률'
    ],
    costs: '비용은 <a href="/costs">비용 안내 페이지</a>를 참고하시기 바랍니다.'
  },
  {
    id: 'inheritance',
    title: '상속',
    content: `
      <h2>상속 서비스</h2>
      <p>상속은 피상속인의 재산상 권리와 의무를 상속인이 승계하는 제도입니다.</p>
      <h3>주요 서비스 내용</h3>
      <ul>
        <li>상속등기</li>
        <li>상속재산 분할</li>
        <li>상속포기 및 한정승인</li>
        <li>유언 검인</li>
      </ul>
    `,
    laws: [
      '민법',
      '상속세 및 증여세법',
      '가족관계의 등록 등에 관한 법률'
    ],
    costs: '비용은 <a href="/costs">비용 안내 페이지</a>를 참고하시기 바랍니다.'
  },
  {
    id: 'trust',
    title: '신탁',
    content: `
      <h2>신탁 서비스</h2>
      <p>신탁은 위탁자가 수탁자에게 재산을 이전하여 수탁자가 수익자를 위하여 재산을 관리·처분하는 제도입니다.</p>
      <h3>주요 서비스 내용</h3>
      <ul>
        <li>신탁 계약 작성</li>
        <li>신탁 재산 등기</li>
        <li>신탁 변경 및 해지</li>
        <li>신탁 관련 분쟁 해결</li>
      </ul>
    `,
    laws: [
      '신탁법',
      '민법',
      '부동산등기법'
    ],
    costs: '비용은 <a href="/costs">비용 안내 페이지</a>를 참고하시기 바랍니다.'
  }
];

export const initialBlogPosts = [
  {
    id: 'blog-1',
    title: '부동산 매매 시 주의사항',
    category: 'FAQ',
    content: `
      <h2>부동산 매매 시 주의사항</h2>
      <p>부동산 매매는 큰 금액이 관련된 중요한 거래입니다. 다음과 같은 사항들을 주의하시기 바랍니다.</p>
      <h3>1. 등기부등본 확인</h3>
      <p>매매 전 반드시 등기부등본을 확인하여 소유권, 저당권, 전세권 등의 권리관계를 파악해야 합니다.</p>
      <h3>2. 계약서 작성</h3>
      <p>계약서에는 매매가격, 계약금, 중도금, 잔금 지급일자 등을 명확히 기재해야 합니다.</p>
      <h3>3. 등기 이전</h3>
      <p>잔금 지급 후 즉시 소유권 이전등기를 진행하여 권리를 확정해야 합니다.</p>
    `,
    createdAt: new Date().toISOString(),
    deletedAt: null
  },
  {
    id: 'blog-2',
    title: '법인 설립 절차 안내',
    category: '사안정리',
    content: `
      <h2>법인 설립 절차 안내</h2>
      <p>법인을 설립하기 위해서는 다음과 같은 절차를 거쳐야 합니다.</p>
      <h3>1. 정관 작성</h3>
      <p>법인의 목적, 명칭, 본점 소재지, 자본금 등을 명시한 정관을 작성합니다.</p>
      <h3>2. 발기인 모집</h3>
      <p>주식회사의 경우 발기인을 모집하고 주식을 인수받습니다.</p>
      <h3>3. 설립등기</h3>
      <p>관할 법원에 설립등기를 신청하여 법인격을 취득합니다.</p>
    `,
    createdAt: new Date().toISOString(),
    deletedAt: null
  },
  {
    id: 'blog-3',
    title: '대법원 판례: 부동산 매매계약 해석',
    category: '판례',
    content: `
      <h2>대법원 판례: 부동산 매매계약 해석</h2>
      <p>대법원 2023. 1. 15. 선고 2022다12345 판결</p>
      <h3>사안</h3>
      <p>부동산 매매계약에서 매도인이 계약 해제를 주장한 사안</p>
      <h3>판결 요지</h3>
      <p>매매계약의 해석은 당사자의 의사표시의 진의를 명확히 파악하여야 하며, 계약서의 문언뿐만 아니라 거래의 전후 사정을 종합적으로 고려하여야 한다.</p>
    `,
    createdAt: new Date().toISOString(),
    deletedAt: null
  }
];

```

레이아웃 컴포넌트 생성 중.


```javascriptreact
import { Link, useLocation } from 'react-router-dom';
import './Navbar.css';

const Navbar = () => {
  const location = useLocation();

  const menuItems = [
    { path: '/', label: '법무사' },
    { path: '/service/real-estate', label: '부동산등기' },
    { path: '/service/corporate-registration', label: '법인등기' },
    { path: '/service/civil-litigation', label: '민사소송' },
    { path: '/service/civil-execution', label: '민사집행' },
    { path: '/service/inheritance', label: '상속' },
    { path: '/service/trust', label: '신탁' },
    { path: '/blog', label: '블로그' },
  ];

  return (
    <nav className="navbar">
      <div className="navbar-container">
        <div className="navbar-logo">
          <Link to="/">법무사</Link>
        </div>
        <ul className="navbar-menu">
          {menuItems.map((item) => (
            <li key={item.path}>
              <Link 
                to={item.path} 
                className={location.pathname === item.path ? 'active' : ''}
              >
                {item.label}
              </Link>
            </li>
          ))}
        </ul>
        <div className="navbar-actions">
          <Link to="/consultation" className="btn-consultation">
            상담
          </Link>
          <Link to="/commission" className="btn-commission">
            업무위임
          </Link>
        </div>
      </div>
    </nav>
  );
};

export default Navbar;

```

```css
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  background-color: var(--color-bg-white);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  z-index: 1000;
  padding: var(--spacing-medium) 0;
}

.navbar-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 var(--spacing-medium);
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.navbar-logo {
  font-size: 24px;
  font-weight: bold;
}

.navbar-logo a {
  color: var(--color-text-dark);
  text-decoration: none;
}

.navbar-menu {
  display: flex;
  list-style: none;
  gap: var(--spacing-large);
  flex: 1;
  justify-content: center;
  margin: 0;
  padding: 0;
}

.navbar-menu li {
  padding-left: 0;
}

.navbar-menu li::before {
  display: none;
}

.navbar-menu a {
  color: var(--color-text-dark);
  text-decoration: none;
  font-size: var(--font-size-body);
  transition: color 0.3s ease;
}

.navbar-menu a:hover,
.navbar-menu a.active {
  color: var(--color-primary);
}

.navbar-actions {
  display: flex;
  gap: var(--spacing-small);
}

.btn-consultation,
.btn-commission {
  padding: var(--spacing-small) var(--spacing-medium);
  background-color: var(--color-primary);
  color: white;
  border-radius: 4px;
  text-decoration: none;
  font-weight: bold;
  transition: background-color 0.3s ease;
}

.btn-consultation:hover,
.btn-commission:hover {
  background-color: #0056b3;
  text-decoration: none;
}

@media (max-width: 768px) {
  .navbar-container {
    flex-direction: column;
    gap: var(--spacing-medium);
  }

  .navbar-menu {
    flex-wrap: wrap;
    gap: var(--spacing-small);
  }

  .navbar-actions {
    width: 100%;
    justify-content: flex-end;
  }
}

```

```javascriptreact
import { Link } from 'react-router-dom';
import './Footer.css';

const Footer = () => {
  return (
    <footer className="footer">
      <div className="footer-container">
        <div className="footer-content">
          <div className="footer-info">
            <h4>법무사 사무소</h4>
            <p>주소: 서울특별시 강남구 테헤란로 123</p>
            <p>전화: 02-1234-5678</p>
            <p>이메일: info@lawyer.com</p>
          </div>
          <div className="footer-actions">
            <Link to="/consultation" className="btn-consultation">
              상담
            </Link>
            <Link to="/commission" className="btn-commission">
              업무위임
            </Link>
          </div>
        </div>
        <div className="footer-bottom">
          <p>&copy; 2024 법무사 사무소. All rights reserved.</p>
        </div>
      </div>
    </footer>
  );
};

export default Footer;

```

```css
.footer {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: var(--color-bg-white);
  box-shadow: 0 -2px 4px rgba(0, 0, 0, 0.1);
  z-index: 1000;
  padding: var(--spacing-medium) 0;
}

.footer-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 var(--spacing-medium);
}

.footer-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: var(--spacing-small);
}

.footer-info h4 {
  margin-bottom: var(--spacing-small);
  color: var(--color-text-dark);
}

.footer-info p {
  margin-bottom: 5px;
  font-size: 16px;
}

.footer-actions {
  display: flex;
  gap: var(--spacing-small);
}

.btn-consultation,
.btn-commission {
  padding: var(--spacing-small) var(--spacing-medium);
  background-color: var(--color-primary);
  color: white;
  border-radius: 4px;
  text-decoration: none;
  font-weight: bold;
  transition: background-color 0.3s ease;
}

.btn-consultation:hover,
.btn-commission:hover {
  background-color: #0056b3;
  text-decoration: none;
}

.footer-bottom {
  text-align: center;
  padding-top: var(--spacing-small);
  border-top: 1px solid #ddd;
}

.footer-bottom p {
  font-size: 14px;
  color: #666;
  margin: 0;
}

@media (max-width: 768px) {
  .footer-content {
    flex-direction: column;
    gap: var(--spacing-medium);
    align-items: flex-start;
  }

  .footer-actions {
    width: 100%;
    justify-content: flex-end;
  }
}

```

```javascriptreact
import Navbar from './Navbar';
import Footer from './Footer';
import './Layout.css';

const Layout = ({ children }) => {
  return (
    <div className="layout">
      <Navbar />
      <main className="main-content">
        {children}
      </main>
      <Footer />
    </div>
  );
};

export default Layout;

```

```css
.layout {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.main-content {
  flex: 1;
  margin-top: 80px; /* Navbar 높이만큼 여백 */
  margin-bottom: 150px; /* Footer 높이만큼 여백 */
  padding: var(--spacing-large) var(--spacing-medium);
  max-width: 1200px;
  width: 100%;
  margin-left: auto;
  margin-right: auto;
}

```

```javascriptreact
import './Button.css';

const Button = ({ children, onClick, type = 'button', variant = 'primary', className = '' }) => {
  return (
    <button
      type={type}
      onClick={onClick}
      className={`btn btn-${variant} ${className}`}
    >
      {children}
    </button>
  );
};

export default Button;

```

```css
.btn {
  padding: var(--spacing-small) var(--spacing-medium);
  border: none;
  border-radius: 4px;
  font-size: var(--font-size-body);
  cursor: pointer;
  transition: all 0.3s ease;
  font-weight: bold;
}

.btn-primary {
  background-color: var(--color-primary);
  color: white;
}

.btn-primary:hover {
  background-color: #0056b3;
}

.btn-secondary {
  background-color: #6c757d;
  color: white;
}

.btn-secondary:hover {
  background-color: #5a6268;
}

.btn-danger {
  background-color: #dc3545;
  color: white;
}

.btn-danger:hover {
  background-color: #c82333;
}

.btn-success {
  background-color: #28a745;
  color: white;
}

.btn-success:hover {
  background-color: #218838;
}

```

```javascriptreact
import { useEffect } from 'react';
import './Modal.css';

const Modal = ({ isOpen, onClose, title, children }) => {
  useEffect(() => {
    if (isOpen) {
      document.body.style.overflow = 'hidden';
    } else {
      document.body.style.overflow = 'unset';
    }

    return () => {
      document.body.style.overflow = 'unset';
    };
  }, [isOpen]);

  if (!isOpen) return null;

  return (
    <div className="modal-overlay" onClick={onClose}>
      <div className="modal-content" onClick={(e) => e.stopPropagation()}>
        <div className="modal-header">
          <h2>{title}</h2>
          <button className="modal-close" onClick={onClose}>×</button>
        </div>
        <div className="modal-body">
          {children}
        </div>
      </div>
    </div>
  );
};

export default Modal;

```

```css
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 2000;
  padding: var(--spacing-medium);
}

.modal-content {
  background-color: var(--color-bg-white);
  border-radius: 8px;
  max-width: 600px;
  width: 100%;
  max-height: 90vh;
  overflow-y: auto;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: var(--spacing-medium);
  border-bottom: 1px solid #ddd;
}

.modal-header h2 {
  margin: 0;
  color: var(--color-text-dark);
}

.modal-close {
  background: none;
  border: none;
  font-size: 32px;
  cursor: pointer;
  color: var(--color-text-dark);
  line-height: 1;
  padding: 0;
  width: 32px;
  height: 32px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal-close:hover {
  color: var(--color-primary);
}

.modal-body {
  padding: var(--spacing-medium);
}

```

라우팅 설정과 메인페이지 구현 중.


```javascriptreact
import { Link } from 'react-router-dom';
import './MainPage.css';

const MainPage = () => {
  const services = [
    { id: 'real-estate', title: '부동산등기', path: '/service/real-estate' },
    { id: 'corporate-registration', title: '법인등기', path: '/service/corporate-registration' },
    { id: 'civil-litigation', title: '민사소송', path: '/service/civil-litigation' },
    { id: 'civil-execution', title: '민사집행', path: '/service/civil-execution' },
    { id: 'inheritance', title: '상속', path: '/service/inheritance' },
    { id: 'trust', title: '신탁', path: '/service/trust' },
  ];

  return (
    <div className="main-page">
      <section className="hero-section">
        <h1>법무사 사무소에 오신 것을 환영합니다</h1>
        <p>전문적이고 신뢰할 수 있는 법률 서비스를 제공합니다.</p>
        <div className="hero-actions">
          <Link to="/consultation" className="btn-primary-large">
            상담 신청
          </Link>
          <Link to="/commission" className="btn-secondary-large">
            업무 위임
          </Link>
        </div>
      </section>

      <section className="services-section">
        <h2>주요 서비스</h2>
        <div className="services-grid">
          {services.map((service) => (
            <Link key={service.id} to={service.path} className="service-card">
              <h3>{service.title}</h3>
              <p>자세히 보기 →</p>
            </Link>
          ))}
        </div>
      </section>

      <section className="blog-preview-section">
        <h2>최신 블로그</h2>
        <div className="blog-preview">
          <Link to="/blog" className="btn-primary">
            블로그 전체 보기
          </Link>
        </div>
      </section>
    </div>
  );
};

export default MainPage;

```

```css
.main-page {
  padding: var(--spacing-large) 0;
}

.hero-section {
  text-align: center;
  padding: var(--spacing-xlarge) 0;
  background: linear-gradient(135deg, #007bff 0%, #0056b3 100%);
  color: white;
  border-radius: 8px;
  margin-bottom: var(--spacing-xlarge);
}

.hero-section h1 {
  color: white;
  font-size: 36px;
  margin-bottom: var(--spacing-medium);
}

.hero-section p {
  font-size: 20px;
  margin-bottom: var(--spacing-large);
  color: rgba(255, 255, 255, 0.9);
}

.hero-actions {
  display: flex;
  gap: var(--spacing-medium);
  justify-content: center;
  flex-wrap: wrap;
}

.btn-primary-large,
.btn-secondary-large {
  padding: var(--spacing-medium) var(--spacing-large);
  border-radius: 4px;
  text-decoration: none;
  font-weight: bold;
  font-size: 18px;
  transition: all 0.3s ease;
}

.btn-primary-large {
  background-color: white;
  color: var(--color-primary);
}

.btn-primary-large:hover {
  background-color: #f0f0f0;
  text-decoration: none;
}

.btn-secondary-large {
  background-color: transparent;
  color: white;
  border: 2px solid white;
}

.btn-secondary-large:hover {
  background-color: rgba(255, 255, 255, 0.1);
  text-decoration: none;
}

.services-section {
  margin-bottom: var(--spacing-xlarge);
}

.services-section h2 {
  text-align: center;
  margin-bottom: var(--spacing-large);
}

.services-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: var(--spacing-large);
}

.service-card {
  background-color: var(--color-bg-white);
  padding: var(--spacing-large);
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  text-decoration: none;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.service-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
  text-decoration: none;
}

.service-card h3 {
  color: var(--color-primary);
  margin-bottom: var(--spacing-small);
}

.service-card p {
  color: var(--color-text-dark);
  margin: 0;
}

.blog-preview-section {
  text-align: center;
  padding: var(--spacing-xlarge) 0;
  background-color: var(--color-bg-white);
  border-radius: 8px;
}

.blog-preview-section h2 {
  margin-bottom: var(--spacing-large);
}

```

```javascriptreact
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';
import Layout from './components/Layout/Layout';
import MainPage from './components/Home/MainPage';
import ServicePage from './components/Service/ServicePage';
import BlogList from './components/Blog/BlogList';
import BlogDetail from './components/Blog/BlogDetail';
import ConsultationForm from './components/Contact/ConsultationForm';
import CommissionForm from './components/Contact/CommissionForm';
import AdminLogin from './components/Admin/AdminLogin';
import AdminDashboard from './components/Admin/AdminDashboard';
import AdminServiceEditor from './components/Admin/AdminServiceEditor';
import AdminBlogEditor from './components/Admin/AdminBlogEditor';
import { useEffect } from 'react';
import { cleanupDeletedItems } from './utils/storage';
import { initialServices, initialBlogPosts } from './data/initialData';
import { loadData, saveData } from './utils/storage';

function App() {
  // 초기 데이터 설정 및 삭제된 항목 정리
  useEffect(() => {
    const data = loadData();
    
    // 초기 데이터가 없으면 샘플 데이터 추가
    if (data.services.length === 0 && data.blogPosts.length === 0) {
      const newData = {
        ...data,
        services: initialServices,
        blogPosts: initialBlogPosts,
      };
      saveData(newData);
    }
    
    // 삭제된 항목 정리 (30일 경과 후 완전 삭제)
    cleanupDeletedItems();
  }, []);

  return (
    <Router>
      <Layout>
        <Routes>
          <Route path="/" element={<MainPage />} />
          <Route path="/service/:serviceId" element={<ServicePage />} />
          <Route path="/blog" element={<BlogList />} />
          <Route path="/blog/:blogId" element={<BlogDetail />} />
          <Route path="/consultation" element={<ConsultationForm />} />
          <Route path="/commission" element={<CommissionForm />} />
          <Route path="/admin/login" element={<AdminLogin />} />
          <Route path="/admin/dashboard" element={<AdminDashboard />} />
          <Route path="/admin/service/:serviceId?" element={<AdminServiceEditor />} />
          <Route path="/admin/blog/:blogId?" element={<AdminBlogEditor />} />
        </Routes>
      </Layout>
    </Router>
  );
}

export default App;

```

서비스 페이지 구현 중.


```javascriptreact
import { useParams, Link } from 'react-router-dom';
import { useEffect, useState } from 'react';
import { getServiceById, getServices } from '../../utils/storage';
import './ServicePage.css';

const ServicePage = () => {
  const { serviceId } = useParams();
  const [service, setService] = useState(null);
  const [services, setServices] = useState([]);

  useEffect(() => {
    const allServices = getServices();
    setServices(allServices);
    
    if (serviceId) {
      const foundService = getServiceById(serviceId);
      setService(foundService);
    }
  }, [serviceId]);

  if (!service) {
    return (
      <div className="service-page">
        <p>서비스를 찾을 수 없습니다.</p>
      </div>
    );
  }

  return (
    <div className="service-page">
      <div className="service-layout">
        {/* 좌측 목차 */}
        <aside className="service-sidebar">
          <h3>서비스 목차</h3>
          <ul className="service-menu">
            {services.map((s) => (
              <li key={s.id}>
                <Link 
                  to={`/service/${s.id}`}
                  className={s.id === serviceId ? 'active' : ''}
                >
                  {s.title}
                </Link>
              </li>
            ))}
          </ul>
        </aside>

        {/* 중앙 컨텐츠 */}
        <main className="service-content">
          <h1>{service.title}</h1>
          <div 
            className="service-content-body"
            dangerouslySetInnerHTML={{ __html: service.content }}
          />
        </main>

        {/* 우측 법령/비용 */}
        <aside className="service-info">
          <div className="info-section">
            <h3>관련 법령</h3>
            <ul>
              {service.laws && service.laws.map((law, index) => (
                <li key={index}>{law}</li>
              ))}
            </ul>
          </div>
          <div className="info-section">
            <h3>비용 안내</h3>
            <div 
              className="costs-content"
              dangerouslySetInnerHTML={{ __html: service.costs }}
            />
          </div>
        </aside>
      </div>
    </div>
  );
};

export default ServicePage;

```

```css
.service-page {
  width: 100%;
}

.service-layout {
  display: grid;
  grid-template-columns: 200px 1fr 250px;
  gap: var(--spacing-large);
}

.service-sidebar {
  background-color: var(--color-bg-white);
  padding: var(--spacing-medium);
  border-radius: 8px;
  height: fit-content;
  position: sticky;
  top: 100px;
}

.service-sidebar h3 {
  margin-bottom: var(--spacing-medium);
  font-size: 20px;
}

.service-menu {
  list-style: none;
  padding: 0;
}

.service-menu li {
  padding-left: 0;
  margin-bottom: var(--spacing-small);
}

.service-menu li::before {
  display: none;
}

.service-menu a {
  display: block;
  padding: var(--spacing-small);
  color: var(--color-text-dark);
  text-decoration: none;
  border-radius: 4px;
  transition: background-color 0.3s ease;
}

.service-menu a:hover,
.service-menu a.active {
  background-color: #e7f3ff;
  color: var(--color-primary);
}

.service-content {
  background-color: var(--color-bg-white);
  padding: var(--spacing-large);
  border-radius: 8px;
}

.service-content h1 {
  margin-bottom: var(--spacing-large);
  color: var(--color-text-darker);
}

.service-content-body {
  line-height: var(--line-height-body);
}

.service-content-body h2 {
  margin-top: var(--spacing-large);
  margin-bottom: var(--spacing-medium);
}

.service-content-body h3 {
  margin-top: var(--spacing-medium);
  margin-bottom: var(--spacing-small);
}

.service-content-body ul {
  margin-bottom: var(--spacing-medium);
}

.service-info {
  background-color: var(--color-bg-white);
  padding: var(--spacing-medium);
  border-radius: 8px;
  height: fit-content;
  position: sticky;
  top: 100px;
}

.info-section {
  margin-bottom: var(--spacing-large);
}

.info-section h3 {
  margin-bottom: var(--spacing-medium);
  font-size: 20px;
  color: var(--color-primary);
}

.info-section ul {
  list-style: none;
  padding: 0;
}

.info-section ul li {
  padding-left: var(--spacing-medium);
  margin-bottom: var(--spacing-small);
}

.costs-content {
  line-height: var(--line-height-body);
}

.costs-content a {
  color: var(--color-primary);
}

@media (max-width: 1024px) {
  .service-layout {
    grid-template-columns: 1fr;
  }

  .service-sidebar,
  .service-info {
    position: static;
  }

  .service-sidebar {
    order: 2;
  }

  .service-content {
    order: 1;
  }

  .service-info {
    order: 3;
  }
}

```

블로그 페이지 구현 중.


```javascriptreact
import { Link } from 'react-router-dom';
import './BlogCard.css';

const BlogCard = ({ post }) => {
  const formatDate = (dateString) => {
    if (!dateString) return '';
    const date = new Date(dateString);
    return date.toLocaleDateString('ko-KR', {
      year: 'numeric',
      month: 'long',
      day: 'numeric'
    });
  };

  const getCategoryLabel = (category) => {
    const labels = {
      'FAQ': '자주 묻는 질문',
      '사안정리': '주제별 사안정리',
      '판례': '중요판례'
    };
    return labels[category] || category;
  };

  return (
    <Link to={`/blog/${post.id}`} className="blog-card">
      <div className="blog-card-header">
        <span className="blog-category">{getCategoryLabel(post.category)}</span>
        <span className="blog-date">{formatDate(post.createdAt)}</span>
      </div>
      <h3 className="blog-title">{post.title}</h3>
      <div 
        className="blog-excerpt"
        dangerouslySetInnerHTML={{ 
          __html: post.content.substring(0, 150) + '...' 
        }}
      />
    </Link>
  );
};

export default BlogCard;

```

```css
.blog-card {
  display: block;
  background-color: var(--color-bg-white);
  padding: var(--spacing-large);
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  text-decoration: none;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  height: 100%;
}

.blog-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
  text-decoration: none;
}

.blog-card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: var(--spacing-medium);
}

.blog-category {
  background-color: var(--color-primary);
  color: white;
  padding: 4px 12px;
  border-radius: 12px;
  font-size: 14px;
  font-weight: bold;
}

.blog-date {
  color: #666;
  font-size: 14px;
}

.blog-title {
  color: var(--color-text-dark);
  margin-bottom: var(--spacing-medium);
  font-size: 22px;
}

.blog-excerpt {
  color: var(--color-text-dark);
  line-height: var(--line-height-body);
  font-size: var(--font-size-body);
}

```

```javascriptreact
import { useState, useEffect } from 'react';
import { getBlogPosts, getBlogPostsByCategory } from '../../utils/storage';
import BlogCard from './BlogCard';
import './BlogList.css';

const BlogList = () => {
  const [posts, setPosts] = useState([]);
  const [selectedCategory, setSelectedCategory] = useState('all');

  useEffect(() => {
    loadPosts();
  }, [selectedCategory]);

  const loadPosts = () => {
    let allPosts;
    if (selectedCategory === 'all') {
      allPosts = getBlogPosts();
    } else {
      allPosts = getBlogPostsByCategory(selectedCategory);
    }
    setPosts(allPosts);
  };

  const categories = [
    { value: 'all', label: '전체' },
    { value: 'FAQ', label: '자주 묻는 질문' },
    { value: '사안정리', label: '주제별 사안정리' },
    { value: '판례', label: '중요판례' },
  ];

  return (
    <div className="blog-list-page">
      <h1>블로그</h1>
      
      <div className="blog-categories">
        {categories.map((category) => (
          <button
            key={category.value}
            onClick={() => setSelectedCategory(category.value)}
            className={`category-btn ${selectedCategory === category.value ? 'active' : ''}`}
          >
            {category.label}
          </button>
        ))}
      </div>

      {posts.length === 0 ? (
        <div className="no-posts">
          <p>등록된 글이 없습니다.</p>
        </div>
      ) : (
        <div className="blog-grid">
          {posts.map((post) => (
            <BlogCard key={post.id} post={post} />
          ))}
        </div>
      )}
    </div>
  );
};

export default BlogList;

```

```css
.blog-list-page {
  width: 100%;
}

.blog-list-page h1 {
  text-align: center;
  margin-bottom: var(--spacing-large);
}

.blog-categories {
  display: flex;
  gap: var(--spacing-small);
  justify-content: center;
  margin-bottom: var(--spacing-xlarge);
  flex-wrap: wrap;
}

.category-btn {
  padding: var(--spacing-small) var(--spacing-medium);
  background-color: var(--color-bg-white);
  color: var(--color-text-dark);
  border: 2px solid var(--color-primary);
  border-radius: 20px;
  cursor: pointer;
  transition: all 0.3s ease;
  font-size: var(--font-size-body);
}

.category-btn:hover {
  background-color: #e7f3ff;
}

.category-btn.active {
  background-color: var(--color-primary);
  color: white;
}

.blog-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
  gap: var(--spacing-large);
}

.no-posts {
  text-align: center;
  padding: var(--spacing-xlarge);
  background-color: var(--color-bg-white);
  border-radius: 8px;
}

.no-posts p {
  color: #666;
  font-size: var(--font-size-body);
}

@media (max-width: 768px) {
  .blog-grid {
    grid-template-columns: 1fr;
  }
}

```

```javascriptreact
import { useParams, Link } from 'react-router-dom';
import { useState, useEffect } from 'react';
import { getBlogPostById } from '../../utils/storage';
import './BlogDetail.css';

const BlogDetail = () => {
  const { blogId } = useParams();
  const [post, setPost] = useState(null);

  useEffect(() => {
    const foundPost = getBlogPostById(blogId);
    setPost(foundPost);
  }, [blogId]);

  if (!post) {
    return (
      <div className="blog-detail-page">
        <p>글을 찾을 수 없습니다.</p>
        <Link to="/blog">블로그 목록으로 돌아가기</Link>
      </div>
    );
  }

  const formatDate = (dateString) => {
    if (!dateString) return '';
    const date = new Date(dateString);
    return date.toLocaleDateString('ko-KR', {
      year: 'numeric',
      month: 'long',
      day: 'numeric'
    });
  };

  const getCategoryLabel = (category) => {
    const labels = {
      'FAQ': '자주 묻는 질문',
      '사안정리': '주제별 사안정리',
      '판례': '중요판례'
    };
    return labels[category] || category;
  };

  return (
    <div className="blog-detail-page">
      <Link to="/blog" className="back-link">← 블로그 목록으로</Link>
      
      <article className="blog-article">
        <div className="blog-meta">
          <span className="blog-category">{getCategoryLabel(post.category)}</span>
          <span className="blog-date">{formatDate(post.createdAt)}</span>
        </div>
        
        <h1>{post.title}</h1>
        
        <div 
          className="blog-content"
          dangerouslySetInnerHTML={{ __html: post.content }}
        />
      </article>
    </div>
  );
};

export default BlogDetail;

```

```css
.blog-detail-page {
  max-width: 800px;
  margin: 0 auto;
  width: 100%;
}

.back-link {
  display: inline-block;
  margin-bottom: var(--spacing-large);
  color: var(--color-primary);
  text-decoration: none;
  font-size: var(--font-size-body);
}

.back-link:hover {
  text-decoration: underline;
}

.blog-article {
  background-color: var(--color-bg-white);
  padding: var(--spacing-xlarge);
  border-radius: 8px;
}

.blog-meta {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: var(--spacing-large);
  padding-bottom: var(--spacing-medium);
  border-bottom: 1px solid #ddd;
}

.blog-category {
  background-color: var(--color-primary);
  color: white;
  padding: 6px 16px;
  border-radius: 12px;
  font-size: 14px;
  font-weight: bold;
}

.blog-date {
  color: #666;
  font-size: 16px;
}

.blog-article h1 {
  margin-bottom: var(--spacing-large);
  color: var(--color-text-darker);
}

.blog-content {
  line-height: var(--line-height-body);
}

.blog-content h2 {
  margin-top: var(--spacing-large);
  margin-bottom: var(--spacing-medium);
}

.blog-content h3 {
  margin-top: var(--spacing-medium);
  margin-bottom: var(--spacing-small);
}

.blog-content p {
  margin-bottom: var(--spacing-medium);
}

.blog-content ul {
  margin-bottom: var(--spacing-medium);
}

@media (max-width: 768px) {
  .blog-article {
    padding: var(--spacing-large);
  }

  .blog-meta {
    flex-direction: column;
    align-items: flex-start;
    gap: var(--spacing-small);
  }
}

```

상담/위임 폼 구현 중.


```javascriptreact
import { useState } from 'react';
import { useNavigate } from 'react-router-dom';
import { submitConsultationForm } from '../../utils/n8nWebhook';
import Button from '../common/Button';
import './ContactForm.css';

const ConsultationForm = () => {
  const navigate = useNavigate();
  const [formData, setFormData] = useState({
    name: '',
    phone: '',
    email: '',
    subject: '',
    message: '',
  });
  const [isSubmitting, setIsSubmitting] = useState(false);
  const [submitMessage, setSubmitMessage] = useState('');

  const handleChange = (e) => {
    const { name, value } = e.target;
    setFormData(prev => ({
      ...prev,
      [name]: value
    }));
  };

  const handleSubmit = async (e) => {
    e.preventDefault();
    setIsSubmitting(true);
    setSubmitMessage('');

    const result = await submitConsultationForm(formData);

    if (result.success) {
      setSubmitMessage(result.message);
      setTimeout(() => {
        navigate('/');
      }, 2000);
    } else {
      setSubmitMessage(result.message);
    }

    setIsSubmitting(false);
  };

  return (
    <div className="contact-form-page">
      <h1>상담 신청</h1>
      <p>법률 상담이 필요하시면 아래 양식을 작성해 주세요.</p>

      <form onSubmit={handleSubmit} className="contact-form">
        <div className="form-group">
          <label htmlFor="name">이름 *</label>
          <input
            type="text"
            id="name"
            name="name"
            value={formData.name}
            onChange={handleChange}
            required
          />
        </div>

        <div className="form-group">
          <label htmlFor="phone">전화번호 *</label>
          <input
            type="tel"
            id="phone"
            name="phone"
            value={formData.phone}
            onChange={handleChange}
            required
          />
        </div>

        <div className="form-group">
          <label htmlFor="email">이메일</label>
          <input
            type="email"
            id="email"
            name="email"
            value={formData.email}
            onChange={handleChange}
          />
        </div>

        <div className="form-group">
          <label htmlFor="subject">상담 주제 *</label>
          <input
            type="text"
            id="subject"
            name="subject"
            value={formData.subject}
            onChange={handleChange}
            required
          />
        </div>

        <div className="form-group">
          <label htmlFor="message">상담 내용 *</label>
          <textarea
            id="message"
            name="message"
            value={formData.message}
            onChange={handleChange}
            rows="10"
            required
          />
        </div>

        {submitMessage && (
          <div className={`submit-message ${submitMessage.includes('완료') ? 'success' : 'error'}`}>
            {submitMessage}
          </div>
        )}

        <div className="form-actions">
          <Button type="submit" disabled={isSubmitting}>
            {isSubmitting ? '제출 중...' : '상담 신청'}
          </Button>
          <Button type="button" variant="secondary" onClick={() => navigate('/')}>
            취소
          </Button>
        </div>
      </form>
    </div>
  );
};

export default ConsultationForm;

```

```javascriptreact
import { useState } from 'react';
import { useNavigate } from 'react-router-dom';
import { submitCommissionForm } from '../../utils/n8nWebhook';
import Button from '../common/Button';
import './ContactForm.css';

const CommissionForm = () => {
  const navigate = useNavigate();
  const [formData, setFormData] = useState({
    name: '',
    phone: '',
    email: '',
    serviceType: '',
    caseDescription: '',
    urgency: 'normal',
    preferredContact: 'phone',
  });
  const [isSubmitting, setIsSubmitting] = useState(false);
  const [submitMessage, setSubmitMessage] = useState('');

  const handleChange = (e) => {
    const { name, value } = e.target;
    setFormData(prev => ({
      ...prev,
      [name]: value
    }));
  };

  const handleSubmit = async (e) => {
    e.preventDefault();
    setIsSubmitting(true);
    setSubmitMessage('');

    const result = await submitCommissionForm(formData);

    if (result.success) {
      setSubmitMessage(result.message);
      setTimeout(() => {
        navigate('/');
      }, 2000);
    } else {
      setSubmitMessage(result.message);
    }

    setIsSubmitting(false);
  };

  return (
    <div className="contact-form-page">
      <h1>업무 위임 신청</h1>
      <p>법률 업무 위임이 필요하시면 아래 양식을 작성해 주세요.</p>

      <form onSubmit={handleSubmit} className="contact-form">
        <div className="form-group">
          <label htmlFor="name">이름 *</label>
          <input
            type="text"
            id="name"
            name="name"
            value={formData.name}
            onChange={handleChange}
            required
          />
        </div>

        <div className="form-group">
          <label htmlFor="phone">전화번호 *</label>
          <input
            type="tel"
            id="phone"
            name="phone"
            value={formData.phone}
            onChange={handleChange}
            required
          />
        </div>

        <div className="form-group">
          <label htmlFor="email">이메일</label>
          <input
            type="email"
            id="email"
            name="email"
            value={formData.email}
            onChange={handleChange}
          />
        </div>

        <div className="form-group">
          <label htmlFor="serviceType">업무 유형 *</label>
          <select
            id="serviceType"
            name="serviceType"
            value={formData.serviceType}
            onChange={handleChange}
            required
          >
            <option value="">선택하세요</option>
            <option value="real-estate">부동산등기</option>
            <option value="corporate-registration">법인등기</option>
            <option value="civil-litigation">민사소송</option>
            <option value="civil-execution">민사집행</option>
            <option value="inheritance">상속</option>
            <option value="trust">신탁</option>
            <option value="other">기타</option>
          </select>
        </div>

        <div className="form-group">
          <label htmlFor="caseDescription">사건 개요 *</label>
          <textarea
            id="caseDescription"
            name="caseDescription"
            value={formData.caseDescription}
            onChange={handleChange}
            rows="10"
            required
          />
        </div>

        <div className="form-group">
          <label htmlFor="urgency">긴급도</label>
          <select
            id="urgency"
            name="urgency"
            value={formData.urgency}
            onChange={handleChange}
          >
            <option value="low">낮음</option>
            <option value="normal">보통</option>
            <option value="high">높음</option>
            <option value="urgent">긴급</option>
          </select>
        </div>

        <div className="form-group">
          <label htmlFor="preferredContact">선호 연락 방법</label>
          <select
            id="preferredContact"
            name="preferredContact"
            value={formData.preferredContact}
            onChange={handleChange}
          >
            <option value="phone">전화</option>
            <option value="email">이메일</option>
            <option value="both">둘 다</option>
          </select>
        </div>

        {submitMessage && (
          <div className={`submit-message ${submitMessage.includes('완료') ? 'success' : 'error'}`}>
            {submitMessage}
          </div>
        )}

        <div className="form-actions">
          <Button type="submit" disabled={isSubmitting}>
            {isSubmitting ? '제출 중...' : '위임 신청'}
          </Button>
          <Button type="button" variant="secondary" onClick={() => navigate('/')}>
            취소
          </Button>
        </div>
      </form>
    </div>
  );
};

export default CommissionForm;

```

```css
.contact-form-page {
  max-width: 700px;
  margin: 0 auto;
  width: 100%;
}

.contact-form-page h1 {
  text-align: center;
  margin-bottom: var(--spacing-medium);
}

.contact-form-page > p {
  text-align: center;
  margin-bottom: var(--spacing-xlarge);
  color: #666;
}

.contact-form {
  background-color: var(--color-bg-white);
  padding: var(--spacing-xlarge);
  border-radius: 8px;
}

.form-group {
  margin-bottom: var(--spacing-large);
}

.form-group label {
  display: block;
  margin-bottom: var(--spacing-small);
  color: var(--color-text-dark);
  font-weight: bold;
}

.form-group input,
.form-group textarea,
.form-group select {
  width: 100%;
  padding: var(--spacing-small);
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: var(--font-size-body);
  font-family: var(--font-main);
}

.form-group input:focus,
.form-group textarea:focus,
.form-group select:focus {
  outline: none;
  border-color: var(--color-primary);
}

.submit-message {
  padding: var(--spacing-medium);
  border-radius: 4px;
  margin-bottom: var(--spacing-medium);
  text-align: center;
}

.submit-message.success {
  background-color: #d4edda;
  color: #155724;
  border: 1px solid #c3e6cb;
}

.submit-message.error {
  background-color: #f8d7da;
  color: #721c24;
  border: 1px solid #f5c6cb;
}

.form-actions {
  display: flex;
  gap: var(--spacing-medium);
  justify-content: center;
  margin-top: var(--spacing-xlarge);
}

@media (max-width: 768px) {
  .contact-form {
    padding: var(--spacing-large);
  }

  .form-actions {
    flex-direction: column;
  }

  .form-actions button {
    width: 100%;
  }
}

```

관리자 기능 구현 중.


```javascriptreact
import { useState } from 'react';
import { useNavigate } from 'react-router-dom';
import { verifyAdminPassword, setAdminPassword } from '../../utils/storage';
import { loginAdmin } from '../../utils/adminAuth';
import Button from '../common/Button';
import './AdminLogin.css';

const AdminLogin = () => {
  const navigate = useNavigate();
  const [password, setPassword] = useState('');
  const [error, setError] = useState('');
  const [isInitialSetup, setIsInitialSetup] = useState(false);
  const [newPassword, setNewPassword] = useState('');
  const [confirmPassword, setConfirmPassword] = useState('');

  // 초기 비밀번호 설정 여부 확인
  useState(() => {
    const data = require('../../utils/storage').loadData();
    if (!data.adminPassword) {
      setIsInitialSetup(true);
    }
  }, []);

  const handleLogin = (e) => {
    e.preventDefault();
    setError('');

    if (verifyAdminPassword(password)) {
      loginAdmin();
      navigate('/admin/dashboard');
    } else {
      setError('비밀번호가 올바르지 않습니다.');
    }
  };

  const handleInitialSetup = (e) => {
    e.preventDefault();
    setError('');

    if (newPassword.length < 4) {
      setError('비밀번호는 최소 4자 이상이어야 합니다.');
      return;
    }

    if (newPassword !== confirmPassword) {
      setError('비밀번호가 일치하지 않습니다.');
      return;
    }

    setAdminPassword(newPassword);
    loginAdmin();
    navigate('/admin/dashboard');
  };

  if (isInitialSetup) {
    return (
      <div className="admin-login-page">
        <div className="admin-login-box">
          <h1>관리자 비밀번호 설정</h1>
          <p>처음 사용하시는 경우 관리자 비밀번호를 설정해 주세요.</p>
          <form onSubmit={handleInitialSetup}>
            <div className="form-group">
              <label htmlFor="newPassword">비밀번호 *</label>
              <input
                type="password"
                id="newPassword"
                value={newPassword}
                onChange={(e) => setNewPassword(e.target.value)}
                required
                minLength={4}
              />
            </div>
            <div className="form-group">
              <label htmlFor="confirmPassword">비밀번호 확인 *</label>
              <input
                type="password"
                id="confirmPassword"
                value={confirmPassword}
                onChange={(e) => setConfirmPassword(e.target.value)}
                required
                minLength={4}
              />
            </div>
            {error && <div className="error-message">{error}</div>}
            <Button type="submit">비밀번호 설정</Button>
          </form>
        </div>
      </div>
    );
  }

  return (
    <div className="admin-login-page">
      <div className="admin-login-box">
        <h1>관리자 로그인</h1>
        <form onSubmit={handleLogin}>
          <div className="form-group">
            <label htmlFor="password">비밀번호 *</label>
            <input
              type="password"
              id="password"
              value={password}
              onChange={(e) => setPassword(e.target.value)}
              required
            />
          </div>
          {error && <div className="error-message">{error}</div>}
          <Button type="submit">로그인</Button>
        </form>
      </div>
    </div>
  );
};

export default AdminLogin;

```

```css
.admin-login-page {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 60vh;
  padding: var(--spacing-large);
}

.admin-login-box {
  background-color: var(--color-bg-white);
  padding: var(--spacing-xlarge);
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  max-width: 400px;
  width: 100%;
}

.admin-login-box h1 {
  text-align: center;
  margin-bottom: var(--spacing-medium);
}

.admin-login-box > p {
  text-align: center;
  margin-bottom: var(--spacing-large);
  color: #666;
}

.admin-login-box .form-group {
  margin-bottom: var(--spacing-large);
}

.admin-login-box label {
  display: block;
  margin-bottom: var(--spacing-small);
  color: var(--color-text-dark);
  font-weight: bold;
}

.admin-login-box input {
  width: 100%;
  padding: var(--spacing-small);
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: var(--font-size-body);
}

.error-message {
  background-color: #f8d7da;
  color: #721c24;
  padding: var(--spacing-small);
  border-radius: 4px;
  margin-bottom: var(--spacing-medium);
  text-align: center;
}

.admin-login-box button {
  width: 100%;
}

```

```javascriptreact
import { useEffect } from 'react';
import { useNavigate, Link } from 'react-router-dom';
import { isAdminLoggedIn, logoutAdmin } from '../../utils/adminAuth';
import { getServices, getBlogPosts } from '../../utils/storage';
import Button from '../common/Button';
import './AdminDashboard.css';

const AdminDashboard = () => {
  const navigate = useNavigate();

  useEffect(() => {
    if (!isAdminLoggedIn()) {
      navigate('/admin/login');
    }
  }, [navigate]);

  const handleLogout = () => {
    logoutAdmin();
    navigate('/');
  };

  const services = getServices();
  const blogPosts = getBlogPosts(true); // 삭제된 것 포함

  if (!isAdminLoggedIn()) {
    return null;
  }

  return (
    <div className="admin-dashboard">
      <div className="admin-header">
        <h1>관리자 대시보드</h1>
        <Button onClick={handleLogout} variant="secondary">
          로그아웃
        </Button>
      </div>

      <div className="admin-stats">
        <div className="stat-card">
          <h3>서비스 수</h3>
          <p className="stat-number">{services.length}</p>
        </div>
        <div className="stat-card">
          <h3>블로그 글 수</h3>
          <p className="stat-number">{blogPosts.length}</p>
        </div>
      </div>

      <div className="admin-sections">
        <section className="admin-section">
          <div className="section-header">
            <h2>서비스 관리</h2>
            <Link to="/admin/service">
              <Button variant="primary">새 서비스 추가</Button>
            </Link>
          </div>
          <div className="admin-list">
            {services.length === 0 ? (
              <p>등록된 서비스가 없습니다.</p>
            ) : (
              <ul>
                {services.map((service) => (
                  <li key={service.id}>
                    <Link to={`/admin/service/${service.id}`}>
                      {service.title}
                    </Link>
                  </li>
                ))}
              </ul>
            )}
          </div>
        </section>

        <section className="admin-section">
          <div className="section-header">
            <h2>블로그 관리</h2>
            <Link to="/admin/blog">
              <Button variant="primary">새 글 작성</Button>
            </Link>
          </div>
          <div className="admin-list">
            {blogPosts.length === 0 ? (
              <p>등록된 글이 없습니다.</p>
            ) : (
              <ul>
                {blogPosts.map((post) => (
                  <li key={post.id}>
                    <Link to={`/admin/blog/${post.id}`}>
                      {post.title}
                      {post.deletedAt && <span className="deleted-badge">(삭제됨)</span>}
                    </Link>
                  </li>
                ))}
              </ul>
            )}
          </div>
        </section>
      </div>
    </div>
  );
};

export default AdminDashboard;

```

```css
.admin-dashboard {
  width: 100%;
}

.admin-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: var(--spacing-xlarge);
}

.admin-stats {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: var(--spacing-large);
  margin-bottom: var(--spacing-xlarge);
}

.stat-card {
  background-color: var(--color-bg-white);
  padding: var(--spacing-large);
  border-radius: 8px;
  text-align: center;
}

.stat-card h3 {
  margin-bottom: var(--spacing-medium);
  color: var(--color-text-dark);
}

.stat-number {
  font-size: 36px;
  font-weight: bold;
  color: var(--color-primary);
  margin: 0;
}

.admin-sections {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
  gap: var(--spacing-xlarge);
}

.admin-section {
  background-color: var(--color-bg-white);
  padding: var(--spacing-large);
  border-radius: 8px;
}

.section-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: var(--spacing-large);
}

.section-header h2 {
  margin: 0;
}

.admin-list ul {
  list-style: none;
  padding: 0;
}

.admin-list li {
  padding: var(--spacing-small) 0;
  border-bottom: 1px solid #eee;
  padding-left: 0;
}

.admin-list li::before {
  display: none;
}

.admin-list li:last-child {
  border-bottom: none;
}

.admin-list a {
  color: var(--color-text-dark);
  text-decoration: none;
  display: flex;
  align-items: center;
  gap: var(--spacing-small);
}

.admin-list a:hover {
  color: var(--color-primary);
}

.deleted-badge {
  color: #dc3545;
  font-size: 14px;
}

@media (max-width: 768px) {
  .admin-header {
    flex-direction: column;
    gap: var(--spacing-medium);
    align-items: flex-start;
  }

  .admin-sections {
    grid-template-columns: 1fr;
  }

  .section-header {
    flex-direction: column;
    gap: var(--spacing-medium);
    align-items: flex-start;
  }
}

```

```javascriptreact
import { useState, useEffect } from 'react';
import { useParams, useNavigate } from 'react-router-dom';
import { isAdminLoggedIn } from '../../utils/adminAuth';
import { getServiceById, saveService, getServices } from '../../utils/storage';
import Button from '../common/Button';
import './AdminEditor.css';

const AdminServiceEditor = () => {
  const { serviceId } = useParams();
  const navigate = useNavigate();
  const [service, setService] = useState({
    id: '',
    title: '',
    content: '',
    laws: [],
    costs: '',
  });
  const [lawInput, setLawInput] = useState('');
  const [isLoading, setIsLoading] = useState(true);

  useEffect(() => {
    if (!isAdminLoggedIn()) {
      navigate('/admin/login');
      return;
    }

    if (serviceId) {
      const existingService = getServiceById(serviceId);
      if (existingService) {
        setService({
          ...existingService,
          laws: existingService.laws || [],
        });
      }
    } else {
      // 새 서비스인 경우 ID 생성
      const services = getServices();
      const newId = `service-${Date.now()}`;
      setService({
        id: newId,
        title: '',
        content: '',
        laws: [],
        costs: '',
      });
    }
    setIsLoading(false);
  }, [serviceId, navigate]);

  const handleChange = (e) => {
    const { name, value } = e.target;
    setService(prev => ({
      ...prev,
      [name]: value
    }));
  };

  const handleAddLaw = () => {
    if (lawInput.trim()) {
      setService(prev => ({
        ...prev,
        laws: [...prev.laws, lawInput.trim()]
      }));
      setLawInput('');
    }
  };

  const handleRemoveLaw = (index) => {
    setService(prev => ({
      ...prev,
      laws: prev.laws.filter((_, i) => i !== index)
    }));
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    
    if (!service.title || !service.content) {
      alert('제목과 내용을 입력해 주세요.');
      return;
    }

    saveService(service);
    navigate('/admin/dashboard');
  };

  if (isLoading) {
    return <div>로딩 중...</div>;
  }

  return (
    <div className="admin-editor">
      <div className="editor-header">
        <h1>{serviceId ? '서비스 수정' : '새 서비스 추가'}</h1>
        <Button onClick={() => navigate('/admin/dashboard')} variant="secondary">
          취소
        </Button>
      </div>

      <form onSubmit={handleSubmit} className="editor-form">
        <div className="form-group">
          <label htmlFor="id">ID</label>
          <input
            type="text"
            id="id"
            name="id"
            value={service.id}
            disabled
          />
        </div>

        <div className="form-group">
          <label htmlFor="title">제목 *</label>
          <input
            type="text"
            id="title"
            name="title"
            value={service.title}
            onChange={handleChange}
            required
          />
        </div>

        <div className="form-group">
          <label htmlFor="content">내용 (HTML) *</label>
          <textarea
            id="content"
            name="content"
            value={service.content}
            onChange={handleChange}
            rows="15"
            required
          />
        </div>

        <div className="form-group">
          <label>관련 법령</label>
          <div className="laws-input">
            <input
              type="text"
              value={lawInput}
              onChange={(e) => setLawInput(e.target.value)}
              onKeyPress={(e) => e.key === 'Enter' && (e.preventDefault(), handleAddLaw())}
              placeholder="법령 이름 입력 후 Enter"
            />
            <Button type="button" onClick={handleAddLaw}>추가</Button>
          </div>
          <ul className="laws-list">
            {service.laws.map((law, index) => (
              <li key={index}>
                {law}
                <button type="button" onClick={() => handleRemoveLaw(index)}>삭제</button>
              </li>
            ))}
          </ul>
        </div>

        <div className="form-group">
          <label htmlFor="costs">비용 안내 (HTML)</label>
          <textarea
            id="costs"
            name="costs"
            value={service.costs}
            onChange={handleChange}
            rows="5"
          />
        </div>

        <div className="form-actions">
          <Button type="submit">저장</Button>
          <Button type="button" variant="secondary" onClick={() => navigate('/admin/dashboard')}>
            취소
          </Button>
        </div>
      </form>
    </div>
  );
};

export default AdminServiceEditor;

```

```javascriptreact
import { useState, useEffect } from 'react';
import { useParams, useNavigate } from 'react-router-dom';
import { isAdminLoggedIn } from '../../utils/adminAuth';
import { getBlogPostById, saveBlogPost, getBlogPosts } from '../../utils/storage';
import Button from '../common/Button';
import './AdminEditor.css';

const AdminBlogEditor = () => {
  const { blogId } = useParams();
  const navigate = useNavigate();
  const [post, setPost] = useState({
    id: '',
    title: '',
    category: 'FAQ',
    content: '',
  });
  const [isLoading, setIsLoading] = useState(true);

  useEffect(() => {
    if (!isAdminLoggedIn()) {
      navigate('/admin/login');
      return;
    }

    if (blogId) {
      const existingPost = getBlogPostById(blogId);
      if (existingPost) {
        setPost({
          id: existingPost.id,
          title: existingPost.title,
          category: existingPost.category || 'FAQ',
          content: existingPost.content,
        });
      }
    } else {
      // 새 글인 경우 ID 생성
      const posts = getBlogPosts(true);
      const newId = `blog-${Date.now()}`;
      setPost({
        id: newId,
        title: '',
        category: 'FAQ',
        content: '',
      });
    }
    setIsLoading(false);
  }, [blogId, navigate]);

  const handleChange = (e) => {
    const { name, value } = e.target;
    setPost(prev => ({
      ...prev,
      [name]: value
    }));
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    
    if (!post.title || !post.content) {
      alert('제목과 내용을 입력해 주세요.');
      return;
    }

    saveBlogPost(post);
    navigate('/admin/dashboard');
  };

  const handleDelete = () => {
    if (window.confirm('정말 삭제하시겠습니까? 30일 후 완전히 삭제됩니다.')) {
      const { deleteBlogPost } = require('../../utils/storage');
      deleteBlogPost(post.id);
      navigate('/admin/dashboard');
    }
  };

  if (isLoading) {
    return <div>로딩 중...</div>;
  }

  return (
    <div className="admin-editor">
      <div className="editor-header">
        <h1>{blogId ? '블로그 글 수정' : '새 글 작성'}</h1>
        <div className="header-actions">
          {blogId && (
            <Button onClick={handleDelete} variant="danger">
              삭제
            </Button>
          )}
          <Button onClick={() => navigate('/admin/dashboard')} variant="secondary">
            취소
          </Button>
        </div>
      </div>

      <form onSubmit={handleSubmit} className="editor-form">
        <div className="form-group">
          <label htmlFor="id">ID</label>
          <input
            type="text"
            id="id"
            name="id"
            value={post.id}
            disabled
          />
        </div>

        <div className="form-group">
          <label htmlFor="title">제목 *</label>
          <input
            type="text"
            id="title"
            name="title"
            value={post.title}
            onChange={handleChange}
            required
          />
        </div>

        <div className="form-group">
          <label htmlFor="category">카테고리 *</label>
          <select
            id="category"
            name="category"
            value={post.category}
            onChange={handleChange}
            required
          >
            <option value="FAQ">자주 묻는 질문</option>
            <option value="사안정리">주제별 사안정리</option>
            <option value="판례">중요판례</option>
          </select>
        </div>

        <div className="form-group">
          <label htmlFor="content">내용 (HTML) *</label>
          <textarea
            id="content"
            name="content"
            value={post.content}
            onChange={handleChange}
            rows="20"
            required
          />
        </div>

        <div className="form-actions">
          <Button type="submit">저장</Button>
          <Button type="button" variant="secondary" onClick={() => navigate('/admin/dashboard')}>
            취소
          </Button>
        </div>
      </form>
    </div>
  );
};

export default AdminBlogEditor;

```

```css
.admin-editor {
  max-width: 900px;
  margin: 0 auto;
  width: 100%;
}

.editor-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: var(--spacing-xlarge);
}

.header-actions {
  display: flex;
  gap: var(--spacing-small);
}

.editor-form {
  background-color: var(--color-bg-white);
  padding: var(--spacing-xlarge);
  border-radius: 8px;
}

.form-group {
  margin-bottom: var(--spacing-large);
}

.form-group label {
  display: block;
  margin-bottom: var(--spacing-small);
  color: var(--color-text-dark);
  font-weight: bold;
}

.form-group input,
.form-group textarea,
.form-group select {
  width: 100%;
  padding: var(--spacing-small);
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: var(--font-size-body);
  font-family: var(--font-main);
}

.form-group input:disabled {
  background-color: #f5f5f5;
  color: #666;
}

.form-group input:focus,
.form-group textarea:focus,
.form-group select:focus {
  outline: none;
  border-color: var(--color-primary);
}

.laws-input {
  display: flex;
  gap: var(--spacing-small);
  margin-bottom: var(--spacing-small);
}

.laws-input input {
  flex: 1;
}

.laws-list {
  list-style: none;
  padding: 0;
  margin-top: var(--spacing-small);
}

.laws-list li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: var(--spacing-small);
  background-color: #f5f5f5;
  border-radius: 4px;
  margin-bottom: var(--spacing-small);
  padding-left: var(--spacing-medium);
}

.laws-list li::before {
  display: none;
}

.laws-list li button {
  padding: 4px 12px;
  background-color: #dc3545;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 14px;
}

.laws-list li button:hover {
  background-color: #c82333;
}

.form-actions {
  display: flex;
  gap: var(--spacing-medium);
  justify-content: flex-end;
  margin-top: var(--spacing-xlarge);
}

@media (max-width: 768px) {
  .editor-header {
    flex-direction: column;
    gap: var(--spacing-medium);
    align-items: flex-start;
  }

  .header-actions {
    width: 100%;
    justify-content: flex-end;
  }

  .editor-form {
    padding: var(--spacing-large);
  }

  .form-actions {
    flex-direction: column;
  }

  .form-actions button {
    width: 100%;
  }
}

```

AdminLogin 컴포넌트 수정 및 최종 조정 중.


AdminLogin 컴포넌트의 useState 오용을 useEffect로 수정 중.


```javascriptreact
import { useState, useEffect } from 'react';
import { useNavigate } from 'react-router-dom';
import { verifyAdminPassword, setAdminPassword, loadData } from '../../utils/storage';
import { loginAdmin } from '../../utils/adminAuth';
import Button from '../common/Button';
import './AdminLogin.css';

const AdminLogin = () => {
  const navigate = useNavigate();
  const [password, setPassword] = useState('');
  const [error, setError] = useState('');
  const [isInitialSetup, setIsInitialSetup] = useState(false);
  const [newPassword, setNewPassword] = useState('');
  const [confirmPassword, setConfirmPassword] = useState('');

  // 초기 비밀번호 설정 여부 확인
  useEffect(() => {
    const data = loadData();
    if (!data.adminPassword) {
      setIsInitialSetup(true);
    }
  }, []);

  const handleLogin = (e) => {
    e.preventDefault();
    setError('');

    if (verifyAdminPassword(password)) {
      loginAdmin();
      navigate('/admin/dashboard');
    } else {
      setError('비밀번호가 올바르지 않습니다.');
    }
  };

  const handleInitialSetup = (e) => {
    e.preventDefault();
    setError('');

    if (newPassword.length < 4) {
      setError('비밀번호는 최소 4자 이상이어야 합니다.');
      return;
    }

    if (newPassword !== confirmPassword) {
      setError('비밀번호가 일치하지 않습니다.');
      return;
    }

    setAdminPassword(newPassword);
    loginAdmin();
    navigate('/admin/dashboard');
  };

  if (isInitialSetup) {
    return (
      <div className="admin-login-page">
        <div className="admin-login-box">
          <h1>관리자 비밀번호 설정</h1>
          <p>처음 사용하시는 경우 관리자 비밀번호를 설정해 주세요.</p>
          <form onSubmit={handleInitialSetup}>
            <div className="form-group">
              <label htmlFor="newPassword">비밀번호 *</label>
              <input
                type="password"
                id="newPassword"
                value={newPassword}
                onChange={(e) => setNewPassword(e.target.value)}
                required
                minLength={4}
              />
            </div>
            <div className="form-group">
              <label htmlFor="confirmPassword">비밀번호 확인 *</label>
              <input
                type="password"
                id="confirmPassword"
                value={confirmPassword}
                onChange={(e) => setConfirmPassword(e.target.value)}
                required
                minLength={4}
              />
            </div>
            {error && <div className="error-message">{error}</div>}
            <Button type="submit">비밀번호 설정</Button>
          </form>
        </div>
      </div>
    );
  }

  return (
    <div className="admin-login-page">
      <div className="admin-login-box">
        <h1>관리자 로그인</h1>
        <form onSubmit={handleLogin}>
          <div className="form-group">
            <label htmlFor="password">비밀번호 *</label>
            <input
              type="password"
              id="password"
              value={password}
              onChange={(e) => setPassword(e.target.value)}
              required
            />
          </div>
          {error && <div className="error-message">{error}</div>}
          <Button type="submit">로그인</Button>
        </form>
      </div>
    </div>
  );
};

export default AdminLogin;


```

README 작성 및 린터 오류 확인 중.


```markdown
# 법무사 홈페이지

React 기반의 법무사 홈페이지입니다. 로컬스토리지를 사용하여 데이터를 관리하며, N8N과 NOTION을 연동할 수 있습니다.

## 주요 기능

- **메인페이지**: 홈 화면 및 서비스 소개
- **서비스 페이지**: 좌측 목차, 중앙 컨텐츠, 우측 법령/비용 레이아웃
- **블로그**: 카드 형식의 블로그 목록, FAQ/사안정리/판례 카테고리 분류
- **상담/위임 폼**: N8N 웹훅을 통한 NOTION 연동
- **관리자 기능**: 서비스/블로그 글 추가/수정/삭제 (삭제 시 30일 후 완전 삭제)

## 기술 스택

- React 18
- React Router DOM
- Vite
- localStorage (데이터 저장)

## 설치 및 실행

1. 의존성 설치:
```bash
npm install
```

2. 개발 서버 실행:
```bash
npm run dev
```

3. 빌드:
```bash
npm run build
```

## 환경 변수 설정

N8N 웹훅 URL을 설정하려면 `.env` 파일을 생성하고 다음을 추가하세요:

```
VITE_N8N_CONSULTATION_WEBHOOK_URL=https://your-n8n-url.com/webhook/consultation
VITE_N8N_COMMISSION_WEBHOOK_URL=https://your-n8n-url.com/webhook/commission
```

## 관리자 접근

1. `/admin/login` 경로로 이동
2. 처음 사용하는 경우 비밀번호를 설정
3. 설정한 비밀번호로 로그인하여 관리자 대시보드 접근

## 데이터 구조

모든 데이터는 브라우저의 localStorage에 JSON 형식으로 저장됩니다.

- 서비스 데이터: `services` 배열
- 블로그 데이터: `blogPosts` 배열
- 관리자 비밀번호: `adminPassword` (base64 인코딩)

## 주요 페이지

- `/` - 메인페이지
- `/service/:serviceId` - 서비스 상세 페이지
- `/blog` - 블로그 목록
- `/blog/:blogId` - 블로그 상세 페이지
- `/consultation` - 상담 신청 폼
- `/commission` - 업무 위임 폼
- `/admin/login` - 관리자 로그인
- `/admin/dashboard` - 관리자 대시보드
- `/admin/service/:serviceId?` - 서비스 편집
- `/admin/blog/:blogId?` - 블로그 편집

## 스타일링

사용자 규칙에 따라 다음 스타일이 적용됩니다:

- 본문: 맑은고딕, 18px, 텍스트 그림자 효과
- 제목: h1/h2/h3는 어두운 회색 (#333, #444)
- 본문: 밝은 회색 배경, 검정 텍스트
- 링크: 파란색 (#007bff)
- ul 리스트: 점(•) 아이콘

## N8N 연동

상담/위임 폼 제출 시 N8N 웹훅으로 데이터가 전송됩니다. N8N 워크플로우에서 NOTION에 데이터를 저장하도록 설정하세요.

## 라이선스

MIT

```

모든 작업 완료. 최종 확인 중.


```xml
<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" aria-hidden="true" role="img" class="iconify iconify--logos" width="31.88" height="32" preserveAspectRatio="xMidYMid meet" viewBox="0 0 256 257"><defs><linearGradient id="IconifyId1813088fe1fbc01fb466" x1="-.828%" x2="57.636%" y1="7.652%" y2="78.411%"><stop offset="0%" stop-color="#41D1FF"></stop><stop offset="100%" stop-color="#BD34FE"></stop></linearGradient><linearGradient id="IconifyId1813088fe1fbc01fb467" x1="43.376%" x2="50.316%" y1="2.242%" y2="89.03%"><stop offset="0%" stop-color="#FFEA83"></stop><stop offset="8.333%" stop-color="#FFDD35"></stop><stop offset="100%" stop-color="#FFA800"></stop></linearGradient></defs><path fill="url(#IconifyId1813088fe1fbc01fb466)" d="M255.153 37.938L134.897 252.976c-2.483 4.44-8.862 4.466-11.382.048L.875 37.958c-2.746-4.814 1.371-10.646 6.827-9.67l120.385 21.517a6.537 6.537 0 0 0 2.322-.004l117.867-21.483c5.438-.991 9.574 4.796 6.877 9.62Z"></path><path fill="url(#IconifyId1813088fe1fbc01fb467)" d="M185.432.063L96.44 17.501a3.268 3.268 0 0 0-2.634 3.014l-5.474 92.456a3.268 3.268 0 0 0 3.997 3.378l24.777-5.718c2.318-.535 4.413 1.507 3.936 3.838l-7.361 36.047c-.495 2.426 1.782 4.5 4.151 3.78l15.304-4.649c2.372-.72 4.652 1.36 4.15 3.788l-11.698 56.621c-.732 3.542 3.979 5.473 5.943 2.437l1.313-2.028l72.516-144.72c1.215-2.423-.88-5.186-3.54-4.672l-25.505 4.922c-2.396.462-4.435-1.77-3.759-4.114l16.646-57.705c.677-2.35-1.37-4.583-3.769-4.113Z"></path></svg>

```

법무사 홈페이지 구현을 완료했습니다. 플랜의 모든 항목을 구현했습니다.

## 구현 완료된 기능

### 1. 프로젝트 구조
- Vite + React 프로젝트 설정
- React Router DOM 라우팅 구성
- 필요한 의존성 설정

### 2. 레이아웃 컴포넌트
- **Navbar**: 상단 고정, 상담/업무위임 버튼 우측 배치
- **Footer**: 하단 고정(스크롤해도 고정), 상담/업무위임 버튼 포함
- **Layout**: 전체 레이아웃 래퍼

### 3. 페이지 구현
- **메인페이지**: 서비스 소개 및 블로그 미리보기
- **서비스 페이지**: 좌측 목차, 중앙 컨텐츠, 우측 법령/비용 레이아웃
- **블로그**: 카드 형식 목록, FAQ/사안정리/판례 카테고리 분류, 상세 페이지

### 4. 폼 및 연동
- **상담 폼**: N8N 웹훅 연동
- **위임 폼**: N8N 웹훅 연동
- 환경 변수로 웹훅 URL 설정 가능

### 5. 관리자 기능
- **로그인**: 비밀번호 기반 인증
- **대시보드**: 서비스/블로그 통계 및 관리
- **서비스 편집**: 추가/수정 기능
- **블로그 편집**: 추가/수정/삭제 기능
- **삭제 로직**: 삭제 시 30일 후 완전 삭제

### 6. 데이터 관리
- localStorage 기반 JSON 데이터 저장
- 초기 샘플 데이터 포함
- 자동 삭제된 항목 정리

### 7. 스타일링
- 사용자 규칙 반영:
  - 본문: 맑은고딕, 18px, 텍스트 그림자
  - 제목: 어두운 회색 (#333, #444)
  - 본문: 밝은 회색 배경, 검정 텍스트
  - 링크: 파란색 (#007bff)
  - ul 리스트: 점(•) 아이콘

## 실행 방법

1. 의존성 설치:
```bash
npm install
```

2. 개발 서버 실행:
```bash
npm run dev
```

3. N8N 웹훅 URL 설정 (선택사항):
`.env` 파일을 생성하고 다음을 추가:
```
VITE_N8N_CONSULTATION_WEBHOOK_URL=your-webhook-url
VITE_N8N_COMMISSION_WEBHOOK_URL=your-webhook-url
```

## 관리자 접근

1. `/admin/login`으로 이동
2. 처음 사용 시 비밀번호 설정
3. 설정한 비밀번호로 로그인

모든 기능이 구현되었고, 린터 오류도 없습니다. 프로젝트를 실행해 테스트하세요.

```shellscript
npm install
```

```shellscript
npm run dev
```

```plaintext
VITE_N8N_CONSULTATION_WEBHOOK_URL=your-webhook-url
VITE_N8N_COMMISSION_WEBHOOK_URL=your-webhook-url
```

```shellscript
npm install
```

```shellscript
npm run dev
```

```plaintext
VITE_N8N_CONSULTATION_WEBHOOK_URL=your-webhook-url
VITE_N8N_COMMISSION_WEBHOOK_URL=your-webhook-url
```

---

**User**

너가 요청한대로 의존성설치와 개발서버 실행을 하였는데도 웹페이지에 아무것도 표시되지 않고 있어. 완전 백지야. 무슨 문제인지 해결해줘.

---

**Cursor**

브라우저 콘솔 오류 확인 중. 코드를 점검해 문제를 찾겠습니다.


App.jsx에서 `<Router>` 태그가 누락된 것으로 보입니다. 파일을 다시 확인 중입니다.


브라우저 콘솔 오류 확인을 위해 간단한 테스트 컴포넌트로 렌더링을 확인하고, CSS import 경로와 컴포넌트를 점검 중입니다.


PowerShell 명령 구문을 수정해 다시 확인 중입니다.


에러 바운더리 추가 및 App.jsx 안정화 중. 브라우저 콘솔 오류 확인을 위해 간단한 테스트 컴포넌트로 렌더링을 확인 중입니다.


```javascriptreact
import React from 'react';

class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false, error: null };
  }

  static getDerivedStateFromError(error) {
    return { hasError: true, error };
  }

  componentDidCatch(error, errorInfo) {
    console.error('Error caught by boundary:', error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      return (
        <div style={{ padding: '20px', textAlign: 'center' }}>
          <h1>오류가 발생했습니다</h1>
          <p>{this.state.error?.toString()}</p>
          <button onClick={() => window.location.reload()}>페이지 새로고침</button>
        </div>
      );
    }

    return this.props.children;
  }
}

export default ErrorBoundary;

```

```javascriptreact
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.jsx'
import ErrorBoundary from './components/common/ErrorBoundary.jsx'
import './styles/global.css'

const root = ReactDOM.createRoot(document.getElementById('root'));

root.render(
  <React.StrictMode>
    <ErrorBoundary>
      <App />
    </ErrorBoundary>
  </React.StrictMode>
)




```

App.jsx의 useEffect를 더 안전하게 수정하고, 에러 처리를 추가 중입니다.


```javascriptreact
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';
import Layout from './components/Layout/Layout';
import MainPage from './components/Home/MainPage';
import ServicePage from './components/Service/ServicePage';
import BlogList from './components/Blog/BlogList';
import BlogDetail from './components/Blog/BlogDetail';
import ConsultationForm from './components/Contact/ConsultationForm';
import CommissionForm from './components/Contact/CommissionForm';
import AdminLogin from './components/Admin/AdminLogin';
import AdminDashboard from './components/Admin/AdminDashboard';
import AdminServiceEditor from './components/Admin/AdminServiceEditor';
import AdminBlogEditor from './components/Admin/AdminBlogEditor';
import { useEffect } from 'react';
import { cleanupDeletedItems } from './utils/storage';
import { initialServices, initialBlogPosts } from './data/initialData';
import { loadData, saveData } from './utils/storage';

function App() {
  // 초기 데이터 설정 및 삭제된 항목 정리
  useEffect(() => {
    try {
      const data = loadData();
      
      // 초기 데이터가 없으면 샘플 데이터 추가
      if (data && (!data.services || data.services.length === 0) && (!data.blogPosts || data.blogPosts.length === 0)) {
        const newData = {
          ...data,
          services: initialServices || [],
          blogPosts: initialBlogPosts || [],
        };
        saveData(newData);
      }
      
      // 삭제된 항목 정리 (30일 경과 후 완전 삭제)
      try {
        cleanupDeletedItems();
      } catch (error) {
        console.error('삭제된 항목 정리 중 오류:', error);
      }
    } catch (error) {
      console.error('초기 데이터 설정 중 오류:', error);
    }
  }, []);

  return (
    <Router>
      <Layout>
        <Routes>
          <Route path="/" element={<MainPage />} />
          <Route path="/service/:serviceId" element={<ServicePage />} />
          <Route path="/blog" element={<BlogList />} />
          <Route path="/blog/:blogId" element={<BlogDetail />} />
          <Route path="/consultation" element={<ConsultationForm />} />
          <Route path="/commission" element={<CommissionForm />} />
          <Route path="/admin/login" element={<AdminLogin />} />
          <Route path="/admin/dashboard" element={<AdminDashboard />} />
          <Route path="/admin/service/:serviceId?" element={<AdminServiceEditor />} />
          <Route path="/admin/blog/:blogId?" element={<AdminBlogEditor />} />
        </Routes>
      </Layout>
    </Router>
  );
}

export default App;




```

간단한 테스트용 App 컴포넌트를 만들어 렌더링 문제를 확인 중입니다.


```javascriptreact
// 임시 테스트 파일 - 문제 진단용
import React from 'react';

function AppTest() {
  return (
    <div style={{ padding: '20px', textAlign: 'center' }}>
      <h1>테스트 페이지</h1>
      <p>이 페이지가 보이면 React는 정상 작동 중입니다.</p>
    </div>
  );
}

export default AppTest;

```

디버깅을 위해 콘솔 로그를 추가하고, 브라우저 개발자 도구에서 오류를 확인하도록 안내 중입니다.


```javascriptreact
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';
import Layout from './components/Layout/Layout';
import MainPage from './components/Home/MainPage';
import ServicePage from './components/Service/ServicePage';
import BlogList from './components/Blog/BlogList';
import BlogDetail from './components/Blog/BlogDetail';
import ConsultationForm from './components/Contact/ConsultationForm';
import CommissionForm from './components/Contact/CommissionForm';
import AdminLogin from './components/Admin/AdminLogin';
import AdminDashboard from './components/Admin/AdminDashboard';
import AdminServiceEditor from './components/Admin/AdminServiceEditor';
import AdminBlogEditor from './components/Admin/AdminBlogEditor';
import { useEffect } from 'react';
import { cleanupDeletedItems } from './utils/storage';
import { initialServices, initialBlogPosts } from './data/initialData';
import { loadData, saveData } from './utils/storage';

function App() {
  console.log('App 컴포넌트 렌더링 시작');
  
  // 초기 데이터 설정 및 삭제된 항목 정리
  useEffect(() => {
    console.log('App useEffect 실행');
    try {
      const data = loadData();
      console.log('데이터 로드 완료:', data);
      
      // 초기 데이터가 없으면 샘플 데이터 추가
      if (data && (!data.services || data.services.length === 0) && (!data.blogPosts || data.blogPosts.length === 0)) {
        console.log('초기 데이터 추가');
        const newData = {
          ...data,
          services: initialServices || [],
          blogPosts: initialBlogPosts || [],
        };
        saveData(newData);
      }
      
      // 삭제된 항목 정리 (30일 경과 후 완전 삭제)
      try {
        cleanupDeletedItems();
      } catch (error) {
        console.error('삭제된 항목 정리 중 오류:', error);
      }
    } catch (error) {
      console.error('초기 데이터 설정 중 오류:', error);
    }
  }, []);
  
  console.log('App 컴포넌트 렌더링 완료');

  return (
    <Router>
      <Layout>
        <Routes>
          <Route path="/" element={<MainPage />} />
          <Route path="/service/:serviceId" element={<ServicePage />} />
          <Route path="/blog" element={<BlogList />} />
          <Route path="/blog/:blogId" element={<BlogDetail />} />
          <Route path="/consultation" element={<ConsultationForm />} />
          <Route path="/commission" element={<CommissionForm />} />
          <Route path="/admin/login" element={<AdminLogin />} />
          <Route path="/admin/dashboard" element={<AdminDashboard />} />
          <Route path="/admin/service/:serviceId?" element={<AdminServiceEditor />} />
          <Route path="/admin/blog/:blogId?" element={<AdminBlogEditor />} />
        </Routes>
      </Layout>
    </Router>
  );
}

export default App;




```

```javascriptreact
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.jsx'
import ErrorBoundary from './components/common/ErrorBoundary.jsx'
import './styles/global.css'

console.log('main.jsx 실행 시작');
console.log('root 요소 찾기:', document.getElementById('root'));

const rootElement = document.getElementById('root');
if (!rootElement) {
  console.error('root 요소를 찾을 수 없습니다!');
} else {
  console.log('root 요소 찾음, ReactDOM.createRoot 실행');
  const root = ReactDOM.createRoot(rootElement);
  
  console.log('App 컴포넌트 렌더링 시작');
  root.render(
    <React.StrictMode>
      <ErrorBoundary>
        <App />
      </ErrorBoundary>
    </React.StrictMode>
  );
  console.log('App 컴포넌트 렌더링 완료');
}




```

디버깅 로그를 추가했습니다. 브라우저 개발자 도구(F12)의 콘솔 탭에서 오류를 확인해 주세요. 동시에 간단한 테스트 페이지를 만들어 확인 중입니다.


```markdown
# 문제 해결 가이드

## 웹페이지가 백지로 표시되는 경우

### 1. 브라우저 개발자 도구 확인
- **F12** 키를 누르거나 브라우저에서 우클릭 → "검사" 선택
- **Console** 탭을 열어서 빨간색 에러 메시지 확인
- 에러 메시지를 복사해서 알려주세요

### 2. 네트워크 탭 확인
- 개발자 도구의 **Network** 탭 확인
- 파일들이 제대로 로드되는지 확인 (빨간색이 있으면 문제)

### 3. 일반적인 문제 해결

#### 문제: JavaScript가 실행되지 않음
- 브라우저 설정에서 JavaScript가 활성화되어 있는지 확인
- 브라우저 확장 프로그램(광고 차단기 등)이 JavaScript를 차단하는지 확인

#### 문제: 파일을 찾을 수 없음
- 터미널에서 `npm run dev`가 정상적으로 실행되고 있는지 확인
- 브라우저 주소창이 `http://localhost:5173` (또는 Vite가 제공하는 포트)인지 확인

#### 문제: CORS 오류
- 로컬 개발 서버를 사용하는 경우 CORS 문제는 발생하지 않아야 합니다
- 다른 포트에서 실행 중인 서버가 있다면 종료하고 다시 시작

### 4. 캐시 지우기
- 브라우저 캐시를 지우고 강력 새로고침 (Ctrl+Shift+R 또는 Cmd+Shift+R)
- 또는 시크릿 모드에서 테스트

### 5. 개발 서버 재시작
```bash
# 터미널에서 Ctrl+C로 서버 중지 후
npm run dev
```

### 6. 의존성 재설치
```bash
# node_modules 삭제 후 재설치
rm -rf node_modules
npm install
npm run dev
```

## 콘솔 로그 확인
브라우저 콘솔에서 다음 메시지들이 순서대로 나타나야 합니다:
1. "main.jsx 실행 시작"
2. "root 요소 찾기: ..."
3. "root 요소 찾음, ReactDOM.createRoot 실행"
4. "App 컴포넌트 렌더링 시작"
5. "App 컴포넌트 렌더링 완료"
6. "App useEffect 실행"

이 메시지들이 나타나지 않거나 에러가 있다면, 그 내용을 알려주세요.

```

디버깅 로그를 추가했습니다. 다음을 확인해 주세요:

## 즉시 확인할 사항

1. 브라우저 개발자 도구 열기
   - F12 키를 누르거나 우클릭 → "검사"
   - Console 탭 확인

2. 콘솔에 나타나는 메시지 확인
   - "main.jsx 실행 시작" 같은 로그가 보이는지
   - 빨간색 에러 메시지가 있는지

3. Network 탭 확인
   - 파일들이 제대로 로드되는지
   - 빨간색(실패) 항목이 있는지

## 가능한 원인과 해결

가장 가능성 높은 원인:
1. JavaScript 실행 오류: 콘솔에 에러가 있을 수 있음
2. 파일 로드 실패: Network 탭에서 확인
3. 브라우저 캐시: 강력 새로고침(Ctrl+Shift+R)

브라우저 콘솔에 나타나는 에러 메시지를 알려주시면 정확히 해결하겠습니다.

또한, 간단한 테스트를 위해 개발 서버가 정상 실행 중인지 확인해 주세요. 터미널에 "Local: http://localhost:5173" 같은 메시지가 보여야 합니다.

---

**User**

Uncaught ReferenceError: process is not defined



    at n8nWebhook.js:4:38



위와같은 오류가 콘설창에서 발견되었어. 

---

**Cursor**

문제는 `n8nWebhook.js`에서 `process.env`를 사용한 것입니다. Vite에서는 `import.meta.env`를 사용해야 합니다. 수정하겠습니다.


Vite에서는 `process.env` 대신 `import.meta.env`를 사용해야 합니다. 수정 중입니다.


```javascript
// N8N 웹훅 호출 함수

// N8N 웹훅 URL (환경 변수나 설정 파일에서 가져올 수 있음)
const N8N_CONSULTATION_WEBHOOK_URL = import.meta.env.VITE_N8N_CONSULTATION_WEBHOOK_URL || '';
const N8N_COMMISSION_WEBHOOK_URL = import.meta.env.VITE_N8N_COMMISSION_WEBHOOK_URL || '';

// 상담 폼 제출
export const submitConsultationForm = async (formData) => {
  if (!N8N_CONSULTATION_WEBHOOK_URL) {
    console.warn('N8N 상담 웹훅 URL이 설정되지 않았습니다.');
    return { success: false, message: '웹훅 URL이 설정되지 않았습니다.' };
  }

  try {
    const response = await fetch(N8N_CONSULTATION_WEBHOOK_URL, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({
        type: 'consultation',
        ...formData,
        submittedAt: new Date().toISOString(),
      }),
    });

    if (response.ok) {
      return { success: true, message: '상담 신청이 완료되었습니다.' };
    } else {
      return { success: false, message: '상담 신청 중 오류가 발생했습니다.' };
    }
  } catch (error) {
    console.error('N8N 웹훅 호출 실패:', error);
    return { success: false, message: '네트워크 오류가 발생했습니다.' };
  }
};

// 위임 폼 제출
export const submitCommissionForm = async (formData) => {
  if (!N8N_COMMISSION_WEBHOOK_URL) {
    console.warn('N8N 위임 웹훅 URL이 설정되지 않았습니다.');
    return { success: false, message: '웹훅 URL이 설정되지 않았습니다.' };
  }

  try {
    const response = await fetch(N8N_COMMISSION_WEBHOOK_URL, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({
        type: 'commission',
        ...formData,
        submittedAt: new Date().toISOString(),
      }),
    });

    if (response.ok) {
      return { success: true, message: '위임 신청이 완료되었습니다.' };
    } else {
      return { success: false, message: '위임 신청 중 오류가 발생했습니다.' };
    }
  } catch (error) {
    console.error('N8N 웹훅 호출 실패:', error);
    return { success: false, message: '네트워크 오류가 발생했습니다.' };
  }
};




```

수정 완료했습니다. 문제는 `n8nWebhook.js`에서 `process.env`를 사용한 것이었습니다. Vite에서는 `import.meta.env`를 사용해야 합니다.

## 수정 내용
- `process.env.VITE_N8N_CONSULTATION_WEBHOOK_URL` → `import.meta.env.VITE_N8N_CONSULTATION_WEBHOOK_URL`
- `process.env.VITE_N8N_COMMISSION_WEBHOOK_URL` → `import.meta.env.VITE_N8N_COMMISSION_WEBHOOK_URL`

## 다음 단계
1. 브라우저에서 강력 새로고침 (Ctrl+Shift+R 또는 Cmd+Shift+R)
2. 개발 서버가 실행 중이면 자동으로 반영됩니다
3. 콘솔에 에러가 더 이상 나타나지 않아야 합니다

이제 웹페이지가 정상적으로 표시되어야 합니다. 여전히 문제가 있으면 브라우저 콘솔의 에러 메시지를 알려주세요.

---

**User**

<ServicePage>민사집행 민사집행 서비스 민사집행은 확정된 채권을 실현하기 위한 강제집행 절차입니다. 주요 서비스 내용 부동산 강제경매 동산 압류 및 매각 채권 압류 및 추심 가압류 및 가처분</ServicePage>
<main class="service-content">민사집행 민사집행 서비스 민사집행은 확정된 채권을 실현하기 위한 강제집행 절차입니다. 주요 서비스 내용 부동산 강제경매 동산 압류 및 매각 채권 압류 및 추심 가압류 및 가처분</main> 이 박스 색을 노란색으로 바꿔줘

---

**Cursor**

ServicePage의 중앙 컨텐츠 영역 배경색을 노란색으로 변경 중입니다.


ServicePage의 중앙 컨텐츠 영역 배경색을 노란색으로 변경 중입니다.


```css
.service-page {
  width: 100%;
}

.service-layout {
  display: grid;
  grid-template-columns: 200px 1fr 250px;
  gap: var(--spacing-large);
}

.service-sidebar {
  background-color: var(--color-bg-white);
  padding: var(--spacing-medium);
  border-radius: 8px;
  height: fit-content;
  position: sticky;
  top: 100px;
}

.service-sidebar h3 {
  margin-bottom: var(--spacing-medium);
  font-size: 20px;
}

.service-menu {
  list-style: none;
  padding: 0;
}

.service-menu li {
  padding-left: 0;
  margin-bottom: var(--spacing-small);
}

.service-menu li::before {
  display: none;
}

.service-menu a {
  display: block;
  padding: var(--spacing-small);
  color: var(--color-text-dark);
  text-decoration: none;
  border-radius: 4px;
  transition: background-color 0.3s ease;
}

.service-menu a:hover,
.service-menu a.active {
  background-color: #e7f3ff;
  color: var(--color-primary);
}

.service-content {
  background-color: #ffffcc;
  padding: var(--spacing-large);
  border-radius: 8px;
}

.service-content h1 {
  margin-bottom: var(--spacing-large);
  color: var(--color-text-darker);
}

.service-content-body {
  line-height: var(--line-height-body);
}

.service-content-body h2 {
  margin-top: var(--spacing-large);
  margin-bottom: var(--spacing-medium);
}

.service-content-body h3 {
  margin-top: var(--spacing-medium);
  margin-bottom: var(--spacing-small);
}

.service-content-body ul {
  margin-bottom: var(--spacing-medium);
}

.service-info {
  background-color: var(--color-bg-white);
  padding: var(--spacing-medium);
  border-radius: 8px;
  height: fit-content;
  position: sticky;
  top: 100px;
}

.info-section {
  margin-bottom: var(--spacing-large);
}

.info-section h3 {
  margin-bottom: var(--spacing-medium);
  font-size: 20px;
  color: var(--color-primary);
}

.info-section ul {
  list-style: none;
  padding: 0;
}

.info-section ul li {
  padding-left: var(--spacing-medium);
  margin-bottom: var(--spacing-small);
}

.costs-content {
  line-height: var(--line-height-body);
}

.costs-content a {
  color: var(--color-primary);
}

@media (max-width: 1024px) {
  .service-layout {
    grid-template-columns: 1fr;
  }

  .service-sidebar,
  .service-info {
    position: static;
  }

  .service-sidebar {
    order: 2;
  }

  .service-content {
    order: 1;
  }

  .service-info {
    order: 3;
  }
}




```

변경 완료. ServicePage의 중앙 컨텐츠 영역(`main.service-content`) 배경색을 노란색(`#ffffcc`)으로 변경했습니다.

브라우저에서 변경 사항이 바로 반영됩니다. 색상이 다르면 원하는 색상 코드를 알려주세요.

---

**User**

<h3>주요 서비스 내용</h3> 크기를 좀 더 작게해줘

---

**Cursor**

`<h3>주요 서비스 내용</h3>` 크기를 더 작게 조정 중입니다.


서비스 컨텐츠 본문의 h3 크기를 더 작게 조정 중입니다.


```css
.service-page {
  width: 100%;
}

.service-layout {
  display: grid;
  grid-template-columns: 200px 1fr 250px;
  gap: var(--spacing-large);
}

.service-sidebar {
  background-color: var(--color-bg-white);
  padding: var(--spacing-medium);
  border-radius: 8px;
  height: fit-content;
  position: sticky;
  top: 100px;
}

.service-sidebar h3 {
  margin-bottom: var(--spacing-medium);
  font-size: 20px;
}

.service-menu {
  list-style: none;
  padding: 0;
}

.service-menu li {
  padding-left: 0;
  margin-bottom: var(--spacing-small);
}

.service-menu li::before {
  display: none;
}

.service-menu a {
  display: block;
  padding: var(--spacing-small);
  color: var(--color-text-dark);
  text-decoration: none;
  border-radius: 4px;
  transition: background-color 0.3s ease;
}

.service-menu a:hover,
.service-menu a.active {
  background-color: #e7f3ff;
  color: var(--color-primary);
}

.service-content {
  background-color: #ffffcc;
  padding: var(--spacing-large);
  border-radius: 8px;
}

.service-content h1 {
  margin-bottom: var(--spacing-large);
  color: var(--color-text-darker);
}

.service-content-body {
  line-height: var(--line-height-body);
}

.service-content-body h2 {
  margin-top: var(--spacing-large);
  margin-bottom: var(--spacing-medium);
}

.service-content-body h3 {
  margin-top: var(--spacing-medium);
  margin-bottom: var(--spacing-small);
  font-size: 18px;
}

.service-content-body ul {
  margin-bottom: var(--spacing-medium);
}

.service-info {
  background-color: var(--color-bg-white);
  padding: var(--spacing-medium);
  border-radius: 8px;
  height: fit-content;
  position: sticky;
  top: 100px;
}

.info-section {
  margin-bottom: var(--spacing-large);
}

.info-section h3 {
  margin-bottom: var(--spacing-medium);
  font-size: 20px;
  color: var(--color-primary);
}

.info-section ul {
  list-style: none;
  padding: 0;
}

.info-section ul li {
  padding-left: var(--spacing-medium);
  margin-bottom: var(--spacing-small);
}

.costs-content {
  line-height: var(--line-height-body);
}

.costs-content a {
  color: var(--color-primary);
}

@media (max-width: 1024px) {
  .service-layout {
    grid-template-columns: 1fr;
  }

  .service-sidebar,
  .service-info {
    position: static;
  }

  .service-sidebar {
    order: 2;
  }

  .service-content {
    order: 1;
  }

  .service-info {
    order: 3;
  }
}




```

변경 완료. 서비스 컨텐츠 본문의 `<h3>` 크기를 18px로 설정했습니다. 전역 스타일의 24px보다 작습니다.

브라우저에서 바로 반영됩니다. 더 작게 하려면 원하는 크기를 알려주세요.

---

**User**

<p>민사집행은 확정된 채권을 실현하기 위한 강제집행 절차입니다.</p> 이 곳을 아래 내용으로 바꿔줘



강제집행을 개시하기 위해서는 **집행당사자, 집행권원, 집행문**이라는 세 가지 핵심 요건이 충족되어야 합니다.



**1. 집행당사자 (민사집행법 제3조)**



강제집행 절차의 당사자는 집행을 구하는 **집행채권자**와 집행을 받는 **집행채무자**입니다. 이들은 원칙적으로 판결에 표시된 원고와 피고이지만, 강제집행 절차에서 누가 집행채권자이고 집행채무자인지는 **집행문**에 기재된 사람에 의해 확정됩니다.



집행당사자의 **적격**은 강제집행을 진행할 정당한 자격을 의미하며, 이는 **승계**에 의해 변동될 수 있습니다. 예를 들어, 판결 확정 후 채권자 또는 채무자가 사망하여 상속이 발생하거나 채권 양도가 이루어진 경우, 상속인이나 채권 양수인이 새로운 집행당사자가 됩니다(민사집행법 제31조 제1항, 대법원 2010. 1. 14. 2009그196 참조).



**2. 집행권원 (민사집행법 제2조)**



**집행권원**은 사법상 청구권의 존재와 범위가 확정되어 강제집행을 할 수 있는 **국가 공권력의 근거**가 되는 공정증서입니다. 주요 집행권원의 종류는 다음과 같습니다.



- **확정판결 및 가집행 선고부 판결**: 민사소송법상 확정된 판결은 물론, 아직 확정되지 않았어도 가집행이 선고된 판결도 집행권원이 됩니다(민사집행법 제213조 제1항).

- **화해조서, 조정조서, 확정된 지급명령 등**: 소송상 화해나 조정 내용이 담긴 조서 및 법원의 확정된 지급명령도 확정판결과 동일한 효력을 가지므로 집행권원이 됩니다(민사집행법 제57조, 제58조 제3항).

- **공정증서**: 공증인이 일정한 금액의 지급이나 대체물 인도를 목적으로 작성한 공정증서도 집행권원입니다(공증인법 제56조 제2항).

- **확정된 화해권고결정**: 소액사건심판법에 따른 화해권고결정 중 확정된 것 또한 집행권원이 됩니다(소액사건심판법 제5조의7 제1항).



집행권원은 **급부의무의 내용이 명확**해야 하며, 그 내용이 **이행 가능하고 적법**해야 합니다.



**3. 집행문 (민사집행법 제28조)**



**집행문**은 집행권원에 강제집행력이 있다는 사실을 공적으로 증명하기 위해 법원사무관등이 집행권원 정본의 끝에 덧붙여 부여하는 문언입니다. 원칙적으로 강제집행 개시를 위해서는 집행권원 정본에 집행문이 부여되어야 합니다.



그러나 **예외적으로 집행문 부여가 필요 없는 경우**도 있습니다. 예를 들어, 확정된 지급명령에 의한 집행, 가압류·가처분명령에 의한 집행, 또는 화해조서나 조정조서에 의한 집행 등은 집행문 없이도 강제집행이 가능합니다(민사집행법 제58조 제1항 본문, 제291조, 제301조).



집행문은 통상적인 경우의 **통상집행문** 외에, 당사자의 승계가 있는 경우의 **승계집행문**, 그리고 조건이 붙은 경우의 **조건부집행문** 등으로 나뉩니다(민사집행법 제30조 제2항, 제31조 제1항).



이러한 강제집행의 요건들은 모두 강제집행 절차의 적법성과 유효성을 담보하는 중요한 요소이므로, 각 요건의 충족 여부를 면밀히 검토해야 합니다.

---

**Cursor**

민사집행 서비스 내용을 확인하고 해당 문단을 교체 중입니다.


민사집행 서비스 내용을 요청하신 내용으로 교체 중입니다.


```javascript
// 초기 데이터 구조 및 샘플 데이터

export const initialServices = [
  {
    id: 'real-estate',
    title: '부동산등기',
    content: `
      <h2>부동산등기 서비스</h2>
      <p>부동산등기는 부동산의 권리관계를 명확히 하고 거래의 안전을 보장하기 위한 중요한 제도입니다.</p>
      <h3>주요 서비스 내용</h3>
      <ul>
        <li>소유권 이전등기</li>
        <li>저당권 설정등기</li>
        <li>전세권 설정등기</li>
        <li>지상권 설정등기</li>
      </ul>
    `,
    laws: [
      '부동산등기법',
      '민법',
      '부동산 실권리자명의 등기에 관한 법률'
    ],
    costs: '비용은 <a href="/costs">비용 안내 페이지</a>를 참고하시기 바랍니다.'
  },
  {
    id: 'corporate-registration',
    title: '법인등기',
    content: `
      <h2>법인등기 서비스</h2>
      <p>법인등기는 법인의 설립, 변경, 해산 등 법인의 중요한 사항을 공시하는 제도입니다.</p>
      <h3>주요 서비스 내용</h3>
      <ul>
        <li>법인 설립등기</li>
        <li>법인 변경등기</li>
        <li>법인 해산등기</li>
        <li>법인 청산등기</li>
      </ul>
    `,
    laws: [
      '상법',
      '법인세법',
      '부가가치세법'
    ],
    costs: '비용은 <a href="/costs">비용 안내 페이지</a>를 참고하시기 바랍니다.'
  },
  {
    id: 'civil-litigation',
    title: '민사소송',
    content: `
      <h2>민사소송 서비스</h2>
      <p>민사소송은 개인 간의 권리관계에 관한 분쟁을 법원을 통해 해결하는 절차입니다.</p>
      <h3>주요 서비스 내용</h3>
      <ul>
        <li>소장 작성 및 제출</li>
        <li>변론 준비 및 대리</li>
        <li>화해 및 조정</li>
        <li>항소 및 상고</li>
      </ul>
    `,
    laws: [
      '민사소송법',
      '민법',
      '소송촉진 등에 관한 특례법'
    ],
    costs: '비용은 <a href="/costs">비용 안내 페이지</a>를 참고하시기 바랍니다.'
  },
  {
    id: 'civil-execution',
    title: '민사집행',
    content: `
      <h2>민사집행 서비스</h2>
      <p>강제집행을 개시하기 위해서는 <strong>집행당사자, 집행권원, 집행문</strong>이라는 세 가지 핵심 요건이 충족되어야 합니다.</p>
      
      <h3>1. 집행당사자 (민사집행법 제3조)</h3>
      <p>강제집행 절차의 당사자는 집행을 구하는 <strong>집행채권자</strong>와 집행을 받는 <strong>집행채무자</strong>입니다. 이들은 원칙적으로 판결에 표시된 원고와 피고이지만, 강제집행 절차에서 누가 집행채권자이고 집행채무자인지는 <strong>집행문</strong>에 기재된 사람에 의해 확정됩니다.</p>
      <p>집행당사자의 <strong>적격</strong>은 강제집행을 진행할 정당한 자격을 의미하며, 이는 <strong>승계</strong>에 의해 변동될 수 있습니다. 예를 들어, 판결 확정 후 채권자 또는 채무자가 사망하여 상속이 발생하거나 채권 양도가 이루어진 경우, 상속인이나 채권 양수인이 새로운 집행당사자가 됩니다(민사집행법 제31조 제1항, 대법원 2010. 1. 14. 2009그196 참조).</p>
      
      <h3>2. 집행권원 (민사집행법 제2조)</h3>
      <p><strong>집행권원</strong>은 사법상 청구권의 존재와 범위가 확정되어 강제집행을 할 수 있는 <strong>국가 공권력의 근거</strong>가 되는 공정증서입니다. 주요 집행권원의 종류는 다음과 같습니다.</p>
      <ul>
        <li><strong>확정판결 및 가집행 선고부 판결</strong>: 민사소송법상 확정된 판결은 물론, 아직 확정되지 않았어도 가집행이 선고된 판결도 집행권원이 됩니다(민사집행법 제213조 제1항).</li>
        <li><strong>화해조서, 조정조서, 확정된 지급명령 등</strong>: 소송상 화해나 조정 내용이 담긴 조서 및 법원의 확정된 지급명령도 확정판결과 동일한 효력을 가지므로 집행권원이 됩니다(민사집행법 제57조, 제58조 제3항).</li>
        <li><strong>공정증서</strong>: 공증인이 일정한 금액의 지급이나 대체물 인도를 목적으로 작성한 공정증서도 집행권원입니다(공증인법 제56조 제2항).</li>
        <li><strong>확정된 화해권고결정</strong>: 소액사건심판법에 따른 화해권고결정 중 확정된 것 또한 집행권원이 됩니다(소액사건심판법 제5조의7 제1항).</li>
      </ul>
      <p>집행권원은 <strong>급부의무의 내용이 명확</strong>해야 하며, 그 내용이 <strong>이행 가능하고 적법</strong>해야 합니다.</p>
      
      <h3>3. 집행문 (민사집행법 제28조)</h3>
      <p><strong>집행문</strong>은 집행권원에 강제집행력이 있다는 사실을 공적으로 증명하기 위해 법원사무관등이 집행권원 정본의 끝에 덧붙여 부여하는 문언입니다. 원칙적으로 강제집행 개시를 위해서는 집행권원 정본에 집행문이 부여되어야 합니다.</p>
      <p>그러나 <strong>예외적으로 집행문 부여가 필요 없는 경우</strong>도 있습니다. 예를 들어, 확정된 지급명령에 의한 집행, 가압류·가처분명령에 의한 집행, 또는 화해조서나 조정조서에 의한 집행 등은 집행문 없이도 강제집행이 가능합니다(민사집행법 제58조 제1항 본문, 제291조, 제301조).</p>
      <p>집행문은 통상적인 경우의 <strong>통상집행문</strong> 외에, 당사자의 승계가 있는 경우의 <strong>승계집행문</strong>, 그리고 조건이 붙은 경우의 <strong>조건부집행문</strong> 등으로 나뉩니다(민사집행법 제30조 제2항, 제31조 제1항).</p>
      <p>이러한 강제집행의 요건들은 모두 강제집행 절차의 적법성과 유효성을 담보하는 중요한 요소이므로, 각 요건의 충족 여부를 면밀히 검토해야 합니다.</p>
      
      <h3>주요 서비스 내용</h3>
      <ul>
        <li>부동산 강제경매</li>
        <li>동산 압류 및 매각</li>
        <li>채권 압류 및 추심</li>
        <li>가압류 및 가처분</li>
      </ul>
    `,
    laws: [
      '민사집행법',
      '민법',
      '채권자회생 및 파산에 관한 법률'
    ],
    costs: '비용은 <a href="/costs">비용 안내 페이지</a>를 참고하시기 바랍니다.'
  },
  {
    id: 'inheritance',
    title: '상속',
    content: `
      <h2>상속 서비스</h2>
      <p>상속은 피상속인의 재산상 권리와 의무를 상속인이 승계하는 제도입니다.</p>
      <h3>주요 서비스 내용</h3>
      <ul>
        <li>상속등기</li>
        <li>상속재산 분할</li>
        <li>상속포기 및 한정승인</li>
        <li>유언 검인</li>
      </ul>
    `,
    laws: [
      '민법',
      '상속세 및 증여세법',
      '가족관계의 등록 등에 관한 법률'
    ],
    costs: '비용은 <a href="/costs">비용 안내 페이지</a>를 참고하시기 바랍니다.'
  },
  {
    id: 'trust',
    title: '신탁',
    content: `
      <h2>신탁 서비스</h2>
      <p>신탁은 위탁자가 수탁자에게 재산을 이전하여 수탁자가 수익자를 위하여 재산을 관리·처분하는 제도입니다.</p>
      <h3>주요 서비스 내용</h3>
      <ul>
        <li>신탁 계약 작성</li>
        <li>신탁 재산 등기</li>
        <li>신탁 변경 및 해지</li>
        <li>신탁 관련 분쟁 해결</li>
      </ul>
    `,
    laws: [
      '신탁법',
      '민법',
      '부동산등기법'
    ],
    costs: '비용은 <a href="/costs">비용 안내 페이지</a>를 참고하시기 바랍니다.'
  }
];

export const initialBlogPosts = [
  {
    id: 'blog-1',
    title: '부동산 매매 시 주의사항',
    category: 'FAQ',
    content: `
      <h2>부동산 매매 시 주의사항</h2>
      <p>부동산 매매는 큰 금액이 관련된 중요한 거래입니다. 다음과 같은 사항들을 주의하시기 바랍니다.</p>
      <h3>1. 등기부등본 확인</h3>
      <p>매매 전 반드시 등기부등본을 확인하여 소유권, 저당권, 전세권 등의 권리관계를 파악해야 합니다.</p>
      <h3>2. 계약서 작성</h3>
      <p>계약서에는 매매가격, 계약금, 중도금, 잔금 지급일자 등을 명확히 기재해야 합니다.</p>
      <h3>3. 등기 이전</h3>
      <p>잔금 지급 후 즉시 소유권 이전등기를 진행하여 권리를 확정해야 합니다.</p>
    `,
    createdAt: new Date().toISOString(),
    deletedAt: null
  },
  {
    id: 'blog-2',
    title: '법인 설립 절차 안내',
    category: '사안정리',
    content: `
      <h2>법인 설립 절차 안내</h2>
      <p>법인을 설립하기 위해서는 다음과 같은 절차를 거쳐야 합니다.</p>
      <h3>1. 정관 작성</h3>
      <p>법인의 목적, 명칭, 본점 소재지, 자본금 등을 명시한 정관을 작성합니다.</p>
      <h3>2. 발기인 모집</h3>
      <p>주식회사의 경우 발기인을 모집하고 주식을 인수받습니다.</p>
      <h3>3. 설립등기</h3>
      <p>관할 법원에 설립등기를 신청하여 법인격을 취득합니다.</p>
    `,
    createdAt: new Date().toISOString(),
    deletedAt: null
  },
  {
    id: 'blog-3',
    title: '대법원 판례: 부동산 매매계약 해석',
    category: '판례',
    content: `
      <h2>대법원 판례: 부동산 매매계약 해석</h2>
      <p>대법원 2023. 1. 15. 선고 2022다12345 판결</p>
      <h3>사안</h3>
      <p>부동산 매매계약에서 매도인이 계약 해제를 주장한 사안</p>
      <h3>판결 요지</h3>
      <p>매매계약의 해석은 당사자의 의사표시의 진의를 명확히 파악하여야 하며, 계약서의 문언뿐만 아니라 거래의 전후 사정을 종합적으로 고려하여야 한다.</p>
    `,
    createdAt: new Date().toISOString(),
    deletedAt: null
  }
];




```

민사집행 서비스 내용을 요청하신 내용으로 교체했습니다.

**참고사항:**
- 이미 브라우저에 localStorage 데이터가 저장되어 있다면, 기존 데이터가 우선 표시될 수 있습니다.
- 새 내용을 보려면:
  1. 브라우저 개발자 도구(F12) → Application 탭 → Local Storage → 해당 사이트 → `lawyer_website_data` 삭제 후 새로고침
  2. 또는 관리자 페이지(`/admin/login`)에서 민사집행 서비스를 수정

새로고침 후 변경된 내용이 표시됩니다.

---

**User**

내장 브라우즈 안에서는 개발자도구가 열리지 않아.  이럴 경우 어떻게 하면 되지? 

---

**Cursor**


내장 브라우저에서는 개발자 도구 접근이 제한될 수 있습니다. 다음 방법을 사용하세요:

## 해결 방법

### 방법 1: 외부 브라우저 사용 (권장)
개발 서버가 실행 중이면:
1. 터미널에 표시된 URL 확인 (예: `http://localhost:5173`)
2. Chrome, Edge, Firefox 등 외부 브라우저에서 해당 URL 열기
3. F12로 개발자 도구 열기
4. Application 탭 → Local Storage → `lawyer_website_data` 삭제

### 방법 2: 코드로 localStorage 초기화 기능 추가
초기화 버튼을 추가하거나, 콘솔에서 실행할 수 있는 코드를 제공할 수 있습니다.

다음 코드를 `src/utils/storage.js`에 추가하세요:

```javascript
// localStorage 초기화 함수 추가
export const clearAllData = () => {
  try {
    localStorage.removeItem(STORAGE_KEY);
    return true;
  } catch (error) {
    console.error('데이터 초기화 실패:', error);
    return false;
  }
};
```

그리고 관리자 대시보드나 메인 페이지에 초기화 버튼을 추가할 수 있습니다.

### 방법 3: 관리자 페이지에서 수정
1. `/admin/login`으로 이동
2. 비밀번호 입력 후 로그인
3. `/admin/service/civil-execution`으로 이동
4. 내용을 직접 수정하여 저장

### 방법 4: 간단한 초기화 스크립트
브라우저 주소창에 다음을 입력해 실행:

```javascript
javascript:localStorage.removeItem('lawyer_website_data'); location.reload();
```

또는 콘솔에서:
```javascript
localStorage.removeItem('lawyer_website_data');
location.reload();
```

가장 간단한 방법은 방법 1(외부 브라우저 사용)입니다. 외부 브라우저를 사용할 수 있나요? 아니면 코드에 초기화 기능을 추가할까요?

```javascript
// localStorage 초기화 함수 추가
export const clearAllData = () => {
  try {
    localStorage.removeItem(STORAGE_KEY);
    return true;
  } catch (error) {
    console.error('데이터 초기화 실패:', error);
    return false;
  }
};
```

```javascript
javascript:localStorage.removeItem('lawyer_website_data'); location.reload();
```

```javascript
localStorage.removeItem('lawyer_website_data');
location.reload();
```

---

**User**

<h3>주요 서비스 내용</h3> 이 내용의 다음에 아래 내요을 넣어줘.



집행문 부여 등에 관한 이의신청



**1. 집행문 부여 거절처분에 대한 이의신청**



1.1. 의의

법원사무관등(민집 34조 1항)이나 공증인(민집 59조 2항)이 집행문 부여 신청을 거절한 경우 채권자는 그 거절처분에 대하여 이의신청을 할 수 있습니다. 재판장의 명령에 불복하는 인도 등 공증서에 대한 법원단독판사의 집행문 부여 불허가 결정에 대해서도 공증인 처분에 대한 이의로 다투어야 합니다.



1.2. 신청과 절차

이 이의신청은 민사집행의 신청이 아니므로 민사집행법 4조의 규정이 적용되지 않으며, 서면 또는 말로 할 수 있습니다(민집 23조 1항, 민사 161조 1항). 이의사유는 집행문 부여 신청의 흠결 등입니다. 관할은 법원사무관등의 처분은 소속 법원, 공증인의 처분은 사무소 소재지 관할 지방법원 단독판사입니다(민집 34조 1항, 59조 2항). 신청 시 1,000원의 인지를 붙여야 하며, 신청사건으로 접수됩니다(재민 91-1).



1.3. 심리와 재판

법원은 임의적 변론을 거쳐 결정으로 재판합니다. 이의신청에 정당한 이유가 있다고 인정되면 집행문 부여기관에 집행문 부여를 명하며, 이 결정이 있으면 집행문 부여기관은 당연히 집행문을 내어주어야 합니다. 재판이 확정되면 채권자는 다시 집행문 부여를 신청할 수 있습니다.



1.4. 불복방법

이의신청에 대한 재판의 불복방법은 통상항고입니다(민집 34조 1항). 그러나 판례는 이의신청에 대한 재판은 통상항고가 아닌 특별항고만 가능하다고 보거나(대법 1995. 5. 13. 94마2132, 대법 1997. 6. 20. 97마250, 대법 2017. 12. 28. 2017그100), 통상항고를 허용하는 경우도 있습니다(대법 2016. 6. 21. 2016마5082). 집행문 부여 거절처분 인용 결정에 대한 채무자의 불복은 특별항고가 가능합니다(대법 2015. 8. 6. 2015그288).



**2. 집행문 부여에 대한 이의신청**



2.1. 의의

집행문 부여에 대한 이의신청은 집행문 부여가 부적법함을 주장하여 그 취소 등의 시정을 구하는 채무자의 신청을 말합니다(민집 34조 1항, 59조 2항). 재판장의 명령에 의한 법원사무관등의 처분이나 공증인의 처분이 그 대상이며, 특히 공증서에 대한 법원단독판사의 허가 후 집행문이 부여된 경우에도 이의신청이 가능합니다(대법 2015. 8. 6. 2015그288 참조).



2.2. 이의사유

이의사유는 집행문 부여기관이 조사하여야 할 모든 요건의 흠결을 포함합니다. 집행권원의 형식적 흠결, 조건 불성취, 당사자 승계의 부존재 등도 이의사유에 해당합니다(민집 45조 단서). 간접강제결정상 의무이행 기간이 경과하여 효력이 상실된 경우, 그에 따른 집행문 취소도 이의신청으로 구할 수 있습니다(대법 2017. 4. 7. 2013다80627). 이의사유의 존부에 관한 판단 기준시는 이의를 판단하는 시점입니다.



2.3. 신청절차

2.3.1. 관할

집행문 부여를 한 법원사무관등이 속한 법원입니다(민집 34조 1항). 제1심 법원일 때도 있고 상급법원일 때도 있습니다(민집 28조 2항). 공증인이 작성한 집행증서의 경우, 공증인 사무소가 있는 곳을 관할하는 지방법원 단독판사가 관할합니다(민집 59조 2항).



2.3.2. 이의신청 시기

채무자는 집행문이 부여된 후 언제든지 이의신청을 할 수 있으며, 현실적으로 집행이 개시되기 전까지 가능합니다. 그러나 집행문이 부여된 집행권원의 정본에 의한 집행이 완료된 후에는 이의 이익이 없어 이의신청을 할 수 없습니다.



2.3.3. 신청과 접수

이의신청은 서면이나 말로 할 수 있으며(민사 161조 2항, 3항), 신청서에는 1,000원의 인지를 붙여야 하고, 신청이 제출되면 신청사건으로 접수됩니다(재민 91-1).



2.4. 심리와 재판

법원은 임의적 변론을 거쳐 결정의 형식으로 재판합니다. 법원이 이의사유가 정당하다고 인정할 때에는 집행문 부여 자체를 취소하고 그 집행권원의 정본에 기한 강제집행을 불허하는 재판을 합니다. 이 인용 결정은 민사집행법 49조 1호의 서류에 해당하므로, 채무자는 이 인용 결정을 집행기관에 제출하여 강제집행의 취소를 구할 수 있습니다(민집 49조 1호, 50조 1항).



2.5. 불복방법

집행문 부여에 대한 이의신청에 대한 재판(인용 또는 기각의 결정)에 대한 불복방법은 통상항고입니다(민집 34조 1항). 그러나 판례는 이의신청에 대한 재판은 통상항고가 아닌 특별항고만 가능하다고 보거나(대법 1995. 5. 13. 94마2132, 대법 1997. 6. 20. 97마250), 경우에 따라 통상항고를 허용한다고 보기도 합니다(대법 2016. 6. 21. 2016마5082).

---

**Cursor**


`<h3>주요 서비스 내용</h3>` 다음에 추가할 위치를 확인 중입니다.



`src/data/initialData.js` 파일의 민사집행 서비스 부분을 다음과 같이 수정하세요:

**수정할 위치**: 94-100줄의 `<h3>주요 서비스 내용</h3>` 섹션 다음에 새 내용을 추가하세요.

```javascript
      <h3>주요 서비스 내용</h3>
      <ul>
        <li>부동산 강제경매</li>
        <li>동산 압류 및 매각</li>
        <li>채권 압류 및 추심</li>
        <li>가압류 및 가처분</li>
      </ul>
      
      <h3>집행문 부여 등에 관한 이의신청</h3>
      
      <h4>1. 집행문 부여 거절처분에 대한 이의신청</h4>
      
      <h4>1.1. 의의</h4>
      <p>법원사무관등(민집 34조 1항)이나 공증인(민집 59조 2항)이 집행문 부여 신청을 거절한 경우 채권자는 그 거절처분에 대하여 이의신청을 할 수 있습니다. 재판장의 명령에 불복하는 인도 등 공증서에 대한 법원단독판사의 집행문 부여 불허가 결정에 대해서도 공증인 처분에 대한 이의로 다투어야 합니다.</p>
      
      <h4>1.2. 신청과 절차</h4>
      <p>이 이의신청은 민사집행의 신청이 아니므로 민사집행법 4조의 규정이 적용되지 않으며, 서면 또는 말로 할 수 있습니다(민집 23조 1항, 민사 161조 1항). 이의사유는 집행문 부여 신청의 흠결 등입니다. 관할은 법원사무관등의 처분은 소속 법원, 공증인의 처분은 사무소 소재지 관할 지방법원 단독판사입니다(민집 34조 1항, 59조 2항). 신청 시 1,000원의 인지를 붙여야 하며, 신청사건으로 접수됩니다(재민 91-1).</p>
      
      <h4>1.3. 심리와 재판</h4>
      <p>법원은 임의적 변론을 거쳐 결정으로 재판합니다. 이의신청에 정당한 이유가 있다고 인정되면 집행문 부여기관에 집행문 부여를 명하며, 이 결정이 있으면 집행문 부여기관은 당연히 집행문을 내어주어야 합니다. 재판이 확정되면 채권자는 다시 집행문 부여를 신청할 수 있습니다.</p>
      
      <h4>1.4. 불복방법</h4>
      <p>이의신청에 대한 재판의 불복방법은 통상항고입니다(민집 34조 1항). 그러나 판례는 이의신청에 대한 재판은 통상항고가 아닌 특별항고만 가능하다고 보거나(대법 1995. 5. 13. 94마2132, 대법 1997. 6. 20. 97마250, 대법 2017. 12. 28. 2017그100), 통상항고를 허용하는 경우도 있습니다(대법 2016. 6. 21. 2016마5082). 집행문 부여 거절처분 인용 결정에 대한 채무자의 불복은 특별항고가 가능합니다(대법 2015. 8. 6. 2015그288).</p>
      
      <h4>2. 집행문 부여에 대한 이의신청</h4>
      
      <h4>2.1. 의의</h4>
      <p>집행문 부여에 대한 이의신청은 집행문 부여가 부적법함을 주장하여 그 취소 등의 시정을 구하는 채무자의 신청을 말합니다(민집 34조 1항, 59조 2항). 재판장의 명령에 의한 법원사무관등의 처분이나 공증인의 처분이 그 대상이며, 특히 공증서에 대한 법원단독판사의 허가 후 집행문이 부여된 경우에도 이의신청이 가능합니다(대법 2015. 8. 6. 2015그288 참조).</p>
      
      <h4>2.2. 이의사유</h4>
      <p>이의사유는 집행문 부여기관이 조사하여야 할 모든 요건의 흠결을 포함합니다. 집행권원의 형식적 흠결, 조건 불성취, 당사자 승계의 부존재 등도 이의사유에 해당합니다(민집 45조 단서). 간접강제결정상 의무이행 기간이 경과하여 효력이 상실된 경우, 그에 따른 집행문 취소도 이의신청으로 구할 수 있습니다(대법 2017. 4. 7. 2013다80627). 이의사유의 존부에 관한 판단 기준시는 이의를 판단하는 시점입니다.</p>
      
      <h4>2.3. 신청절차</h4>
      
      <h4>2.3.1. 관할</h4>
      <p>집행문 부여를 한 법원사무관등이 속한 법원입니다(민집 34조 1항). 제1심 법원일 때도 있고 상급법원일 때도 있습니다(민집 28조 2항). 공증인이 작성한 집행증서의 경우, 공증인 사무소가 있는 곳을 관할하는 지방법원 단독판사가 관할합니다(민집 59조 2항).</p>
      
      <h4>2.3.2. 이의신청 시기</h4>
      <p>채무자는 집행문이 부여된 후 언제든지 이의신청을 할 수 있으며, 현실적으로 집행이 개시되기 전까지 가능합니다. 그러나 집행문이 부여된 집행권원의 정본에 의한 집행이 완료된 후에는 이의 이익이 없어 이의신청을 할 수 없습니다.</p>
      
      <h4>2.3.3. 신청과 접수</h4>
      <p>이의신청은 서면이나 말로 할 수 있으며(민사 161조 2항, 3항), 신청서에는 1,000원의 인지를 붙여야 하고, 신청이 제출되면 신청사건으로 접수됩니다(재민 91-1).</p>
      
      <h4>2.4. 심리와 재판</h4>
      <p>법원은 임의적 변론을 거쳐 결정의 형식으로 재판합니다. 법원이 이의사유가 정당하다고 인정할 때에는 집행문 부여 자체를 취소하고 그 집행권원의 정본에 기한 강제집행을 불허하는 재판을 합니다. 이 인용 결정은 민사집행법 49조 1호의 서류에 해당하므로, 채무자는 이 인용 결정을 집행기관에 제출하여 강제집행의 취소를 구할 수 있습니다(민집 49조 1호, 50조 1항).</p>
      
      <h4>2.5. 불복방법</h4>
      <p>집행문 부여에 대한 이의신청에 대한 재판(인용 또는 기각의 결정)에 대한 불복방법은 통상항고입니다(민집 34조 1항). 그러나 판례는 이의신청에 대한 재판은 통상항고가 아닌 특별항고만 가능하다고 보거나(대법 1995. 5. 13. 94마2132, 대법 1997. 6. 20. 97마250), 경우에 따라 통상항고를 허용한다고 보기도 합니다(대법 2016. 6. 21. 2016마5082).</p>
    `,
```

**참고사항:**
- 현재 ask mode라 직접 수정할 수 없습니다. 위 코드를 복사해 `src/data/initialData.js`의 94-100줄을 교체하세요.
- 또는 agent mode로 전환하면 자동으로 수정하겠습니다.

수정 후 브라우저를 새로고침하면 변경 사항이 반영됩니다. localStorage에 기존 데이터가 있으면 관리자 페이지에서 수정하거나 외부 브라우저에서 localStorage를 삭제하세요.

```javascript
      <h3>주요 서비스 내용</h3>
      <ul>
        <li>부동산 강제경매</li>
        <li>동산 압류 및 매각</li>
        <li>채권 압류 및 추심</li>
        <li>가압류 및 가처분</li>
      </ul>
      
      <h3>집행문 부여 등에 관한 이의신청</h3>
      
      <h4>1. 집행문 부여 거절처분에 대한 이의신청</h4>
      
      <h4>1.1. 의의</h4>
      <p>법원사무관등(민집 34조 1항)이나 공증인(민집 59조 2항)이 집행문 부여 신청을 거절한 경우 채권자는 그 거절처분에 대하여 이의신청을 할 수 있습니다. 재판장의 명령에 불복하는 인도 등 공증서에 대한 법원단독판사의 집행문 부여 불허가 결정에 대해서도 공증인 처분에 대한 이의로 다투어야 합니다.</p>
      
      <h4>1.2. 신청과 절차</h4>
      <p>이 이의신청은 민사집행의 신청이 아니므로 민사집행법 4조의 규정이 적용되지 않으며, 서면 또는 말로 할 수 있습니다(민집 23조 1항, 민사 161조 1항). 이의사유는 집행문 부여 신청의 흠결 등입니다. 관할은 법원사무관등의 처분은 소속 법원, 공증인의 처분은 사무소 소재지 관할 지방법원 단독판사입니다(민집 34조 1항, 59조 2항). 신청 시 1,000원의 인지를 붙여야 하며, 신청사건으로 접수됩니다(재민 91-1).</p>
      
      <h4>1.3. 심리와 재판</h4>
      <p>법원은 임의적 변론을 거쳐 결정으로 재판합니다. 이의신청에 정당한 이유가 있다고 인정되면 집행문 부여기관에 집행문 부여를 명하며, 이 결정이 있으면 집행문 부여기관은 당연히 집행문을 내어주어야 합니다. 재판이 확정되면 채권자는 다시 집행문 부여를 신청할 수 있습니다.</p>
      
      <h4>1.4. 불복방법</h4>
      <p>이의신청에 대한 재판의 불복방법은 통상항고입니다(민집 34조 1항). 그러나 판례는 이의신청에 대한 재판은 통상항고가 아닌 특별항고만 가능하다고 보거나(대법 1995. 5. 13. 94마2132, 대법 1997. 6. 20. 97마250, 대법 2017. 12. 28. 2017그100), 통상항고를 허용하는 경우도 있습니다(대법 2016. 6. 21. 2016마5082). 집행문 부여 거절처분 인용 결정에 대한 채무자의 불복은 특별항고가 가능합니다(대법 2015. 8. 6. 2015그288).</p>
      
      <h4>2. 집행문 부여에 대한 이의신청</h4>
      
      <h4>2.1. 의의</h4>
      <p>집행문 부여에 대한 이의신청은 집행문 부여가 부적법함을 주장하여 그 취소 등의 시정을 구하는 채무자의 신청을 말합니다(민집 34조 1항, 59조 2항). 재판장의 명령에 의한 법원사무관등의 처분이나 공증인의 처분이 그 대상이며, 특히 공증서에 대한 법원단독판사의 허가 후 집행문이 부여된 경우에도 이의신청이 가능합니다(대법 2015. 8. 6. 2015그288 참조).</p>
      
      <h4>2.2. 이의사유</h4>
      <p>이의사유는 집행문 부여기관이 조사하여야 할 모든 요건의 흠결을 포함합니다. 집행권원의 형식적 흠결, 조건 불성취, 당사자 승계의 부존재 등도 이의사유에 해당합니다(민집 45조 단서). 간접강제결정상 의무이행 기간이 경과하여 효력이 상실된 경우, 그에 따른 집행문 취소도 이의신청으로 구할 수 있습니다(대법 2017. 4. 7. 2013다80627). 이의사유의 존부에 관한 판단 기준시는 이의를 판단하는 시점입니다.</p>
      
      <h4>2.3. 신청절차</h4>
      
      <h4>2.3.1. 관할</h4>
      <p>집행문 부여를 한 법원사무관등이 속한 법원입니다(민집 34조 1항). 제1심 법원일 때도 있고 상급법원일 때도 있습니다(민집 28조 2항). 공증인이 작성한 집행증서의 경우, 공증인 사무소가 있는 곳을 관할하는 지방법원 단독판사가 관할합니다(민집 59조 2항).</p>
      
      <h4>2.3.2. 이의신청 시기</h4>
      <p>채무자는 집행문이 부여된 후 언제든지 이의신청을 할 수 있으며, 현실적으로 집행이 개시되기 전까지 가능합니다. 그러나 집행문이 부여된 집행권원의 정본에 의한 집행이 완료된 후에는 이의 이익이 없어 이의신청을 할 수 없습니다.</p>
      
      <h4>2.3.3. 신청과 접수</h4>
      <p>이의신청은 서면이나 말로 할 수 있으며(민사 161조 2항, 3항), 신청서에는 1,000원의 인지를 붙여야 하고, 신청이 제출되면 신청사건으로 접수됩니다(재민 91-1).</p>
      
      <h4>2.4. 심리와 재판</h4>
      <p>법원은 임의적 변론을 거쳐 결정의 형식으로 재판합니다. 법원이 이의사유가 정당하다고 인정할 때에는 집행문 부여 자체를 취소하고 그 집행권원의 정본에 기한 강제집행을 불허하는 재판을 합니다. 이 인용 결정은 민사집행법 49조 1호의 서류에 해당하므로, 채무자는 이 인용 결정을 집행기관에 제출하여 강제집행의 취소를 구할 수 있습니다(민집 49조 1호, 50조 1항).</p>
      
      <h4>2.5. 불복방법</h4>
      <p>집행문 부여에 대한 이의신청에 대한 재판(인용 또는 기각의 결정)에 대한 불복방법은 통상항고입니다(민집 34조 1항). 그러나 판례는 이의신청에 대한 재판은 통상항고가 아닌 특별항고만 가능하다고 보거나(대법 1995. 5. 13. 94마2132, 대법 1997. 6. 20. 97마250), 경우에 따라 통상항고를 허용한다고 보기도 합니다(대법 2016. 6. 21. 2016마5082).</p>
    `,
```

---

**User**

agent mode로 변경하였으니 수정해줘

---

**Cursor**


`src/data/initialData.js`의 민사집행 서비스 부분에 내용을 추가 중입니다.



민사집행 서비스 내용에 새로운 섹션 추가 중입니다.


```javascript
// 초기 데이터 구조 및 샘플 데이터

export const initialServices = [
  {
    id: 'real-estate',
    title: '부동산등기',
    content: `
      <h2>부동산등기 서비스</h2>
      <p>부동산등기는 부동산의 권리관계를 명확히 하고 거래의 안전을 보장하기 위한 중요한 제도입니다.</p>
      <h3>주요 서비스 내용</h3>
      <ul>
        <li>소유권 이전등기</li>
        <li>저당권 설정등기</li>
        <li>전세권 설정등기</li>
        <li>지상권 설정등기</li>
      </ul>
    `,
    laws: [
      '부동산등기법',
      '민법',
      '부동산 실권리자명의 등기에 관한 법률'
    ],
    costs: '비용은 <a href="/costs">비용 안내 페이지</a>를 참고하시기 바랍니다.'
  },
  {
    id: 'corporate-registration',
    title: '법인등기',
    content: `
      <h2>법인등기 서비스</h2>
      <p>법인등기는 법인의 설립, 변경, 해산 등 법인의 중요한 사항을 공시하는 제도입니다.</p>
      <h3>주요 서비스 내용</h3>
      <ul>
        <li>법인 설립등기</li>
        <li>법인 변경등기</li>
        <li>법인 해산등기</li>
        <li>법인 청산등기</li>
      </ul>
    `,
    laws: [
      '상법',
      '법인세법',
      '부가가치세법'
    ],
    costs: '비용은 <a href="/costs">비용 안내 페이지</a>를 참고하시기 바랍니다.'
  },
  {
    id: 'civil-litigation',
    title: '민사소송',
    content: `
      <h2>민사소송 서비스</h2>
      <p>민사소송은 개인 간의 권리관계에 관한 분쟁을 법원을 통해 해결하는 절차입니다.</p>
      <h3>주요 서비스 내용</h3>
      <ul>
        <li>소장 작성 및 제출</li>
        <li>변론 준비 및 대리</li>
        <li>화해 및 조정</li>
        <li>항소 및 상고</li>
      </ul>
    `,
    laws: [
      '민사소송법',
      '민법',
      '소송촉진 등에 관한 특례법'
    ],
    costs: '비용은 <a href="/costs">비용 안내 페이지</a>를 참고하시기 바랍니다.'
  },
  {
    id: 'civil-execution',
    title: '민사집행',
    content: `
      <h2>민사집행 서비스</h2>
      <p>강제집행을 개시하기 위해서는 <strong>집행당사자, 집행권원, 집행문</strong>이라는 세 가지 핵심 요건이 충족되어야 합니다.</p>
      
      <h3>1. 집행당사자 (민사집행법 제3조)</h3>
      <p>강제집행 절차의 당사자는 집행을 구하는 <strong>집행채권자</strong>와 집행을 받는 <strong>집행채무자</strong>입니다. 이들은 원칙적으로 판결에 표시된 원고와 피고이지만, 강제집행 절차에서 누가 집행채권자이고 집행채무자인지는 <strong>집행문</strong>에 기재된 사람에 의해 확정됩니다.</p>
      <p>집행당사자의 <strong>적격</strong>은 강제집행을 진행할 정당한 자격을 의미하며, 이는 <strong>승계</strong>에 의해 변동될 수 있습니다. 예를 들어, 판결 확정 후 채권자 또는 채무자가 사망하여 상속이 발생하거나 채권 양도가 이루어진 경우, 상속인이나 채권 양수인이 새로운 집행당사자가 됩니다(민사집행법 제31조 제1항, 대법원 2010. 1. 14. 2009그196 참조).</p>
      
      <h3>2. 집행권원 (민사집행법 제2조)</h3>
      <p><strong>집행권원</strong>은 사법상 청구권의 존재와 범위가 확정되어 강제집행을 할 수 있는 <strong>국가 공권력의 근거</strong>가 되는 공정증서입니다. 주요 집행권원의 종류는 다음과 같습니다.</p>
      <ul>
        <li><strong>확정판결 및 가집행 선고부 판결</strong>: 민사소송법상 확정된 판결은 물론, 아직 확정되지 않았어도 가집행이 선고된 판결도 집행권원이 됩니다(민사집행법 제213조 제1항).</li>
        <li><strong>화해조서, 조정조서, 확정된 지급명령 등</strong>: 소송상 화해나 조정 내용이 담긴 조서 및 법원의 확정된 지급명령도 확정판결과 동일한 효력을 가지므로 집행권원이 됩니다(민사집행법 제57조, 제58조 제3항).</li>
        <li><strong>공정증서</strong>: 공증인이 일정한 금액의 지급이나 대체물 인도를 목적으로 작성한 공정증서도 집행권원입니다(공증인법 제56조 제2항).</li>
        <li><strong>확정된 화해권고결정</strong>: 소액사건심판법에 따른 화해권고결정 중 확정된 것 또한 집행권원이 됩니다(소액사건심판법 제5조의7 제1항).</li>
      </ul>
      <p>집행권원은 <strong>급부의무의 내용이 명확</strong>해야 하며, 그 내용이 <strong>이행 가능하고 적법</strong>해야 합니다.</p>
      
      <h3>3. 집행문 (민사집행법 제28조)</h3>
      <p><strong>집행문</strong>은 집행권원에 강제집행력이 있다는 사실을 공적으로 증명하기 위해 법원사무관등이 집행권원 정본의 끝에 덧붙여 부여하는 문언입니다. 원칙적으로 강제집행 개시를 위해서는 집행권원 정본에 집행문이 부여되어야 합니다.</p>
      <p>그러나 <strong>예외적으로 집행문 부여가 필요 없는 경우</strong>도 있습니다. 예를 들어, 확정된 지급명령에 의한 집행, 가압류·가처분명령에 의한 집행, 또는 화해조서나 조정조서에 의한 집행 등은 집행문 없이도 강제집행이 가능합니다(민사집행법 제58조 제1항 본문, 제291조, 제301조).</p>
      <p>집행문은 통상적인 경우의 <strong>통상집행문</strong> 외에, 당사자의 승계가 있는 경우의 <strong>승계집행문</strong>, 그리고 조건이 붙은 경우의 <strong>조건부집행문</strong> 등으로 나뉩니다(민사집행법 제30조 제2항, 제31조 제1항).</p>
      <p>이러한 강제집행의 요건들은 모두 강제집행 절차의 적법성과 유효성을 담보하는 중요한 요소이므로, 각 요건의 충족 여부를 면밀히 검토해야 합니다.</p>
      
      <h3>주요 서비스 내용</h3>
      <ul>
        <li>부동산 강제경매</li>
        <li>동산 압류 및 매각</li>
        <li>채권 압류 및 추심</li>
        <li>가압류 및 가처분</li>
      </ul>
      
      <h3>집행문 부여 등에 관한 이의신청</h3>
      
      <h4>1. 집행문 부여 거절처분에 대한 이의신청</h4>
      
      <h4>1.1. 의의</h4>
      <p>법원사무관등(민집 34조 1항)이나 공증인(민집 59조 2항)이 집행문 부여 신청을 거절한 경우 채권자는 그 거절처분에 대하여 이의신청을 할 수 있습니다. 재판장의 명령에 불복하는 인도 등 공증서에 대한 법원단독판사의 집행문 부여 불허가 결정에 대해서도 공증인 처분에 대한 이의로 다투어야 합니다.</p>
      
      <h4>1.2. 신청과 절차</h4>
      <p>이 이의신청은 민사집행의 신청이 아니므로 민사집행법 4조의 규정이 적용되지 않으며, 서면 또는 말로 할 수 있습니다(민집 23조 1항, 민사 161조 1항). 이의사유는 집행문 부여 신청의 흠결 등입니다. 관할은 법원사무관등의 처분은 소속 법원, 공증인의 처분은 사무소 소재지 관할 지방법원 단독판사입니다(민집 34조 1항, 59조 2항). 신청 시 1,000원의 인지를 붙여야 하며, 신청사건으로 접수됩니다(재민 91-1).</p>
      
      <h4>1.3. 심리와 재판</h4>
      <p>법원은 임의적 변론을 거쳐 결정으로 재판합니다. 이의신청에 정당한 이유가 있다고 인정되면 집행문 부여기관에 집행문 부여를 명하며, 이 결정이 있으면 집행문 부여기관은 당연히 집행문을 내어주어야 합니다. 재판이 확정되면 채권자는 다시 집행문 부여를 신청할 수 있습니다.</p>
      
      <h4>1.4. 불복방법</h4>
      <p>이의신청에 대한 재판의 불복방법은 통상항고입니다(민집 34조 1항). 그러나 판례는 이의신청에 대한 재판은 통상항고가 아닌 특별항고만 가능하다고 보거나(대법 1995. 5. 13. 94마2132, 대법 1997. 6. 20. 97마250, 대법 2017. 12. 28. 2017그100), 통상항고를 허용하는 경우도 있습니다(대법 2016. 6. 21. 2016마5082). 집행문 부여 거절처분 인용 결정에 대한 채무자의 불복은 특별항고가 가능합니다(대법 2015. 8. 6. 2015그288).</p>
      
      <h4>2. 집행문 부여에 대한 이의신청</h4>
      
      <h4>2.1. 의의</h4>
      <p>집행문 부여에 대한 이의신청은 집행문 부여가 부적법함을 주장하여 그 취소 등의 시정을 구하는 채무자의 신청을 말합니다(민집 34조 1항, 59조 2항). 재판장의 명령에 의한 법원사무관등의 처분이나 공증인의 처분이 그 대상이며, 특히 공증서에 대한 법원단독판사의 허가 후 집행문이 부여된 경우에도 이의신청이 가능합니다(대법 2015. 8. 6. 2015그288 참조).</p>
      
      <h4>2.2. 이의사유</h4>
      <p>이의사유는 집행문 부여기관이 조사하여야 할 모든 요건의 흠결을 포함합니다. 집행권원의 형식적 흠결, 조건 불성취, 당사자 승계의 부존재 등도 이의사유에 해당합니다(민집 45조 단서). 간접강제결정상 의무이행 기간이 경과하여 효력이 상실된 경우, 그에 따른 집행문 취소도 이의신청으로 구할 수 있습니다(대법 2017. 4. 7. 2013다80627). 이의사유의 존부에 관한 판단 기준시는 이의를 판단하는 시점입니다.</p>
      
      <h4>2.3. 신청절차</h4>
      
      <h4>2.3.1. 관할</h4>
      <p>집행문 부여를 한 법원사무관등이 속한 법원입니다(민집 34조 1항). 제1심 법원일 때도 있고 상급법원일 때도 있습니다(민집 28조 2항). 공증인이 작성한 집행증서의 경우, 공증인 사무소가 있는 곳을 관할하는 지방법원 단독판사가 관할합니다(민집 59조 2항).</p>
      
      <h4>2.3.2. 이의신청 시기</h4>
      <p>채무자는 집행문이 부여된 후 언제든지 이의신청을 할 수 있으며, 현실적으로 집행이 개시되기 전까지 가능합니다. 그러나 집행문이 부여된 집행권원의 정본에 의한 집행이 완료된 후에는 이의 이익이 없어 이의신청을 할 수 없습니다.</p>
      
      <h4>2.3.3. 신청과 접수</h4>
      <p>이의신청은 서면이나 말로 할 수 있으며(민사 161조 2항, 3항), 신청서에는 1,000원의 인지를 붙여야 하고, 신청이 제출되면 신청사건으로 접수됩니다(재민 91-1).</p>
      
      <h4>2.4. 심리와 재판</h4>
      <p>법원은 임의적 변론을 거쳐 결정의 형식으로 재판합니다. 법원이 이의사유가 정당하다고 인정할 때에는 집행문 부여 자체를 취소하고 그 집행권원의 정본에 기한 강제집행을 불허하는 재판을 합니다. 이 인용 결정은 민사집행법 49조 1호의 서류에 해당하므로, 채무자는 이 인용 결정을 집행기관에 제출하여 강제집행의 취소를 구할 수 있습니다(민집 49조 1호, 50조 1항).</p>
      
      <h4>2.5. 불복방법</h4>
      <p>집행문 부여에 대한 이의신청에 대한 재판(인용 또는 기각의 결정)에 대한 불복방법은 통상항고입니다(민집 34조 1항). 그러나 판례는 이의신청에 대한 재판은 통상항고가 아닌 특별항고만 가능하다고 보거나(대법 1995. 5. 13. 94마2132, 대법 1997. 6. 20. 97마250), 경우에 따라 통상항고를 허용한다고 보기도 합니다(대법 2016. 6. 21. 2016마5082).</p>
    `,
    laws: [
      '민사집행법',
      '민법',
      '채권자회생 및 파산에 관한 법률'
    ],
    costs: '비용은 <a href="/costs">비용 안내 페이지</a>를 참고하시기 바랍니다.'
  },
  {
    id: 'inheritance',
    title: '상속',
    content: `
      <h2>상속 서비스</h2>
      <p>상속은 피상속인의 재산상 권리와 의무를 상속인이 승계하는 제도입니다.</p>
      <h3>주요 서비스 내용</h3>
      <ul>
        <li>상속등기</li>
        <li>상속재산 분할</li>
        <li>상속포기 및 한정승인</li>
        <li>유언 검인</li>
      </ul>
    `,
    laws: [
      '민법',
      '상속세 및 증여세법',
      '가족관계의 등록 등에 관한 법률'
    ],
    costs: '비용은 <a href="/costs">비용 안내 페이지</a>를 참고하시기 바랍니다.'
  },
  {
    id: 'trust',
    title: '신탁',
    content: `
      <h2>신탁 서비스</h2>
      <p>신탁은 위탁자가 수탁자에게 재산을 이전하여 수탁자가 수익자를 위하여 재산을 관리·처분하는 제도입니다.</p>
      <h3>주요 서비스 내용</h3>
      <ul>
        <li>신탁 계약 작성</li>
        <li>신탁 재산 등기</li>
        <li>신탁 변경 및 해지</li>
        <li>신탁 관련 분쟁 해결</li>
      </ul>
    `,
    laws: [
      '신탁법',
      '민법',
      '부동산등기법'
    ],
    costs: '비용은 <a href="/costs">비용 안내 페이지</a>를 참고하시기 바랍니다.'
  }
];

export const initialBlogPosts = [
  {
    id: 'blog-1',
    title: '부동산 매매 시 주의사항',
    category: 'FAQ',
    content: `
      <h2>부동산 매매 시 주의사항</h2>
      <p>부동산 매매는 큰 금액이 관련된 중요한 거래입니다. 다음과 같은 사항들을 주의하시기 바랍니다.</p>
      <h3>1. 등기부등본 확인</h3>
      <p>매매 전 반드시 등기부등본을 확인하여 소유권, 저당권, 전세권 등의 권리관계를 파악해야 합니다.</p>
      <h3>2. 계약서 작성</h3>
      <p>계약서에는 매매가격, 계약금, 중도금, 잔금 지급일자 등을 명확히 기재해야 합니다.</p>
      <h3>3. 등기 이전</h3>
      <p>잔금 지급 후 즉시 소유권 이전등기를 진행하여 권리를 확정해야 합니다.</p>
    `,
    createdAt: new Date().toISOString(),
    deletedAt: null
  },
  {
    id: 'blog-2',
    title: '법인 설립 절차 안내',
    category: '사안정리',
    content: `
      <h2>법인 설립 절차 안내</h2>
      <p>법인을 설립하기 위해서는 다음과 같은 절차를 거쳐야 합니다.</p>
      <h3>1. 정관 작성</h3>
      <p>법인의 목적, 명칭, 본점 소재지, 자본금 등을 명시한 정관을 작성합니다.</p>
      <h3>2. 발기인 모집</h3>
      <p>주식회사의 경우 발기인을 모집하고 주식을 인수받습니다.</p>
      <h3>3. 설립등기</h3>
      <p>관할 법원에 설립등기를 신청하여 법인격을 취득합니다.</p>
    `,
    createdAt: new Date().toISOString(),
    deletedAt: null
  },
  {
    id: 'blog-3',
    title: '대법원 판례: 부동산 매매계약 해석',
    category: '판례',
    content: `
      <h2>대법원 판례: 부동산 매매계약 해석</h2>
      <p>대법원 2023. 1. 15. 선고 2022다12345 판결</p>
      <h3>사안</h3>
      <p>부동산 매매계약에서 매도인이 계약 해제를 주장한 사안</p>
      <h3>판결 요지</h3>
      <p>매매계약의 해석은 당사자의 의사표시의 진의를 명확히 파악하여야 하며, 계약서의 문언뿐만 아니라 거래의 전후 사정을 종합적으로 고려하여야 한다.</p>
    `,
    createdAt: new Date().toISOString(),
    deletedAt: null
  }
];




```


수정 완료. 린터 오류 확인 중입니다.



수정 완료. 민사집행 서비스 페이지의 `<h3>주요 서비스 내용</h3>` 다음에 "집행문 부여 등에 관한 이의신청" 섹션을 추가했습니다.

**추가된 내용:**
- 1. 집행문 부여 거절처분에 대한 이의신청 (의의, 신청과 절차, 심리와 재판, 불복방법)
- 2. 집행문 부여에 대한 이의신청 (의의, 이의사유, 신청절차, 심리와 재판, 불복방법)

**참고사항:**
- 이미 localStorage에 기존 데이터가 저장되어 있다면, 관리자 페이지(`/admin/login`)에서 민사집행 서비스를 수정하거나 브라우저의 localStorage를 삭제해야 새 내용이 반영됩니다.
- 브라우저를 새로고침하면 변경 사항이 표시됩니다.

변경 사항이 반영되었는지 확인해 주세요.

