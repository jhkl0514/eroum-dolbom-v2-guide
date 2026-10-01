# 이로움돌봄 v2.0 — UI/UX 개발 이관 가이드

개발팀에 전달하는 핸드오프 문서. 단일 파일 `index.html`(빌드 없음, GitHub에 그대로 배포).
담당: 이진희

## 기준 자료 (Figma)

스펙은 **Figma 내용을 기준으로** 정리한다. Figma MCP로 프레임을 직접 읽어서 반영하고, 추측으로 채우지 않는다.

| 용도 | 파일 |
|---|---|
| 작업 파일 (운영·유지보수 설계) | [[디자인] 2026 이로움돌봄 운영 유지보수](https://www.figma.com/design/FYOh7DYsBck0b5Quy7k2HI) — fileKey `FYOh7DYsBck0b5Quy7k2HI` |
| 컴포넌트 및 최종 파일 | [[디자인] App_이로움돌봄](https://www.figma.com/design/LxoOpkMeQ9cMgZJI8qX7vM) — fileKey `LxoOpkMeQ9cMgZJI8qX7vM` |

- 신규·변경 스펙은 작업 파일에서, 확정된 컴포넌트 수치(색상·패딩·라운드 등)는 최종 파일에서 확인한다.
- Figma에 없는 값은 `(개발 확인 필요)`로 표시하거나 사용자에게 묻는다.
- `TC 확인` 뱃지는 UI/UX TC v1(2026.02.23)로 검증된 항목에만 붙인다.

## 문서 구조

- 사이드바 `nav-group` 2개: **공통 가이드**, **화면별 가이드**
- 상단 목차 `toc-box`: 번호(`toc-n`) 01~ 순서
- 섹션 하나 = `<div class="sec" id="...">`

새 섹션을 추가하면 **사이드바 nav-item, 목차 toc-link, 섹션 본문** 세 곳을 모두 추가한다. 신규 항목에는 사이드바 NEW 뱃지를 붙인다(기존 `returns`·`notice` 마크업 참고).

## 스펙 마크업

```html
<div class="sec" id="welfare">
  <div class="sec-badge">복지용구</div>
  <h2 class="sec-h2">복지용구 주문</h2>
  <p class="sec-desc">최종 업데이트 : YYYY.MM.DD · 프레임: ...</p>   <!-- 선택 -->
  <div class="sec-hr"></div>

  <div class="acc">
    <div class="acc-hd"><div class="acc-bar"></div><span class="acc-title">항목명 (화면ID)</span><span class="acc-tc">TC 확인</span></div>
    <div class="acc-body">
      <div class="sub">
        <div class="sub-hd"><div class="sub-dot"></div><span class="sub-title">소제목</span></div>
        <div class="rows">
          <div class="row"><div class="row-icon"></div><span class="lbl">라벨:</span> 값 <span class="cd">200ms</span></div>
        </div>
      </div>
    </div>
  </div>
</div>
```

- 항목 제목: `항목명 (화면ID)` — 예: `상품 목록 (WE_006)`
- 수치·코드값: `<span class="cd">`
- 주의·미확정: `<div class="notice">⚠ ...</div>`
- 플로우: `<span class="flow">플로우: A → B → C</span>`
- 문장은 짧은 명사형/개조식 (`~ 시 노출`, `~ 활성화`)

## 업데이트 이력 (변경할 때마다 필수)

1. `changelog-panel` > `cl-body` **맨 위**에 `cl-entry` 추가
   ```html
   <div class="cl-entry">
     <div class="cl-date">YYYY.MM.DD</div>
     <div class="cl-ver">v2.N</div>
     <div class="cl-items">
       <div class="cl-item"><span class="cl-tag">섹션명</span>변경 내용 요약 (세부 키워드) 추가</div>
     </div>
   </div>
   ```
2. 버전은 마이너 +0.1 (같은 날 여러 건이면 한 entry에 cl-item 여러 개)
3. 상단바 `tb-meta`(날짜)와 `tb-ver`(버전)도 같이 갱신
4. 날짜가 있는 신규 기능 섹션은 h2 우측에 `등록일 YYYY.MM.DD` 표기(`pinchzoom` 참고)

## 커밋

- 한글 한 줄: `○○ 섹션에 ○○ 추가` / `○○ 수정`
- push는 사용자가 요청할 때만
