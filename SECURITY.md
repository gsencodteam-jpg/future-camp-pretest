<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Future Camp 사전과제</title>
<style>
* { box-sizing: border-box; margin: 0; padding: 0; }
body { background: #f9fafb; font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif; }
.wrap { max-width: 1000px; margin: 0 auto; padding: 1.5rem 1rem; }

/* 역할 선택 */
.role-selector { display: flex; gap: 10px; margin-bottom: 2rem; }
.role-btn { flex: 1; padding: 12px; font-size: 14px; font-weight: 600; border: 1px solid #d1d5db; border-radius: 8px; background: #f9fafb; color: #6b7280; cursor: pointer; transition: all 0.2s; }
.role-btn.active { background: #185FA5; color: #fff; border-color: #185FA5; }

/* TEST 페이지 */
.page { display: none; }
.page.active { display: block; }
.top-bar { margin-bottom: 1.25rem; }
.top-bar h1 { font-size: 20px; font-weight: 600; color: #1f2937; }
.top-bar p { font-size: 14px; color: #6b7280; margin-top: 4px; }
.info-row { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-bottom: 1.25rem; }
.info-row input { width: 100%; padding: 10px 12px; font-size: 14px; border: 1px solid #d1d5db; border-radius: 6px; background: #fff; color: #1f2937; }
.progress-bar { width: 100%; height: 4px; background: #e5e7eb; border-radius: 2px; margin-bottom: 1.25rem; }
.progress-fill { height: 4px; background: #185FA5; transition: width 0.3s; }

.q-card { background: #fff; border: 1px solid #e5e7eb; border-radius: 8px; padding: 1.25rem; margin-bottom: 1rem; }
.q-card.correct { border-color: #1D9E75; background: #ecfdf5; }
.q-card.wrong { border-color: #dc2626; background: #fef2f2; }
.q-num { font-size: 12px; font-weight: 600; color: #6b7280; margin-bottom: 6px; }
.q-text { font-size: 15px; font-weight: 500; color: #1f2937; margin-bottom: 12px; line-height: 1.6; }
.options { display: flex; flex-direction: column; gap: 8px; }
.opt-btn { display: flex; align-items: flex-start; gap: 10px; text-align: left; padding: 10px 13px; font-size: 14px; border: 1px solid #d1d5db; border-radius: 6px; background: #f9fafb; color: #1f2937; cursor: pointer; transition: all 0.15s; }
.opt-btn:hover { background: #f3f4f6; }
.opt-btn.selected { background: #185FA5; border-color: #0C447C; color: #fff !important; box-shadow: 0 4px 12px rgba(24,95,165,0.3); font-weight: 600; }
.opt-btn.selected-correct, .opt-btn.reveal-correct { background: #d1fae5; border-color: #10b981; color: #065f46; }
.opt-btn.selected-wrong { background: #fee2e2; border-color: #dc2626; color: #7f1d1d; }

.text-input { width: 100%; padding: 10px 12px; font-size: 14px; border: 1px solid #d1d5db; border-radius: 6px; background: #f9fafb; color: #1f2937; }
.result-panel { display: none; margin-top: 12px; }
.result-panel.show { display: block; }
.result-correct { background: #ecfdf5; border: 1px solid #1D9E75; border-radius: 6px; padding: 10px 13px; font-size: 13px; color: #065f46; font-weight: 500; }
.result-wrong { background: #fef2f2; border: 1px solid #dc2626; border-radius: 6px; overflow: hidden; }
.result-wrong-header { padding: 10px 13px; border-bottom: 1px solid #fecaca; font-size: 13px; color: #7f1d1d; font-weight: 600; }
.explanation { padding: 12px 13px; }
.explanation-label { font-size: 10px; font-weight: 600; color: #7f1d1d; margin-bottom: 6px; }
.explanation-text { font-size: 13px; color: #7f1d1d; line-height: 1.6; margin-bottom: 10px; }
.video-btn { display: inline-flex; align-items: center; gap: 6px; padding: 8px 14px; background: #185FA5; color: #fff; font-size: 13px; font-weight: 500; border-radius: 6px; cursor: pointer; border: none; }
.watch-badge { display: none; align-items: center; gap: 5px; font-size: 11px; font-weight: 500; padding: 4px 10px; border-radius: 6px; background: #ecfdf5; color: #065f46; border: 1px solid #1D9E75; margin-left: 8px; }
.watch-badge.show { display: inline-flex; }

.subj-card { background: #fff; border: 1px solid #e5e7eb; border-radius: 8px; padding: 1.25rem; margin-bottom: 1rem; }
.subj-textarea { width: 100%; min-height: 120px; padding: 10px 12px; font-size: 14px; border: 1px solid #d1d5db; border-radius: 6px; background: #f9fafb; color: #1f2937; resize: vertical; font-family: inherit; line-height: 1.6; }
.submit-btn { width: 100%; padding: 12px; font-size: 14px; font-weight: 600; border: none; border-radius: 6px; background: #185FA5; color: #fff; cursor: pointer; transition: all 0.2s; }
.submit-btn:hover:not(:disabled) { background: #0C447C; }
.submit-btn:disabled { background: #d1d5db; cursor: not-allowed; opacity: 0.6; }

.score-card { display: none; background: #f9fafb; border: 1px solid #e5e7eb; border-radius: 8px; padding: 1.5rem; margin-top: 1rem; text-align: center; }
.score-card.show { display: block; }
.score-big { font-size: 40px; font-weight: 700; color: #1f2937; margin: 0.5rem 0; }
.badge { display: inline-block; padding: 6px 14px; border-radius: 6px; font-size: 13px; font-weight: 600; margin-top: 8px; }
.badge.pass { background: #d1fae5; color: #065f46; }
.badge.fail { background: #fee2e2; color: #7f1d1d; }
.cert-box { margin-top: 1rem; background: #fff; border: 1px solid #e5e7eb; border-radius: 6px; padding: 1rem; font-size: 12px; display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }

/* 모달 알림창 */
.alert-modal { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5); z-index: 9999; align-items: center; justify-content: center; }
.alert-modal.show { display: flex; }
.alert-box { background: #fff; border-radius: 12px; padding: 2rem; max-width: 500px; text-align: center; box-shadow: 0 10px 40px rgba(0,0,0,0.2); }
.alert-box h2 { font-size: 24px; font-weight: 700; margin-bottom: 1rem; color: #1f2937; }
.alert-box p { font-size: 15px; color: #6b7280; line-height: 1.8; margin-bottom: 1.5rem; white-space: pre-line; }
.alert-btn { padding: 10px 24px; background: #185FA5; color: #fff; border: none; border-radius: 6px; font-size: 14px; font-weight: 600; cursor: pointer; }
.alert-btn:hover { background: #0C447C; }

/* Admin */
.stats { display: grid; grid-template-columns: repeat(4, 1fr); gap: 12px; margin-bottom: 2rem; }
.stat-card { background: #fff; border: 1px solid #e5e7eb; border-radius: 8px; padding: 1.5rem; text-align: center; }
.stat-num { font-size: 32px; font-weight: 700; margin-bottom: 0.5rem; }
.stat-num.blue { color: #185FA5; }
.stat-num.green { color: #10b981; }
.stat-num.red { color: #ef4444; }
.stat-label { font-size: 12px; color: #6b7280; font-weight: 500; }

.filter-row { display: flex; gap: 8px; margin-bottom: 1.5rem; align-items: center; }
.filter-row input { flex: 1; padding: 8px 12px; font-size: 13px; border: 1px solid #d1d5db; border-radius: 6px; background: #fff; }
.filter-btn { padding: 8px 14px; font-size: 12px; border: 1px solid #d1d5db; border-radius: 6px; background: #f9fafb; color: #6b7280; cursor: pointer; white-space: nowrap; }
.filter-btn.active { background: #185FA5; color: #fff; border-color: #185FA5; }
.export-btn { padding: 8px 14px; font-size: 12px; font-weight: 600; border: none; border-radius: 6px; background: #185FA5; color: #fff; cursor: pointer; }

.roster-table { width: 100%; border-collapse: collapse; font-size: 13px; background: #fff; border: 1px solid #e5e7eb; border-radius: 8px; overflow: hidden; }
.roster-table th { padding: 12px; text-align: left; font-size: 11px; font-weight: 600; color: #6b7280; border-bottom: 1px solid #e5e7eb; background: #f9fafb; }
.roster-table td { padding: 12px; border-bottom: 1px solid #e5e7eb; color: #1f2937; }
.roster-table tr:hover td { background: #f9fafb; }
.pill { display: inline-block; padding: 3px 10px; border-radius: 20px; font-size: 11px; font-weight: 500; }
.pill.pass { background: #d1fae5; color: #065f46; }
.pill.fail { background: #fee2e2; color: #7f1d1d; }
.empty-msg { text-align: center; padding: 3rem; font-size: 13px; color: #6b7280; }
</style>
</head>
<body>
<div class="wrap">
  <!-- 역할 선택 -->
  <div class="role-selector">
    <button class="role-btn active" onclick="setRole('test')">📝 사전과제 응시</button>
    <button class="role-btn" onclick="setRole('admin')">📊 관리자 현황</button>
  </div>

  <!-- TEST 페이지 -->
  <div class="page active" id="page-test">
    <div class="top-bar">
      <h1>Future Camp 자가진단 TEST</h1>
      <p>이 과정은 Future Camp 문제해결과정에 기본이 되는 내용으로 구성되었습니다.<br>총 11개의 문항을 작성하시고, 내용을 확인하고 싶은 영상이 있으시면 [▶영상보기] 버튼을 눌러주세요</p>
    </div>
    <div class="info-row">
      <input type="text" id="emp-id" placeholder="사번 (필수)" oninput="checkSubmitButton()" />
      <input type="text" id="emp-name" placeholder="성명 (필수)" oninput="checkSubmitButton()" />
    </div>
    <div class="progress-bar"><div class="progress-fill" id="progress"></div></div>
    <div id="questions"></div>
    <div class="subj-card">
      <div class="q-num">문항 12 · 주관식</div>
      <div class="q-text">최근 현업에서 '<strong style="text-decoration: underline; font-size: 16px;">비즈니스 의사결정을 위해 경영진 설득</strong>'을 했던 사례가 있으신가요? 어떤 경험이 있으신지 아래에 작성해 주세요.</div>
      <textarea class="subj-textarea" id="subj-answer" placeholder="예시) 설득 상대/과정에서 가장 어려웠던 점/보고상대가 동의하지 않은 이유/최종 결과 등" oninput="checkSubmitButton()"></textarea>
    </div>
    <button class="submit-btn" id="submit-btn" onclick="submitTest()" disabled>📤 제출하기</button>
    <div class="score-card" id="score-card">
      <div style="font-size:13px;color:#6b7280;margin-bottom:0.5rem;">채점 결과</div>
      <div class="score-big" id="score-display"></div>
      <div id="badge-area"></div>
      <div id="status-msg"></div>
      <div class="cert-box" id="cert-box"></div>
    </div>
  </div>

  <!-- Admin 페이지 -->
  <div class="page" id="page-admin">
    <div class="top-bar">
      <h1>📊 Future Camp 운영 현황</h1>
      <p>사전과제 응시 현황을 실시간으로 확인하세요</p>
    </div>
    <div class="stats">
      <div class="stat-card"><div class="stat-num blue" id="st-total">0</div><div class="stat-label">전체 응시</div></div>
      <div class="stat-card"><div class="stat-num green" id="st-pass">0</div><div class="stat-label">수료</div></div>
      <div class="stat-card"><div class="stat-num red" id="st-fail">0</div><div class="stat-label">미수료</div></div>
      <div class="stat-card"><div class="stat-num" id="st-rate">0%</div><div class="stat-label">수료율</div></div>
    </div>

    <div class="filter-row">
      <input type="text" id="search-input" placeholder="사번 또는 성명 검색..." oninput="renderRoster()" />
      <button class="filter-btn active" id="f-all" onclick="setFilter('all')">전체</button>
      <button class="filter-btn" id="f-pass" onclick="setFilter('pass')">수료</button>
      <button class="filter-btn" id="f-fail" onclick="setFilter('fail')">미수료</button>
      <button class="export-btn" onclick="exportCSV()">📥 CSV 내보내기</button>
    </div>

    <table class="roster-table">
      <thead>
        <tr>
          <th>#</th><th>사번</th><th>성명</th><th>점수</th><th>정답률</th><th>상태</th><th>영상시청</th><th>제출일시</th>
        </tr>
      </thead>
      <tbody id="roster-body"></tbody>
    </table>
  </div>
</div>

<!-- 모달 알림창 -->
<div class="alert-modal" id="alert-modal">
  <div class="alert-box">
    <h2 id="alert-title"></h2>
    <p id="alert-msg"></p>
    <button class="alert-btn" onclick="closeAlert()">확인</button>
  </div>
</div>

<script>
const NUMS = ['①','②','③','④'];
const questions = [
  { id:1, type:'short', text:'피라미드 구조, 로직 트리처럼 비즈니스 현장에서 활용되는 사고의 틀을 무엇이라 하는가?', answers:['framework', '프레임워크', '프레임 워크'], answerDisplay:'Framework', explanation:'비즈니스 현장에서 복잡한 문제를 체계적으로 분석·정리하기 위한 사고의 틀을 프레임워크(Framework)라고 합니다.', videoUrl:'https://gsenc.hunet.co.kr/Edu/Imagine/Detail?goodsId=Y00134796&IsSeries=Y' },
  { id:2, type:'mc', text:'다음 중 전체 구조를 명확히 하고 내용을 효과적으로 전달할 때 사용하는 것은?', options:['피라미드 구조','로직트리','매트릭스','프로세스'], answer:0, explanation:'피라미드 구조는 결론을 먼저 제시하고 근거를 아래에 배치하는 방식으로 효과적입니다.', videoUrl:'https://gsenc.hunet.co.kr/Edu/Imagine/Detail?goodsId=Y00134797&IsSeries=Y' },
  { id:3, type:'mc', text:'다음 중 피라미드 스트럭처에 대한 설명으로 틀린 것은?', options:['결론이나 주장의 논리적 전달이 목적이다','내용을 피라미드 형태로 구조화하여 정리할 수 있다','세부 정보부터 설명한 뒤 마지막에 결론을 제시한다','전체 흐름을 한눈에 논리적으로 파악할 수 있다'], answer:2, explanation:'피라미드 스트럭처는 결론을 먼저 제시하는 하향식(Top-down) 구조입니다.', videoUrl:'https://gsenc.hunet.co.kr/Edu/Imagine/Detail?goodsId=Y00134799&IsSeries=Y' },
  { id:4, type:'short', text:'정보를 중복과 누락 없이 분류하는 방법을 무엇이라 하는가?', answers:['mece', 'MECE'], answerDisplay:'MECE', explanation:'MECE는 항목들이 서로 중복되지 않으면서 전체를 빠짐없이 포함하는 분류 방법입니다.', videoUrl:'https://gsenc.hunet.co.kr/Edu/Imagine/Detail?goodsId=Y00134802&IsSeries=Y' },
  { id:5, type:'mc', text:'다음 중 중복과 누락 없이 분류한 것은?', options:['카드 52장을(조커제외) 스페이드/파트/클로버/다이아몬드로 분류한 것','0~9의 숫자를 \'5 초과\'와 \'5 미만\'으로 분류한 것','영화 장르를 액션/스릴러/공포/코미디로 분류한 것','사람들을 남자/아저씨/여자/아줌마로 분류한 것'], answer:0, explanation:'카드 52장을 4가지 무늬로 분류하면 중복 없이 누락 없이 분류됩니다.', videoUrl:'https://gsenc.hunet.co.kr/Edu/Imagine/Detail?goodsId=Y00134803&IsSeries=Y' },
  { id:6, type:'mc', text:'어느 범위까지 문제를 해결할지 처음에 정해두는 것을 무엇이라 하나?', options:['Scope','Issue','Gap','Logic'], answer:0, explanation:'Scope(스코프)란 문제 해결의 범위를 사전에 명확히 정해두는 것입니다.', videoUrl:'https://gsenc.hunet.co.kr/Edu/Imagine/Detail?goodsId=Y00134804&IsSeries=Y' },
  { id:7, type:'short', text:'어떤 주제나 문제를 나무 형태로 세분화해 정리하는 툴을 무엇이라 하나?', answers:['logic tree', 'logictree', '로직트리', '로직 트리'], answerDisplay:'Logic Tree', explanation:'Logic Tree(로직트리)는 문제를 나무 구조로 세분화하여 분석하는 도구입니다.', videoUrl:'https://gsenc.hunet.co.kr/Edu/Imagine/Detail?goodsId=Y00134811&IsSeries=Y' },
  { id:8, type:'mc', text:'어떤 대상의 현재 수준과 바람직한 수준의 차이(Gap)를 무엇이라고 하는가?', options:['인식','변화','문제','관계'], answer:2, explanation:'현재 상태와 목표 상태 사이의 Gap을 \'문제\'라고 정의합니다.', videoUrl:'https://gsenc.hunet.co.kr/Edu/Imagine/Detail?goodsId=Y00134808&IsSeries=Y' },
  { id:9, type:'mc', text:'다음 중 로직트리의 장점이 아닌 것은?', options:['1페이지로 전체를 조망하며 생각할 수 있다','생각을 논리적이고 체계적으로 전개할 수 있다','창의적인 해결방안을 도출할 수 있다','많은 양의 정보를 글로 나열할 수 있다'], answer:3, explanation:'로직트리는 정보를 구조화하는 도구이며, 글로 나열하는 것은 장점이 아닙니다.', videoUrl:'https://gsenc.hunet.co.kr/Edu/Imagine/Detail?goodsId=Y00134812&IsSeries=Y' },
  { id:10, type:'mc', text:'다음의 로직트리 중 문제에 깊이 숨어 있는 근본 원인을 찾을 수 있는 것은?', options:['What Tree','Why Tree','How Tree','When Tree'], answer:1, explanation:'Why Tree는 "왜?"를 반복하며 근본 원인을 찾는 로직트리입니다.', videoUrl:'https://gsenc.hunet.co.kr/Edu/Imagine/Detail?goodsId=Y00134813&IsSeries=Y' },
  { id:11, type:'mc', text:'다음 중 가설 기반 검증 접근법의 특징으로 가장 거리가 먼 것은?', options:['뚜렷한 방향(가설) 설정 후 분석하라','사실에 기반한 가설을 수립하라','가장 그럴듯한 내용의 가설을 수립하라','근거가 부족하더라도 빠르게 가설을 수립해 검증하라'], answer:3, explanation:'가설 기반 접근법은 사실에 근거하여 가설을 세우는 것이 핵심입니다.', videoUrl:'https://gsenc.hunet.co.kr/Edu/Imagine/Detail?goodsId=Y00176936&IsSeries=Y' }
];

const userAnswers = {}, watchedVideos = {};
let submitted = false, wrongCount = 0, currentFilter = 'all';

function setRole(role) {
  if (role === 'admin') {
    const pwd = prompt('관리자 비밀번호를 입력하세요');
    if (pwd !== 'ODT1234') {
      alert('비밀번호가 틀렸습니다');
      return;
    }
  }
  
  document.querySelectorAll('.role-btn').forEach(b => b.classList.remove('active'));
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  
  if (role === 'test') {
    document.querySelectorAll('.role-btn')[0].classList.add('active');
    document.getElementById('page-test').classList.add('active');
  } else {
    document.querySelectorAll('.role-btn')[1].classList.add('active');
    document.getElementById('page-admin').classList.add('active');
    refreshDash();
  }
}

function checkSubmitButton() {
  const empId = document.getElementById('emp-id').value.trim();
  const empName = document.getElementById('emp-name').value.trim();
  const subj = document.getElementById('subj-answer').value.trim();
  const allAnswered = Object.keys(userAnswers).length === questions.length;
  
  const canSubmit = empId && empName && subj && allAnswered;
  document.getElementById('submit-btn').disabled = !canSubmit;
}

function renderQuestions() {
  const c = document.getElementById('questions');
  c.innerHTML = '';
  questions.forEach((q, idx) => {
    const card = document.createElement('div');
    card.className = 'q-card';
    card.id = 'q-card-' + q.id;
    
    let inp = '';
    if (q.type === 'short') {
      inp = `<input class="text-input" id="ans-${q.id}" placeholder="답변을 입력하세요" oninput="userAnswers[${q.id}]=this.value.trim(); checkSubmitButton()"/>`;
    } else {
      inp = `<div class="options">${q.options.map((o,i)=>`<button class="opt-btn" id="opt-${q.id}-${i}" onclick="selectMC(${q.id},${i})"><span style="font-weight:600;min-width:16px;">${NUMS[i]}</span><span>${o}</span></button>`).join('')}</div>`;
    }
    
    const lbl = q.type==='short' ? '단답형' : '객관식';
    card.innerHTML = `<div class="q-num">문항 ${idx+1} · ${lbl}</div><div class="q-text">${q.text}</div>${inp}<div class="result-panel" id="rp-${q.id}"></div>`;
    c.appendChild(card);
  });
}

function selectMC(qId, idx) {
  userAnswers[qId] = idx;
  const q = questions.find(q => q.id === qId);
  q.options.forEach((_, i) => { 
    const btn = document.getElementById(`opt-${qId}-${i}`);
    btn.className = 'opt-btn';
    btn.style.backgroundColor = '';
  });
  const selBtn = document.getElementById(`opt-${qId}-${idx}`);
  selBtn.className = 'opt-btn selected';
  selBtn.style.backgroundColor = '#185FA5';
  checkSubmitButton();
}

function openVideo(qId, url) {
  watchedVideos[qId] = true;
  const badge = document.getElementById('wb-' + qId);
  if (badge) badge.classList.add('show');
  
  // localStorage 실시간 업데이트
  const empId = document.getElementById('emp-id').value;
  const empName = document.getElementById('emp-name').value;
  if (empId && empName) {
    const arr = JSON.parse(localStorage.getItem('fc_results')||'[]');
    const idx = arr.findIndex(r => r.empId === empId && r.empName === empName);
    if (idx !== -1) {
      arr[idx].watchedCount = Object.keys(watchedVideos).length;
      localStorage.setItem('fc_results', JSON.stringify(arr));
      refreshDash(); // Admin 페이지 실시간 업데이트
    }
  }
  
  if (submitted && Object.keys(watchedVideos).length === wrongCount) {
    updatePassStatus();
  }
  
  window.open(url, '_blank');
}

function checkShortAnswer(q, input) {
  if (!input) return false;
  const normalize = (str) => str.toLowerCase().replace(/\s/g, '');
  return q.answers.some(ans => normalize(ans) === normalize(input));
}

function updatePassStatus() {
  const pass = Object.keys(watchedVideos).length === wrongCount;
  const statusMsg = document.getElementById('status-msg');
  const badgeArea = document.getElementById('badge-area');
  const certBox = document.getElementById('cert-box');
  
  if (pass) {
    statusMsg.innerHTML = '<div style="background:#d1fae5;border:1px solid #10b981;border-radius:6px;padding:12px;color:#065f46;font-size:14px;font-weight:600;margin-top:1rem;">✅ 수료처리가 되었습니다!</div>';
    badgeArea.innerHTML = '<span class="badge pass">✅ 수료 완료</span>';
    
    const empId = document.getElementById('emp-id').value;
    const empName = document.getElementById('emp-name').value;
    const now = new Date();
    const dateStr = `${now.getFullYear()}.${String(now.getMonth()+1).padStart(2,'0')}.${String(now.getDate()).padStart(2,'0')} ${String(now.getHours()).padStart(2,'0')}:${String(now.getMinutes()).padStart(2,'0')}`;
    const correct = questions.length - wrongCount;
    const pct = Math.round((correct / questions.length) * 100);
    
    certBox.innerHTML = `
      <div><strong>사번</strong><br>${empId}</div>
      <div><strong>성명</strong><br>${empName}</div>
      <div><strong>점수</strong><br>${correct}/${questions.length}</div>
      <div><strong>정답률</strong><br>${pct}%</div>
      <div><strong>영상시청</strong><br>${wrongCount}/${wrongCount}개</div>
      <div><strong>제출일시</strong><br>${dateStr}</div>
    `;
  }
}

function showAlert(title, message) {
  document.getElementById('alert-title').textContent = title;
  document.getElementById('alert-msg').textContent = message;
  document.getElementById('alert-modal').classList.add('show');
}

function closeAlert() {
  document.getElementById('alert-modal').classList.remove('show');
}

function submitTest() {
  const empId = document.getElementById('emp-id').value.trim();
  const empName = document.getElementById('emp-name').value.trim();
  const subj = document.getElementById('subj-answer').value.trim();
  
  if (!empId) { alert('사번을 입력하세요'); return; }
  if (!empName) { alert('성명을 입력하세요'); return; }
  if (!subj) { alert('12번 주관식 답변을 작성해 주세요'); return; }
  
  const allAnswered = Object.keys(userAnswers).length === questions.length;
  if (!allAnswered) { alert('모든 문항에 답변해 주세요'); return; }

  submitted = true;
  let correct = 0;
  wrongCount = 0;
  
  questions.forEach(q => {
    const rp = document.getElementById('rp-' + q.id);
    let ok = false;

    if (q.type === 'short') {
      ok = checkShortAnswer(q, userAnswers[q.id] || '');
      const inp = document.getElementById('ans-' + q.id);
      if (inp) inp.disabled = true;
    } else {
      ok = userAnswers[q.id] === q.answer;
      q.options.forEach((_, i) => {
        const btn = document.getElementById(`opt-${q.id}-${i}`);
        btn.disabled = true;
        btn.className = 'opt-btn';
        if (i === userAnswers[q.id] && !ok) btn.classList.add('selected-wrong');
        if (i === q.answer) btn.classList.add('reveal-correct');
      });
    }

    rp.className = 'result-panel show';
    if (ok) {
      correct++;
      document.getElementById('q-card-' + q.id).className = 'q-card correct';
      rp.innerHTML = `<div class="result-correct">✅ 정답입니다!</div>`;
    } else {
      wrongCount++;
      const alreadyWatched = !!watchedVideos[q.id];
      document.getElementById('q-card-' + q.id).className = 'q-card wrong';
      rp.innerHTML = `<div class="result-wrong"><div class="result-wrong-header">❌ 오답입니다${q.type==='short' ? ' (정답: '+q.answerDisplay+')' : ''}</div><div class="explanation"><div class="explanation-label">해설</div><div class="explanation-text">${q.explanation}</div><button class="video-btn" onclick="openVideo(${q.id},'${q.videoUrl}')">▶ 영상 보기</button><span class="watch-badge ${alreadyWatched?'show':''}" id="wb-${q.id}">✓ 시청 완료</span></div></div>`;
    }
  });

  const pct = Math.round((correct / questions.length) * 100);
  const now = new Date();
  const dateStr = `${now.getFullYear()}.${String(now.getMonth()+1).padStart(2,'0')}.${String(now.getDate()).padStart(2,'0')} ${String(now.getHours()).padStart(2,'0')}:${String(now.getMinutes()).padStart(2,'0')}`;

  // localStorage에 저장
  const arr = JSON.parse(localStorage.getItem('fc_results')||'[]');
  arr.push({ empId, empName, correct, total: questions.length, pct, date: dateStr, watchedCount: Object.values(watchedVideos).filter(Boolean).length, wrongCount });
  localStorage.setItem('fc_results', JSON.stringify(arr));

  document.getElementById('progress').style.width = '100%';
  const sc = document.getElementById('score-card');
  sc.className = 'score-card show';
  document.getElementById('score-display').textContent = correct + ' / ' + questions.length + '점';
  
  const watchedCount = Object.keys(watchedVideos).length;
  const badgeArea = document.getElementById('badge-area');
  const certBox = document.getElementById('cert-box');
  
  // 모달 알림창 표시
  if (wrongCount === 0) {
    showAlert('축하합니다! 🎉', `점수: ${correct}/${questions.length}점\n정답률: ${pct}%\n\n모든 문제를 맞추셨습니다!`);
    document.getElementById('status-msg').innerHTML = '<div style="background:#d1fae5;border:1px solid #10b981;border-radius:6px;padding:12px;color:#065f46;font-size:14px;font-weight:600;margin-top:1rem;">✅ 수료처리가 되었습니다!</div>';
    badgeArea.innerHTML = '<span class="badge pass">✅ 수료 완료</span>';
    certBox.innerHTML = `
      <div><strong>사번</strong><br>${empId}</div>
      <div><strong>성명</strong><br>${empName}</div>
      <div><strong>점수</strong><br>${correct}/${questions.length}</div>
      <div><strong>정답률</strong><br>${pct}%</div>
      <div><strong>영상시청</strong><br>0/0개</div>
      <div><strong>제출일시</strong><br>${dateStr}</div>
    `;
  } else {
    showAlert('채점 완료! 📝', `점수: ${correct}/${questions.length}점\n정답률: ${pct}%\n\n❗ 틀린문제(${wrongCount}개)의 영상을 시청해주세요!\n\n영상을 모두 시청하면 수료됩니다.`);
    badgeArea.innerHTML = `<span class="badge fail">🔄 미수료 — ${wrongCount - watchedCount}개 영상 더 시청 필요</span>`;
    certBox.innerHTML = `
      <div><strong>사번</strong><br>${empId}</div>
      <div><strong>성명</strong><br>${empName}</div>
      <div><strong>점수</strong><br>${correct}/${questions.length}</div>
      <div><strong>정답률</strong><br>${pct}%</div>
      <div><strong>영상시청</strong><br>${watchedCount}/${wrongCount}개</div>
      <div><strong>제출일시</strong><br>${dateStr}</div>
    `;
  }
  
  sc.scrollIntoView({ behavior: 'smooth' });
}

function refreshDash() {
  const results = JSON.parse(localStorage.getItem('fc_results')||'[]');
  const passArr = results.filter(r => r.wrongCount === 0 || r.watchedCount === r.wrongCount);
  const total = results.length;
  const rate = total ? Math.round(passArr.length / total * 100) : 0;

  document.getElementById('st-total').textContent = total;
  document.getElementById('st-pass').textContent = passArr.length;
  document.getElementById('st-fail').textContent = total - passArr.length;
  document.getElementById('st-rate').textContent = rate + '%';
  
  renderRoster();
}

function setFilter(f) {
  currentFilter = f;
  ['all','pass','fail'].forEach(k => document.getElementById('f-'+k).classList.toggle('active', k===f));
  renderRoster();
}

function renderRoster() {
  const results = JSON.parse(localStorage.getItem('fc_results')||'[]');
  const q = (document.getElementById('search-input').value || '').toLowerCase();
  
  const filtered = results.filter(r => {
    const pass = r.wrongCount === 0 || r.watchedCount === r.wrongCount;
    const mf = currentFilter==='all' || (currentFilter==='pass'&&pass) || (currentFilter==='fail'&&!pass);
    const mq = !q || (r.empId&&r.empId.toLowerCase().includes(q)) || (r.empName&&r.empName.toLowerCase().includes(q));
    return mf && mq;
  });
  
  const tbody = document.getElementById('roster-body');
  if (!filtered.length) {
    tbody.innerHTML = `<tr><td colspan="8" class="empty-msg">아직 응시 데이터가 없습니다.</td></tr>`;
    return;
  }
  
  tbody.innerHTML = filtered.map((r, i) => {
    const pass = r.wrongCount === 0 || r.watchedCount === r.wrongCount;
    const wc = r.watchedCount||0, wt = r.wrongCount||0;
    const watchTxt = wt===0 ? '오답없음' : wc===wt ? `<span style="color:#10b981;font-weight:600;">✓ ${wc}/${wt}</span>` : `${wc}/${wt}`;
    return `<tr>
      <td>${i+1}</td>
      <td>${r.empId}</td>
      <td style="font-weight:500;">${r.empName}</td>
      <td>${r.correct}/${r.total}</td>
      <td>${r.pct}%</td>
      <td><span class="pill ${pass?'pass':'fail'}">${pass?'수료':'미수료'}</span></td>
      <td>${watchTxt}</td>
      <td style="font-size:12px;color:#6b7280;">${r.date}</td>
    </tr>`;
  }).join('');
}

function exportCSV() {
  const results = JSON.parse(localStorage.getItem('fc_results')||'[]');
  if (!results.length) { alert('내보낼 데이터가 없습니다.'); return; }
  const rows = [['#','사번','성명','점수','정답률','상태','영상시청','제출일시'],
    ...results.map((r,i) => {
      const pass = r.wrongCount === 0 || r.watchedCount === r.wrongCount;
      return [i+1, r.empId, r.empName, `${r.correct}/${r.total}`, r.pct+'%', pass?'수료':'미수료', `${r.watchedCount||0}/${r.wrongCount||0}`, r.date];
    })];
  const csv = rows.map(r => r.join(',')).join('\n');
  const blob = new Blob(['\uFEFF'+csv], {type:'text/csv;charset=utf-8'});
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = 'FutureCamp_결과_' + new Date().toISOString().slice(0,10) + '.csv';
  a.click();
}

renderQuestions();
</script>
</body>
</html>
