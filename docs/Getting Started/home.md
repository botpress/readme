---
title: Home
excerpt: >-
  Botpress is an all-in-one platform for building AI agents powered by the
  latest LLMs.
deprecated: false
hidden: false
metadata:
  title: Botpress Documentation
  description: >-
    Botpress is an all-in-one platform for build AI agents powered by the latest
    LLMs.
  keywords:
    - botpress
    - documentation
  robots: index
---
<HTMLBlock>{`
<style>
  /* Preload fonts */
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap');

:root {
  --primary: #2563eb;
  --secondary: #3b82f6;
  --text: #f8fafc;
  --card: #1f2937;
  --hover: #3b82f6;
  --sublink: #374151;
  --sublink-hover: #4b5563;
  --desc: #e2e8f0;
}

.botpress-landing {
  font-family: Inter, system-ui, sans-serif;
  color: var(--text);
  line-height: 1.6;
  max-width: 1200px;
  margin: 0 auto;
  padding: 2.5rem 1.25rem;
}

.header {
  text-align: center;
  margin-bottom: 3.75rem;
  display: flex;
  align-items: flex-end;
  justify-content: center;
  gap: 1rem;
}

.header svg {
  width: 3rem;
  height: 3rem;
  margin-bottom: 1.2rem;
}

.header h1 {
  font-size: 3.5rem;
  margin: 0 0 1.25rem;
  background: linear-gradient(135deg, var(--primary), var(--secondary));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  line-height: 1;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1.875rem;
  margin-top: 2.5rem;
  animation: fadeIn .6s ease-out;
  content-visibility: auto;
}

.card {
  background: var(--card);
  padding: 2rem;
  border-radius: 1rem;
  box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1);
  transition: transform .2s, box-shadow .2s;
  position: relative;
  overflow: hidden;
  isolation: isolate;
}

.card::before {
  content: '';
  position: absolute;
  inset: 0 0 auto;
  height: 4px;
  background: linear-gradient(90deg, var(--primary), var(--secondary));
  transform: translateY(-100%);
  transition: transform .2s;
  will-change: transform;
}

.card:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 15px -3px rgb(0 0 0 / 0.1);
}

.card:hover::before {
  transform: translateY(0);
}

.card h2 {
  font-size: 1.8rem;
  margin-bottom: 1.25rem;
  color: var(--primary);
  display: flex;
  align-items: center;
}

.card p {
  color: var(--desc);
  margin-bottom: 1.5rem;
}

.btn {
  display: inline-block;
  padding: .75rem 1.5rem;
  font-size: 1rem;
  font-weight: 600;
  color: #fff;
  background-color: var(--primary);
  text-decoration: none;
  border-radius: .5rem;
  transition: .2s;
  position: relative;
  overflow: hidden;
}

.btn::after {
  content: '';
  position: absolute;
  inset: 0;
  background: rgb(255 255 255 / .1);
  transform: translateX(-100%);
  transition: transform .3s;
}

.btn:hover {
  background-color: var(--hover);
  transform: translateY(-2px);
}

.btn:hover::after {
  transform: translateX(0);
}

.links-container {
  margin-top: 1.875rem;
}

.sub-link {
  display: block;
  padding: .75rem 1rem;
  margin: .625rem 0;
  color: var(--text);
  text-decoration: none;
  border-radius: .5rem;
  transition: .2s;
  background-color: var(--sublink);
}

.sub-link:hover {
  background-color: var(--sublink-hover);
  color: var(--primary);
  padding-left: 1.25rem;
}

.links-container h3 {
  color: var(--secondary);
}

@media (max-width: 768px) {
  .botpress-landing {
    padding: 1.25rem;
  }
  
  .header h1 {
    font-size: 3rem;
  }
  
  .card {
    padding: 1.5rem;
  }
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
}
</style>

<div class="botpress-landing">
  <div class="header">
    <svg width="32" height="32" viewBox="0 0 32 32" fill="none" xmlns="http://www.w3.org/2000/svg">
      <rect width="32" height="32" rx="8" fill="#21201C"/>
      <path fill-rule="evenodd" clip-rule="evenodd" d="M21.0204 17.5548L23.5267 18.978C23.8173 19.1381 24.017 19.4583 23.9989 19.7963V22.6249C23.9989 22.963 23.8173 23.2654 23.5267 23.4433L21.0204 24.8666C20.7298 25.0445 20.3666 25.0445 20.0578 24.8666L17.5516 23.4433C17.2611 23.2833 17.0612 22.963 17.0795 22.6249V19.9565L11.2315 16.6475L12.3757 18.3198L10.941 19.1381C10.6504 19.316 10.2872 19.316 9.97842 19.1381L7.47219 17.7148C7.18161 17.5548 7 17.2523 7 16.9144V14.0679C7 13.7299 7.18161 13.4274 7.47219 13.2495L9.97842 11.8264C10.269 11.6484 10.6322 11.6484 10.941 11.8264L12.1941 12.5379L13.3019 13.1605L17.0795 11.0258V8.375C17.0795 8.03698 17.2611 7.73455 17.5516 7.55665L20.0578 6.13342C20.3484 5.95553 20.7116 5.95553 21.0204 6.13342L23.5267 7.55665C23.8173 7.71676 24.017 8.03698 23.9989 8.375V11.2037C23.9989 11.5417 23.8173 11.8441 23.5267 12.022L21.0204 13.4452C20.7298 13.6231 20.3666 13.6231 20.0578 13.4452L18.8047 12.7336L18.7321 12.698L20.0578 10.7945L17.715 12.1288L13.9376 14.2635V16.772L17.715 18.9068L18.8229 18.2842L20.076 17.5726C20.3484 17.3769 20.7298 17.3947 21.0204 17.5548Z" fill="#FDFDFC"/>
    </svg>
    <h1>Botpress Documentation</h1>
  </div>

  <!-- Optionally add a short header-description block if desired
  <div class="header-description">
    <p>Your subheading or short introduction text here...</p>
  </div> -->

  <div class="grid">
    <div class="card">
      <h2>
        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" style="margin-right: 8px;">
          <path d="M2 3h6a4 4 0 0 1 4 4v14a3 3 0 0 0-3-3H2V3zm20 0h-6a4 4 0 0 0-4 4v14a3 3 0 0 1 3-3h7V3z" stroke="currentColor" stroke-width="2"/>
        </svg>
        Guides
      </h2>
      <p>Explore Botpress features, tools, and best practices for building and deploying AI chatbots and agents.</p>
      <a href="/docs/build" class="btn">Browse Guides</a>
      
      <div class="links-container">
        <h3>Popular Pages</h3>
        <a href="/docs/embedded-webchat-getting-started" class="sub-link">Place a bot on your website</a>
        <a href="/docs/variables" class="sub-link">Use variables to store data</a>
        <a href="/docs/using-integrations" class="sub-link">Install an integration</a>
      </div>
    </div>
    
    <div class="card">
      <h2>
        <svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor" style="margin-right: 8px;">
          <path d="M20 4C21.1 4 22 4.9 22 6V18C22 19.1 21.1 20 20 20H4C2.9 20 2 19.1 2 18V6C2 4.9 2.9 4 4 4H20M20 18V8H4V18H20M9 10H7V16H9V10M13 10H11V16H13V10M17 10H15V16H17V10Z"/>
        </svg>
        API Reference
      </h2>
      <p>Dive into technical insights about Botpress API endpoints to integrate and extend the platform effectively.</p>
      <a href="/reference/introduction" class="btn">View API Docs</a>
      
      <div class="links-container">
        <h3>Popular Pages</h3>
        <a href="https://botpress.com/reference/createconversation" class="sub-link">Manage conversations</a>
        <a href="https://botpress.com/reference/what-is-the-files-api" class="sub-link">Manage files</a>
        <a href="https://botpress.com/reference/introduction" class="sub-link">Learn about the Chat API</a>
      </div>
    </div>
  </div>
</div>
`}</HTMLBlock>