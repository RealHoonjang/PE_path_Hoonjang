# 🚀 배포 가이드

## 배포 옵션 비교

### 1. GitHub Pages (권장) ⭐
**장점:**
- ✅ 기존 HTML/CSS/JavaScript 디자인 **완벽하게 유지**
- ✅ 무료 호스팅
- ✅ 커스텀 도메인 지원
- ✅ CDN을 통한 빠른 로딩
- ✅ 설정이 매우 간단

**단점:**
- ❌ 정적 사이트만 가능 (서버 사이드 로직 불가)

### 2. Streamlit Cloud
**장점:**
- ✅ Python 백엔드 로직 사용 가능
- ✅ 무료 호스팅

**단점:**
- ❌ 기존 디자인을 완전히 재현하기 어려움
- ❌ Streamlit의 기본 UI 컴포넌트 사용 필요
- ❌ 커스텀 HTML/CSS 적용이 제한적

### 3. Netlify / Vercel
**장점:**
- ✅ 기존 디자인 완벽 유지
- ✅ 무료 호스팅
- ✅ 자동 배포 (Git 연동)
- ✅ 빠른 CDN

**단점:**
- ❌ 정적 사이트만 가능

---

## GitHub Pages 배포 방법 (권장)

### 1단계: GitHub 저장소 생성

1. GitHub에 로그인
2. 새 저장소 생성 (예: `go_on_to_school2`)
3. 저장소를 Public으로 설정 (무료 계정의 경우)

### 2단계: 프로젝트 업로드

```bash
# Git 초기화 (아직 안 했다면)
git init

# 모든 파일 추가
git add .

# 첫 커밋
git commit -m "Initial commit: 체육 진로 진학 프로그램"

# GitHub 저장소 연결 (YOUR_USERNAME과 YOUR_REPO_NAME을 실제 값으로 변경)
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git

# 메인 브랜치로 푸시
git branch -M main
git push -u origin main
```

### 3단계: GitHub Pages 활성화

1. GitHub 저장소 페이지로 이동
2. **Settings** 탭 클릭
3. 왼쪽 메뉴에서 **Pages** 클릭
4. **Source**에서 **Deploy from a branch** 선택
5. **Branch**를 `main` 선택
6. **Folder**를 `/ (root)` 선택
7. **Save** 클릭

### 4단계: 배포 확인

- 몇 분 후 `https://YOUR_USERNAME.github.io/YOUR_REPO_NAME/` 접속
- 사이트가 정상적으로 표시되는지 확인

### 5단계: index.html 경로 문제 해결

GitHub Pages에서 `index.html`이 루트에 있으면 자동으로 인식됩니다.
만약 하위 폴더에 있다면, 저장소 이름을 URL에 포함해야 합니다.

**현재 프로젝트 구조:**
```
go_on_to_school2/
├── index.html
├── script.js
├── style.css
├── data/
└── jinro/
```

이 구조는 GitHub Pages에서 바로 작동합니다!

---

## Netlify 배포 방법 (대안)

### 1단계: Netlify 가입
1. [netlify.com](https://www.netlify.com) 접속
2. GitHub 계정으로 로그인

### 2단계: 프로젝트 배포
1. **Add new site** → **Import an existing project**
2. GitHub 저장소 선택
3. 빌드 설정:
   - **Build command**: (비워둠)
   - **Publish directory**: `/` (루트)
4. **Deploy site** 클릭

### 3단계: 커스텀 도메인 (선택사항)
- Settings → Domain management에서 도메인 추가 가능

---

## Vercel 배포 방법 (대안)

### 1단계: Vercel 가입
1. [vercel.com](https://vercel.com) 접속
2. GitHub 계정으로 로그인

### 2단계: 프로젝트 배포
1. **Add New Project** 클릭
2. GitHub 저장소 선택
3. 빌드 설정:
   - **Framework Preset**: Other
   - **Root Directory**: `./`
4. **Deploy** 클릭

---

## Streamlit 사용 시 주의사항

만약 Streamlit을 사용한다면, 기존 디자인을 최대한 유사하게 만들기 위해:

1. **커스텀 CSS 적용**
```python
# app.py에 추가
st.markdown("""
<style>
    /* 기존 style.css 내용을 여기에 복사 */
</style>
""", unsafe_allow_html=True)
```

2. **HTML 컴포넌트 사용**
```python
import streamlit.components.v1 as components
components.html("""
    <!-- 기존 HTML 코드 -->
""", height=600)
```

하지만 **완전히 동일한 디자인을 유지하기는 어렵습니다.**

---

## 추천 사항

**현재 프로젝트의 경우:**
- ✅ **GitHub Pages**를 강력히 추천합니다
- 이유: 기존 HTML/CSS/JavaScript 디자인을 그대로 유지할 수 있고, 설정이 간단하며, 무료입니다.

**Streamlit을 사용해야 하는 경우:**
- Python 백엔드 로직이 필요한 경우
- 데이터베이스 연동이 필요한 경우
- 복잡한 서버 사이드 처리가 필요한 경우

---

## 배포 후 확인사항

1. ✅ 모든 데이터 파일이 올바른 경로에 있는지 확인
2. ✅ 이미지 파일(로고)이 표시되는지 확인
3. ✅ JSON/CSV 파일이 정상적으로 로드되는지 확인
4. ✅ 모바일에서도 정상 작동하는지 확인

---

## 문제 해결

### 문제: 데이터 파일이 로드되지 않음
**해결:** GitHub Pages에서 상대 경로가 올바른지 확인
- 로컬: `data/seoul.json`
- GitHub Pages: `data/seoul.json` (동일)

### 문제: CORS 오류
**해결:** GitHub Pages는 CORS 문제가 없습니다. 로컬에서만 발생할 수 있습니다.

### 문제: 이미지가 표시되지 않음
**해결:** 이미지 경로가 상대 경로인지 확인 (`logo/logo.jpg`)

---

## 도움이 필요하신가요?

배포 중 문제가 발생하면:
1. 브라우저 개발자 도구(F12)에서 콘솔 오류 확인
2. GitHub 저장소의 Issues 탭에서 문제 보고
3. 파일 경로와 대소문자 확인 (Linux 서버는 대소문자 구분)

