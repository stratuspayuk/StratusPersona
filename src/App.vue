<template>
  <nav class="new-sticky-header">
    <div class="container new-sticky-header-inner">
      <div class="flex" style="gap: 16px; align-items: center;">
        <!-- Logo -->
        <img src="@/assets/logo.png" alt="StratusPersona Logo" style="height: 40px; width: auto;" />
        <span class="new-header-title">Stratus<span class="brand-highlight">Persona</span></span>
      </div>
      <div class="flex" style="gap: 24px;">
        <span style="color: #666; font-family: var(--font-mono); font-size: 0.9rem;">v1.0.0.4</span>
      </div>
    </div>
  </nav>

  <header class="container" style="margin-top: 40px; text-align: center;">
    <h1>Create your <span class="brand-highlight">AI Agent</span> Persona</h1>
    <p class="lead" style="margin-bottom: 0;">Fill in the configuration details below to effortlessly generate an optimized markdown persona file.</p>
  </header>

  <section class="container">
    <div class="interface">
      <PersonaForm v-model="personaState" />
      <MarkdownPreview :persona="personaState" />
    </div>
  </section>
</template>

<script setup>
import { reactive } from 'vue'
import PersonaForm from './components/PersonaForm.vue'
import MarkdownPreview from './components/MarkdownPreview.vue'

const personaState = reactive({
  name: '',
  role: '',
  specialisms: [],
  background: '',
  seriousness: 3,
  creativity: 3,
  chattiness: 3,
  autonomy: 3,
  rigidity: 3,
  constraints: ''
})
</script>
