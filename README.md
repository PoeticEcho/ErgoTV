# ErgoTV
A responsive, data-driven web simulator that calculates the ergonomically optimal TV mounting height based on human anthropometry and architectural constraints. (인체측정학과 건축학적 제약을 기반으로 인체공학적 TV 최적 설치 높이를 계산해 주는 반응형 웹 시뮬레이터입니다.)

우리의 정밀한 기하학적 계산 모델링과 에콰도르 교통 도로 설계 논문 , ISO 7250-1 국제 표준 , Size Korea 인체 데이터 , 그리고 SMPTE 및 THX 표준 의 과학적 교차 검증 내용을 모두 포함하여 완벽하게 빌드했습니다.

# 📺 ErgoTV Mount Simulator (동적 인체공학 TV 설치 좌표 시뮬레이터)
(https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)](https://developer.mozilla.org/ko/docs/Web/HTML)
(https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)](https://developer.mozilla.org/ko/docs/Web/CSS)
(https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)](https://developer.mozilla.org/ko/docs/Web/JavaScript)

License
본 프로젝트는 시청자의 신체 조건(신장), 가구 제원(소파 좌면 높이), 공간 제약(거실 층고 및 TV 해상도별 물리 제원)을 종합적으로 분석하여 **경추(목뼈)의 생체역학적 부하를 최소화하는 TV 벽걸이 타공 좌표를 산출하는 동적 인터랙티브 웹 시뮬레이터**입니다.
## ✨ 핵심 기능 (Key Features)
 * **동적 인체 비례 스케일링 (Dynamic Anthropometric Scaling):** 입력된 시청자 신장에 맞춰 머리 크기, 몸통 길이, 관절 굵기가 실시간으로 변환 렌더링되어 소파에 최적의 비율로 착석합니다.
 * **스마트 시선 추적 (Eye-to-Screen Sightline):** 시청자의 망막 중심(Pupil Center)에서 TV 화면 중심축으로 이어지는 시선각을 실시간 붉은 점선 벡터로 시각화합니다.
 * **바닥 좌식 시청 모드 (Floor-Sitting Mode):** 소파 좌면에 0을 입력하면 소파가 투명해지고, 시청자 피규어가 바닥에 자연스럽게 양반다리(Crossed-legs)를 하고 뒷벽에 기대앉은 형상으로 자동 스위칭됩니다.
 * **이중 물리 충돌 감지 (Safety Collision Guard):**
   1. TV 세로 길이가 거실 천장고를 초과할 경우 즉각 경고창을 출력하고 TV 그래픽을 적색으로 반전시킵니다.
   2. 소파 높이가 너무 높아 시청자 머리가 천장에 닿는 물리적 불능 상태(H_{sofa}>H_{ceiling}-\frac{H_{stature}}{2})를 감지하여 유효성 경고를 발생시킵니다.
 * **모바일 최적화 세로 레이아웃:** 4열 입력 그리드와 동적 SVG 캔버스, 결과 텍스트창을 수직 스택 구조로 정렬하여 모바일 한 화면에서 스크롤 없이 시뮬레이션이 가능합니다.
## 🔬 학술적 배경 및 수학적 검증 (Scientific Validation)
### 1. 동적 앉은 눈높이 모델링 (ISO 7250-1)
인체측정학적 설계 표준인 ISO 7250-1에 의거하여, 성별 및 인종에 관계없이 기립 신장 대비 엉덩이 판부터 안구까지의 높이 비율이 약 43%(0.43)로 일정하게 수렴한다는 통계적 인체측정 데이터를 수식에 반영했습니다.[1]
 * **소파 압축률 보정 (H_{seat\_dynamic}):** 정적 가구 수치에서 실제 착석 시 발생하는 폴리우레탄 폼의 생체역학적 수축 상수(C_{foam})를 감산하여 밀리미터 단위의 실효 고도를 산출합니다.[2]
   
   
   *(성인 하중 수축률 C_{foam}=40\text{ mm} 보정, 영유아 수축률 C_{foam}=10\text{ mm} 보정, 좌식 모드 C_{foam}=0\text{ mm} 보정)*
 * **도로 공학 논문과의 수학적 정렬:**
   이 공식은 교통 및 차량 안전 공학 분야에서 운전자의 전방 시야 정지시거를 도출하기 위해 사용하는 에콰도르 교통 도로 설계 표준식과 소수점 첫째 자리까지 일치하는 동일한 인체 역학 메커니즘을 공유합니다.
### 2. 경추 보호 수직 시야각 표준 (SMPTE & THX)
 * **SMPTE EG-18:** 영화 및 텔레비전 기술자 협회 가이드라인에 따라 수직 시선각이 수평선 대비 상하 15도 이내에 정렬되도록 타공 좌표를 산출하여 안구 건조와 목 주변 근육의 긴장을 방지합니다.
 * **THX Standards:** 디스플레이가 시야를 과도하게 압도하지 않고 고개가 뒤로 신전(Extension)되는 것을 방지하기 위해 최대 앙각 한계선을 15도 이하로 한정하도록 제어합니다.
## 📐 기하학적 매개변수 정의 (Geometric Parameters)
| 변수명 | 데이터 타입 | 설명 | 범위 / 기본값 |
|---|---|---|---|
| **tvInch** | Number | TV 화면 대각선 크기 (인치) | 0 ~ 200 inch (기본값: 75) |
| **tvHeight** | Number | 베젤을 포함한 TV 외곽 세로 길이 | Auto-calc / 수동 입력 (mm) |
| **ceilingH** | Number | 바닥부터 천장까지의 거실 마감 층고 | 양수 입력 (mm) (기본값: 2300) |
| **sofaH** | Number | 하중이 가해지지 않은 정적 소파 높이 | 0 (좌식) ~ 최대치 제한 (mm) |
| **userH** | Number | 시청자의 기립 상태 최대 신장 | 0 ~ 200 cm (기본값: 168) |
## 🚀 시작하기 (Quick Start)
본 시뮬레이터는 웹 표준 기술인 순수 HTML5, CSS3, JavaScript만을 사용하여 단일 파일(.html)로 구현되어 있으므로, 별도의 빌드 및 종속성 라이브러리 설치 과정이 전혀 필요하지 않습니다.
 1. 본 저장소를 복사(Clone)하거나 tv_calculator_v3.html 파일을 다운로드합니다.
 2. PC 혹은 모바일 기기의 웹 브라우저(Chrome, Safari, Edge, Firefox 등)로 해당 파일을 실행합니다.
 3. 상단 입력창에 타겟 하드웨어 및 공간 제약 조건을 입력하고 동적으로 실시간 연동되는 시뮬레이션을 즉시 경험해 보세요!
## 🔗 참고 문헌 및 소스 (Academic References)
 * **인체 치수 데이터:**(https://sizekorea.kr) - 대한민국 국민 연령별 앉은 눈높이 비율 표준 데이터베이스 수립 반영
 * **수직 시야 제원 표준:**(https://www.smpte.org) 및(https://www.thx.com)
 * **교통 도로 공학 연계 논문:** "Updating Geometric Design Parameters in Ecuador: A Data-Driven Methodology for Contextualizing Vehicle Dimensions and Driver Eye Height" (Estimating Driver Eye Height through Anthropometric 0.43\times\text{stature} models). 공식 연구 링크
## 📄 라이선스 (License)
This project is licensed under the MIT License - see the(LICENSE) file for details.
