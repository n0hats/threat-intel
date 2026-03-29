---
layout: default
title: "Threat Intel"
---

<h1 class="page-heading"><span class="prompt">$</span> threat-feed --live</h1>

<p style="color: var(--text-secondary); font-family: var(--font-mono); font-size: 0.85rem; margin-bottom: 2rem;">
  Tracking active CVEs, 0-days, and exploits. Updated continuously. Sources: NVD · CISA KEV · GitHub Advisories · Exploit-DB.
</p>

{% assign posts_by_severity = "" | split: "" %}
{% assign critical_posts = site.posts | where: "severity", "critical" %}
{% assign high_posts     = site.posts | where: "severity", "high" %}
{% assign medium_posts   = site.posts | where: "severity", "medium" %}
{% assign low_posts      = site.posts | where: "severity", "low" %}

{% if site.posts.size == 0 %}
  <p style="color: var(--text-dim); font-family: var(--font-mono);">No threat posts yet. Stand by.</p>
{% else %}

{% for post in site.posts %}
  {% assign sev = post.severity | downcase | default: "low" %}
  <div class="post-card severity-{{ sev }}">
    <div class="post-meta">
      {% if post.severity %}
        <span class="badge badge-{{ sev }}">{{ post.severity | upcase }}</span>
      {% endif %}
      <time style="font-family: var(--font-mono); font-size: 0.78rem; color: var(--text-dim);">
        {{ post.date | date: "%Y-%m-%d" }}
      </time>
    </div>
    <div class="post-card-title">
      <a href="{{ post.url | relative_url }}" style="color: var(--text-primary);">{{ post.title }}</a>
    </div>
    {% if post.excerpt %}
      <div class="post-card-excerpt">{{ post.excerpt | strip_html | truncate: 200 }}</div>
    {% endif %}
    {% if post.tags and post.tags.size > 0 %}
      <div class="tags">
        {% for tag in post.tags %}
          <span class="tag">#{{ tag }}</span>
        {% endfor %}
      </div>
    {% endif %}
  </div>
{% endfor %}

{% endif %}
