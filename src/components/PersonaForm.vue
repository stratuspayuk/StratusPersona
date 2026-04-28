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
        <option value="Oracle HCM Functional Developer">Oracle HCM Functional Developer</option>
      </select>
    </div>

    <div class="control-group" v-if="persona.role">
      <label>Specialisms (Multi-select)</label>
      <div class="multiselect-container">
        <select v-model="persona.specialisms" multiple size="5">
          <option v-for="spec in getSpecialisms()" :key="spec" :value="spec">
            {{ spec }}
          </option>
        </select>
      </div>
      <div v-if="persona.specialisms && persona.specialisms.length > 0" class="selected-tags">
        <span v-for="spec in persona.specialisms" :key="spec" class="tag">
          {{ spec }}
          <button type="button" @click="removeSpecialism(spec)" class="tag-close">×</button>
        </span>
      </div>
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

// Specialisms mapping by role
const specialismsMap = {
  'Software Developer': [
    'DevOps Engineer',
    'Database Administrator',
    'Front-end Expert',
    'Back-end Expert',
    'Full-Stack Specialist',
    'Cloud Infrastructure',
    'Mobile Development',
    'Security Specialist',
    'Performance Optimization',
    'System Architecture'
  ],
  'Frontend Engineer': [
    'UI Component Library Specialist',
    'Accessibility Expert',
    'Performance Optimization',
    'Web Animation Expert',
    'CSS Specialist',
    'JavaScript Framework Expert',
    'Testing Specialist',
    'Design System Expert',
    'TypeScript Expert',
    'Progressive Web App Specialist'
  ],
  'Data Scientist': [
    'Machine Learning Specialist',
    'Deep Learning Expert',
    'Statistics Expert',
    'Big Data Specialist',
    'Data Visualization Expert',
    'NLP Specialist',
    'Computer Vision Expert',
    'Business Analytics',
    'Predictive Modeling',
    'Data Engineering'
  ],
  'UX/UI Designer': [
    'User Research Specialist',
    'Visual Design Expert',
    'Interaction Design',
    'Accessibility Specialist',
    'Design Systems Expert',
    'Prototyping Specialist',
    'Usability Testing Expert',
    'Information Architecture',
    'Motion Design',
    'Brand Design'
  ],
  'Product Manager': [
    'Growth Strategy Specialist',
    'Data-Driven Analytics',
    'User Research Expert',
    'Roadmap Planning',
    'Stakeholder Management',
    'Competitive Analysis',
    'Market Research',
    'Product Strategy',
    'Metrics & KPI Expert',
    'Launch Specialist'
  ],
  'Accountant': [
    'Tax Specialist',
    'Audit Specialist',
    'Financial Reporting',
    'Cost Analysis',
    'Bookkeeping Expert',
    'Payroll Specialist',
    'Regulatory Compliance',
    'Corporate Accounting',
    'SQL & Data Analysis',
    'Financial Planning'
  ],
  'Financial Analyst': [
    'Equity Research',
    'Fixed Income Specialist',
    'Valuation Expert',
    'Investment Analysis',
    'Risk Analysis',
    'Forecasting Specialist',
    'Corporate Finance',
    'Commodities Specialist',
    'Portfolio Analysis',
    'Economic Analysis'
  ],
  'Fiction Writer': [
    'Fantasy Genre Specialist',
    'Science Fiction Expert',
    'Romance Author',
    'Mystery & Thriller Writer',
    'Historical Fiction',
    'Literary Fiction',
    'Young Adult Specialist',
    'Character Development',
    'Worldbuilding Expert',
    'Dialogue Specialist'
  ],
  'Copywriter': [
    'SEO Copywriter',
    'Email Marketing Specialist',
    'Advertising Copy Expert',
    'UX Writing',
    'Social Media Copy',
    'Landing Page Specialist',
    'Content Strategist',
    'Blog Writer',
    'Product Description Expert',
    'Headlines & Hooks Specialist'
  ],
  'Legal Advisor': [
    'Corporate Law Specialist',
    'Contract Specialist',
    'Intellectual Property Expert',
    'Employment Law',
    'Tax Law Specialist',
    'Real Estate Specialist',
    'Litigation Expert',
    'Compliance Specialist',
    'Regulatory Affairs',
    'Mergers & Acquisitions'
  ],
  'Teacher/Educator': [
    'Curriculum Design Expert',
    'Special Education Specialist',
    'STEM Specialist',
    'Language Arts Specialist',
    'Assessment Expert',
    'Online Learning Specialist',
    'Student Engagement Specialist',
    'Differentiation Expert',
    'Cultural Competence',
    'Technology Integration'
  ],
  'Customer Support Representative': [
    'Technical Support Specialist',
    'Chat Support Expert',
    'Email Support Specialist',
    'Phone Support Expert',
    'Complaint Resolution',
    'Product Knowledge Expert',
    'Escalation Management',
    'Multilingual Support',
    'Social Media Support',
    'Documentation Specialist'
  ],
  'Sales Executive': [
    'Enterprise Sales Specialist',
    'Account Management',
    'Sales Strategy Expert',
    'Negotiation Specialist',
    'Pipeline Management',
    'Territory Development',
    'Consultative Selling',
    'Channel Sales Expert',
    'Lead Generation Specialist',
    'Relationship Building Expert'
  ],
  'Oracle HCM Functional Developer': [
    'System Configuration',
    'Requirements Gathering and Fit-Gap Analysis',
    'Workflow and Approval Setup',
    'Security Configuration',
    'Data Load Management',
    'Reporting and Analytics',
    'Testing and Support',
    'Release Management'
  ]
}

const getSpecialisms = () => {
  return specialismsMap[persona.value.role] || []
}

const removeSpecialism = (spec) => {
  const specialisms = persona.value.specialisms || []
  const index = specialisms.indexOf(spec)
  if (index > -1) {
    specialisms.splice(index, 1)
    persona.value = { ...persona.value, specialisms: [...specialisms] }
  }
}
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

.multiselect-container {
  margin-bottom: 12px;
}

.multiselect-container select {
  width: 100%;
  padding: 8px;
  border: 1px solid var(--border-color, #333);
  border-radius: 4px;
  background-color: var(--surface);
  color: var(--text-color);
  font-family: inherit;
  cursor: pointer;
}

.multiselect-container select:focus {
  outline: none;
  border-color: var(--primary);
  box-shadow: 0 0 0 2px rgba(255, 140, 0, 0.1);
}

.multiselect-container select option {
  background-color: var(--surface);
  color: var(--text-color);
  padding: 4px;
}

.multiselect-container select option:checked {
  background: var(--primary);
  background-image: linear-gradient(var(--primary), var(--primary));
  color: white;
}

.selected-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-top: 12px;
}

.tag {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  padding: 6px 12px;
  background-color: var(--primary);
  color: white;
  border-radius: 20px;
  font-size: 0.85rem;
  font-weight: 500;
}

.tag-close {
  background: none;
  border: none;
  color: white;
  cursor: pointer;
  font-size: 1.2rem;
  padding: 0;
  display: flex;
  align-items: center;
  line-height: 1;
  transition: opacity 0.2s;
}

.tag-close:hover {
  opacity: 0.8;
}
</style>
