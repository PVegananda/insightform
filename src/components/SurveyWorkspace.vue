<script setup>
import { ref } from 'vue'

const activeFilter = ref('All surveys')

const filters = ['All surveys', 'Published', 'Drafts']

const surveys = [
  {
    title: 'Customer experience pulse',
    description: 'Understand what keeps customers coming back.',
    responses: 248,
    status: 'Published',
    updated: 'Updated 2 hours ago',
    accent: 'blue'
  },
  {
    title: 'Remote work check-in',
    description: 'A monthly snapshot of how the team is doing.',
    responses: 86,
    status: 'Published',
    updated: 'Updated yesterday',
    accent: 'violet'
  },
  {
    title: 'Product discovery interviews',
    description: 'Collect early signals before the next release.',
    responses: 0,
    status: 'Draft',
    updated: 'Edited 3 days ago',
    accent: 'amber'
  },
  {
    title: 'Yang Menjual',
    description: 'Understand what customers value most when choosing where to buy.',
    responses: 124,
    status: 'Published',
    updated: 'Updated 5 hours ago',
    accent: 'blue'
  },
  {
    title: 'Rapo',
    description: 'Collect clear feedback from the Rapo community and turn it into next steps.',
    responses: 42,
    status: 'Published',
    updated: 'Updated Monday',
    accent: 'violet'
  }
]
</script>

<template>
  <main class="app-shell">
    <header class="topbar">
      <a class="brand" href="/" aria-label="InsightForm home">
        <span class="brand-mark">I</span>
        <span>InsightForm</span>
      </a>
      <nav class="topbar-nav" aria-label="Main navigation">
        <a class="active" href="/">Workspace</a>
        <a href="/">Templates</a>
        <a href="/">Settings</a>
      </nav>
      <button class="avatar" type="button" aria-label="Open profile menu">PV</button>
    </header>

    <section class="workspace">
      <div class="intro">
        <div>
          <p class="eyebrow">Your workspace</p>
          <h1>Make every question count.</h1>
          <p class="intro-copy">Create focused surveys and turn honest feedback into your next best move.</p>
        </div>
        <button class="primary-button" type="button">
          <span aria-hidden="true">+</span>
          New survey
        </button>
      </div>

      <div class="summary-grid" aria-label="Workspace summary">
        <article class="summary-card">
          <span class="summary-label">Total responses</span>
          <strong>500</strong>
          <span class="summary-change">+18.4% this month</span>
        </article>
        <article class="summary-card">
          <span class="summary-label">Published surveys</span>
          <strong>4</strong>
          <span class="summary-note">1 draft in progress</span>
        </article>
        <article class="summary-card accent-card">
          <span class="summary-label">Average completion</span>
          <strong>78%</strong>
          <span class="summary-note">Across all active surveys</span>
        </article>
      </div>

      <div class="section-heading">
        <h2>Surveys</h2>
        <div class="filters" role="group" aria-label="Filter surveys">
          <button
            v-for="filter in filters"
            :key="filter"
            :class="{ selected: activeFilter === filter }"
            type="button"
            @click="activeFilter = filter"
          >
            {{ filter }}
          </button>
        </div>
      </div>

      <div class="survey-list">
        <article v-for="survey in surveys" :key="survey.title" class="survey-card">
          <div :class="['survey-icon', survey.accent]">{{ survey.title.charAt(0) }}</div>
          <div class="survey-details">
            <div class="survey-title-row">
              <h3>{{ survey.title }}</h3>
              <span :class="['status', survey.status.toLowerCase()]">{{ survey.status }}</span>
            </div>
            <p>{{ survey.description }}</p>
            <div class="survey-meta">
              <span>{{ survey.responses }} responses</span>
              <span>{{ survey.updated }}</span>
            </div>
          </div>
          <button class="more-button" type="button" :aria-label="`More options for ${survey.title}`">•••</button>
        </article>
      </div>
    </section>
  </main>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700&family=Plus+Jakarta+Sans:wght@600;700&display=swap');

