<template>
  <div class="sidebar">
    <h3 style="margin-bottom: 24px; color: var(--primary);">Agent Configuration</h3>

    <PersonaGraph :persona="persona" />

    <div class="control-group">
      <label>Agent Name</label>
      <input type="text" v-model="persona.name" placeholder="E.g. Developer Assistant" />
    </div>

    <div class="control-group">
      <label>Role / Function</label>
      <select v-model="persona.role">
        <option value="" disabled>Select a role...</option>
        <option value="Software Developer">Software Developer</option>
        <option value="Frontend Engineer">Frontend Engineer</option>
        <option value="Data Scientist">Data Scientist</option>
        <option value="UX/UI Designer">UX/UI Designer</option>
        <option value="Product Manager">Product Manager</option>
        <option value="Accountant">Accountant</option>
        <option value="Financial Analyst">Financial Analyst</option>
        <option value="Fiction Writer">Fiction Writer</option>
        <option value="Copywriter">Copywriter</option>
        <option value="Legal Advisor">Legal Advisor</option>
        <option value="Teacher/Educator">Teacher/Educator</option>
        <option value="Customer Support Representative">Customer Support Representative</option>
        <option value="Sales Executive">Sales Executive</option>
      </select>
    </div>

    
    <div class="control-group">
      <label>Creativity</label>
      <input type="range" min="1" max="5" step="1" v-model.number="persona.creativity" class="slider" />
      <div class="flex" style="justify-content: space-between; font-size: 0.75rem; color: #888;">
        <span>Strongly Technical</span>
        <span>Strongly Creative</span>
      </div>
    </div>

    <div class="control-group">
      <label>Seriousness</label>
      <input type="range" min="1" max="5" step="1" v-model.number="persona.seriousness" class="slider" />
      <div class="flex" style="justify-content: space-between; font-size: 0.75rem; color: #888;">
        <span>Fun & Comedic</span>
        <span>Very Serious</span>
      </div>
    </div>

    <div class="control-group">
      <label>Chattiness</label>
      <input type="range" min="1" max="5" step="1" v-model.number="persona.chattiness" class="slider" />
      <div class="flex" style="justify-content: space-between; font-size: 0.75rem; color: #888;">
        <span>Verbose & Elaborate</span>
        <span>Concise & Short</span>
      </div>
    </div>

    <div class="control-group">
      <label>Autonomy</label>
      <input type="range" min="1" max="5" step="1" v-model.number="persona.autonomy" class="slider" />
      <div class="flex" style="justify-content: space-between; font-size: 0.75rem; color: #888;">
        <span>Strictly Reactive</span>
        <span>Highly Proactive</span>
      </div>
    </div>

    <div class="control-group">
      <label>Rigidity</label>
      <input type="range" min="1" max="5" step="1" v-model.number="persona.rigidity" class="slider" />
      <div class="flex" style="justify-content: space-between; font-size: 0.75rem; color: #888;">
        <span>Plain Text</span>
        <span>Highly Structured</span>
      </div>
    </div>

    <div class="control-group">
      <label>Additional Context</label>
      <textarea v-model="persona.background" rows="4" placeholder="Describe the environment or context the agent operates in..."></textarea>
    </div>

    <div class="control-group">
      <label>Constraints / Rules</label>
      <textarea v-model="persona.constraints" rows="4" placeholder="List any hard rules the agent must never break..."></textarea>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'
import PersonaGraph from './PersonaGraph.vue'

const props = defineProps({
  modelValue: {
    type: Object,
    required: true
  }
})

const emit = defineEmits(['update:modelValue'])

const persona = computed({
  get: () => props.modelValue,
  set: (val) => emit('update:modelValue', val)
})
</script>

<style scoped>
.slider {
  -webkit-appearance: none;
  width: 100%;
  height: 6px;
  border-radius: 3px;
  background: #1A1B1D;
  outline: none;
  border: 1px solid #333;
  margin: 10px 0;
  padding: 0;
}
.slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 18px;
  height: 18px;
  border-radius: 50%;
  background: var(--primary);
  cursor: pointer;
  transition: all 0.2s;
}
.slider::-webkit-slider-thumb:hover {
  transform: scale(1.2);
  box-shadow: 0 0 10px var(--primary-glow);
}
</style>
