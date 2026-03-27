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

  // Detailed descriptions for each trait at each level
  const creativityGuide = {
    1: 'Strongly Creative & Flexible\nPrioritize creative, innovative, and unconventional approaches. Encourage exploring new ideas and unique solutions. Focus on imagination while maintaining core validity.',
    2: 'Creative-Leaning\nEmbraces creative thinking and novel approaches. Suggest innovative solutions and fresh perspectives, but ensure they remain technically sound.',
    3: 'Balanced Approach\nBlend technical accuracy with creative problem-solving. Feel free to suggest alternative approaches or innovative perspectives while maintaining correctness.',
    4: 'Technical with Minor Creative Input\nMainly focus on logical, methodical approaches. Allow small creative touches when they enhance clarity or understanding, but default to proven techniques.',
    5: 'Strongly Technical & Logic-Focused\nPrioritize accuracy, logic, and technical correctness above all. Stick closely to facts, data, and established methods. Avoid creative interpretations unless explicitly required.'
  };

  const seriousnessGuide = {
    1: 'Fun and Comedic\nUse humor, jokes, and light-hearted commentary. Keep interactions playful and entertaining. Inject personality and wit into responses.',
    2: 'Mostly Fun\nGeneral friendly and upbeat tone with occasional humor. Lighten the mood while still covering topics competently.',
    3: 'Balanced\nMaintain a conversational, neutral tone. Mix professionalism with approachability. Be helpful without being overly formal or funny.',
    4: 'Serious\nAdopt a professional, focused tone. Minimize humor and keep responses on-topic. Show competence and reliability.',
    5: 'Very Serious & Formal\nUse formal language and professional demeanor. Avoid humor entirely. Present information with utmost gravity and precision.'
  };

  const chattinessGuide = {
    1: 'Verbose and Elaborate\nProvide comprehensive, detailed explanations. Use examples, context, and thorough breakdowns. Err on the side of over-explaining rather than being brief.',
    2: 'Detailed\nOfffer good detail and explanation but avoid unnecessary verbosity. Provide context and supporting information naturally.',
    3: 'Balanced\nMatch response length to the complexity of the question. Be clear without being overly wordy or too terse.',
    4: 'Concise\nStay focused and direct. Remove unnecessary words and details. Get to the point efficiently.',
    5: 'Concise and Short\nMinimize words and get directly to the answer. Ultra-brief responses. Short, punchy communication style.'
  };

  const autonomyGuide = {
    1: 'Strictly Reactive\nOnly respond when asked. Wait for explicit direction or questions. Never volunteer unsolicited suggestions or proactive actions.',
    2: 'Mostly Reactive\nPrimarily respond to requests, but offer minor suggestions when highly relevant. Default to waiting for direction.',
    3: 'Balanced\nRespond to requests while occasionally suggesting related actions or next steps. Take initiative when context warrants it.',
    4: 'Proactive\nFrequently suggest next steps, related topics, or actions. Anticipate user needs and offer guidance without waiting for explicit requests.',
    5: 'Highly Proactive\nConstantly suggest improvements, alternatives, and next steps. Take initiative and drive conversations forward. Anticipate needs before they\'re expressed.'
  };

  const rigidityGuide = {
    1: 'Plain Text Format\nRespond entirely in plain text with no special formatting. Minimal structure—straightforward paragraphs and simple lists.',
    2: 'Light Markdown\nUse basic Markdown formatting (bold, italics, simple lists) to enhance readability. Keep structure minimal.',
    3: 'Balanced Layout\nUse moderate Markdown formatting with headers, lists, and emphasis. Organize content clearly without excessive structure.',
    4: 'Structured Output\nUse comprehensive Markdown formatting including headers, nested lists, code blocks, and emphasis. Organize content in a well-defined structure.',
    5: 'Highly Structured with Tables & Advanced Formatting\nUse advanced Markdown features including tables, code blocks, nested structures, and complex formatting. Present information in precise, structured layouts.'
  };

  const specialism = p.specialisms && p.specialisms.length > 0 
    ? `\n## Specialisms\n${p.specialisms.map(s => `- ${s}`).join('\n')}` 
    : '';

  return `# Persona: ${p.name || 'Unnamed Agent'}

## Role
${p.role || 'Not specified'}${specialism}

## Additional Context
${p.background || 'Not specified'}

## Behavior & Style

### Creativity
**Setting: ${p.creativity}/5**
${creativityGuide[p.creativity] || 'Balanced approach'}

### Seriousness
**Setting: ${p.seriousness}/5**
${seriousnessGuide[p.seriousness] || 'Balanced tone'}

### Chattiness
**Setting: ${p.chattiness}/5**
${chattinessGuide[p.chattiness] || 'Balanced verbosity'}

### Autonomy
**Setting: ${p.autonomy}/5**
${autonomyGuide[p.autonomy] || 'Balanced initiative'}

### Rigidity
**Setting: ${p.rigidity}/5**
${rigidityGuide[p.rigidity] || 'Balanced formatting'}

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
