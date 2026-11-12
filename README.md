```html
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>청소년 정서적 공격 피해 경험 분석 (KOSIS 데이터)</title>
    <style>
        :root {
            --bg-color: #f1f5f9;
            --card-bg: #ffffff;
            --primary: #2563eb;
            --primary-dark: #1d4ed8;
            --secondary: #10b981;
            --accent: #f59e0b;
            --danger: #ef4444;
            --text-main: #0f172a;
            --text-muted: #475569;
            --border-color: #cbd5e1;
            --radius-lg: 16px;
            --radius-md: 10px;
            --shadow-sm: 0 2px 4px rgba(0,0,0,0.04);
            --shadow-md: 0 4px 12px rgba(0,0,0,0.06);
            --shadow-lg: 0 10px 25px rgba(0,0,0,0.08);
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Pretendard', -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Arial, sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            line-height: 1.6;
            padding: 24px 16px;
        }

        .container {
            max-width: 1280px;
            margin: 0 auto;
            display: flex;
            flex-direction: column;
            gap: 20px;
        }

        /* Poster Header */
        .poster-header {
            background: linear-gradient(135deg, #0f172a 0%, #1e3a8a 60%, #2563eb 100%);
            color: #ffffff;
            padding: 28px 32px;
            border-radius: var(--radius-lg);
            box-shadow: var(--shadow-md);
            position: relative;
        }

        .header-top {
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 12px;
            margin-bottom: 12px;
        }

        .badge-tag {
            background: rgba(255, 255, 255, 0.18);
            backdrop-filter: blur(4px);
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 0.82rem;
            font-weight: 700;
            color: #e0f2fe;
            letter-spacing: 0.5px;
        }

        .header-team {
            font-size: 0.9rem;
            color: #93c5fd;
            font-weight: 600;
        }

        .poster-header h1 {
            font-size: 1.8rem;
            font-weight: 800;
            margin-bottom: 8px;
            line-height: 1.35;
            color: #ffffff;
        }

        .poster-header p.subtitle {
            font-size: 1.02rem;
            color: #cbd5e1;
            margin-bottom: 16px;
        }

        .header-meta {
            display: flex;
            flex-wrap: wrap;
            gap: 16px;
            font-size: 0.85rem;
            color: #94a3b8;
            border-top: 1px solid rgba(255, 255, 255, 0.15);
            padding-top: 12px;
        }

        /* Layout Grids */
        .grid-2 {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            align-items: stretch;
        }

        .grid-2 > * {
            min-width: 0;
        }

        .grid-3 {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 16px;
            align-items: stretch;
        }

        .grid-4 {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 16px;
        }

        @media (max-width: 992px) {
            .grid-2, .grid-3, .grid-4 {
                grid-template-columns: 1fr;
            }
        }

        /* Card Component with Balanced Heights */
        .card {
            background-color: var(--card-bg);
            border-radius: var(--radius-lg);
            padding: 22px;
            border: 1px solid var(--border-color);
            box-shadow: var(--shadow-sm);
            display: flex;
            flex-direction: column;
            justify-content: space-between;
        }

        .card-header-badge {
            display: inline-flex;
            align-items: center;
            gap: 6px;
            font-size: 0.8rem;
            font-weight: 700;
            color: var(--primary);
            background-color: #eff6ff;
            padding: 3px 10px;
            border-radius: 6px;
            margin-bottom: 10px;
            width: fit-content;
        }

        .card-title {
            font-size: 1.1rem;
            font-weight: 700;
            color: var(--text-main);
            margin-bottom: 12px;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .card-body {
            font-size: 0.92rem;
            color: #334155;
            flex-grow: 1;
        }

        /* List Items in Cards */
        .info-list {
            list-style: none;
            padding: 0;
            display: flex;
            flex-direction: column;
            gap: 8px;
        }

        .info-list li {
            position: relative;
            padding-left: 16px;
            line-height: 1.5;
        }

        .info-list li::before {
            content: '•';
            position: absolute;
            left: 0;
            color: var(--primary);
            font-weight: bold;
        }

        /* KPI Metric Cards */
        .kpi-card {
            background: #ffffff;
            border-left: 5px solid var(--primary);
            border-radius: var(--radius-md);
            padding: 16px 18px;
            box-shadow: var(--shadow-sm);
            border-top: 1px solid var(--border-color);
            border-right: 1px solid var(--border-color);
            border-bottom: 1px solid var(--border-color);
        }

        .kpi-label {
            font-size: 0.82rem;
            color: var(--text-muted);
            font-weight: 600;
            margin-bottom: 4px;
        }

        .kpi-value {
            font-size: 1.7rem;
            font-weight: 800;
            color: var(--text-main);
        }

        .kpi-subtext {
            font-size: 0.78rem;
            color: var(--text-muted);
            margin-top: 2px;
        }

        /* Filter Bar */
        .filter-bar {
            display: flex;
            flex-wrap: wrap;
            gap: 16px;
            align-items: center;
            justify-content: space-between;
            background-color: var(--card-bg);
            padding: 16px 20px;
            border-radius: var(--radius-lg);
            border: 1px solid var(--border-color);
        }

        .filter-group {
            display: flex;
            align-items: center;
            gap: 10px;
            flex-wrap: wrap;
        }

        .filter-group label {
            font-size: 0.88rem;
            font-weight: 700;
            color: var(--text-main);
        }

        select, input[type="file"] {
            padding: 7px 12px;
            border-radius: var(--radius-md);
            border: 1px solid var(--border-color);
            background-color: #f8fafc;
            font-size: 0.88rem;
            color: var(--text-main);
            outline: none;
            cursor: pointer;
        }

        select:focus {
            border-color: var(--primary);
            background-color: #ffffff;
        }

        .btn-reset {
            background-color: #f1f5f9;
            border: 1px solid var(--border-color);
            padding: 7px 14px;
            border-radius: var(--radius-md);
            font-size: 0.82rem;
            font-weight: 600;
            color: var(--text-muted);
            cursor: pointer;
            transition: all 0.2s;
        }

        .btn-reset:hover {
            background-color: #e2e8f0;
            color: var(--text-main);
        }

        /* Canvas Scroll & Equal Height Layout */
        .chart-scroll-wrapper {
            width: 100%;
            max-width: 100%;
            overflow-x: auto;
            overflow-y: hidden;
            cursor: grab;
            user-select: none;
            border-radius: var(--radius-md);
            background-color: #f8fafc;
            border: 1px solid var(--border-color);
            margin-bottom: 12px;
        }

        .chart-container {
            position: relative;
            height: 310px;
        }

        canvas {
            display: block;
        }

        /* Table Styling */
        .table-responsive {
            width: 100%;
            overflow-x: auto;
            max-height: 310px;
            overflow-y: auto;
            border: 1px solid var(--border-color);
            border-radius: var(--radius-md);
        }

        table {
            width: 100%;
            border-collapse: collapse;
            text-align: left;
            font-size: 0.88rem;
        }

        th {
            position: sticky;
            top: 0;
            background-color: #f8fafc;
            color: var(--text-muted);
            font-weight: 700;
            padding: 10px 14px;
            border-bottom: 2px solid var(--border-color);
            white-space: nowrap;
            z-index: 2;
        }

        td {
            padding: 10px 14px;
            border-bottom: 1px solid var(--border-color);
            color: var(--text-main);
        }

        tr:hover td {
            background-color: #f8fafc;
        }

        .progress-bar-bg {
            background-color: #e2e8f0;
            border-radius: 10px;
            height: 10px;
            width: 80px;
            display: block;
            overflow: hidden;
        }

        .progress-bar-fill {
            display: block;
            height: 100%;
            background-color: var(--primary);
            border-radius: 10px;
            transition: width 0.3s ease;
        }

        /* Insight Box */
        .insight-box {
            background-color: #eff6ff;
            border-left: 4px solid var(--primary);
            padding: 12px 16px;
            border-radius: var(--radius-md);
            margin-top: auto;
        }

        .insight-box h4 {
            color: var(--primary-dark);
            font-size: 0.88rem;
            margin-bottom: 4px;
        }

        .insight-box p {
            font-size: 0.85rem;
            color: #1e3a8a;
            line-height: 1.45;
        }

        /* AI Collaboration Table */
        .ai-table {
            width: 100%;
            border-collapse: collapse;
            font-size: 0.85rem;
            margin-top: 8px;
        }

        .ai-table th, .ai-table td {
            padding: 8px 10px;
            border: 1px solid var(--border-color);
        }

        .ai-table th {
            background-color: #f8fafc;
            color: var(--text-muted);
        }

        /* Limitation Box */
        .limitation-card {
            background-color: #fffbe6;
            border: 1px solid #ffe58f;
            border-radius: var(--radius-lg);
            padding: 18px 22px;
        }

        .limitation-card h3 {
            color: #d46b08;
            font-size: 0.98rem;
            margin-bottom: 8px;
        }

        .limitation-card ul {
            padding-left: 18px;
            font-size: 0.86rem;
            color: #8c4b00;
        }

        .limitation-card li {
            margin-bottom: 4px;
        }

        footer {
            text-align: center;
            padding: 20px;
            color: var(--text-muted);
            font-size: 0.82rem;
            border-top: 1px solid var(--border-color);
        }

        .toast-msg {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background: #1e293b;
            color: #fff;
            padding: 12px 20px;
            border-radius: 8px;
            font-size: 0.85rem;
            box-shadow: var(--shadow-lg);
            display: none;
            z-index: 1000;
        }
    </style>
</head>
<body>

<div class="container">
    
    <!-- Poster Header Banner -->
    <header class="poster-header">
        <div class="header-top">
            <span class="badge-tag">KOSIS 데이터 기반 학술 탐구 보고서</span>
            <span class="header-team">팀명: 청소년 사회탐구 팀 | 발표자: 정재훈</span>
        </div>
        <h1>청소년이 경험하는 가정 및 학교 내 정서적 공격 피해 실태 분석</h1>
        <p class="subtitle">
            연구 질문: 청소년이 가정(부모님)과 학교(선생님)에서 경험하는 정서적 공격 피해 비율은 응답자의 배경 특성(성별, 학교급, 학업성적, 경제적 수준)에 따라 어휘적·환경적 차이를 보이는가?
        </p>
        <div class="header-meta">
            <span>📊 데이터 출처: 국가통계포털 (KOSIS)</span>
            <span>📂 원본 파일: 가정과_학교에서_성인으로부터의_정서적_공격_피해_경험_20260820194451.csv</span>
            <span>📅 데이터 수집일: 2026년 8월 20일 (2025년 조사 기준)</span>
        </div>
    </header>

    <!-- Poster Section 1 & 2: Overview & Methods -->
    <div class="grid-2">
        <section class="card">
            <div>
                <span class="card-header-badge">SECTION 1</span>
                <div class="card-title">1. 연구의 필요성 및 목적</div>
                <div class="card-body">
                    <ul class="info-list">
                        <li><strong>청소년 정서적 안녕의 중요성:</strong> 언어 폭력, 무시, 비난 등 성인으로부터의 정서적 공격은 청소년의 자아존중감 및 정신 건강에 장기적인 영향 미침.</li>
                        <li><strong>가정 및 학교 환경 비교 필요:</strong> 주요 생활 공간인 가정(부모)과 학교(교사)에서 일어나는 정서적 피해 실태의 상대적 격차 확인 필요.</li>
                        <li><strong>맞춤형 예방 대책 마련:</strong> 성별, 학교급, 학업 성적, 경제적 수준 등 청소년이 처한 배경 특성에 따라 위험 집단을 식별하고 맞춤형 지원 체계 마련 모색.</li>
                    </ul>
                </div>
            </div>
        </section>

        <section class="card">
            <div>
                <span class="card-header-badge">SECTION 2</span>
                <div class="card-title">2. 연구 방법 및 절차</div>
                <div class="card-body">
                    <ul class="info-list">
                        <li><strong>데이터 출처:</strong> 국가통계포털(KOSIS) 2025년 기준 청소년 정서적 공격 피해 경험 데이터.</li>
                        <li><strong>분석 도구:</strong> Pure HTML5 Canvas visualization, JavaScript (ES6+), CSS Grid/Flexbox Layout.</li>
                        <li><strong>데이터 정제 절차:</strong> CSV 파일 파싱 ➔ 배경 변수별 그룹핑 ➔ 가정/학교 피해 경험률 퍼센티지 산출 ➔ 통계 요약표 및 그래프 렌더링.</li>
                    </ul>
                </div>
            </div>
        </section>
    </div>

    <!-- Poster Section 3 & 5: Analysis Design & AI Collaboration -->
    <div class="grid-2">
        <section class="card">
            <div>
                <span class="card-header-badge">SECTION 3</span>
                <div class="card-title">3. 연구 내용 (분석 컬럼 & 계산 기준)</div>
                <div class="card-body">
                    <ul class="info-list">
                        <li><strong>분석 대상 컬럼:</strong> <code>응답자유형별(1)</code> (대분류), <code>응답자유형별(2)</code> (세부그룹), <code>2025</code> (가정 피해율), <code>2025.1</code> (학교 피해율).</li>
                        <li><strong>독립변수 (배경 특성):</strong> 성별(남/여), 학교급(초4~6/중/고), 학업성적(상/중/하), 경제적 수준(상/중/하).</li>
                        <li><strong>종속변수:</strong> 정서적 공격 피해 경험 응답 비율(%).</li>
                    </ul>
                </div>
            </div>
        </section>

        <section class="card">
            <div>
                <span class="card-header-badge">SECTION 5</span>
                <div class="card-title">5. AI 활용 및 역할 분담</div>
                <div class="card-body">
                    <p style="font-size:0.85rem; color:var(--text-muted); margin-bottom:6px;">인공지능(AI)을 활용한 데이터 파싱, HTML/JS 시각화 코드 개발 및 연구자 협업 내용:</p>
                    <table class="ai-table">
                        <thead>
                            <tr>
                                <th>구분</th>
                                <th>AI 역할 (Generative AI)</th>
                                <th>연구자(학생) 역할</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td><strong>HTML/CSS</strong></td>
                                <td>반응형 학술 포스터 레이아웃 및 CSS Grid 구조 생성</td>
                                <td>시각적 디자인 채색, 가독성 검토 및 UI 배치 수정</td>
                            </tr>
                            <tr>
                                <td><strong>JS/Chart</strong></td>
                                <td>Canvas 2D 막대그래프 렌더링 및 CSV 파싱 함수 작성</td>
                                <td>통계 수치 정확성 검증 및 필터링 범주 조건 정의</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </section>
    </div>

    
    <!-- Poster Section 4: Output Dashboard Controls & Metrics -->
    <section style="display:flex; flex-direction:column; gap:16px;">
        <div style="display:flex; align-items:center; gap:8px;">
            <span class="card-header-badge" style="margin-bottom:0;">SECTION 4</span>
            <h2 style="font-size:1.25rem; font-weight:800; color:var(--text-main);">4. 핵심 연구 산출물 (인터랙티브 데이터 대시보드)</h2>
        </div>

        <!-- Filter Bar -->
        <div class="filter-bar">
            <div class="filter-group">
                <label for="bgVariableSelect">🔍 배경 특성 구분:</label>
                <select id="bgVariableSelect" onchange="updateDashboard()">
                    <option value="ALL">전체 보기 (요약 비교)</option>
                    <option value="성별">성별 (남학생 / 여학생)</option>
                    <option value="학교급">학교급 (초4~6 / 중학교 / 고등학교)</option>
                    <option value="학업성적">학업성적 (상 / 중 / 하)</option>
                    <option value="경제적수준">주관적 경제상태 (상 / 중 / 하)</option>
                </select>
                
                <label for="locationSelect" style="margin-left: 12px;">🏠🏫 발생 장소:</label>
                <select id="locationSelect" onchange="updateDashboard()">
                    <option value="BOTH">가정(부모) & 학교(교사) 모두</option>
                    <option value="HOME">가정 (부모님)</option>
                    <option value="SCHOOL">학교 (선생님)</option>
                </select>
            </div>

            <div class="filter-group">
                <label for="csvFileInput" style="font-size:0.82rem; color:var(--text-muted);">📁 사용자 CSV 파일 탑재:</label>
                <input type="file" id="csvFileInput" accept=".csv" onchange="handleFileUpload(event)">
                <button class="btn-reset" onclick="resetToDefaultData()">초기 데이터 복원</button>
                <button class="btn-reset" onclick="openQrModal()" style="background:#2563eb; color:#ffffff; border:none; font-weight:700;">📱 포스터용 QR 생성</button>
            </div>
        </div>

        <!-- KPI Metric Cards -->
        <div class="grid-4">
            <div class="kpi-card" style="border-left-color: #3b82f6;">
                <div class="kpi-label">전체 평균 가정(부모) 피해 경험률</div>
                <div class="kpi-value" id="kpiHomeRate">14.2%</div>
                <div class="kpi-subtext">조사 대상 청소년 평균 비율</div>
            </div>
            <div class="kpi-card" style="border-left-color: #10b981;">
                <div class="kpi-label">전체 평균 학교(교사) 피해 경험률</div>
                <div class="kpi-value" id="kpiSchoolRate">4.5%</div>
                <div class="kpi-subtext">조사 대상 청소년 평균 비율</div>
            </div>
            <div class="kpi-card" style="border-left-color: #f59e0b;">
                <div class="kpi-label">최대 피해 경험 집단</div>
                <div class="kpi-value" id="kpiMaxGroup" style="font-size: 1.25rem;">경제 하 (20.1%)</div>
                <div class="kpi-subtext" id="kpiMaxGroupSub">가정(부모님) 정서적 공격 기준</div>
            </div>
            <div class="kpi-card" style="border-left-color: #ef4444;">
                <div class="kpi-label">배경 집단 간 최대 격차</div>
                <div class="kpi-value" id="kpiGap">9.6%p</div>
                <div class="kpi-subtext" id="kpiGapSub">주관적 경제상태 (상 vs 하)</div>
            </div>
        </div>

        <!-- Balanced Chart & Table Grid -->
        <div class="grid-2">
            <!-- Visualization Card -->
            <div class="card">
                <div class="card-title">
                    <span>📈 배경 특성별 피해 경험 비율 시각화</span>
                    <span style="font-size:0.75rem; color:var(--text-muted);">↔️ 좌우 드래그 이동</span>
                </div>
                <div class="chart-scroll-wrapper" id="chartScrollWrapper">
                    <div class="chart-container" id="chartContainer">
                        <canvas id="analysisChart"></canvas>
                    </div>
                </div>
                <div class="insight-box">
                    <h4>💡 시각화 관전 포인트</h4>
                    <p id="chartInsightText">가정과 학교 모두 배경 특성에 따라 정서적 공격 경험 비율 차이가 존재하며, 전반적으로 가정(부모)에서의 경험 비율이 학교(교사)보다 상대적으로 높게 집계됩니다.</p>
                </div>
            </div>

            <!-- Summary Data Table Card -->
            <div class="card">
                <div class="card-title">
                    <span>📋 상세 데이터 분석 요약표</span>
                    <span style="font-size:0.75rem; color:var(--text-muted);">KOSIS 정제 데이터</span>
                </div>
                <div class="table-responsive">
                    <table id="dataTable">
                        <thead>
                            <tr>
                                <th>배경 구분</th>
                                <th>세부 항목</th>
                                <th>가정 (%)</th>
                                <th>학교 (%)</th>
                                <th>비율 시각화 (0~100%)</th>
                            </tr>
                        </thead>
                        <tbody id="tableBody">
                            <!-- Dynamically filled by JS -->
                        </tbody>
                    </table>
                </div>
                <div class="insight-box">
                    <h4>🔍 수치 집계 요약</h4>
                    <p id="tableInsightText">성적 하위 집단과 경제적 하위 집단에서 상대적으로 피해 경험 응답 비율이 다소 높게 나타나는 패턴이 관찰됩니다.</p>
                </div>
            </div>
        </div>
    </section>

    
    <!-- Poster Section 6: Research Findings in Detail -->
    <section class="card">
        <div>
            <span class="card-header-badge">SECTION 6</span>
            <div class="card-title">6. 연구 결과 및 주요 근거 요약</div>
            <div id="dynamicResearchFindings" class="card-body" style="display:flex; flex-direction:column; gap:12px;">
                <!-- Dynamically populated by JS updateResearchFindings() -->
            </div>
        </div>
    </section>

    <!-- Poster Section 7: Conclusion & Limitations -->
    <div class="grid-2">
        <section class="card">
            <div>
                <span class="card-header-badge">SECTION 7-A</span>
                <div class="card-title">7. 결론 및 정책적 제언</div>
                <div id="dynamicConclusions" class="card-body">
                    <!-- Dynamically populated by JS updateConclusions() -->
                </div>
            </div>
        </section>

        <section class="limitation-card card" style="justify-content:flex-start;">
            <span class="card-header-badge" style="background:#fef3c7; color:#d97706;">SECTION 7-B</span>
            <h3>⚠️ 데이터 한계 및 윤리적 유의사항</h3>
            <ul>
                <li><strong>주관적 자기보고 데이터:</strong> 설문 응답자의 주관적 인지에 의존한 데이터로 법적/객관적 아동학대 판단 기준과는 차이가 존재합니다.</li>
                <li><strong>인과관계 추론의 경계:</strong> 성적·경제적 수준과 정서적 피해 간의 상관관계는 관찰되나 이를 일방적인 원인-결과로 단정할 수 없습니다.</li>
                <li><strong>낙인 효과 방지:</strong> 특정 배경 그룹에 대한 편견이나 낙인을 정당화하는 근거로 오용되어서는 안 됩니다.</li>
            </ul>
        </section>
    </div>

    <!-- Footer -->
    <footer>
        <p>본 고등학교 학술 탐구 포스터 대시보드는 KOSIS 국가통계포털 공공데이터를 기반으로 제작되었습니다.</p>
        <p>© 2026 청소년 사회탐구 프로젝트 팀 | 데이터 원본: <code>가정과_학교에서_성인으로부터의_정서적_공격_피해_경험_20260820194451.csv</code></p>
    </footer>
</div>

<div id="toast" class="toast-msg"></div>

<!-- QR Code Modal Component -->
<div id="qrModal" style="display:none; position:fixed; inset:0; background:rgba(15,23,42,0.6); backdrop-filter:blur(4px); z-index:2000; align-items:center; justify-content:center;">
    <div style="background:#ffffff; padding:24px; border-radius:16px; max-width:420px; width:90%; text-align:center; box-shadow:0 20px 25px -5px rgba(0,0,0,0.1);">
        <h3 style="margin-bottom:8px; font-size:1.15rem; color:#0f172a; font-weight:800;">📱 학술 포스터용 QR 코드 생성기</h3>
        <p style="font-size:0.84rem; color:#475569; margin-bottom:16px; line-height:1.4;">
            웹에 배포한 URL(GitHub Pages, Netlify 등)을 입력하시면 실물 포스터 부착용 QR 코드가 자동으로 생성됩니다.
        </p>
        <input type="text" id="qrUrlInput" placeholder="예: https://my-username.github.io/poster" style="width:100%; padding:10px 14px; margin-bottom:14px; border:1px solid #cbd5e1; border-radius:8px; font-size:0.88rem; outline:none;">
        <div style="margin-bottom:16px; display:flex; justify-content:center; align-items:center; min-height:200px; background:#f8fafc; border-radius:12px; border:2px dashed #cbd5e1;">
            <img id="qrCodeImg" src="" alt="QR Code Preview" style="display:none; width:180px; height:180px; border-radius:8px;">
            <span id="qrPlaceholder" style="font-size:0.85rem; color:#94a3b8;">URL을 입력하고 [QR 생성] 버튼을 누르세요.</span>
        </div>
        <div style="display:flex; gap:8px; justify-content:center;">
            <button onclick="generateQRCode()" style="background:#2563eb; color:#ffffff; padding:8px 16px; border:none; border-radius:8px; cursor:pointer; font-weight:700; font-size:0.85rem;">QR 생성</button>
            <button onclick="downloadQRCode()" style="background:#10b981; color:#ffffff; padding:8px 16px; border:none; border-radius:8px; cursor:pointer; font-weight:700; font-size:0.85rem;">이미지 저장</button>
            <button onclick="closeQrModal()" style="background:#f1f5f9; color:#475569; padding:8px 16px; border:1px solid #cbd5e1; border-radius:8px; cursor:pointer; font-size:0.85rem;">닫기</button>
        </div>
    </div>
</div>

<script>
    function openQrModal() {
        const modal = document.getElementById('qrModal');
        const urlInput = document.getElementById('qrUrlInput');
        if (window.location.href && !window.location.href.startsWith('about:') && !window.location.href.startsWith('file:')) {
            urlInput.value = window.location.href;
        }
        modal.style.display = 'flex';
    }

    function closeQrModal() {
        document.getElementById('qrModal').style.display = 'none';
    }

    function generateQRCode() {
        const url = document.getElementById('qrUrlInput').value.trim();
        if (!url) {
            showToast('⚠️ QR 코드로 생성할 URL을 입력해주세요.');
            return;
        }
        const qrImg = document.getElementById('qrCodeImg');
        const placeholder = document.getElementById('qrPlaceholder');
        
        const qrApiUrl = `https://api.qrserver.com/v1/create-qr-code/?size=250x250&data=${encodeURIComponent(url)}`;
        qrImg.src = qrApiUrl;
        qrImg.onload = function() {
            qrImg.style.display = 'block';
            placeholder.style.display = 'none';
            showToast('✅ QR 코드가 성공적으로 생성되었습니다!');
        };
    }

    function downloadQRCode() {
        const qrImg = document.getElementById('qrCodeImg');
        if (!qrImg.src || qrImg.style.display === 'none') {
            showToast('⚠️ 먼저 QR 코드를 생성해주세요.');
            return;
        }
        const a = document.createElement('a');
        a.href = qrImg.src;
        a.download = 'poster_qr_code.png';
        a.target = '_blank';
        document.body.appendChild(a);
        a.click();
        document.body.removeChild(a);
    }

    /* Global Data Store representing KOSIS CSV Structure */
    const DEFAULT_KOSIS_DATA = [
        { category1: "성별", category2: "남학생", homeRate: 12.8, schoolRate: 5.1 },
        { category1: "성별", category2: "여학생", homeRate: 15.7, schoolRate: 3.9 },
        { category1: "학교급", category2: "초등학생(4~6)", homeRate: 11.5, schoolRate: 3.2 },
        { category1: "학교급", category2: "중학생", homeRate: 16.4, schoolRate: 5.3 },
        { category1: "학교급", category2: "고등학생", homeRate: 14.8, schoolRate: 4.8 },
        { category1: "학업성적", category2: "상", homeRate: 11.2, schoolRate: 3.4 },
        { category1: "학업성적", category2: "중", homeRate: 13.9, schoolRate: 4.3 },
        { category1: "학업성적", category2: "하", homeRate: 18.6, schoolRate: 6.1 },
        { category1: "경제적수준", category2: "상", homeRate: 10.5, schoolRate: 3.1 },
        { category1: "경제적수준", category2: "중", homeRate: 13.8, schoolRate: 4.2 },
        { category1: "경제적수준", category2: "하", homeRate: 20.1, schoolRate: 7.2 }
    ];

    let currentDataset = [...DEFAULT_KOSIS_DATA];
    let chartCanvas = null;
    let ctx = null;
    let isDragging = false;
    let startX = 0;
    let scrollLeft = 0;

    window.onload = function() {
        chartCanvas = document.getElementById('analysisChart');
        ctx = chartCanvas.getContext('2d');
        
        setupDragToScroll();

        window.addEventListener('resize', () => {
            updateDashboard();
        });

        updateDashboard();
    };

    function setupDragToScroll() {
        const wrapper = document.getElementById('chartScrollWrapper');
        if (!wrapper) return;

        wrapper.addEventListener('mousedown', (e) => {
            isDragging = true;
            startX = e.pageX - wrapper.offsetLeft;
            scrollLeft = wrapper.scrollLeft;
        });

        wrapper.addEventListener('mouseleave', () => {
            isDragging = false;
        });

        wrapper.addEventListener('mouseup', () => {
            isDragging = false;
        });

        wrapper.addEventListener('mousemove', (e) => {
            if (!isDragging) return;
            e.preventDefault();
            const x = e.pageX - wrapper.offsetLeft;
            const walk = (x - startX) * 1.5;
            wrapper.scrollLeft = scrollLeft - walk;
        });
    }

    function showToast(msg) {
        const toast = document.getElementById('toast');
        toast.innerText = msg;
        toast.style.display = 'block';
        setTimeout(() => {
            toast.style.display = 'none';
        }, 3000);
    }

    function updateDashboard() {
        const bgFilter = document.getElementById('bgVariableSelect').value;
        const locFilter = document.getElementById('locationSelect').value;

        // Filter data
        let filteredData = currentDataset;
        if (bgFilter !== 'ALL') {
            filteredData = currentDataset.filter(d => d.category1 === bgFilter);
        }

        // 1. Update Key Metrics (KPIs)
        calculateKPIs(currentDataset, filteredData);

        // 2. Render Table
        renderTable(filteredData, locFilter);

        // 3. Render Canvas Chart with dynamic responsive width
        renderChart(filteredData, locFilter);

        // 4. Update dynamic insights
        updateInsights(bgFilter, filteredData);

        // 5. Update dynamic research findings section
        updateResearchFindings(currentDataset, filteredData, bgFilter);

        // 6. Update dynamic conclusions section
        updateConclusions(currentDataset, filteredData, bgFilter);
    }

    function updateConclusions(allData, filteredData, bgFilter) {
        const container = document.getElementById('dynamicConclusions');
        if (!container) return;

        if (!filteredData || filteredData.length === 0) {
            container.innerHTML = '<p style="color:var(--text-muted);">결론을 도출할 수 있는 데이터가 없습니다.</p>';
            return;
        }

        // Find max home group and max school group in current selection
        let maxHomeItem = filteredData[0];
        let maxSchoolItem = filteredData[0];
        filteredData.forEach(d => {
            if ((d.homeRate || 0) > (maxHomeItem.homeRate || 0)) maxHomeItem = d;
            if ((d.schoolRate || 0) > (maxSchoolItem.schoolRate || 0)) maxSchoolItem = d;
        });

        const avgHomeVal = filteredData.reduce((acc, d) => acc + (d.homeRate || 0), 0) / filteredData.length;
        const avgSchoolVal = filteredData.reduce((acc, d) => acc + (d.schoolRate || 0), 0) / filteredData.length;

        // Gap calculation
        const homeRates = filteredData.map(d => d.homeRate || 0);
        const maxHome = Math.max(...homeRates);
        const minHome = Math.min(...homeRates);
        const gapHome = (maxHome - minHome).toFixed(1);

        let mainFindingText = `성인으로부터의 정서적 공격 피해 비율은 선택된 범주(${bgFilter === 'ALL' ? '전체 집단' : bgFilter})에서 배경 특성에 따른 차이를 보입니다.`;
        if (avgHomeVal > avgSchoolVal) {
            mainFindingText += ` 특히 학교(${avgSchoolVal.toFixed(1)}%) 대비 가정(${avgHomeVal.toFixed(1)}%)에서의 피해 경험 비율이 상대적으로 더 높게 나타났습니다.`;
        } else if (avgSchoolVal > avgHomeVal) {
            mainFindingText += ` 특히 가정(${avgHomeVal.toFixed(1)}%) 대비 학교(${avgSchoolVal.toFixed(1)}%)에서의 피해 경험 비율이 상대적으로 더 높게 나타났습니다.`;
        } else {
            mainFindingText += ` 가정과 학교에서의 피해 경험 비율이 유사한 수준으로 관찰되었습니다.`;
        }

        let html = `
            <ul class="info-list">
                <li>
                    <strong>연구 질문에 대한 답:</strong> ${mainFindingText}
                    ${gapHome > 0 ? ` 분석 대상 집단 내 최대 격차는 <strong>${gapHome}%p</strong>로 확인됩니다.` : ''}
                </li>
                <li>
                    <strong>맞춤형 정서 지원 체계 강화:</strong> 
                    ${avgHomeVal >= avgSchoolVal ? 
                        `가정 내 피해 경험 비율(${avgHomeVal.toFixed(1)}%)이 높게 나타나는 특성을 반영하여, 가정 내 올바른 대화법 교육 프로그램 및 가정 방문 심리 상담 지원 확대가 시급합니다.` : 
                        `학교 내 피해 경험 비율(${avgSchoolVal.toFixed(1)}%)이 높게 나타나는 특성을 반영하여, 교원 대상 정서적 인권 존중 교육 강화 및 교내 심리 상담 안전망 확충이 요구됩니다.`}
                </li>
                <li>
                    <strong>고위험 취약 집단 집중 케어:</strong> 
                    가정 피해 기준 최대 수치를 기록한 <strong>${maxHomeItem.category1} - ${maxHomeItem.category2} (${maxHomeItem.homeRate}%)</strong> 집단과 같이 정서적 취약성이 집중되는 청소년 그룹을 우선 발굴하고 맞춤형 케어 솔루션을 제공할 필요가 있습니다.
                </li>
            </ul>
        `;

        container.innerHTML = html;
    }

    function updateResearchFindings(allData, filteredData, bgFilter) {
        const container = document.getElementById('dynamicResearchFindings');
        if (!container) return;

        if (!filteredData || filteredData.length === 0) {
            container.innerHTML = '<p style="color:var(--text-muted);">분석할 수 있는 유효한 데이터가 없습니다.</p>';
            return;
        }

        // 1. Home vs School Average & Ratio Calculation
        const avgHomeVal = filteredData.reduce((acc, d) => acc + (d.homeRate || 0), 0) / filteredData.length;
        const avgSchoolVal = filteredData.reduce((acc, d) => acc + (d.schoolRate || 0), 0) / filteredData.length;
        
        const avgHome = avgHomeVal.toFixed(1);
        const avgSchool = avgSchoolVal.toFixed(1);
        const ratio = avgSchoolVal > 0 ? (avgHomeVal / avgSchoolVal).toFixed(1) : '-';

        // Find Max Home & Max School items
        let maxHomeItem = filteredData[0];
        let maxSchoolItem = filteredData[0];
        filteredData.forEach(d => {
            if ((d.homeRate || 0) > (maxHomeItem.homeRate || 0)) maxHomeItem = d;
            if ((d.schoolRate || 0) > (maxSchoolItem.schoolRate || 0)) maxSchoolItem = d;
        });

        let html = `
            <div>
                <strong style="color:var(--primary-dark); font-size:0.95rem;">1. 발생 장소별 실태 비교 (가정 vs 학교):</strong>
                <p style="margin-top:4px; font-size:0.9rem; line-height:1.5;">
                    분석 대상 그룹 평균 기준, 가정(부모) 내 정서적 공격 피해 비율은 <strong>${avgHome}%</strong>, 학교(교사) 내 피해 비율은 <strong>${avgSchool}%</strong>로 측정되었습니다. 
                    ${ratio !== '-' ? `가정에서의 피해 경험률이 학교 대비 약 <strong>${ratio}배</strong> 높게 나타나는 특징을 보입니다.` : ''}
                    <br><span style="font-size:0.85rem; color:var(--text-muted);">(최고 피해 경험 집단 — 가정: <strong>${maxHomeItem.category2} ${maxHomeItem.homeRate}%</strong> / 학교: <strong>${maxSchoolItem.category2} ${maxSchoolItem.schoolRate}%</strong>)</span>
                </p>
            </div>
            <div>
                <strong style="color:var(--primary-dark); font-size:0.95rem;">2. 배경 변수별 세부 분석 결과:</strong>
                <ul class="info-list" style="margin-top:6px;">
        `;

        // 2. Category-based Breakdown
        const categories = Array.from(new Set(filteredData.map(d => d.category1)));

        categories.forEach(cat => {
            const catData = filteredData.filter(d => d.category1 === cat);
            if (catData.length === 0) return;

            let highestHome = catData[0];
            let lowestHome = catData[0];
            catData.forEach(d => {
                if ((d.homeRate || 0) > (highestHome.homeRate || 0)) highestHome = d;
                if ((d.homeRate || 0) < (lowestHome.homeRate || 0)) lowestHome = d;
            });

            const gapHome = ((highestHome.homeRate || 0) - (lowestHome.homeRate || 0)).toFixed(1);
            const itemsSummary = catData.map(d => `<strong>${d.category2}</strong>(가정 ${d.homeRate}%, 학교 ${d.schoolRate}%)`).join(', ');

            html += `
                <li>
                    <strong>[${cat}]</strong> ${itemsSummary}. 
                    <br><span style="font-size:0.83rem; color:var(--text-muted);">└ 가정 피해 최곳값: <strong>${highestHome.category2} (${highestHome.homeRate}%)</strong>, 집단 내 최대 격차: <strong>${gapHome}%p</strong></span>
                </li>
            `;
        });

        html += `
                </ul>
            </div>
        `;

        container.innerHTML = html;
    }

    function calculateKPIs(allData, filteredData) {
        if (!allData || allData.length === 0) return;
        const targetSet = filteredData && filteredData.length > 0 ? filteredData : allData;

        // Calculate averages safely with 100% clamp
        const avgHomeVal = allData.reduce((acc, cur) => acc + (cur.homeRate || 0), 0) / allData.length;
        const avgSchoolVal = allData.reduce((acc, cur) => acc + (cur.schoolRate || 0), 0) / allData.length;
        
        const avgHome = Math.min(100, Math.max(0, avgHomeVal)).toFixed(1);
        const avgSchool = Math.min(100, Math.max(0, avgSchoolVal)).toFixed(1);

        document.getElementById('kpiHomeRate').innerText = `${avgHome}%`;
        document.getElementById('kpiSchoolRate').innerText = `${avgSchool}%`;

        // Find max rate item in target dataset safely
        let maxItem = targetSet[0];
        targetSet.forEach(item => {
            if ((item.homeRate || 0) > (maxItem.homeRate || 0)) maxItem = item;
        });

        const safeMaxHome = Math.min(100, Math.max(0, maxItem.homeRate || 0));
        document.getElementById('kpiMaxGroup').innerText = `${maxItem.category2} (${safeMaxHome}%)`;
        document.getElementById('kpiMaxGroupSub').innerText = `${maxItem.category1} 집단 (가정 피해 기준)`;

        // Calculate max gap in filtered dataset safely
        const rates = targetSet.map(d => Math.min(100, Math.max(0, d.homeRate || 0)));
        const minRate = Math.min(...rates);
        const maxRate = Math.max(...rates);
        const gap = (maxRate - minRate).toFixed(1);

        document.getElementById('kpiGap').innerText = `${gap}%p`;
        document.getElementById('kpiGapSub').innerText = `선택한 집단 내 (최대 ${maxRate}% vs 최소 ${minRate}%)`;
    }

    function renderTable(data, locFilter) {
        const tbody = document.getElementById('tableBody');
        tbody.innerHTML = '';

        if (!data || data.length === 0) {
            tbody.innerHTML = '<tr><td colspan="5" style="text-align:center;">표시할 데이터가 없습니다.</td></tr>';
            return;
        }

        // Absolute scale base (100%) so progress bar width strictly matches actual percentage
        const maxValInSet = 100;

        data.forEach(row => {
            const tr = document.createElement('tr');
            
            const safeHome = Math.min(100, Math.max(0, row.homeRate || 0));
            const safeSchool = Math.min(100, Math.max(0, row.schoolRate || 0));

            const homeWidth = Math.min(100, Math.max(0, (safeHome / maxValInSet) * 100));
            const schoolWidth = Math.min(100, Math.max(0, (safeSchool / maxValInSet) * 100));

            let visualHtml = '';
            if (locFilter === 'BOTH' || locFilter === 'HOME') {
                visualHtml += `
                    <div style="display: flex; align-items: center; gap: 8px; margin-bottom: 4px;">
                        <span class="progress-bar-bg"><span class="progress-bar-fill" style="width:${homeWidth}%; background-color:#3b82f6;"></span></span>
                        <span style="font-size:0.75rem; color:#3b82f6; font-weight:bold; white-space: nowrap;">가정 ${safeHome}%</span>
                    </div>
                `;
            }
            if (locFilter === 'BOTH' || locFilter === 'SCHOOL') {
                visualHtml += `
                    <div style="display: flex; align-items: center; gap: 8px;">
                        <span class="progress-bar-bg"><span class="progress-bar-fill" style="width:${schoolWidth}%; background-color:#10b981;"></span></span>
                        <span style="font-size:0.75rem; color:#10b981; font-weight:bold; white-space: nowrap;">학교 ${safeSchool}%</span>
                    </div>
                `;
            }

            tr.innerHTML = `
                <td><span class="badge-tag" style="background:#e0f2fe; color:#0369a1; padding:2px 8px; border-radius:4px;">${row.category1}</span></td>
                <td><strong>${row.category2}</strong></td>
                <td>${safeHome}%</td>
                <td>${safeSchool}%</td>
                <td>${visualHtml}</td>
            `;
            tbody.appendChild(tr);
        });
    }

    function renderChart(data, locFilter) {
        const wrapper = document.getElementById('chartScrollWrapper');
        const container = document.getElementById('chartContainer');
        const wrapperWidth = wrapper.clientWidth || 450;
        const height = 290;

        const groupCount = data ? data.length : 0;
        const idealGroupWidth = 85; 
        const neededWidth = groupCount * idealGroupWidth + 80;
        const requiredWidth = Math.max(wrapperWidth, neededWidth);

        container.style.width = requiredWidth + 'px';
        container.style.height = height + 'px';

        const dpr = window.devicePixelRatio || 1;
        chartCanvas.width = requiredWidth * dpr;
        chartCanvas.height = height * dpr;
        chartCanvas.style.width = requiredWidth + 'px';
        chartCanvas.style.height = height + 'px';

        ctx.resetTransform();
        ctx.scale(dpr, dpr);

        const width = requiredWidth;
        ctx.clearRect(0, 0, width, height);

        if (!data || data.length === 0) {
            ctx.fillStyle = '#64748b';
            ctx.font = '14px sans-serif';
            ctx.textAlign = 'center';
            ctx.fillText('표시할 데이터가 없습니다.', width / 2, height / 2);
            return;
        }

        const paddingLeft = 55;
        const paddingRight = 25;
        const paddingTop = 40;
        const paddingBottom = 60;

        const chartW = width - paddingLeft - paddingRight;
        const chartH = height - paddingTop - paddingBottom;

        // Balance layout for small group counts to avoid awkward empty side spaces
        let effectiveChartW = chartW;
        let startOffsetX = paddingLeft;

        const maxGroupWidth = 130;
        if (groupCount > 0 && (chartW / groupCount) > maxGroupWidth) {
            effectiveChartW = groupCount * maxGroupWidth;
            startOffsetX = paddingLeft + (chartW - effectiveChartW) / 2;
        }

        let maxDataVal = 10;
        data.forEach(item => {
            if (locFilter === 'BOTH' || locFilter === 'HOME') maxDataVal = Math.max(maxDataVal, item.homeRate || 0);
            if (locFilter === 'BOTH' || locFilter === 'SCHOOL') maxDataVal = Math.max(maxDataVal, item.schoolRate || 0);
        });

        let maxY = Math.min(100, Math.ceil((maxDataVal * 1.22) / 5) * 5);
        if (maxY < 10) maxY = 10;
        const ySteps = 5;

        ctx.strokeStyle = '#e2e8f0';
        ctx.lineWidth = 1;
        ctx.fillStyle = '#64748b';
        ctx.font = '11px sans-serif';
        ctx.textAlign = 'right';

        for (let i = 0; i <= ySteps; i++) {
            const val = Math.round((maxY / ySteps) * i * 10) / 10;
            const y = paddingTop + chartH - (val / maxY) * chartH;

            ctx.beginPath();
            ctx.moveTo(paddingLeft, y);
            ctx.lineTo(width - paddingRight, y);
            ctx.stroke();

            ctx.fillText(`${val}%`, paddingLeft - 8, y + 4);
        }

        const groupWidth = effectiveChartW / groupCount;
        const barWidth = locFilter === 'BOTH' ? Math.min(22, groupWidth * 0.32) : Math.min(32, groupWidth * 0.45);

        data.forEach((item, idx) => {
            const groupCenterX = startOffsetX + idx * groupWidth + groupWidth / 2;

            if (locFilter === 'BOTH') {
                const homeH = Math.min(chartH, Math.max(0, (item.homeRate / maxY) * chartH));
                const homeX = groupCenterX - barWidth - 3;
                const homeY = paddingTop + chartH - homeH;

                ctx.fillStyle = '#3b82f6';
                drawRoundedRect(ctx, homeX, homeY, barWidth, homeH, 4);
                
                ctx.fillStyle = '#1d4ed8';
                ctx.textAlign = 'center';
                ctx.font = 'bold 10.5px sans-serif';
                ctx.fillText(`${item.homeRate}%`, homeX + barWidth/2, Math.max(paddingTop - 5, homeY - 4));

                const schoolH = Math.min(chartH, Math.max(0, (item.schoolRate / maxY) * chartH));
                const schoolX = groupCenterX + 3;
                const schoolY = paddingTop + chartH - schoolH;

                ctx.fillStyle = '#10b981';
                drawRoundedRect(ctx, schoolX, schoolY, barWidth, schoolH, 4);

                ctx.fillStyle = '#047857';
                ctx.fillText(`${item.schoolRate}%`, schoolX + barWidth/2, Math.max(paddingTop - 5, schoolY - 4));

            } else if (locFilter === 'HOME') {
                const homeH = Math.min(chartH, Math.max(0, (item.homeRate / maxY) * chartH));
                const homeX = groupCenterX - barWidth / 2;
                const homeY = paddingTop + chartH - homeH;

                ctx.fillStyle = '#3b82f6';
                drawRoundedRect(ctx, homeX, homeY, barWidth, homeH, 5);

                ctx.fillStyle = '#1d4ed8';
                ctx.textAlign = 'center';
                ctx.font = 'bold 11px sans-serif';
                ctx.fillText(`${item.homeRate}%`, groupCenterX, Math.max(paddingTop - 5, homeY - 5));

            } else if (locFilter === 'SCHOOL') {
                const schoolH = Math.min(chartH, Math.max(0, (item.schoolRate / maxY) * chartH));
                const schoolX = groupCenterX - barWidth / 2;
                const schoolY = paddingTop + chartH - schoolH;

                ctx.fillStyle = '#10b981';
                drawRoundedRect(ctx, schoolX, schoolY, barWidth, schoolH, 5);

                ctx.fillStyle = '#047857';
                ctx.textAlign = 'center';
                ctx.font = 'bold 11px sans-serif';
                ctx.fillText(`${item.schoolRate}%`, groupCenterX, Math.max(paddingTop - 5, schoolY - 5));
            }

            ctx.fillStyle = '#1e293b';
            ctx.font = 'bold 11px sans-serif';
            ctx.textAlign = 'center';
            
            const labelStr = item.category2;
            ctx.fillText(labelStr, groupCenterX, paddingTop + chartH + 18);

            const selectVal = document.getElementById('bgVariableSelect').value;
            if (selectVal === 'ALL') {
                ctx.fillStyle = '#64748b';
                ctx.font = '10px sans-serif';
                ctx.fillText(`(${item.category1})`, groupCenterX, paddingTop + chartH + 34);
            }
        });

        drawLegend(width, paddingTop, locFilter);
    }

    /* Helper function to draw rounded bar */
    function drawRoundedRect(ctx, x, y, width, height, radius) {
        if (height <= 0) return;
        ctx.beginPath();
        ctx.moveTo(x, y + height);
        ctx.lineTo(x, y + radius);
        ctx.arcTo(x, y, x + radius, y, radius);
        ctx.lineTo(x + width - radius, y);
        ctx.arcTo(x + width, y, x + width, y + radius, radius);
        ctx.lineTo(x + width, y + height);
        ctx.closePath();
        ctx.fill();
    }

    /* Helper function to draw chart legend */
    function drawLegend(width, paddingTop, locFilter) {
        const legendY = 20;
        ctx.textAlign = 'left';
        ctx.font = '12px sans-serif';

        if (locFilter === 'BOTH' || locFilter === 'HOME') {
            ctx.fillStyle = '#3b82f6';
            ctx.fillRect(width - 210, legendY - 10, 14, 14);
            ctx.fillStyle = '#334155';
            ctx.fillText('가정 (부모님)', width - 190, legendY);
        }

        if (locFilter === 'BOTH' || locFilter === 'SCHOOL') {
            const startX = locFilter === 'BOTH' ? width - 100 : width - 210;
            ctx.fillStyle = '#10b981';
            ctx.fillRect(startX, legendY - 10, 14, 14);
            ctx.fillStyle = '#334155';
            ctx.fillText('학교 (선생님)', startX + 20, legendY);
        }
    }

    function updateInsights(bgFilter, data) {
        const chartInsight = document.getElementById('chartInsightText');
        const tableInsight = document.getElementById('tableInsightText');

        if (bgFilter === '성별') {
            chartInsight.innerText = "성별 비교: 가정에서의 정서적 공격 피해 경험은 여학생(15.7%)이 남학생(12.8%)보다 높게 집계된 반면, 학교에서는 남학생(5.1%)이 여학생(3.9%)보다 상대적으로 높게 집계되었습니다.";
            tableInsight.innerText = "성별에 따른 피해 발생 장소의 미세한 패턴 차이가 관찰되나, 전반적으로 가정에서의 경험 비율이 학교에 비해 높다는 공통점이 있습니다.";
        } else if (bgFilter === '학교급') {
            chartInsight.innerText = "학교급 비교: 중학생 집단에서 가정(16.4%) 및 학교(5.3%) 모두 정서적 공격 피해 응답 비율이 가장 높게 관찰되며, 사춘기 및 학교급 전환기의 심리적 특성이 반영되었을 가능성이 있습니다.";
            tableInsight.innerText = "초등학생(4~6학년)에 비해 중·고등학생 연령대에서 정서적 공격 인지 및 경험 비율이 높게 나타납니다.";
        } else if (bgFilter === '학업성적') {
            chartInsight.innerText = "학업성적 비교: 학업 성적이 '상'(11.2%)에서 '하'(18.6%)로 낮아질수록 가정에서의 정서적 공격 경험 응답 비율이 지속적으로 상승하는 경향이 관찰됩니다.";
            tableInsight.innerText = "학업 스트레스 및 성적 관련 갈등이 가정 내 정서적 공격 경험 인지 수준에 영향을 미쳤을 가능성을 참고해 볼 수 있습니다.";
        } else if (bgFilter === '경제적수준') {
            chartInsight.innerText = "주관적 경제상태 비교: 경제 상태 '하' 집단(가정 20.1%, 학교 7.2%)이 '상' 집단(가정 10.5%, 학교 3.1%)에 비해 피해 경험 응답 비율이 2배 가량 높은 격차를 보입니다.";
            tableInsight.innerText = "가정의 경제적 취약성이 청소년이 경험하는 정서적 안녕과 스트레스 환경에 직간접적인 연관을 줄 수 있음을 보여줍니다.";
        } else {
            chartInsight.innerText = "전체 종합 비교: 모든 배경 특성에 걸쳐 가정(부모) 내 정서적 공격 경험률이 학교(교사) 대비 높게 관찰되며, 특히 주관적 경제 수준 및 학업 성적 하위 집단에서 상대적으로 높습니다.";
            tableInsight.innerText = "본 통계표는 청소년이 처한 환경적 배경에 따라 정서적 보호 체계의 필요성이 다르게 나타날 수 있음을 시사합니다.";
        }
    }

    function handleFileUpload(event) {
        const file = event.target.files[0];
        if (!file) return;

        const reader = new FileReader();
        reader.onload = function(e) {
            try {
                const csvText = e.target.result;
                const parsedData = parseCSV(csvText);
                if (parsedData.length > 0) {
                    currentDataset = parsedData;
                    updateCategoryOptions();
                    updateDashboard();
                    showToast(`✅ "${file.name}" 파일이 성공적으로 불러와졌습니다.`);
                } else {
                    showToast('⚠️ CSV 데이터 형식이 올바르지 않거나 유효한 수치 데이터가 없습니다.');
                }
            } catch (err) {
                console.error(err);
                showToast('❌ 파일 처리 중 오류가 발생했습니다.');
            }
        };
        reader.readAsText(file, 'UTF-8');
    }

    /* Helper function to parse user CSV with headers & type safety */
    function parseCSV(text) {
        const rawLines = text.split(/\r\n|\n/).map(line => line.trim()).filter(line => line !== '');
        if (rawLines.length < 2) return [];

        // Parse CSV into 2D array of trimmed string cells handling quotes
        const matrix = rawLines.map(line => {
            const cells = [];
            let current = '';
            let inQuotes = false;
            for (let i = 0; i < line.length; i++) {
                const char = line[i];
                if (char === '"') {
                    inQuotes = !inQuotes;
                } else if (char === ',' && !inQuotes) {
                    cells.push(current.trim().replace(/^"|"$/g, ''));
                    current = '';
                } else {
                    current += char;
                }
            }
            cells.push(current.trim().replace(/^"|"$/g, ''));
            return cells;
        });

        const headerKeywords = ['응답자유형', '구분', '시점', '항목', '성별', '학교급', '대분류', '소분류', '2025', '2026', '가정', '학교', '부모', '교사', '피해', '경험', '없음', '있음', '비율'];
        
        let dataStartIdx = 0;
        let homeColIdx = -1;
        let schoolColIdx = -1;
        const colHeaders = [];
        
        // Scan up to 5 top rows for headers
        for (let i = 0; i < Math.min(matrix.length, 5); i++) {
            const row = matrix[i];
            const isHeader = row.some(cell => {
                const str = cell.toLowerCase();
                return headerKeywords.some(kw => str.includes(kw)) || isNaN(parseFloat(cell));
            });

            if (isHeader) {
                dataStartIdx = i + 1;
                row.forEach((cell, cIdx) => {
                    colHeaders[cIdx] = (colHeaders[cIdx] ? colHeaders[cIdx] + ' ' : '') + cell;
                });
            } else {
                break;
            }
        }

        // Map column headers if text is explicit
        colHeaders.forEach((hdr, idx) => {
            const h = hdr.replace(/\s+/g, '');
            const isHome = h.includes('가정') || h.includes('부모');
            const isSchool = h.includes('학교') || h.includes('교사') || h.includes('선생님');
            const isNo = h.includes('없음') || h.includes('미경험');
            const isYes = h.includes('있음') || h.includes('경험함') || h.includes('피해률') || h.includes('피해경험');

            if (isHome && (isYes || (!isNo && homeColIdx === -1))) {
                homeColIdx = idx;
            } else if (isSchool && (isYes || (!isNo && schoolColIdx === -1))) {
                schoolColIdx = idx;
            }
        });

        const result = [];

        for (let i = dataStartIdx; i < matrix.length; i++) {
            const cols = matrix[i];
            if (cols.length < 3) continue;

            const cat1 = cols[0] || "일반";
            const cat2 = cols[1] || `항목${i}`;

            if (headerKeywords.some(kw => cat1.includes(kw) || cat2.includes(kw))) {
                continue;
            }

            const numbers = [];
            for (let c = 2; c < cols.length; c++) {
                const val = parseFloat(cols[c]);
                if (!isNaN(val) && val <= 1000) {
                    numbers.push(val);
                }
            }

            if (numbers.length === 0) continue;

            let home = null;
            let school = null;

            if (homeColIdx !== -1 && cols[homeColIdx] !== undefined) {
                const val = parseFloat(cols[homeColIdx]);
                if (!isNaN(val)) home = val;
            }
            if (schoolColIdx !== -1 && cols[schoolColIdx] !== undefined) {
                const val = parseFloat(cols[schoolColIdx]);
                if (!isNaN(val)) school = val;
            }

            // Fallback & Smart Pair Analysis (Distinguishing 'No Harm' vs 'Harm Experienced')
            if (home === null || school === null) {
                if (numbers.length >= 4) {
                    const sum01 = numbers[0] + numbers[1];
                    home = (sum01 >= 90 && sum01 <= 110) ? Math.min(numbers[0], numbers[1]) : numbers[0];

                    const sum23 = numbers[2] + numbers[3];
                    school = (sum23 >= 90 && sum23 <= 110) ? Math.min(numbers[2], numbers[3]) : numbers[1];
                } else if (numbers.length >= 2) {
                    const sum01 = numbers[0] + numbers[1];
                    if (sum01 >= 90 && sum01 <= 110) {
                        home = Math.min(numbers[0], numbers[1]);
                        school = numbers[2] !== undefined ? numbers[2] : 0;
                    } else {
                        home = numbers[0];
                        school = numbers[1];
                    }
                } else if (numbers.length === 1) {
                    home = numbers[0];
                    school = 0;
                }
            }

            // Safety inversion if 'No Harm' rate (>50%) was accidentally picked up instead of 'Harm Experienced'
            if (home !== null && home > 50) {
                if (numbers.length >= 2 && Math.abs(home + numbers[1] - 100) < 10) {
                    home = numbers[1];
                } else {
                    home = 100 - home;
                }
            }

            if (school !== null && school > 50) {
                if (numbers.length >= 4 && Math.abs(school + numbers[3] - 100) < 10) {
                    school = numbers[3];
                } else {
                    school = 100 - school;
                }
            }

            if (home !== null && home > 0 && home <= 1) home = home * 100;
            if (school !== null && school > 0 && school <= 1) school = school * 100;

            const safeHome = Math.min(100, Math.max(0, home !== null ? home : 0));
            const safeSchool = Math.min(100, Math.max(0, school !== null ? school : 0));

            result.push({ 
                category1: cat1, 
                category2: cat2, 
                homeRate: Math.round(safeHome * 10) / 10, 
                schoolRate: Math.round(safeSchool * 10) / 10 
            });
        }
        return result;
    }

    /* Dynamically update category select options based on current dataset */
    function updateCategoryOptions() {
        const select = document.getElementById('bgVariableSelect');
        const categories = Array.from(new Set(currentDataset.map(d => d.category1)));
        
        let html = '<option value="ALL">전체 보기 (요약 비교)</option>';
        categories.forEach(cat => {
            html += `<option value="${cat}">${cat}</option>`;
        });
        select.innerHTML = html;
        select.value = 'ALL';
    }

    function resetToDefaultData() {
        currentDataset = [...DEFAULT_KOSIS_DATA];
        document.getElementById('csvFileInput').value = '';
        updateCategoryOptions();
        document.getElementById('locationSelect').value = 'BOTH';
        updateDashboard();
        showToast('🔄 KOSIS 기본 데이터 세트로 복원되었습니다.');
    }
</script>
</body>
</html>
```
