<template>
    <div class="lotto-science">
      <!-- 헤더 섹션 -->
      <div class="header">
        <h1>🧬 로또 과학연구소</h1>
        <p>세계 최첨단 확률 분석 시스템으로 당신만의 행운 번호를 도출합니다</p>
        <p class="sub-text">
          ※ 본 시스템은 MIT, 하버드, 서울대 공동 연구진이 개발한 혁신적 알고리즘을 사용합니다
        </p>
      </div>
  
      <!-- 1단계: 심층 개인 분석 -->
      <div class="process-card">
        <div class="process-title">
          <div class="process-number">1</div>
          <div class="process-name">🧬 심층 개인 분석 과학적 전략</div>
        </div>
        <div class="process-description">
          생체 정보와 성격 유형을 기반으로 개인 맞춤형 확률 모델을 구축합니다. 
          바이오리듬 분석과 뉴로마케팅 이론을 결합한 혁신적 접근법입니다.
        </div>
        
        <div class="form-grid">
          <div class="form-group">
            <label>생년월일</label>
            <input 
              type="date" 
              v-model="personalData.birthdate" 
              placeholder="YYYY-MM-DD"
            >
          </div>
          <div class="form-group">
            <label>혈액형</label>
            <select v-model="personalData.bloodtype">
              <option value="">선택하세요</option>
              <option value="A">A형</option>
              <option value="B">B형</option>
              <option value="AB">AB형</option>
              <option value="O">O형</option>
            </select>
          </div>
          <div class="form-group">
            <label>MBTI</label>
            <select v-model="personalData.mbti">
              <option value="">선택하세요</option>
              <option v-for="mbti in mbtiOptions" :key="mbti" :value="mbti">
                {{ mbti }}
              </option>
            </select>
          </div>
        </div>
        
        <button 
          class="analyze-btn" 
          :class="{ completed: analysisSteps.personal }"
          :disabled="analysisSteps.personal || isAnalyzing.personal"
          @click="analyzePersonal"
        >
          {{ getButtonText('personal', '🧬 바이오리듬 분석 시작') }}
        </button>
        
        <div v-if="showResults.personal" class="result-area">
          <div class="progress-bar">
            <div class="progress-fill" :style="{ width: progress.personal + '%' }"></div>
          </div>
          <div class="terminal" ref="terminal1"></div>
          <div v-if="results.personal" class="result-numbers">
            <div class="result-title">🧬 개인 맞춤형 바이오 번호</div>
            <div class="numbers">
              <div 
                v-for="number in results.personal.numbers" 
                :key="number" 
                class="number-ball"
              >
                {{ number }}
              </div>
            </div>
            <div class="result-description">
              {{ results.personal.description }}
            </div>
          </div>
        </div>
      </div>
  
      <!-- 2단계: 다중 전략 포트폴리오 -->
      <div class="process-card">
        <div class="process-title">
          <div class="process-number">2</div>
          <div class="process-name">🎯 다중 전략 포트폴리오 시스템</div>
        </div>
        <div class="process-description">
          게임이론, 양자역학, 딥러닝 신경망을 융합한 복합 전략으로 
          최적의 번호 조합을 도출합니다.
        </div>
        
        <button 
          class="analyze-btn" 
          :class="{ completed: analysisSteps.portfolio }"
          :disabled="analysisSteps.portfolio || isAnalyzing.portfolio"
          @click="analyzePortfolio"
        >
          {{ getButtonText('portfolio', '🤖 AI 복합 알고리즘 실행') }}
        </button>
        
        <div v-if="showResults.portfolio" class="result-area">
          <div class="progress-bar">
            <div class="progress-fill" :style="{ width: progress.portfolio + '%' }"></div>
          </div>
          <div class="terminal" ref="terminal2"></div>
          <div v-if="results.portfolio" class="result-numbers portfolio">
            <div class="result-title">🎯 AI 융합 전략 번호</div>
            <div class="numbers">
              <div 
                v-for="number in results.portfolio.numbers" 
                :key="number" 
                class="number-ball"
              >
                {{ number }}
              </div>
            </div>
            <div class="result-description">
              {{ results.portfolio.description }}
            </div>
          </div>
        </div>
      </div>
  
      <!-- 3단계: 실시간 빅데이터 분석 -->
      <div class="process-card">
        <div class="process-title">
          <div class="process-number">3</div>
          <div class="process-name">📊 실시간 빅데이터 통계 분석</div>
        </div>
        <div class="process-description">
          최근 100회차 당첨 패턴을 실시간으로 분석하여 
          통계적 우위를 점할 수 있는 번호를 추출합니다.
        </div>
        
        <button 
          class="analyze-btn" 
          :class="{ completed: analysisSteps.bigdata }"
          :disabled="analysisSteps.bigdata || isAnalyzing.bigdata"
          @click="analyzeBigData"
        >
          {{ getButtonText('bigdata', '📈 빅데이터 크롤링 시작') }}
        </button>
        
        <div v-if="showResults.bigdata" class="result-area">
          <div class="progress-bar">
            <div class="progress-fill" :style="{ width: progress.bigdata + '%' }"></div>
          </div>
          <div class="terminal" ref="terminal3"></div>
          <div v-if="results.bigdata" class="result-numbers bigdata">
            <div class="result-title">📊 빅데이터 통계 번호</div>
            <div class="numbers">
              <div 
                v-for="number in results.bigdata.numbers" 
                :key="number" 
                class="number-ball"
              >
                {{ number }}
              </div>
            </div>
            <div class="result-description">
              {{ results.bigdata.description }}
            </div>
          </div>
        </div>
      </div>
  
      <!-- 4단계: 동양 철학 융합 -->
      <div class="process-card">
        <div class="process-title">
          <div class="process-number">4</div>
          <div class="process-name">☯️ 동양철학 융합 운세 분석</div>
        </div>
        <div class="process-description">
          음양오행, 사주팔자, 서양 점성술을 AI로 분석하여 
          우주의 기운과 조화를 이루는 번호를 찾아냅니다.
        </div>
        
        <button 
          class="analyze-btn" 
          :class="{ completed: analysisSteps.philosophy }"
          :disabled="analysisSteps.philosophy || isAnalyzing.philosophy"
          @click="analyzePhilosophy"
        >
          {{ getButtonText('philosophy', '🔮 우주 에너지 스캔') }}
        </button>
        
        <div v-if="showResults.philosophy" class="result-area">
          <div class="progress-bar">
            <div class="progress-fill" :style="{ width: progress.philosophy + '%' }"></div>
          </div>
          <div class="terminal" ref="terminal4"></div>
          <div v-if="results.philosophy" class="result-numbers philosophy">
            <div class="result-title">☯️ 동서양 철학 융합 번호</div>
            <div class="numbers">
              <div 
                v-for="number in results.philosophy.numbers" 
                :key="number" 
                class="number-ball"
              >
                {{ number }}
              </div>
            </div>
            <div class="result-description">
              {{ results.philosophy.description }}
            </div>
          </div>
        </div>
      </div>
  
      <!-- 5단계: 특별 재미 요소 -->
      <div class="process-card">
        <div class="process-title">
          <div class="process-number">5</div>
          <div class="process-name">🎲 랜덤 행운 증폭 시스템</div>
        </div>
        <div class="process-description">
          순수한 확률의 힘을 믿고 우주의 무작위성을 활용한 
          예측 불가능한 행운의 번호를 생성합니다.
        </div>
        
        <button 
          class="analyze-btn" 
          :class="{ completed: analysisSteps.random }"
          :disabled="analysisSteps.random || isAnalyzing.random"
          @click="analyzeFun"
        >
          {{ getButtonText('random', '✨ 운명의 주사위 굴리기') }}
        </button>
        
        <div v-if="showResults.random" class="result-area">
          <div class="progress-bar">
            <div class="progress-fill" :style="{ width: progress.random + '%' }"></div>
          </div>
          <div class="terminal" ref="terminal5"></div>
          <div v-if="results.random" class="result-numbers random">
            <div class="result-title">🎲 순수 행운 증폭 번호</div>
            <div class="numbers">
              <div 
                v-for="number in results.random.numbers" 
                :key="number" 
                class="number-ball"
              >
                {{ number }}
              </div>
            </div>
            <div class="result-description">
              {{ results.random.description }}
            </div>
          </div>
        </div>
      </div>
  
      <!-- 최종 결과 -->
      <div v-if="showFinalResult" class="final-result">
        <h2>🏆 최종 분석 완료!</h2>
        <p>5가지 과학적 방법론으로 도출된 당신만의 행운 번호입니다</p>
        <div class="final-numbers">
          <div 
            v-for="(combo, index) in finalCombinations" 
            :key="index" 
            class="final-combo"
          >
            <div class="combo-name">{{ index + 1 }}게임: {{ combo.name }}</div>
            <div class="numbers">
              <div 
                v-for="number in combo.numbers" 
                :key="number" 
                class="number-ball"
              >
                {{ number }}
              </div>
            </div>
          </div>
        </div>
        <p class="disclaimer">
          ※ 각 번호는 서로 다른 과학적 근거를 바탕으로 생성되었습니다<br>
          ※ 본 분석 결과는 엔터테인먼트 목적이며 실제 당첨을 보장하지 않습니다
        </p>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, reactive, computed, nextTick } from 'vue'
  
  // 반응형 데이터 정의
  const personalData = reactive({
    birthdate: '',
    bloodtype: '',
    mbti: ''
  })
  
  // MBTI 옵션 배열
  const mbtiOptions = [
    'INTJ', 'INTP', 'ENTJ', 'ENTP',
    'INFJ', 'INFP', 'ENFJ', 'ENFP',
    'ISTJ', 'ISFJ', 'ESTJ', 'ESFJ',
    'ISTP', 'ISFP', 'ESTP', 'ESFP'
  ]
  
  // 분석 상태 관리
  const analysisSteps = reactive({
    personal: false,
    portfolio: false,
    bigdata: false,
    philosophy: false,
    random: false
  })
  
  const isAnalyzing = reactive({
    personal: false,
    portfolio: false,
    bigdata: false,
    philosophy: false,
    random: false
  })
  
  const showResults = reactive({
    personal: false,
    portfolio: false,
    bigdata: false,
    philosophy: false,
    random: false
  })
  
  const progress = reactive({
    personal: 0,
    portfolio: 0,
    bigdata: 0,
    philosophy: 0,
    random: 0
  })
  
  const results = reactive({
    personal: null,
    portfolio: null,
    bigdata: null,
    philosophy: null,
    random: null
  })
  
  // 터미널 참조
  const terminal1 = ref(null)
  const terminal2 = ref(null)
  const terminal3 = ref(null)
  const terminal4 = ref(null)
  const terminal5 = ref(null)
  
  // 최종 결과 관리
  const finalCombinations = ref([])
  const showFinalResult = ref(false)
  
  // 완료된 단계 수 계산
  const completedStepsCount = computed(() => {
    return Object.values(analysisSteps).filter(Boolean).length
  })
  
  /**
   * 번호 생성 함수 - 시드 기반 의사 랜덤 생성
   * @param {number} seed - 시드값
   * @param {number} count - 생성할 번호 개수
   * @returns {number[]} - 정렬된 번호 배열
   */
  function generateNumbers(seed, count = 6) {
    const numbers = new Set()
    let current = seed
    
    while (numbers.size < count) {
      current = (current * 9301 + 49297) % 233280
      const num = (current % 45) + 1
      numbers.add(num)
    }
    
    return Array.from(numbers).sort((a, b) => a - b)
  }
  
  /**
   * 터미널 타이핑 애니메이션 함수
   * @param {HTMLElement} terminal - 터미널 요소
   * @param {Array} lines - 출력할 라인 배열
   * @param {Function} callback - 완료 후 콜백
   */
  function typeCode(terminal, lines, callback) {
    let lineIndex = 0
    let currentLineElement = null
    
    function addNewLine() {
      if (lineIndex >= lines.length) {
        // 마지막 커서 제거하고 "분석중....." 애니메이션 시작
        const cursor = terminal.querySelector('.typing-cursor')
        if (cursor) cursor.remove()
        
        showAnalyzingDots(terminal, callback)
        return
      }
      
      const line = lines[lineIndex]
      currentLineElement = document.createElement('div')
      currentLineElement.className = `code-line ${line.class || ''}`
      currentLineElement.innerHTML = `${line.prefix || ''}<span class="typing-text"></span><span class="typing-cursor">_</span>`
      terminal.appendChild(currentLineElement)
      
      typeLine()
    }
    
    function typeLine() {
      const line = lines[lineIndex]
      const typingText = currentLineElement.querySelector('.typing-text')
      const cursor = currentLineElement.querySelector('.typing-cursor')
      
      let charIndex = 0
      
      function typeChar() {
        if (charIndex < line.content.length) {
          typingText.textContent = line.content.substring(0, charIndex + 1)
          charIndex++
          // 타이핑 속도 조절
          setTimeout(typeChar, Math.random() * 50 + 30)
        } else {
          // 타이핑 완료, 커서 제거하고 다음 라인으로
          cursor.remove()
          lineIndex++
          setTimeout(addNewLine, Math.random() * 300 + 200)
        }
      }
      
      typeChar()
    }
    
    terminal.innerHTML = ''
    addNewLine()
  }
  
  /**
   * 분석중 애니메이션 표시 함수
   * @param {HTMLElement} terminal - 터미널 요소
   * @param {Function} callback - 완료 후 콜백
   */
  function showAnalyzingDots(terminal, callback) {
    const analyzingElement = document.createElement('div')
    analyzingElement.className = 'code-line warning-text'
    analyzingElement.innerHTML = '[PROCESS] <span class="analyzing-text">분석중</span><span class="typing-cursor">_</span>'
    terminal.appendChild(analyzingElement)
    
    const analyzingText = analyzingElement.querySelector('.analyzing-text')
    let dotCount = 0
    
    function addDot() {
      if (dotCount < 5) {
        dotCount++
        analyzingText.textContent = '분석중' + '.'.repeat(dotCount)
        setTimeout(addDot, 1000)
      } else {
        // 분석 완료 후 최종 성공 메시지
        setTimeout(() => {
          analyzingElement.remove()
          const successElement = document.createElement('div')
          successElement.className = 'code-line success-text'
          successElement.innerHTML = '[SUCCESS] 분석 완료! <span class="typing-cursor">_</span>'
          terminal.appendChild(successElement)
          
          setTimeout(() => {
            const cursor = successElement.querySelector('.typing-cursor')
            if (cursor) cursor.remove()
            if (callback) callback()
          }, 1000)
        }, 500)
      }
    }
    
    setTimeout(addDot, 1000)
  }
  
  /**
   * 진행률 업데이트 함수
   * @param {string} type - 분석 유형
   */
  function updateProgress(type) {
    const progressInterval = setInterval(() => {
      progress[type] += Math.random() * 15 + 5
      if (progress[type] > 100) {
        progress[type] = 100
        clearInterval(progressInterval)
      }
    }, 300)
  }
  
  /**
   * 버튼 텍스트 반환 함수
   * @param {string} type - 분석 유형
   * @param {string} defaultText - 기본 텍스트
   * @returns {string} - 버튼 텍스트
   */
  function getButtonText(type, defaultText) {
    if (analysisSteps[type]) return '✅ 분석 완료'
    if (isAnalyzing[type]) return '분석 중...'
    return defaultText
  }
  
  /**
   * 1단계: 개인 분석 실행
   */
  async function analyzePersonal() {
    // 입력값 검증
    if (!personalData.birthdate || !personalData.bloodtype || !personalData.mbti) {
      alert('모든 정보를 입력해주세요!')
      return
    }
    
    // 상태 설정
    isAnalyzing.personal = true
    showResults.personal = true
    
    await nextTick()
    
    // 진행률 업데이트 시작
    updateProgress('personal')
    
    // 생년월일 파싱
    const birth = new Date(personalData.birthdate)
    const year = birth.getFullYear()
    const month = birth.getMonth() + 1
    const day = birth.getDate()
    
    // 터미널 애니메이션용 라인 데이터
    const lines = [
      { content: '로또 과학연구소 개인분석 시스템 v3.7.2', prefix: '>>> ', class: 'success-text' },
      { content: '개인 데이터 로딩 중...', prefix: '[INFO] ' },
      { content: `생년월일: ${year}-${month.toString().padStart(2, '0')}-${day.toString().padStart(2, '0')}`, prefix: '[DATA] ' },
      { content: `혈액형: ${personalData.bloodtype}형`, prefix: '[DATA] ' },
      { content: `MBTI 성향: ${personalData.mbti}`, prefix: '[DATA] ' },
      { content: '', prefix: '' },
      { content: 'DNA 헤모글로빈 주파수 분석 시작...', prefix: '[PROCESS] ', class: 'warning-text' },
      { content: `${personalData.bloodtype}_HEMOGLOBIN_FREQUENCY = calculate_freq(${personalData.bloodtype})`, prefix: '>>> ' },
      { content: `결과: ${getBloodTypeFreq(personalData.bloodtype)} Hz`, prefix: '[RESULT] ', class: 'success-text' },
      { content: '', prefix: '' },
      { content: 'MBTI 뉴런 패턴 매칭...', prefix: '[PROCESS] ', class: 'warning-text' },
      { content: `neuron_pattern = mbti_neural_map["${personalData.mbti}"]`, prefix: '>>> ' },
      { content: `for i in range(16): process_neuron(pattern[i])`, prefix: '>>> ' },
      { content: `뉴런 활성화 패턴: ${personalData.mbti} 매칭 완료`, prefix: '[RESULT] ', class: 'success-text' },
      { content: '', prefix: '' },
      { content: '바이오리듬 주기 계산...', prefix: '[PROCESS] ', class: 'warning-text' },
      { content: `days_alive = (current_date - birth_date).days`, prefix: '>>> ' },
      { content: `physical_cycle = sin(2*pi*days_alive/23)`, prefix: '>>> ' },
      { content: `emotional_cycle = sin(2*pi*days_alive/28)`, prefix: '>>> ' },
      { content: `intellectual_cycle = sin(2*pi*days_alive/33)`, prefix: '>>> ' },
      { content: `바이오리듬 동기화율: 97.3%`, prefix: '[RESULT] ', class: 'success-text' },
      { content: '', prefix: '' },
      { content: '개인 맞춤 번호 생성 중...', prefix: '[PROCESS] ', class: 'warning-text' },
      { content: `seed = hash(birthdate + bloodtype + mbti)`, prefix: '>>> ' },
      { content: `lucky_numbers = generate_personalized_numbers(seed)`, prefix: '>>> ' }
    ]
    
    // 터미널 애니메이션 실행
    typeCode(terminal1.value, lines, () => {
      setTimeout(() => {
        // 시드 생성 및 번호 생성
        const seed = birth.getTime() + personalData.bloodtype.charCodeAt(0) + personalData.mbti.charCodeAt(0)
        const numbers = generateNumbers(seed)
        
        // 결과 저장
        results.personal = {
          numbers,
          description: `${personalData.mbti} 성향과 ${personalData.bloodtype}형 혈액의 헤모글로빈 진동 주파수(${getBloodTypeFreq(personalData.bloodtype)}Hz)를 분석한 결과입니다. 개인 생체 리듬과 97.3% 일치하는 번호 조합입니다.`
        }
        
        // 최종 조합에 추가
        finalCombinations.value.push({
          name: '🧬 바이오 분석',
          numbers
        })
        
        // 상태 업데이트
        isAnalyzing.personal = false
        analysisSteps.personal = true
        
        // 모든 단계 완료 시 최종 결과 표시
        checkAllCompleted()
      }, 2000)
    })
  }
  
  /**
   * 2단계: 포트폴리오 분석 실행
   */
  async function analyzePortfolio() {
    isAnalyzing.portfolio = true
    showResults.portfolio = true
    
    await nextTick()
    updateProgress('portfolio')
    
    const lines = [
      { content: 'AI 복합 알고리즘 시스템 초기화...', prefix: '[INIT] ', class: 'success-text' },
      { content: 'import tensorflow as tf', prefix: '>>> ' },
      { content: 'import numpy as np', prefix: '>>> ' },
      { content: 'from quantum_probability import QuantumModel', prefix: '>>> ' },
      { content: 'from game_theory import NashEquilibrium', prefix: '>>> ' },
      { content: '', prefix: '' },
      { content: '게임이론 내쉬균형 계산...', prefix: '[PROCESS] ', class: 'warning-text' },
      { content: 'nash = NashEquilibrium(players=8145060, strategies=45)', prefix: '>>> ' },
      { content: 'equilibrium = nash.calculate_optimal_strategy()', prefix: '>>> ' },
      { content: '내쉬균형 수렴 완료: 97.8% 신뢰도', prefix: '[RESULT] ', class: 'success-text' },
      { content: '', prefix: '' },
      { content: '양자역학 확률 붕괴 시뮬레이션...', prefix: '[PROCESS] ', class: 'warning-text' },
      { content: 'quantum_state = create_superposition(45)', prefix: '>>> ' },
      { content: 'for i in range(10000):', prefix: '>>> ' },
      { content: '    collapsed_state = quantum_state.collapse()', prefix: '>>> ' },
      { content: '    probability_matrix[collapsed_state] += 1', prefix: '>>> ' },
      { content: '양자 확률 분포 계산 완료', prefix: '[RESULT] ', class: 'success-text' },
      { content: '', prefix: '' },
      { content: '딥러닝 신경망 예측...', prefix: '[PROCESS] ', class: 'warning-text' },
      { content: 'model = tf.keras.Sequential([', prefix: '>>> ' },
      { content: '    tf.keras.layers.Dense(256, activation="relu"),', prefix: '>>> ' },
      { content: '    tf.keras.layers.Dense(128, activation="relu"),', prefix: '>>> ' },
      { content: '    tf.keras.layers.Dense(45, activation="softmax")', prefix: '>>> ' },
      { content: '])', prefix: '>>> ' },
      { content: 'prediction = model.predict(input_data)', prefix: '>>> ' },
      { content: '신경망 예측 정확도: 94.7%', prefix: '[RESULT] ', class: 'success-text' },
      { content: '', prefix: '' },
      { content: '5가지 알고리즘 융합 중...', prefix: '[PROCESS] ', class: 'warning-text' },
      { content: 'final_result = ensemble_vote([game_theory, quantum, neural, psychology, coin_theory])', prefix: '>>> ' }
    ]
    
    typeCode(terminal2.value, lines, () => {
      setTimeout(() => {
        const seed = Date.now() % 100000
        const numbers = generateNumbers(seed)
        
        results.portfolio = {
          numbers,
          description: '게임이론(97.8%), 양자역학, 딥러닝(94.7%), 심리학, 동전이론을 융합한 결과입니다. 5가지 AI 알고리즘의 앙상블 예측 신뢰도 96.2%'
        }
        
        finalCombinations.value.push({
          name: '🎯 AI 융합',
          numbers
        })
        
        isAnalyzing.portfolio = false
        analysisSteps.portfolio = true
        checkAllCompleted()
      }, 1500)
    })
  }
  
  /**
   * 3단계: 빅데이터 분석 실행
   */
  async function analyzeBigData() {
    isAnalyzing.bigdata = true
    showResults.bigdata = true
    
    await nextTick()
    updateProgress('bigdata')
    
    const recentNumbers = [
      [4, 15, 17, 23, 27, 36], [1, 5, 8, 16, 28, 33], [7, 12, 19, 25, 31, 42],
      [3, 11, 18, 24, 30, 39], [6, 14, 21, 29, 35, 44], [2, 9, 20, 26, 34, 41]
    ]
    
    const lines = [
      { content: '빅데이터 크롤링 시스템 가동...', prefix: '[INIT] ', class: 'success-text' },
      { content: 'import pandas as pd', prefix: '>>> ' },
      { content: 'import requests', prefix: '>>> ' },
      { content: 'from bs4 import BeautifulSoup', prefix: '>>> ' },
      { content: '', prefix: '' },
      { content: '동행복권 서버 접속 중...', prefix: '[CONNECT] ', class: 'warning-text' },
      { content: 'response = requests.get("https://dhlottery.co.kr")', prefix: '>>> ' },
      { content: 'status_code: 200 OK', prefix: '[RESULT] ', class: 'success-text' },
      { content: '', prefix: '' },
      { content: '최근 100회차 데이터 수집...', prefix: '[CRAWLING] ', class: 'warning-text' },
      { content: 'for round_num in range(1084, 1184):', prefix: '>>> ' },
      { content: '    lotto_data = crawl_round_data(round_num)', prefix: '>>> ' },
      { content: '    frequency_map.update(lotto_data)', prefix: '>>> ' },
      { content: '데이터 수집 완료: 600개 번호', prefix: '[RESULT] ', class: 'success-text' },
      { content: '', prefix: '' },
      { content: '빈도 분석 실행...', prefix: '[ANALYZE] ', class: 'warning-text' },
      ...recentNumbers.slice(0, 3).map((nums, i) => ({
        content: `${1183-i}회: [${nums.join(', ')}]`, prefix: '[DATA] '
      })),
      { content: 'frequency_analysis = Counter(all_numbers)', prefix: '>>> ' },
      { content: 'hot_numbers = frequency_analysis.most_common(20)', prefix: '>>> ' },
      { content: 'cold_numbers = frequency_analysis.least_common(10)', prefix: '>>> ' },
      { content: '', prefix: '' },
      { content: '패턴 매칭 알고리즘 실행...', prefix: '[PATTERN] ', class: 'warning-text' },
      { content: 'pattern_score = calculate_pattern_score(recent_data)', prefix: '>>> ' },
      { content: 'trend_analysis = detect_trends(frequency_data)', prefix: '>>> ' },
      { content: 'statistical_optimization = optimize_probability_matrix()', prefix: '>>> ' }
    ]
    
    typeCode(terminal3.value, lines, () => {
      setTimeout(() => {
        const hotNums = [34, 12, 27, 17, 33, 43]
        const seed = hotNums.reduce((a, b) => a + b, 0) + Date.now() % 1000
        const numbers = generateNumbers(seed)
        
        results.bigdata = {
          numbers,
          description: '최근 100회차(1084~1183회) 당첨 패턴 분석 결과입니다. 실시간 빈도 분석 신뢰도 94.1%, 패턴 매칭 정확도 91.7%'
        }
        
        finalCombinations.value.push({
          name: '📊 빅데이터',
          numbers
        })
        
        isAnalyzing.bigdata = false
        analysisSteps.bigdata = true
        checkAllCompleted()
      }, 1200)
    })
  }
  
  /**
   * 4단계: 동양철학 분석 실행
   */
  async function analyzePhilosophy() {
    isAnalyzing.philosophy = true
    showResults.philosophy = true
    
    await nextTick()
    updateProgress('philosophy')
    
    // 생년월일 정보 (기본값 사용)
    const birthdate = personalData.birthdate || '1990-01-01'
    const birth = new Date(birthdate)
    const year = birth.getFullYear()
    const month = birth.getMonth() + 1
    const day = birth.getDate()
    
    const zodiac = ['쥐', '소', '호랑이', '토끼', '용', '뱀', '말', '양', '원숭이', '닭', '개', '돼지']
    const animal = zodiac[(year - 4) % 12]
    const element = ['금', '목', '수', '화', '토'][(year - 1) % 5]
    
    const lines = [
      { content: '동양철학 융합 시스템 가동...', prefix: '[INIT] ', class: 'success-text' },
      { content: 'from saju import FourPillars', prefix: '>>> ' },
      { content: 'from wuxing import FiveElements', prefix: '>>> ' },
      { content: 'from astrology import WesternAstrology', prefix: '>>> ' },
      { content: '', prefix: '' },
      { content: '사주팔자 분석...', prefix: '[SAJU] ', class: 'warning-text' },
      { content: `birth_info = {"year": ${year}, "month": ${month}, "day": ${day}}`, prefix: '>>> ' },
      { content: `animal_sign = calculate_zodiac(${year}) # ${animal}`, prefix: '>>> ' },
      { content: `element = calculate_element(${year}) # ${element}`, prefix: '>>> ' },
      { content: `사주: ${year}년생 ${animal}띠 ${element}년`, prefix: '[RESULT] ', class: 'success-text' },
      { content: '', prefix: '' },
      { content: '음양오행 기운 측정...', prefix: '[WUXING] ', class: 'warning-text' },
      { content: 'elements = {"금": 0.2, "목": 0.15, "수": 0.25, "화": 0.18, "토": 0.22}', prefix: '>>> ' },
      { content: `primary_element = "${element}"`, prefix: '>>> ' },
      { content: 'harmony_numbers = calculate_five_element_numbers()', prefix: '>>> ' },
      { content: `${element} 기운과 조화로운 번호 추출 완료`, prefix: '[RESULT] ', class: 'success-text' },
      { content: '', prefix: '' },
      { content: '서양 점성술 행성 배치 분석...', prefix: '[ASTRO] ', class: 'warning-text' },
      { content: `birth_chart = create_natal_chart(${year}, ${month}, ${day})`, prefix: '>>> ' },
      { content: 'planetary_positions = get_current_positions()', prefix: '>>> ' },
      { content: 'for planet in planets:', prefix: '>>> ' },
      { content: '    influence = calculate_influence(planet, birth_chart)', prefix: '>>> ' },
      { content: '현재 행성 배치와 출생 차트 조화도: 89.4%', prefix: '[RESULT] ', class: 'success-text' },
      { content: '', prefix: '' },
      { content: '우주 에너지 공명 주파수 탐지...', prefix: '[COSMIC] ', class: 'warning-text' },
      { content: 'cosmic_frequency = detect_universal_resonance()', prefix: '>>> ' },
      { content: 'personal_frequency = calculate_birth_frequency(birth_info)', prefix: '>>> ' },
      { content: 'resonance_match = match_frequencies(cosmic, personal)', prefix: '>>> ' },
      { content: 'harmonic_numbers = generate_cosmic_sequence(resonance_match)', prefix: '>>> ' }
    ]
    
    typeCode(terminal4.value, lines, () => {
      setTimeout(() => {
        const seed = year + month * 100 + day * 10000 + animal.charCodeAt(0)
        const numbers = generateNumbers(seed)
        
        results.philosophy = {
          numbers,
          description: `${year}년생 ${animal}띠 ${element}년의 사주와 현재 행성 배치(조화도 89.4%)를 종합 분석한 결과입니다. 우주 에너지 공명 주파수와 92.8% 일치`
        }
        
        finalCombinations.value.push({
          name: '☯️ 동양철학',
          numbers
        })
        
        isAnalyzing.philosophy = false
        analysisSteps.philosophy = true
        checkAllCompleted()
      }, 1000)
    })
  }
  
  /**
   * 5단계: 랜덤 분석 실행
   */
  async function analyzeFun() {
    isAnalyzing.random = true
    showResults.random = true
    
    await nextTick()
    updateProgress('random')
    
    const lines = [
      { content: '순수 행운 증폭 시스템 초기화...', prefix: '[INIT] ', class: 'success-text' },
      { content: 'import random', prefix: '>>> ' },
      { content: 'import quantum_randomness as qr', prefix: '>>> ' },
      { content: 'from universe import CosmicChaos', prefix: '>>> ' },
      { content: '', prefix: '' },
      { content: '우주의 무작위성 스캔...', prefix: '[CHAOS] ', class: 'warning-text' },
      { content: 'cosmic_noise = qr.sample_quantum_fluctuations()', prefix: '>>> ' },
      { content: 'entropy_level = measure_universe_entropy()', prefix: '>>> ' },
      { content: `현재 우주 엔트로피 레벨: ${(Math.random() * 100).toFixed(1)}%`, prefix: '[RESULT] ', class: 'success-text' },
      { content: '', prefix: '' },
      { content: '순수 확률 필드 생성...', prefix: '[RANDOM] ', class: 'warning-text' },
      { content: 'for i in range(1000):', prefix: '>>> ' },
      { content: '    dice_roll = quantum_dice.roll(45)', prefix: '>>> ' },
      { content: '    probability_field[dice_roll] += 1', prefix: '>>> ' },
      { content: '1000회 양자 주사위 굴리기 완료', prefix: '[RESULT] ', class: 'success-text' },
      { content: '', prefix: '' },
      { content: '행운의 파동 증폭...', prefix: '[LUCK] ', class: 'warning-text' },
      { content: 'luck_amplifier = initialize_fortune_field()', prefix: '>>> ' },
      { content: 'destiny_seed = generate_destiny_number()', prefix: '>>> ' },
      { content: 'random.seed(destiny_seed)', prefix: '>>> ' },
      { content: 'fortune_numbers = [random.randint(1, 45) for _ in range(6)]', prefix: '>>> ' },
      { content: '', prefix: '' },
      { content: '우연의 신 소환 중...', prefix: '[DIVINE] ', class: 'warning-text' },
      { content: 'goddess_fortuna = summon_fortune_goddess()', prefix: '>>> ' },
      { content: 'blessed_numbers = goddess_fortuna.bless(fortune_numbers)', prefix: '>>> ' },
      { content: 'chaos_entropy_level = measure_random_field_strength()', prefix: '>>> ' },
      { content: 'final_blessing = apply_divine_randomness(blessed_numbers)', prefix: '>>> ' }
    ]
    
    typeCode(terminal5.value, lines, () => {
      setTimeout(() => {
        const seed = Math.random() * 1000000 + Date.now() % 100000
        const numbers = generateNumbers(seed)
        
        results.random = {
          numbers,
          description: '1000회 양자 주사위와 우주 엔트로피를 활용해 생성된 순수 우연의 번호입니다. 예측 불가능성 100%, 우연의 신 축복 받음'
        }
        
        finalCombinations.value.push({
          name: '🎲 순수 행운',
          numbers
        })
        
        isAnalyzing.random = false
        analysisSteps.random = true
        checkAllCompleted()
      }, 800)
    })
  }
  
  /**
   * 혈액형별 주파수 반환
   * @param {string} bloodtype - 혈액형
   * @returns {string} - 주파수 값
   */
  function getBloodTypeFreq(bloodtype) {
    const freqMap = {
      'A': '7.32',
      'B': '8.47',
      'AB': '9.15',
      'O': '6.28'
    }
    return freqMap[bloodtype] || '7.00'
  }
  
  /**
   * 모든 단계 완료 확인 및 최종 결과 표시
   */
  function checkAllCompleted() {
    if (completedStepsCount.value === 5) {
      setTimeout(() => {
        showFinalResult.value = true
        // 최종 결과로 스크롤
        nextTick(() => {
          const finalElement = document.querySelector('.final-result')
          if (finalElement) {
            finalElement.scrollIntoView({ behavior: 'smooth' })
          }
        })
      }, 500)
    }
  }
  </script>
  
  <style scoped>
  .lotto-science {
    font-family: 'Consolas', 'Monaco', monospace;
    background: linear-gradient(135deg, #0f0f23, #1a1a2e);
    color: white;
    min-height: 100vh;
    padding: 20px;
  }
  
  .header {
    text-align: center;
    margin-bottom: 40px;
    padding: 20px;
    background: rgba(255,255,255,0.1);
    border-radius: 15px;
    backdrop-filter: blur(10px);
  }
  
  .header h1 {
    font-size: 2.5em;
    margin-bottom: 10px;
    color: #00ff41;
    text-shadow: 0 0 10px #00ff41;
  }
  
  .header p {
    font-size: 1.2em;
    opacity: 0.9;
  }
  
  .sub-text {
    font-size: 0.9em !important;
    opacity: 0.7 !important;
    margin-top: 10px;
  }
  
  .process-card {
    background: rgba(0,0,0,0.8);
    border-radius: 15px;
    padding: 25px;
    margin-bottom: 25px;
    border: 1px solid #00ff41;
    transition: all 0.3s ease;
  }
  
  .process-card:hover {
    border-color: #00ffff;
    box-shadow: 0 0 20px rgba(0,255,255,0.3);
  }
  
  .process-title {
    display: flex;
    align-items: center;
    margin-bottom: 20px;
  }
  
  .process-number {
    background: #00ff41;
    color: #000;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: bold;
    margin-right: 15px;
  }
  
  .process-name {
    font-size: 1.4em;
    font-weight: bold;
    color: #00ff41;
  }
  
  .process-description {
    margin-bottom: 20px;
    line-height: 1.6;
    color: #cccccc;
  }
  
  .form-grid {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 15px;
    margin-bottom: 20px;
  }
  
  .form-group {
    margin-bottom: 15px;
  }
  
  .form-group label {
    display: block;
    margin-bottom: 5px;
    font-weight: bold;
    color: #00ff41;
  }
  
  .form-group input, .form-group select {
    width: 100%;
    padding: 10px;
    border: 1px solid #00ff41;
    border-radius: 8px;
    background: rgba(0,0,0,0.7);
    color: #00ff41;
    font-family: 'Consolas', monospace;
  }
  
  .form-group input::placeholder {
    color: rgba(0,255,65,0.6);
  }
  
  .analyze-btn {
    background: linear-gradient(45deg, #00ff41, #00ffff);
    color: #000;
    border: none;
    padding: 12px 30px;
    border-radius: 25px;
    font-weight: bold;
    cursor: pointer;
    transition: all 0.3s ease;
    font-family: 'Consolas', monospace;
  }
  
  .analyze-btn:hover:not(:disabled) {
    transform: scale(1.05);
    box-shadow: 0 5px 15px rgba(0,255,65,0.4);
  }
  
  .analyze-btn:disabled {
    opacity: 0.5;
    cursor: not-allowed;
  }
  
  .analyze-btn.completed {
    background: linear-gradient(45deg, #00ff41, #00ffaa);
  }
  
  .result-area {
    background: rgba(0,0,0,0.9);
    border: 1px solid #00ff41;
    border-radius: 10px;
    padding: 15px;
    margin-top: 15px;
    min-height: 400px;
  }
  
  .progress-bar {
    width: 100%;
    height: 20px;
    background: rgba(0,0,0,0.5);
    border-radius: 10px;
    margin: 10px 0;
    overflow: hidden;
  }
  
  .progress-fill {
    height: 100%;
    background: linear-gradient(90deg, #00ff41, #00ffff);
    width: 0%;
    transition: width 0.5s ease;
  }
  
  .terminal {
    background: #000;
    color: #00ff41;
    padding: 20px;
    border-radius: 10px;
    min-height: 300px;
    font-family: 'Consolas', monospace;
    font-size: 12px;
    line-height: 1.4;
    overflow-y: auto;
    max-height: 400px;
    text-align: left;
  }
  
  .result-numbers {
    background: rgba(0,255,65,0.1);
    border-radius: 10px;
    padding: 15px;
    margin-top: 20px;
  }
  
  .result-numbers.portfolio {
    background: rgba(0,255,255,0.1);
  }
  
  .result-numbers.bigdata {
    background: rgba(255,165,0,0.1);
  }
  
  .result-numbers.philosophy {
    background: rgba(128,0,128,0.1);
  }
  
  .result-numbers.random {
    background: rgba(255,20,147,0.1);
  }
  
  .result-title {
    font-weight: bold;
    margin-bottom: 10px;
    color: #00ff41;
  }
  
  .result-numbers.portfolio .result-title {
    color: #00ffff;
  }
  
  .result-numbers.bigdata .result-title {
    color: #ffaa00;
  }
  
  .result-numbers.philosophy .result-title {
    color: #aa88ff;
  }
  
  .result-numbers.random .result-title {
    color: #ff69b4;
  }
  
  .numbers {
    display: flex;
    gap: 10px;
    justify-content: center;
    margin: 10px 0;
    flex-wrap: wrap;
  }
  
  .number-ball {
    width: 50px;
    height: 50px;
    background: linear-gradient(45deg, #00ff41, #00ffff);
    color: #000;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: bold;
    font-size: 1.2em;
    animation: bounce 0.5s ease;
  }
  
  .result-description {
    font-size: 0.9em;
    opacity: 0.8;
    margin-top: 10px;
    color: #cccccc;
  }
  
  .final-result {
    background: rgba(0,255,65,0.1);
    border: 2px solid #00ff41;
    border-radius: 15px;
    padding: 30px;
    text-align: center;
    margin-top: 40px;
  }
  
  .final-result h2 {
    margin-bottom: 10px;
    color: #00ff41;
  }
  
  .final-numbers {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 20px;
    margin: 20px 0;
  }
  
  .final-combo {
    background: rgba(0,0,0,0.8);
    padding: 15px;
    border-radius: 10px;
    border: 1px solid #00ff41;
  }
  
  .combo-name {
    font-weight: bold;
    margin-bottom: 10px;
    color: #00ffff;
    font-size: 0.9em;
  }
  
  .disclaimer {
    margin-top: 20px;
    font-size: 0.9em;
    opacity: 0.8;
  }
  
  /* 터미널 애니메이션 관련 스타일 */
  :deep(.code-line) {
    margin: 2px 0;
    opacity: 1;
    transition: opacity 0.2s ease;
  }
  
  :deep(.typing-cursor) {
    animation: blink 1.2s ease-in-out infinite;
    color: #00ff41;
  }
  
  :deep(.success-text) {
    color: #00ff41;
  }
  
  :deep(.warning-text) {
    color: #ffaa00;
  }
  
  :deep(.error-text) {
    color: #ff4444;
  }
  
  @keyframes blink {
    0%, 50% { opacity: 1; }
    51%, 100% { opacity: 0.3; }
  }
  
  @keyframes bounce {
    0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
    40% { transform: translateY(-20px); }
    60% { transform: translateY(-10px); }
  }
  
  /* 반응형 디자인 */
  @media (max-width: 768px) {
    .form-grid {
      grid-template-columns: 1fr;
    }
    
    .final-numbers {
      grid-template-columns: 1fr;
    }
    
    .numbers {
      justify-content: center;
    }
    
    .number-ball {
      width: 40px;
      height: 40px;
      font-size: 1em;
    }
  }
  </style>