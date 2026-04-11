<template>
  <div class="app">
    <!-- 导航 -->
    <nav class="navbar" :class="{ scrolled: isScrolled }">
      <div class="nav-inner">
        <div class="nav-logo">🔮 小六壬占卜</div>
        <div class="nav-links">
          <a href="#intro">占卜简介</a>
          <a href="#method">起卦方法</a>
          <a href="#divine" class="nav-cta">起一卦</a>
        </div>
      </div>
    </nav>

    <!-- Hero -->
    <section class="hero">
      <div class="hero-bg">
        <div class="bagua" v-for="n in 8" :key="n" :style="{ transform: `rotate(${n * 45}deg)` }"></div>
      </div>
      <div class="hero-content">
        <div class="hero-symbol">☯</div>
        <h1 class="hero-title">小六壬</h1>
        <p class="hero-sub">大安 · 留连 · 速喜 · 赤口 · 小吉 · 空亡</p>
        <p class="hero-desc">小六壬，又称马前课、诸葛马前课，是中国古代一种简便的占卜方法。<br />以时辰起卦，推算吉凶，简便易学。</p>
        <a href="#divine" class="hero-btn">🔮 立即起卦</a>
      </div>
    </section>

    <!-- 简介 -->
    <section id="intro" class="section">
      <div class="container">
        <div class="section-header">
          <span class="section-tag">📜 占卜简介</span>
          <h2 class="section-title">什么是小六壬？</h2>
        </div>
        <div class="intro-grid">
          <div class="intro-card">
            <div class="intro-icon">📖</div>
            <h3>历史渊源</h3>
            <p>小六壬相传为诸葛亮所创，又称「诸葛马前课」。是一种流传民间的简便占卜术，因其方法简单、快捷，常用于日常小事的吉凶推断。</p>
          </div>
          <div class="intro-card">
            <div class="intro-icon">🕐</div>
            <h3>以时辰起卦</h3>
            <p>小六壬以农历月、日、时辰为基础，通过简单的计算方法，从「大安、留连、速喜、赤口、小吉、空亡」六神中得出结果。</p>
          </div>
          <div class="intro-card">
            <div class="intro-icon">🎯</div>
            <h3>六神断事</h3>
            <p>六神各有吉凶属性，配合所问之事，可以推断出行、求财、婚姻、考试、疾病等日常事务的吉凶趋势。</p>
          </div>
        </div>
      </div>
    </section>

    <!-- 六神详解 -->
    <section class="section section-alt">
      <div class="container">
        <div class="section-header">
          <span class="section-tag">🔮 六神详解</span>
          <h2 class="section-title">六神吉凶</h2>
        </div>
        <div class="gods-grid">
          <div v-for="god in gods" :key="god.name" class="god-card" :class="god.type">
            <div class="god-name">{{ god.name }}</div>
            <div class="god-type-badge" :class="god.type">{{ god.type === 'good' ? '吉' : god.type === 'bad' ? '凶' : '中' }}</div>
            <div class="god-element">{{ god.element }}</div>
            <p class="god-meaning">{{ god.meaning }}</p>
            <div class="god-detail">
              <div v-for="d in god.details" :key="d.label" class="god-detail-item">
                <span class="detail-label">{{ d.label }}</span>
                <span class="detail-value">{{ d.value }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- 起卦方法 -->
    <section id="method" class="section">
      <div class="container">
        <div class="section-header">
          <span class="section-tag">📐 起卦方法</span>
          <h2 class="section-title">如何起卦？</h2>
        </div>
        <div class="method-steps">
          <div class="method-step" v-for="(step, i) in methodSteps" :key="i">
            <div class="step-circle">{{ i + 1 }}</div>
            <div class="step-content">
              <h3>{{ step.title }}</h3>
              <p>{{ step.desc }}</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- 起卦 -->
    <section id="divine" class="section section-alt">
      <div class="container">
        <div class="section-header">
          <span class="section-tag">🔮 在线起卦</span>
          <h2 class="section-title">起一卦</h2>
          <p class="section-desc">基于当前时辰自动起卦，或选择特定时辰</p>
        </div>

        <div class="divine-panel">
          <div class="current-time-info">
            <div class="time-info-row">
              <span class="time-info-label">📅 公历</span>
              <span class="time-info-value">{{ currentDateTime.solar }}</span>
            </div>
            <div class="time-info-row">
              <span class="time-info-label">🌙 农历</span>
              <span class="time-info-value">{{ currentDateTime.lunar }}</span>
            </div>
            <div class="time-info-row">
              <span class="time-info-label">🕐 时辰</span>
              <span class="time-info-value">{{ currentDateTime.shichen }}</span>
            </div>
          </div>

          <!-- 手掌起卦动画 -->
          <div v-if="showPalm" class="palm-animation">
            <div class="palm-visual">
              <svg viewBox="0 0 340 380" class="palm-svg">
                <!-- 手掌轮廓（含大拇指） -->
                <path class="palm-outline" d="M150,360 L150,220 Q150,200 155,190 L155,190 L160,120 Q160,100 170,90 Q180,80 185,90 L185,160 Q185,170 190,170 L190,80 Q190,60 200,50 Q210,40 215,50 L215,155 Q215,165 220,165 L220,90 Q220,70 230,60 Q240,50 245,60 L245,160 Q245,170 250,170 L250,110 Q250,90 260,80 Q270,70 275,80 L275,180 Q275,200 260,210 L260,360 Z" />
                <!-- 大拇指 -->
                <path class="palm-outline thumb" d="M155,195 Q145,192 135,182 Q125,172 122,160 Q119,148 125,142 Q131,136 137,142 Q148,152 153,168 Q155,175 155,182" />
                <!-- 指节线 -->
                <line class="joint-line" x1="160" y1="170" x2="185" y2="170" />
                <line class="joint-line" x1="190" y1="170" x2="215" y2="170" />
                <line class="joint-line" x1="220" y1="170" x2="245" y2="170" />
                <!-- 六神点位 -->
                <!-- 大安(吉) -->
                <circle class="palm-dot good" :class="{ active: currentDot === 0, landed: landedDots.includes(0), result: !isAnimating && finalDot === 0 }" cx="172" cy="145" r="16" />
                <text class="palm-dot-text good" :class="{ active: currentDot === 0, result: !isAnimating && finalDot === 0 }" x="172" y="150">大安</text>
                <!-- 留连(凶) -->
                <circle class="palm-dot bad" :class="{ active: currentDot === 1, landed: landedDots.includes(1), result: !isAnimating && finalDot === 1 }" cx="172" cy="105" r="16" />
                <text class="palm-dot-text bad" :class="{ active: currentDot === 1, result: !isAnimating && finalDot === 1 }" x="172" y="110">留连</text>
                <!-- 速喜(吉) -->
                <circle class="palm-dot good" :class="{ active: currentDot === 2, landed: landedDots.includes(2), result: !isAnimating && finalDot === 2 }" cx="202" cy="75" r="16" />
                <text class="palm-dot-text good" :class="{ active: currentDot === 2, result: !isAnimating && finalDot === 2 }" x="202" y="80">速喜</text>
                <!-- 赤口(凶) -->
                <circle class="palm-dot bad" :class="{ active: currentDot === 3, landed: landedDots.includes(3), result: !isAnimating && finalDot === 3 }" cx="232" cy="85" r="16" />
                <text class="palm-dot-text bad" :class="{ active: currentDot === 3, result: !isAnimating && finalDot === 3 }" x="232" y="90">赤口</text>
                <!-- 小吉(吉) -->
                <circle class="palm-dot good" :class="{ active: currentDot === 4, landed: landedDots.includes(4), result: !isAnimating && finalDot === 4 }" cx="232" cy="145" r="16" />
                <text class="palm-dot-text good" :class="{ active: currentDot === 4, result: !isAnimating && finalDot === 4 }" x="232" y="150">小吉</text>
                <!-- 空亡(凶) -->
                <circle class="palm-dot bad" :class="{ active: currentDot === 5, landed: landedDots.includes(5), result: !isAnimating && finalDot === 5 }" cx="202" cy="165" r="16" />
                <text class="palm-dot-text bad" :class="{ active: currentDot === 5, result: !isAnimating && finalDot === 5 }" x="202" y="170">空亡</text>
                <!-- 手指指示 -->
                <g v-if="isAnimating" class="finger-pointer" :transform="fingerTransform">
                  <circle cx="0" cy="-22" r="9" fill="#3498db" opacity="0.9" />
                  <line x1="0" y1="-13" x2="0" y2="0" stroke="#3498db" stroke-width="3" stroke-linecap="round" />
                </g>
              </svg>
            </div>
            <div class="palm-step-text">{{ palmStepText }}</div>
            <!-- 计算步骤展示（3行列表） -->
            <div v-if="showCalcSteps" class="calc-steps-list">
              <div class="calc-step-item">
                <span class="step-num">第一步</span>
                <span class="step-desc">从<strong>大安</strong>起，数农历月 <strong>{{ calcSteps.lunarMonth }}</strong> → 落于 <strong class="god-name">{{ calcSteps.step1God }}</strong></span>
              </div>
              <div class="calc-step-item">
                <span class="step-num">第二步</span>
                <span class="step-desc">从<strong>{{ calcSteps.step1God }}</strong>起，数农历日 <strong>{{ calcSteps.lunarDay }}</strong> → 落于 <strong class="god-name">{{ calcSteps.step2God }}</strong></span>
              </div>
              <div class="calc-step-item">
                <span class="step-num">第三步</span>
                <span class="step-desc">从<strong>{{ calcSteps.step2God }}</strong>起，数时辰 <strong>{{ calcSteps.hourName }}（{{ calcSteps.hourNum }}）</strong> → 落于 <strong :class="['god-name', 'final', calcSteps.step3Type]">{{ calcSteps.step3God }}</strong></span>
              </div>
              <div class="calc-lunar-info">
                农历 {{ calcSteps.lunarMonthChinese }}月{{ calcSteps.lunarDayChinese }} · {{ calcSteps.hourName }}
              </div>
            </div>
          </div>

          <button class="divine-btn" @click="startDivination" :disabled="isAnimating">
            <span v-if="!isAnimating">🔮 起卦断事</span>
            <span v-else class="divining">占卜中...</span>
          </button>

          <!-- 结果 -->
          <transition name="fade">
            <div v-if="result" class="result-panel">
              <div class="result-header">
                <div class="result-god" :class="result.type">
                  <div class="result-god-name">{{ result.god }}</div>
                  <div class="result-god-badge" :class="result.type">{{ result.type === 'good' ? '吉' : result.type === 'bad' ? '凶' : '平' }}</div>
                </div>
                <div class="result-info">
                  <div class="result-time">占卜时辰：{{ result.shichen }}</div>
                  <div class="result-element">五行：{{ result.element }}</div>
                </div>
              </div>

              <div class="result-meaning">
                <h3>卦象解读</h3>
                <p>{{ result.meaning }}</p>
              </div>

              <div class="result-readings">
                <h3>各项断语</h3>
                <div class="readings-grid">
                  <div v-for="r in result.readings" :key="r.label" class="reading-item" :class="r.fortune">
                    <span class="reading-icon">{{ r.fortune === 'good' ? '✅' : r.fortune === 'bad' ? '❌' : '⚠️' }}</span>
                    <span class="reading-label">{{ r.label }}</span>
                    <span class="reading-value">{{ r.value }}</span>
                  </div>
                </div>
              </div>

              <div class="result-advice">
                <h3>💡 综合建议</h3>
                <p>{{ result.advice }}</p>
              </div>
            </div>
          </transition>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="footer">
      <p>🔮 小六壬占卜 · 仅供娱乐参考，不作为任何决策依据</p>
      <p class="footer-sub">© 2026 xiaoliuren · MIT License</p>
    </footer>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { Solar } from 'lunar-typescript'

const isScrolled = ref(false)
const selectedShichen = ref(-1)
const isAnimating = ref(false)
const currentDot = ref(-1)
const landedDots = ref([])
const fingerTransform = ref('')
const palmStepText = ref('')
const showPalm = ref(false)
const finalDot = ref(-1)
const showCalcSteps = ref(false)
const calcSteps = ref({})
const result = ref(null)
const currentDateTime = ref({ solar: '', lunar: '', shichen: '' })

const shichens = [
  { name: '子时', time: '23-01' }, { name: '丑时', time: '01-03' },
  { name: '寅时', time: '03-05' }, { name: '卯时', time: '05-07' },
  { name: '辰时', time: '07-09' }, { name: '巳时', time: '09-11' },
  { name: '午时', time: '11-13' }, { name: '未时', time: '13-15' },
  { name: '申时', time: '15-17' }, { name: '酉时', time: '17-19' },
  { name: '戌时', time: '19-21' }, { name: '亥时', time: '21-23' },
]

const gods = [
  {
    name: '大安', type: 'good', element: '木 · 吉',
    meaning: '大安事事吉，求财得财利，出行保安宁，百事皆如意。',
    details: [
      { label: '求财', value: '大吉，可得' },
      { label: '出行', value: '平安顺遂' },
      { label: '婚姻', value: '大吉' },
      { label: '疾病', value: '渐愈' },
      { label: '官讼', value: '得理' },
    ]
  },
  {
    name: '留连', type: 'bad', element: '水 · 凶',
    meaning: '留连事难成，求谋费苦心，凡事多阻滞，宜守不宜进。',
    details: [
      { label: '求财', value: '难求，需等待' },
      { label: '出行', value: '不宜远行' },
      { label: '婚姻', value: '有阻碍' },
      { label: '疾病', value: '缠绵难愈' },
      { label: '官讼', value: '拖延不利' },
    ]
  },
  {
    name: '速喜', type: 'good', element: '火 · 吉',
    meaning: '速喜喜临门，求财正当时，凡事皆顺遂，好运速速来。',
    details: [
      { label: '求财', value: '吉，有喜' },
      { label: '出行', value: '大吉' },
      { label: '婚姻', value: '可成' },
      { label: '疾病', value: '速愈' },
      { label: '官讼', value: '有利' },
    ]
  },
  {
    name: '赤口', type: 'bad', element: '金 · 凶',
    meaning: '赤口主口舌，官非须防范，凡事多小心，切忌冲动行。',
    details: [
      { label: '求财', value: '有损耗' },
      { label: '出行', value: '不宜' },
      { label: '婚姻', value: '有争端' },
      { label: '疾病', value: '注意' },
      { label: '官讼', value: '凶，有口舌' },
    ]
  },
  {
    name: '小吉', type: 'good', element: '木 · 吉',
    meaning: '小吉主小顺，凡事渐称心，虽有波折在，终归得安宁。',
    details: [
      { label: '求财', value: '小有所获' },
      { label: '出行', value: '小吉' },
      { label: '婚姻', value: '可成，需耐心' },
      { label: '疾病', value: '渐安' },
      { label: '官讼', value: '可和解' },
    ]
  },
  {
    name: '空亡', type: 'bad', element: '土 · 凶',
    meaning: '空亡事落空，求谋皆不成，凡事多虚幻，宜静不宜动。',
    details: [
      { label: '求财', value: '落空' },
      { label: '出行', value: '不宜' },
      { label: '婚姻', value: '难成' },
      { label: '疾病', value: '反复' },
      { label: '官讼', value: '不利' },
    ]
  },
]

const methodSteps = [
  { title: '确定时辰', desc: '以占卜时的农历月、日、时辰为基础。时辰对应十二地支：子丑寅卯辰巳午未申酉戌亥。' },
  { title: '月日相加', desc: '将农历月份与日期相加，得出第一个数。若超过 6 则取余数（余 0 为 6）。' },
  { title: '再加时辰', desc: '将上一步的数与时辰序号相加，若超过 6 则取余数。此为第二个数。' },
  { title: '三数定宫', desc: '将两个数再相加，取余数定宫。从「大安」起顺数，即得所落之宫。' },
]

// 小六壬算法
const godsOrder = ['大安', '留连', '速喜', '赤口', '小吉', '空亡']
const godsInfo = {
    '大安': {
      type: 'good', element: '木',
      meaning: '大安事事吉，求财得财利，出行保安宁，百事皆如意。此卦为大吉之象，诸事顺遂，心想事成。',
      readings: [
        { label: '求财', value: '财运亨通，正财偏财皆有所获', fortune: 'good' },
        { label: '出行', value: '一路平安，逢凶化吉', fortune: 'good' },
        { label: '婚姻', value: '天作之合，美满幸福', fortune: 'good' },
        { label: '事业', value: '贵人相助，步步高升', fortune: 'good' },
        { label: '健康', value: '身体安康，无忧无虑', fortune: 'good' },
      ],
      advice: '当前运势极佳，适合积极行动。无论是求财、出行还是谋划大事，都是好时机。把握机会，大胆前行！'
    },
    '留连': {
      type: 'bad', element: '水',
      meaning: '留连事难成，求谋费苦心。凡事多阻滞，进退两难中。此卦为凶象，宜守不宜进，耐心等待时机。',
      readings: [
        { label: '求财', value: '财源受阻，暂难获得', fortune: 'bad' },
        { label: '出行', value: '行程多阻，不宜远行', fortune: 'bad' },
        { label: '婚姻', value: '缘分未到，多有波折', fortune: 'bad' },
        { label: '事业', value: '进展缓慢，需多忍耐', fortune: 'bad' },
        { label: '健康', value: '注意调养，勿操劳过度', fortune: 'bad' },
      ],
      advice: '当前运势低迷，不宜冒进。凡事三思而后行，保守为上。静待时机转变，方可有所作为。'
    },
    '速喜': {
      type: 'good', element: '火',
      meaning: '速喜喜临门，好运速速来。凡事皆顺遂，喜事频频见。此卦为吉象，尤其利于急事、喜事。',
      readings: [
        { label: '求财', value: '财运速至，意外之喜', fortune: 'good' },
        { label: '出行', value: '出行大吉，逢喜相逢', fortune: 'good' },
        { label: '婚姻', value: '喜事将近，良缘天成', fortune: 'good' },
        { label: '事业', value: '捷报频传，功成名就', fortune: 'good' },
        { label: '健康', value: '身体康健，精神焕发', fortune: 'good' },
      ],
      advice: '好运当头！适合积极行动，尤其利于考试、求职、签约等事宜。喜事将近，保持好心态！'
    },
    '赤口': {
      type: 'bad', element: '金',
      meaning: '赤口主口舌，是非须防范。冲动易生祸，三思保平安。此卦为凶象，须谨言慎行。',
      readings: [
        { label: '求财', value: '恐有损耗，谨慎理财', fortune: 'bad' },
        { label: '出行', value: '途中多事，暂缓为佳', fortune: 'bad' },
        { label: '婚姻', value: '恐有争执，需多沟通', fortune: 'bad' },
        { label: '事业', value: '小人当道，谨防口舌', fortune: 'bad' },
        { label: '健康', value: '注意安全，防意外伤', fortune: 'bad' },
      ],
      advice: '当前需格外谨慎，控制情绪，避免与人争执。凡事忍让为上，切忌冲动行事。守口如瓶，静待风平浪静。'
    },
    '小吉': {
      type: 'good', element: '木',
      meaning: '小吉主小顺，渐入佳境中。虽非大富贵，平安即是福。此卦为小吉，诸事平稳向好。',
      readings: [
        { label: '求财', value: '小有收获，积少成多', fortune: 'good' },
        { label: '出行', value: '平安无事，小有收获', fortune: 'good' },
        { label: '婚姻', value: '感情平稳，渐入佳境', fortune: 'good' },
        { label: '事业', value: '稳中有进，厚积薄发', fortune: 'good' },
        { label: '健康', value: '无大碍，注意保养', fortune: 'good' },
      ],
      advice: '运势平稳向好，虽无大喜，也无大忧。适合循序渐进，踏实做事。保持耐心，好事自然来。'
    },
    '空亡': {
      type: 'bad', element: '土',
      meaning: '空亡事落空，一切皆成空。求谋皆不遂，万事不如意。此卦为大凶，凡事不宜。',
      readings: [
        { label: '求财', value: '财帛空亡，不宜投资', fortune: 'bad' },
        { label: '出行', value: '徒劳无功，宜静不宜动', fortune: 'bad' },
        { label: '婚姻', value: '缘分未至，恐成空花', fortune: 'bad' },
        { label: '事业', value: '事与愿违，暂缓计划', fortune: 'bad' },
        { label: '健康', value: '注意身体，宜多休养', fortune: 'bad' },
      ],
      advice: '当前运势极低，万事不宜强求。宜静养身心，韬光养晦。待运势好转后再做打算，切忌急躁冒进。'
    },
  }

function useCurrentTime() {
  const now = new Date()
  const hour = now.getHours()
  // 子时: 23-1, 丑时: 1-3, ...
  let idx
  if (hour === 23 || hour === 0) idx = 0
  else idx = Math.ceil(hour / 2)
  selectedShichen.value = idx

  // 计算当前日期时间信息
  const solar = Solar.fromYmd(now.getFullYear(), now.getMonth() + 1, now.getDate())
  const lunar = solar.getLunar()
  const y = now.getFullYear()
  const m = String(now.getMonth() + 1).padStart(2, '0')
  const d = String(now.getDate()).padStart(2, '0')
  const weekDays = ['日', '一', '二', '三', '四', '五', '六']
  const weekDay = weekDays[now.getDay()]
  currentDateTime.value = {
    solar: `${y}年${m}月${d}日 星期${weekDay}`,
    lunar: `${lunar.getYearInChinese()}年${lunar.getMonthInChinese()}月${lunar.getDayInChinese()}`,
    shichen: `${shichens[idx].name}（第${idx + 1}个，${shichens[idx].time}点）`
  }
}


// 六神点位坐标（与 SVG 中的 cx, cy 对应）
const dotPositions = [
  { x: 172, y: 145, name: '大安' },
  { x: 172, y: 105, name: '留连' },
  { x: 202, y: 75,  name: '速喜' },
  { x: 232, y: 85,  name: '赤口' },
  { x: 232, y: 145, name: '小吉' },
  { x: 202, y: 165, name: '空亡' },
]

function sleep(ms) { return new Promise(r => setTimeout(r, ms)) }

async function animateFinger(sequence) {
  currentDot.value = -1
  landedDots.value = []
  palmStepText.value = '起卦中...'

  for (let i = 0; i < sequence.length; i++) {
    const dotIdx = sequence[i]
    currentDot.value = dotIdx
    const pos = dotPositions[dotIdx]
    fingerTransform.value = `translate(${pos.x}, ${pos.y})`
    palmStepText.value = `第${i + 1}步：${pos.name}`

    await sleep(350)

    if (i < sequence.length - 1) {
      landedDots.value.push(dotIdx)
    }
  }

  // 最后一个点位闪烁
  await sleep(500)
  palmStepText.value = `结果：${dotPositions[sequence[sequence.length - 1]].name}`
  await sleep(600)
}

function startDivination() {
  if (isAnimating.value) return

  const hourIndex = selectedShichen.value >= 0 ? selectedShichen.value : (() => {
    const h = new Date().getHours()
    if (h === 23 || h === 0) return 0
    return Math.ceil(h / 2)
  })()

  if (selectedShichen.value < 0) {
    selectedShichen.value = hourIndex
  }

  isAnimating.value = true
  result.value = null
  showPalm.value = true
  finalDot.value = -1
  showCalcSteps.value = false
  calcSteps.value = {}

  // 获取农历月日
  const now = new Date()
  const solar = Solar.fromYmd(now.getFullYear(), now.getMonth() + 1, now.getDate())
  const lunar = solar.getLunar()
  const lunarMonth = lunar.getMonth()
  const lunarDay = lunar.getDay()
  const lunarMonthChinese = lunar.getMonthInChinese()
  const lunarDayChinese = lunar.getDayInChinese()

  // 小六壬起卦算法（正确版）
  // 六神顺序：0大安 1留连 2速喜 3赤口 4小吉 5空亡
  // 第一步：从大安(0)起，数农历月，落于 step1
  const step1 = (lunarMonth - 1) % 6  // 月=1→大安(0), 月=2→留连(1)...
  // 第二步：从step1起，数农历日，落于 step2
  const step2 = (step1 + lunarDay - 1) % 6
  // 第三步：从step2起，数时辰序号(子=1,丑=2...)，落于 step3
  const hourNum = hourIndex + 1
  const step3 = (step2 + hourNum - 1) % 6

  // 生成手指跳动序列
  const sequence = []
  for (let i = 0; i < lunarMonth; i++) sequence.push(i % 6)
  for (let i = 0; i < lunarDay; i++) sequence.push((step1 + i) % 6)
  for (let i = 0; i < hourNum; i++) sequence.push((step2 + i) % 6)

  // 执行动画后显示结果
  animateFinger(sequence).then(() => {
    const godName = godsOrder[step3]
    const info = godsInfo[godName]

    finalDot.value = step3
    showCalcSteps.value = true
    calcSteps.value = {
      lunarMonth, lunarDay,
      lunarMonthChinese, lunarDayChinese,
      hourName: shichens[hourIndex].name,
      hourNum,
      step1God: godsOrder[step1],
      step2God: godsOrder[step2],
      step3God: godName,
      step3Type: info.type,
    }

    result.value = {
      god: godName,
      type: info.type,
      element: info.element,
      shichen: shichens[hourIndex].name,
      meaning: info.meaning,
      readings: info.readings,
      advice: info.advice,
      steps: [step1, step2, step3]
    }
    isAnimating.value = false
    currentDot.value = -1
    landedDots.value = []
  })
}

function handleScroll() {
  isScrolled.value = window.scrollY > 50
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
  useCurrentTime()
})