:global(*) { box-sizing: border-box; }
:global(body) { margin: 0; background: #f7f8fc; color: #182235; font-family: 'DM Sans', sans-serif; }
button, a { font: inherit; }
button { cursor: pointer; }
.app-shell { min-height: 100vh; }
.topbar { align-items: center; background: #fff; border-bottom: 1px solid #e9edf4; display: flex; height: 76px; padding: 0 clamp(24px, 6vw, 96px); }
.brand { align-items: center; color: #182235; display: flex; font-family: 'Plus Jakarta Sans', sans-serif; font-size: 18px; font-weight: 700; gap: 10px; text-decoration: none; }
.brand-mark { align-items: center; background: #3268ef; border-radius: 9px; color: white; display: flex; font-size: 15px; height: 30px; justify-content: center; width: 30px; }
.topbar-nav { display: flex; gap: 32px; margin-left: clamp(32px, 7vw, 110px); }
.topbar-nav a { color: #78849a; font-size: 14px; text-decoration: none; }
.topbar-nav a.active { color: #3268ef; font-weight: 600; }
.avatar { background: #e9efff; border: 0; border-radius: 50%; color: #3268ef; font-size: 12px; font-weight: 700; height: 34px; margin-left: auto; width: 34px; }
.workspace { margin: 0 auto; max-width: 1120px; padding: 72px 24px 100px; }
.intro { align-items: end; display: flex; justify-content: space-between; margin-bottom: 42px; }
.eyebrow { color: #3268ef; font-size: 12px; font-weight: 700; letter-spacing: .12em; margin: 0 0 14px; text-transform: uppercase; }
h1, h2, h3 { font-family: 'Plus Jakarta Sans', sans-serif; }
h1 { font-size: clamp(30px, 4vw, 44px); letter-spacing: -.04em; line-height: 1.1; margin: 0 0 14px; }
.intro-copy { color: #77839a; font-size: 16px; margin: 0; }
.primary-button { align-items: center; background: #3268ef; border: 0; border-radius: 8px; box-shadow: 0 7px 18px #3268ef33; color: #fff; display: flex; font-size: 14px; font-weight: 600; gap: 10px; padding: 14px 20px; }
.primary-button span { font-size: 20px; font-weight: 400; line-height: 12px; }
.summary-grid { display: grid; gap: 18px; grid-template-columns: repeat(3, 1fr); margin-bottom: 64px; }
.summary-card { background: #fff; border: 1px solid #e9edf4; border-radius: 12px; padding: 24px; }
.summary-card.accent-card { background: #3268ef; border-color: #3268ef; color: #fff; }
.summary-label, .summary-change, .summary-note { display: block; font-size: 13px; }
.summary-label, .summary-note { color: #8994a8; }
.accent-card .summary-label, .accent-card .summary-note { color: #dce6ff; }
.summary-card strong { display: block; font-family: 'Plus Jakarta Sans', sans-serif; font-size: 30px; margin: 12px 0 7px; }
.summary-change { color: #2ca675; font-weight: 600; }
.section-heading { align-items: center; display: flex; justify-content: space-between; margin-bottom: 20px; }
h2 { font-size: 22px; letter-spacing: -.03em; margin: 0; }
.filters { background: #eef1f7; border-radius: 7px; display: flex; gap: 3px; padding: 3px; }
.filters button { background: transparent; border: 0; border-radius: 5px; color: #8994a8; font-size: 12px; padding: 8px 12px; }
.filters button.selected { background: #fff; box-shadow: 0 1px 3px #1a2d4a14; color: #3268ef; font-weight: 600; }
.survey-list { display: grid; gap: 12px; }
.survey-card { align-items: center; background: #fff; border: 1px solid #e9edf4; border-radius: 12px; display: flex; gap: 18px; padding: 20px 22px; }
.survey-icon { align-items: center; border-radius: 10px; display: flex; flex: 0 0 46px; font-family: 'Plus Jakarta Sans', sans-serif; font-size: 17px; height: 46px; justify-content: center; }
.survey-icon.blue { background: #e9efff; color: #3268ef; }
.survey-icon.violet { background: #f1edff; color: #7656d6; }
.survey-icon.amber { background: #fff4df; color: #d79220; }
.survey-details { min-width: 0; width: 100%; }
.survey-title-row { align-items: center; display: flex; gap: 12px; }
h3 { font-size: 15px; margin: 0; }
.survey-details p { color: #8994a8; font-size: 13px; margin: 6px 0 14px; }
.status { border-radius: 20px; font-size: 10px; font-weight: 700; padding: 4px 8px; text-transform: uppercase; }
.status.published { background: #e6f8f0; color: #2ca675; }
.status.draft { background: #fff4df; color: #c58116; }
.survey-meta { color: #a0a9b8; display: flex; font-size: 11px; gap: 20px; }
.more-button { background: transparent; border: 0; color: #a0a9b8; letter-spacing: 2px; padding: 12px 0 12px 12px; }
@media (max-width: 680px) {
  .topbar-nav { display: none; }
  .workspace { padding-top: 48px; }
  .intro { align-items: start; flex-direction: column; gap: 24px; }
  .summary-grid { grid-template-columns: 1fr; margin-bottom: 44px; }
  .section-heading { align-items: start; flex-direction: column; gap: 16px; }
  .survey-card { align-items: start; }
  .survey-title-row { align-items: start; flex-direction: column; gap: 7px; }
}
</style>
