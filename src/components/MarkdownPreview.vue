<template>
  <div class="main-view">
    <div class="code-header">
      <div class="tab">
        <div class="dot active"></div>
        <span>Generated Persona.md</span>
      </div>
    </div>

    <div class="code-content">
      <pre><code>{{ generatedMarkdown }}</code></pre>
    </div>

    <div class="action-bar">
      <button class="btn btn-primary" style="height: 36px; padding: 0 16px; font-size: 0.85rem;" @click="copyToClipboard">Copy Markdown</button>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  persona: {
    type: Object,
    required: true
  }
})

const generatedMarkdown = computed(() => {
  const p = props.persona;

  const seriMap = { 1: 'Fun and Comedic', 2: 'Fun', 3: 'Balanced', 4: 'Serious', 5: 'Very Serious' };
  const creaMap = { 1: 'Strongly Technical', 2: 'Technical', 3: 'Balanced', 4: 'Creative', 5: 'Strongly Creative' };
  const chatMap = { 1: 'Verbose and Elaborate', 2: 'Detailed', 3: 'Balanced', 4: 'Concise', 5: 'Concise and Short' };
  const autoMap = { 1: 'Strictly Reactive', 2: 'Reactive', 3: 'Balanced', 4: 'Proactive', 5: 'Highly Proactive' };
  const rigiMap = { 1: 'Plain Text', 2: 'Light Markdown', 3: 'Balanced Layout', 4: 'Structured', 5: 'Highly Structured / Tables' };

  return `# Persona: ${p.name || 'Unnamed Agent'}

## Role
${p.role || 'Not specified'}

## Additional Context
${p.background || 'Not specified'}

## Behavior & Style
- **Creativity**: ${creaMap[p.creativity] || 'Balanced'} (${p.creativity}/5)
- **Seriousness**: ${seriMap[p.seriousness] || 'Balanced'} (${p.seriousness}/5)
- **Chattiness**: ${chatMap[p.chattiness] || 'Balanced'} (${p.chattiness}/5)
- **Autonomy**: ${autoMap[p.autonomy] || 'Balanced'} (${p.autonomy}/5)
- **Rigidity**: ${rigiMap[p.rigidity] || 'Balanced Layout'} (${p.rigidity}/5)

## Constraints & Rules
${p.constraints || 'Not specified'}
`;
});

const copyToClipboard = () => {
  navigator.clipboard.writeText(generatedMarkdown.value);
  alert('Markdown copied to clipboard!');
};
</script>

<style scoped>
.code-header {
  padding: 12px 24px;
  border-bottom: 1px solid var(--border);
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #0D0E10;
}

.tab {
  font-size: 0.8rem;
  color: #888;
  font-family: var(--font-mono);
  display: flex;
  gap: 8px;
  align-items: center;
}

.dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: #1A1B1D;
}
.dot.active {
  background: var(--success);
  box-shadow: 0 0 8px var(--success);
}

.code-content {
  flex: 1;
  padding: 24px;
  font-family: var(--font-mono);
  font-size: 0.9rem;
  color: #a5d6ff;
  overflow-y: auto;
  min-height: 400px;
}
.code-content pre { margin: 0; white-space: pre-wrap; word-wrap: break-word; }

.action-bar {
  padding: 16px 24px;
  border-top: 1px solid var(--border);
  background: #0D0E10;
  display: flex;
  justify-content: flex-end;
  gap: 12px;
}
</style>