onUnmounted(() => window.removeEventListener('scroll', handleScroll))
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Noto+Serif+SC:wght@400;600;700;900&family=Noto+Sans+SC:wght@300;400;500;600&display=swap');

:root {
  --primary: #1a1a2e;
  --gold: #d4a853;
  --gold-light: #f0d68a;
  --red: #c0392b;
  --green: #27ae60;
  --bg: #faf8f5;
  --bg-alt: #f0ece4;
  --text: #2c2c2c;
  --text-dim: #777;
  --border: #e0dcd4;
  --shadow: 0 4px 20px rgba(0,0,0,0.06);
  --radius: 16px;
}

* { margin: 0; padding: 0; box-sizing: border-box; }

body {
  font-family: 'Noto Sans SC', sans-serif;
  background: var(--bg);
  color: var(--text);
  -webkit-font-smoothing: antialiased;
}

a { color: inherit; text-decoration: none; }
</style>

<style scoped>
/* Navbar */
.navbar { position: fixed; top: 0; left: 0; right: 0; z-index: 100; padding: 16px 0; transition: all 0.3s; }
.navbar .nav-logo { color: #fff; }
.navbar .nav-links a { color: rgba(255,255,255,0.7); }
.navbar .nav-links a:hover { color: #fff; }
.navbar .nav-cta { background: rgba(255,255,255,0.9) !important; color: var(--primary) !important; }
.navbar.scrolled .nav-logo { color: var(--primary); }
.navbar.scrolled .nav-links a { color: var(--text-dim); }
.navbar.scrolled .nav-links a:hover { color: var(--primary); }
.navbar.scrolled .nav-cta { background: var(--primary) !important; color: #fff !important; }
.navbar.scrolled {
  background: rgba(250,248,245,0.95); backdrop-filter: blur(12px);
  box-shadow: 0 2px 12px rgba(0,0,0,0.06); padding: 10px 0;
}
.nav-inner {
  max-width: 1100px; margin: 0 auto; padding: 0 24px;
  display: flex; justify-content: space-between; align-items: center;
}
.nav-logo {
  font-family: 'Noto Serif SC', serif; font-weight: 700;
  font-size: 1.15rem; color: var(--primary);
  transition: color 0.3s;
}
.nav-links { display: flex; gap: 28px; align-items: center; }
.nav-links a { font-size: 0.88rem; font-weight: 500; transition: color 0.3s; }
.nav-links a:hover { color: var(--primary); }
.nav-cta {
  padding: 8px 20px; border-radius: 25px; font-weight: 600 !important;
  transition: all 0.3s;
}

/* Hero */
.hero {
  min-height: 100vh; display: flex; align-items: center; justify-content: center;
  position: relative; overflow: hidden;
  background: linear-gradient(180deg, #1a1a2e 0%, #16213e 40%, #0f3460 100%);
  text-align: center; color: #fff; padding: 80px 24px;
}
.hero-bg { position: absolute; inset: 0; pointer-events: none; }
.bagua {
  position: absolute; top: 50%; left: 50%;
  width: 500px; height: 500px; margin: -250px 0 0 -250px;
  border: 1px solid rgba(212,168,83,0.08); border-radius: 50%;
  transform-origin: center;
}
.hero-content { position: relative; z-index: 1; }
.hero-symbol { font-size: 4rem; margin-bottom: 16px; opacity: 0.9; }
.hero-title {
  font-family: 'Noto Serif SC', serif; font-size: 4rem; font-weight: 900;
  letter-spacing: 8px; margin-bottom: 12px;
  background: linear-gradient(135deg, var(--gold-light), var(--gold));
  -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
}
.hero-sub {
  font-size: 1.1rem; color: rgba(212,168,83,0.8); margin-bottom: 20px;
  letter-spacing: 4px; font-weight: 300;
}
.hero-desc {
  color: rgba(255,255,255,0.6); font-size: 0.95rem; line-height: 1.8;
  margin-bottom: 36px; max-width: 500px; margin-left: auto; margin-right: auto;
}
.hero-btn {
  display: inline-block; background: linear-gradient(135deg, var(--gold), var(--gold-light));
  color: var(--primary); padding: 14px 40px; border-radius: 30px;
  font-weight: 700; font-size: 1.05rem; transition: all 0.3s;
  box-shadow: 0 4px 20px rgba(212,168,83,0.3);
}
.hero-btn:hover { transform: translateY(-2px); box-shadow: 0 6px 30px rgba(212,168,83,0.4); }

/* Sections */
.section { padding: 80px 24px; }
.section-alt { background: var(--bg-alt); }
.container { max-width: 1100px; margin: 0 auto; }
.section-header { text-align: center; margin-bottom: 48px; }
.section-tag {
  display: inline-block; background: rgba(212,168,83,0.1); color: var(--gold);
  padding: 5px 16px; border-radius: 20px; font-size: 0.82rem; font-weight: 600;
  margin-bottom: 12px; border: 1px solid rgba(212,168,83,0.15);
}
.section-title {
  font-family: 'Noto Serif SC', serif; font-size: 2rem; font-weight: 700;
  color: var(--primary); letter-spacing: 2px;
}
.section-desc { color: var(--text-dim); font-size: 0.95rem; margin-top: 8px; }

/* Intro */
.intro-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 24px; }
.intro-card {
  background: #fff; border-radius: var(--radius); padding: 32px;
  box-shadow: var(--shadow); transition: all 0.3s; border: 1px solid var(--border);
}
.intro-card:hover { transform: translateY(-4px); box-shadow: 0 8px 30px rgba(0,0,0,0.1); }
.intro-icon { font-size: 2.2rem; margin-bottom: 16px; }
.intro-card h3 {
  font-family: 'Noto Serif SC', serif; font-size: 1.15rem; margin-bottom: 10px;
}
.intro-card p { color: var(--text-dim); font-size: 0.9rem; line-height: 1.8; }

/* Gods */
.gods-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px; }
.god-card {
  background: #fff; border-radius: var(--radius); padding: 28px;
  box-shadow: var(--shadow); border: 2px solid var(--border); transition: all 0.3s;
}
.god-card:hover { transform: translateY(-4px); }
.god-card.good { border-color: rgba(39,174,96,0.3); }
.god-card.bad { border-color: rgba(192,57,43,0.3); }
.god-card.neutral { border-color: rgba(212,168,83,0.3); }

.god-name {
  font-family: 'Noto Serif SC', serif; font-size: 1.5rem; font-weight: 700;
  display: inline-block;
}
.god-type-badge {
  display: inline-block; padding: 2px 12px; border-radius: 10px;
  font-size: 0.75rem; font-weight: 600; margin-left: 10px; vertical-align: middle;
}
.god-type-badge.good { background: rgba(39,174,96,0.1); color: var(--green); }
.god-type-badge.bad { background: rgba(192,57,43,0.1); color: var(--red); }
.god-type-badge.neutral { background: rgba(212,168,83,0.1); color: var(--gold); }

.god-element { color: var(--text-dim); font-size: 0.85rem; margin-top: 6px; margin-bottom: 12px; }
.god-meaning {
  font-family: 'Noto Serif SC', serif; color: var(--text);
  font-size: 0.92rem; line-height: 1.7; margin-bottom: 16px;
  padding: 12px; background: var(--bg); border-radius: 10px;
}
.god-detail-item {
  display: flex; justify-content: space-between; padding: 6px 0;
  border-bottom: 1px solid var(--border); font-size: 0.85rem;
}
.god-detail-item:last-child { border-bottom: none; }
.detail-label { color: var(--text-dim); }
.detail-value { font-weight: 500; }

/* Method */
.method-steps { max-width: 700px; margin: 0 auto; }
.method-step {
  display: flex; gap: 20px; align-items: flex-start;
  margin-bottom: 24px;
}
.step-circle {
  width: 44px; height: 44px; min-width: 44px; border-radius: 50%;
  background: linear-gradient(135deg, var(--gold), var(--gold-light));
  color: var(--primary); display: flex; align-items: center; justify-content: center;
  font-weight: 800; font-size: 1.1rem;
}
.step-content h3 { font-size: 1.05rem; margin-bottom: 4px; }
.step-content p { color: var(--text-dim); font-size: 0.9rem; line-height: 1.7; }

/* Divine */
.divine-panel {
  max-width: 700px; margin: 0 auto; background: #fff;
  border-radius: 24px; padding: 36px; box-shadow: var(--shadow);
  border: 2px solid var(--border);
}
.current-time-info {
  display: flex;
  gap: 24px;
  justify-content: center;
  flex-wrap: wrap;
  margin-bottom: 24px;
  padding: 16px 24px;
  background: var(--bg);
  border-radius: 12px;
  border: 1px solid var(--border);
}
.time-info-row {
  display: flex;
  align-items: center;
  gap: 8px;
}
.time-info-label {
  font-size: 0.9rem;
  color: var(--text-dim);
}
.time-info-value {
  font-size: 0.95rem;
  font-weight: 600;
  color: var(--text);
}

.divine-btn {
  width: 100%; padding: 18px; border-radius: 16px; border: none;
  background: linear-gradient(135deg, #1a1a2e, #16213e);
  color: var(--gold-light); font-size: 1.15rem; font-weight: 700;
  font-family: 'Noto Serif SC', serif; cursor: pointer;
  transition: all 0.3s; letter-spacing: 4px;
  box-shadow: 0 4px 20px rgba(26,26,46,0.2);
}
.divine-btn:hover:not(:disabled) {
  transform: translateY(-2px);
  box-shadow: 0 6px 30px rgba(26,26,46,0.3);
}
.divine-btn:disabled { opacity: 0.7; cursor: not-allowed; }

/* Palm Animation */
.palm-animation {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 24px;
}

.palm-visual {
  width: 240px;
  height: 280px;
  position: relative;
}

.palm-svg {
  width: 100%;
  height: 100%;
}

.palm-outline {
  fill: none;
  stroke: var(--gold);
  stroke-width: 2.5;
  stroke-linejoin: round;
  stroke-linecap: round;
  opacity: 0.6;
}

.joint-line {
  stroke: var(--gold);
  stroke-width: 1.5;
  opacity: 0.3;
}

.palm-dot {
  fill: rgba(212,168,83,0.1);
  stroke: var(--gold);
  stroke-width: 1.5;
  opacity: 0.5;
  transition: all 0.3s ease;
}

.palm-dot.good {
  stroke: #27ae60;
  fill: rgba(39,174,96,0.08);
}
.palm-dot.bad {
  stroke: #c0392b;
  fill: rgba(192,57,43,0.08);
}

.palm-dot.active {
  fill: rgba(52,152,219,0.3);
  stroke: #3498db;
  stroke-width: 2.5;
  opacity: 1;
  animation: dotPulse 0.6s ease-in-out;
}

.palm-dot.landed {
  fill: rgba(212,168,83,0.2);
  stroke: var(--gold);
  stroke-width: 2;
  opacity: 0.8;
}

.palm-dot.result {
  fill: rgba(192,57,43,0.25);
  stroke: #c0392b;
  stroke-width: 2.5;
  opacity: 1;
  animation: dotGlow 2s ease-in-out infinite;
}

@keyframes dotGlow {
  0%, 100% { filter: drop-shadow(0 0 4px rgba(192,57,43,0.3)); }
  50% { filter: drop-shadow(0 0 10px rgba(192,57,43,0.6)); }
}

@keyframes dotPulse {
  0% { r: 14; }
  50% { r: 20; }
  100% { r: 14; }
}

.palm-dot-text {
  fill: var(--text-dim);
  font-size: 10px;
  text-anchor: middle;
  dominant-baseline: middle;
  font-weight: 600;
  pointer-events: none;
  transition: fill 0.3s;
}
.palm-dot-text.good { fill: #27ae60; }
.palm-dot-text.bad { fill: #c0392b; }

.palm-dot-text.active {
  fill: #3498db;
  font-size: 11px;
}

.palm-dot-text.result {
  fill: #c0392b;
  font-weight: 700;
  font-size: 11px;
}

.finger-pointer {
  transition: transform 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  filter: drop-shadow(0 2px 4px rgba(192,57,43,0.4));
}

.palm-step-text {
  margin-top: 12px;
  font-family: 'Noto Serif SC', serif;
  font-size: 1rem;
  color: var(--gold);
  font-weight: 600;
  letter-spacing: 2px;
}

.palm-fade-enter-active {
  animation: palmFadeIn 0.4s ease;
}

/* Calc Steps List */
.calc-steps-list {
  margin-top: 14px;
  padding: 16px 20px;
  background: var(--bg);
  border-radius: 12px;
  border: 1px solid var(--border);
  animation: fadeIn 0.4s ease;
}

.calc-step-item {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 10px 0;
  border-bottom: 1px dashed var(--border);
}

.calc-step-item:last-of-type {
  border-bottom: none;
}

.step-num {
  font-size: 0.78rem;
  font-weight: 700;
  color: var(--gold);
  background: rgba(212,168,83,0.1);
  padding: 3px 10px;
  border-radius: 8px;
  white-space: nowrap;
}

.step-desc {
  font-size: 0.88rem;
  color: var(--text);
  line-height: 1.6;
}

.step-desc strong {
  color: var(--primary);
}

.god-name {
  color: var(--gold);
  font-family: 'Noto Serif SC', serif;
}

.god-name.final {
  font-size: 1rem;
}
.god-name.final.good { color: #27ae60; }
.god-name.final.bad { color: #c0392b; }

.calc-lunar-info {
  text-align: center;
  margin-top: 10px;
  font-size: 0.82rem;
  color: var(--text-dim);
  font-family: 'Noto Serif SC', serif;
}
.palm-fade-leave-active {
  animation: palmFadeIn 0.3s ease reverse;
}

@keyframes palmFadeIn {
  from { opacity: 0; transform: translateY(-20px) scale(0.9); }
  to { opacity: 1; transform: translateY(0) scale(1); }
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}
.divining::before {
  content: '🔮'; display: inline-block;
  animation: spin 1s linear infinite; margin-right: 8px;
}

/* Result */
.result-panel {
  margin-top: 28px; animation: fadeIn 0.5s ease;
}
@keyframes fadeIn { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

.fade-enter-active { animation: fadeIn 0.5s ease; }
.fade-leave-active { animation: fadeIn 0.3s ease reverse; }

.result-header {
  display: flex; justify-content: space-between; align-items: center;
  padding: 24px; border-radius: 16px; margin-bottom: 20px;
}
.result-header .good { background: linear-gradient(135deg, rgba(39,174,96,0.08), rgba(39,174,96,0.02)); }
.result-header .bad { background: linear-gradient(135deg, rgba(192,57,43,0.08), rgba(192,57,43,0.02)); }

.result-god {
  padding: 16px 20px;
  border-radius: 12px;
}

.result-god-name {
  font-family: 'Noto Serif SC', serif; font-size: 2rem; font-weight: 900;
}
.result-god-badge {
  display: inline-block; padding: 4px 16px; border-radius: 12px;
  font-size: 0.85rem; font-weight: 700; margin-top: 4px;
}
.result-god-badge.good { background: var(--green); color: #fff; }
.result-god-badge.bad { background: var(--red); color: #fff; }

.result-info { text-align: right; }
.result-time, .result-element { font-size: 0.88rem; color: var(--text-dim); }

.result-meaning {
  padding: 20px; background: var(--bg); border-radius: 12px; margin-bottom: 20px;
}
.result-meaning h3 { font-size: 0.95rem; margin-bottom: 8px; }
.result-meaning p {
  font-family: 'Noto Serif SC', serif; font-size: 0.95rem;
  line-height: 1.8; color: var(--text);
}

.readings-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-bottom: 20px; }
.reading-item {
  display: flex; align-items: center; gap: 8px;
  padding: 12px 14px; border-radius: 10px; background: var(--bg);
  font-size: 0.85rem;
}
.reading-icon { font-size: 1rem; }
.reading-label { color: var(--text-dim); min-width: 40px; }
.reading-value { font-weight: 500; flex: 1; }

.result-advice {
  padding: 20px; border-radius: 12px; border: 2px solid rgba(212,168,83,0.2);
  background: rgba(212,168,83,0.03);
}
.result-advice h3 { font-size: 0.95rem; margin-bottom: 8px; }
.result-advice p { font-size: 0.9rem; line-height: 1.8; color: var(--text); }

/* Footer */
.footer {
  text-align: center; padding: 40px 24px; border-top: 1px solid var(--border);
  color: var(--text-dim); font-size: 0.85rem;
}
.footer-sub { margin-top: 6px; font-size: 0.78rem; opacity: 0.6; }

@media (max-width: 768px) {
  .hero-title { font-size: 2.8rem; letter-spacing: 4px; }
  .intro-grid, .gods-grid { grid-template-columns: 1fr; }
  .readings-grid { grid-template-columns: 1fr; }
  .result-header { flex-direction: column; gap: 12px; text-align: center; }
  .section-title { font-size: 1.6rem; }
}
</style>
