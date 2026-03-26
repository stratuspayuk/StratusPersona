<template>
  <div class="graph-wrapper" @click="isZoomed = true">
    <h4 class="graph-title">Persona Graph <span>(Click to zoom)</span></h4>
    <div class="graph-container">
      <Radar :data="chartData" :options="chartOptions" />
    </div>
  </div>

  <div v-if="isZoomed" class="modal-overlay" @click="isZoomed = false">
    <div class="modal-content" style="cursor: pointer;">
      <button class="close-btn" @click="isZoomed = false">&times;</button>
      <h2>Persona Traits Explained</h2>
      
      <div class="modal-body">
        
        <div class="modal-details">
          <p>The Persona Graph maps five core behavioral traits radially on a scale of 1 to 5. The inner layers represent a score of 1, increasing outwards up to the outermost layer (5).</p>
          
          <ul>
            <li><strong>Creativity:</strong> Balances Technical logic (inner) against Creative flexibility (outer).</li>
            <li><strong>Seriousness:</strong> Measures conversational style from Fun and Comedic (inner) to Very Serious (outer).</li>
            <li><strong>Chattiness:</strong> Controls response structure from Verbose and Elaborate (inner) to Concise and Short (outer).</li>
            <li><strong>Autonomy:</strong> Dictates behavior from Strictly Reactive (inner) to Highly Proactive (outer).</li>
            <li><strong>Rigidity:</strong> Adjusts output from Plain Text (inner) to Highly Structured Markdown (outer).</li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed, ref } from 'vue'
import { Radar } from 'vue-chartjs'
import { Chart as ChartJS, RadialLinearScale, PointElement, LineElement, Filler, Tooltip, Legend } from 'chart.js'

ChartJS.register(RadialLinearScale, PointElement, LineElement, Filler, Tooltip, Legend)

const props = defineProps({
  persona: {
    type: Object,
    required: true
  }
})

const isZoomed = ref(false)

const chartData = computed(() => ({
  labels: ['Creativity', 'Seriousness', 'Chattiness', 'Autonomy', 'Rigidity'],
  datasets: [
    {
      label: 'Score',
      backgroundColor: 'rgba(247, 147, 26, 0.4)',
      borderColor: '#F7931A',
      pointBackgroundColor: '#F7931A',
      pointBorderColor: '#fff',
      pointHoverBackgroundColor: '#fff',
      pointHoverBorderColor: '#F7931A',
      borderWidth: 2,
      data: [
        props.persona.creativity,
        props.persona.seriousness,
        props.persona.chattiness,
        props.persona.autonomy,
        props.persona.rigidity
      ]
    }
  ]
}))

const createOptions = (fontSize) => ({
  responsive: true,
  maintainAspectRatio: false,
  scales: {
    r: {
      min: 0,
      max: 5,
      ticks: {
        stepSize: 1,
        display: false
      },
      grid: {
        color: 'rgba(255, 255, 255, 0.1)',
        circular: true
      },
      angleLines: {
        color: 'rgba(255, 255, 255, 0.1)'
      },
      pointLabels: {
        color: '#b0b0b0',
        font: {
          size: fontSize,
          family: 'Inter, sans-serif',
          weight: '600'
        }
      }
    }
  },
  plugins: {
    legend: { display: false },
    tooltip: { enabled: false }
  }
})

const chartOptions = createOptions(11)
</script>

<style scoped>
.graph-wrapper {
  background: #121315;
  border: 1px solid var(--border);
  border-radius: 12px;
  padding: 16px;
  margin-bottom: 24px;
  cursor: pointer;
  transition: all 0.2s;
}
.graph-wrapper:hover {
  border-color: var(--primary);
  box-shadow: 0 4px 20px rgba(247, 147, 26, 0.2);
}

.graph-title {
  color: #fff;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  font-size: 0.75rem;
  margin: 0 0 16px 0;
  text-align: center;
}
.graph-title span {
  color: var(--primary);
  text-transform: none;
  font-weight: normal;
  margin-left: 8px;
}

.graph-container {
  width: 100%;
  max-width: 250px;
  height: 250px;
  margin: 0 auto;
}

/* Modal Styles */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: rgba(0, 0, 0, 0.85);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 2000;
  backdrop-filter: blur(4px);
}

.modal-content {
  background: #0D0E10;
  border: 1px solid var(--primary);
  border-radius: 16px;
  width: 90%;
  max-width: 600px;
  padding: 32px;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.8), 0 0 30px rgba(247, 147, 26, 0.2);
  position: relative;
  animation: slideUp 0.2s ease-out;
}

@keyframes slideUp {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}

.modal-content h2 {
  color: var(--primary);
  margin-top: 0;
  margin-bottom: 24px;
  border-bottom: 1px solid #333;
  padding-bottom: 16px;
}

.close-btn {
  position: absolute;
  top: 24px;
  right: 24px;
  background: none;
  border: none;
  color: #888;
  font-size: 2rem;
  line-height: 1;
  cursor: pointer;
  transition: color 0.2s;
}
.close-btn:hover {
  color: #fff;
}

.modal-body {
  display: block;
}

.modal-details {
  color: #ccc;
  line-height: 1.6;
}
.modal-details p {
  margin-top: 0;
  margin-bottom: 24px;
  font-size: 1.05rem;
}
.modal-details ul {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 16px;
}
.modal-details li {
  background: #1A1B1D;
  padding: 16px;
  border-radius: 8px;
  font-size: 0.95rem;
  border-left: 3px solid var(--primary);
}
.modal-details strong {
  color: #fff;
  display: block;
  margin-bottom: 4px;
  font-size: 1rem;
}
</style>
