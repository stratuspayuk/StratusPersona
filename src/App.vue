<template>
  <nav class="new-sticky-header">
    <div class="container new-sticky-header-inner">
      <div class="flex" style="gap: 16px; align-items: center;">
        <!-- Logo -->
        <img src="@/assets/logo.png" alt="StratusPersona Logo" style="height: 40px; width: auto;" />
        <span class="new-header-title">Stratus<span class="brand-highlight">Persona</span></span>
      </div>
      <div class="version-badge">
        <span style="color: #666; font-family: var(--font-mono);">v1.0.0.5</span>
        <span style="color: #F7931A; font-family: var(--font-mono); font-weight: 600;">beta</span>
      </div>
    </div>
  </nav>

  <!-- Hero Section -->
  <header class="hero container center flex-col">
    <h1 style="text-shadow: 0 8px 24px rgba(0,0,0,1); margin-bottom: 16px;">
      Define your <span class="brand-highlight">AI Agent</span> Persona<br>
      with <span class="brand-highlight">Precision</span>
    </h1>
    <p class="lead" style="text-shadow: 0 2px 10px rgba(0,0,0,0.8); color: #ccc; margin-bottom: 32px;">
      Craft intelligent, consistent personas that guide your AI agents to deliver superior interactions and outcomes.
    </p>
    <div class="flex" style="justify-content: center;">
      <button @click="scrollToDashboard" class="btn btn-primary">
        Start Creating
      </button>
    </div>
  </header>

  <!-- Orange Border -->
  <div class="orange-divider"></div>

  <section class="container" id="dashboard-section">
    <div class="interface">
      <PersonaForm v-model="personaState" />
      <MarkdownPreview :persona="personaState" />
    </div>
  </section>

  <hr class="section-divider">

  <!-- Our Story Section -->
  <section class="container center flex-col" style="padding: 80px 5%; text-align: center;">
    <h2 style="font-size: 2.5rem; letter-spacing: -0.04em; margin-bottom: 32px; line-height: 1;">
      Build Better <span style="color: #F7931A;">AI Personas</span>
    </h2>
    <p class="lead" style="max-width: 750px; font-size: 1.25rem;">
      Unlock the full potential of AI agents with consistent, well-defined personas that drive better outcomes.
    </p>

    <!-- Collapsible Story -->
    <div style="width: 100%; max-width: 800px; text-align: left;">
      <details class="story-details">
        <summary class="flex" style="justify-content: space-between; align-items: center; cursor: pointer; padding: 16px 0; border-bottom: 1px solid #333; gap: 16px;">
          <span style="font-size: 1.25rem; font-weight: 600;">Our <span style="color: #F7931A;">Story</span></span>
          <span class="icon" style="font-size: 1.5rem; font-weight: 300; flex-shrink: 0;">+</span>
        </summary>
        <div class="story-content" style="padding: 24px 0; color: #ccc; line-height: 1.6;">
          <p style="margin-bottom: 16px;">
            StratusPersona was born from the challenge of managing complex AI agent interactions. We recognized that AI agents perform best when given clear, consistent personas that guide their behavior and responses.
          </p>
          <p style="margin-bottom: 16px;">
            Whether you're building customer support bots, content creators, or specialized domain experts, having a standardized way to define and document personas is critical to success. Each trait, specialization, and constraint matters.
          </p>
          <p>
            We built StratusPersona to provide you with an intuitive, professional tool for crafting, documenting, and managing AI agent personas. Transform your agent development process and achieve consistent, high-quality interactions at scale.
          </p>
        </div>
      </details>
    </div>
  </section>

  <!-- Footer -->
  <footer class="container center flex-col" style="padding: 40px 5%;">
    <div class="footer-links" style="text-align: center; width: 100%;">
      <p style="margin: 0 0 16px 0; color: #666;">
        &copy; Aertis Labs UK, 2026. All rights reserved.
      </p>
      <div style="display: flex; gap: 24px; justify-content: center; flex-wrap: wrap; font-size: 0.9rem;">
        <a href="#" style="color: #888; text-decoration: none;">Terms & Conditions</a>
        <a href="#" style="color: #888; text-decoration: none;">Privacy Policy</a>
        <a href="mailto:aertislabsuk@gmail.com" style="color: #888; text-decoration: none;">Contact</a>
      </div>
    </div>
  </footer>
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

const scrollToDashboard = () => {
  const element = document.getElementById('dashboard-section')
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}
</script>
