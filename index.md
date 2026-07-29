---
layout: default
title: "Welcome"
---

<div class="welcome-hero" style="padding: 40px 20px; text-align: center; background: linear-gradient(135deg, var(--badge-bg) 0%, transparent 100%); border-radius: 12px; margin-bottom: 40px; border: 1px solid var(--badge-border);">
  <h2 style="font-size: 2.0rem; margin-top: 0; color: var(--primary-color);">🌿 {{ site.title }}</h2>
  <p style="font-size: 1.1rem; opacity: 0.9; max-width: 600px; margin: 15px auto 0;">
    Welcome to my public digital garden! This website is a dynamic, searchable compilation of public notes synced directly from my private Obsidian vault using the Publish on GitHub plugin.
  </p>
</div>

### 🔍 Navigating the Garden

<div class="navigation-grid" style="display: grid; grid-template-columns: repeat(auto-fit, minmax(240px, 1fr)); gap: 20px; margin-bottom: 40px;">
  <div class="nav-card" style="padding: 20px; border: 1px solid var(--border-color); border-radius: 8px; background: var(--content-bg);">
    <h4 style="margin-top: 0; color: var(--primary-color);">📂 Interactive Explorer</h4>
    <p style="font-size: 0.9rem; margin-bottom: 0; opacity: 0.8; line-height: 1.5;">
      Use the left-hand sidebar to browse through folders and files. It automatically maps and preserves your Obsidian vault folder structures.
    </p>
  </div>
  <div class="nav-card" style="padding: 20px; border: 1px solid var(--border-color); border-radius: 8px; background: var(--content-bg);">
    <h4 style="margin-top: 0; color: var(--primary-color);">⚡ Instant Search</h4>
    <p style="font-size: 0.9rem; margin-bottom: 0; opacity: 0.8; line-height: 1.5;">
      Type anywhere in the left search input to instantly filter through note titles and find specific topics across your published notes.
    </p>
  </div>
  <div class="nav-card" style="padding: 20px; border: 1px solid var(--border-color); border-radius: 8px; background: var(--content-bg);">
    <h4 style="margin-top: 0; color: var(--primary-color);">📍 Table of Contents</h4>
    <p style="font-size: 0.9rem; margin-bottom: 0; opacity: 0.8; line-height: 1.5;">
      Heading tags on active notes populate the right-hand Table of Contents with a ScrollSpy outline to jump seamlessly across sections.
    </p>
  </div>
</div>

### 🛠️ Publishing Your Own Notes

Want to start sharing selective files from your Obsidian vault?
1. Open the **Publish on GitHub** settings inside Obsidian.
2. Configure your publish tag (e.g. `{{ site.publish_tag }}`), repository path, and GitHub remote URL.
3. Tag any note in your vault with your publish tag `{{ site.publish_tag }}` (inline or in frontmatter).
4. Click the ribbon icon or run `Publish Public Notes` from the command palette. The plugin converts wikilinks and pushes automatically!
