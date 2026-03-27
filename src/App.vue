<template>
  <nav class="new-sticky-header">
    <div class="container new-sticky-header-inner">
      <div class="flex" style="gap: 16px; align-items: center;">
        <!-- Logo -->
        <img src="@/assets/logo.png" alt="StratusPersona Logo" style="height: 40px; width: auto;" />
        <span class="new-header-title">Stratus<span class="brand-highlight">Persona</span></span>
      </div>
      <div class="flex" style="gap: 24px; flex-direction: column; align-items: flex-end;">
        <span style="color: #666; font-family: var(--font-mono); font-size: 0.9rem;">v1.0.0.5</span>
        <span style="color: #F7931A; font-family: var(--font-mono); font-size: 0.75rem; font-weight: 600; margin-top: -8px;">beta</span>
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

  <hr class="section-divider">

  <!-- Footer / Contact Section -->
  <footer class="container center flex-col" style="padding: 80px 5%;">
    <h2 style="font-size: 2.5rem; margin-bottom: 24px;">Ready to create your perfect persona?</h2>
    <p class="lead" style="margin-bottom: 32px;">
      Start building smarter AI agents today with StratusPersona.
    </p>
    <a href="mailto:aertislabsuk@gmail.com" class="btn btn-primary" style="margin-bottom: 60px;">
      Get Started
    </a>

    <div class="footer-links" style="text-align: center; border-top: 1px solid #333; padding-top: 32px; width: 100%;">
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
</script>
