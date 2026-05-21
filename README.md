<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>MAISON NOIR — Luxury Fashion House</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400&family=Didact+Gothic&family=Cinzel:wght@400;600&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

  :root {
    --beige: #F5F0E8;
    --beige-dark: #E8E0D0;
    --beige-mid: #D4C9B5;
    --sand: #C4B49A;
    --matte-black: #0E0D0C;
    --charcoal: #1A1917;
    --graphite: #2E2C2A;
    --ash: #6B6560;
    --gold: #B8985A;
    --gold-light: #D4B478;
    --white: #FDFCF9;
    --serif: 'Cormorant Garamond', Georgia, serif;
    --display: 'Cinzel', serif;
    --sans: 'Didact Gothic', sans-serif;
  }

  html { scroll-behavior: smooth; }

  body {
    font-family: var(--sans);
    background: var(--matte-black);
    color: var(--beige);
    cursor: none;
    overflow-x: hidden;
  }

  /* === CUSTOM CURSOR === */
  #cursor-dot {
    position: fixed; top: 0; left: 0; pointer-events: none; z-index: 9999;
    width: 8px; height: 8px;
    background: var(--gold);
    border-radius: 50%;
    transform: translate(-50%, -50%);
    transition: transform 0.1s ease, opacity 0.2s;
    mix-blend-mode: difference;
  }
  #cursor-ring {
    position: fixed; top: 0; left: 0; pointer-events: none; z-index: 9998;
    width: 36px; height: 36px;
    border: 1px solid rgba(184,152,90,0.6);
    border-radius: 50%;
    transform: translate(-50%, -50%);
    transition: transform 0.35s cubic-bezier(0.23,1,0.32,1), width 0.3s, height 0.3s, border-color 0.3s;
  }
  body.hovering #cursor-ring {
    width: 60px; height: 60px;
    border-color: var(--gold);
  }

  /* === NAVIGATION === */
  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 100;
    display: flex; align-items: center; justify-content: space-between;
    padding: 28px 52px;
    transition: padding 0.5s ease, background 0.5s ease, backdrop-filter 0.5s;
  }
  nav.scrolled {
    padding: 18px 52px;
    background: rgba(14,13,12,0.85);
    backdrop-filter: blur(12px);
    border-bottom: 1px solid rgba(184,152,90,0.15);
  }
  .nav-logo {
    font-family: var(--display);
    font-size: 18px;
    letter-spacing: 0.35em;
    color: var(--beige);
    text-decoration: none;
    font-weight: 600;
  }
  .nav-links {
    display: flex; gap: 44px; list-style: none;
  }
  .nav-links a {
    font-family: var(--sans);
    font-size: 11px;
    letter-spacing: 0.2em;
    color: var(--sand);
    text-decoration: none;
    text-transform: uppercase;
    transition: color 0.3s;
    position: relative;
  }
  .nav-links a::after {
    content: ''; position: absolute; bottom: -2px; left: 0; width: 0; height: 1px;
    background: var(--gold); transition: width 0.4s cubic-bezier(0.23,1,0.32,1);
  }
  .nav-links a:hover { color: var(--beige); }
  .nav-links a:hover::after { width: 100%; }
  .nav-actions { display: flex; align-items: center; gap: 24px; }
  .nav-btn {
    font-family: var(--sans);
    font-size: 11px; letter-spacing: 0.2em; text-transform: uppercase;
    color: var(--beige); background: transparent; border: 1px solid rgba(184,152,90,0.4);
    padding: 10px 24px; cursor: none; transition: all 0.3s;
  }
  .nav-btn:hover { background: var(--gold); color: var(--matte-black); border-color: var(--gold); }

  /* === HERO === */
  .hero {
    position: relative; height: 100vh; overflow: hidden;
    display: flex; align-items: flex-end;
  }
  .hero-bg {
    position: absolute; inset: 0;
    background: linear-gradient(160deg, #1A1612 0%, #0E0D0C 40%, #1C1610 100%);
  }
  .hero-texture {
    position: absolute; inset: 0; opacity: 0.04;
    background-image: repeating-linear-gradient(0deg, transparent, transparent 2px, rgba(245,240,232,0.3) 2px, rgba(245,240,232,0.3) 3px);
  }
  .hero-accent {
    position: absolute; top: 0; right: 0; width: 45%; height: 100%;
    background: var(--beige-dark);
    clip-path: polygon(15% 0%, 100% 0%, 100% 100%, 0% 100%);
    overflow: hidden;
  }
  .hero-accent-img {
    position: absolute; inset: 0;
    background: linear-gradient(135deg, #D4C9B5 0%, #C4B49A 30%, #B8A88E 60%, #A89578 100%);
  }
  .hero-accent-overlay {
    position: absolute; inset: 0;
    background: linear-gradient(to right, rgba(14,13,12,0.7) 0%, transparent 40%);
  }
  /* Decorative figure silhouette */
  .hero-figure {
    position: absolute; bottom: 0; right: 8%;
    width: 320px; height: 85%;
  }
  .hero-figure svg { width: 100%; height: 100%; }

  .hero-content {
    position: relative; z-index: 10;
    padding: 0 8% 8%;
    max-width: 680px;
  }
  .hero-eyebrow {
    font-family: var(--sans); font-size: 10px;
    letter-spacing: 0.4em; color: var(--gold); text-transform: uppercase;
    margin-bottom: 28px; display: flex; align-items: center; gap: 16px;
    opacity: 0; animation: fadeUp 1s 0.3s forwards;
  }
  .hero-eyebrow::before { content: ''; width: 40px; height: 1px; background: var(--gold); }
  .hero-title {
    font-family: var(--serif);
    font-size: clamp(64px, 8vw, 104px);
    font-weight: 300; line-height: 0.9;
    color: var(--beige); margin-bottom: 32px;
    opacity: 0; animation: fadeUp 1s 0.6s forwards;
  }
  .hero-title em { font-style: italic; color: var(--sand); }
  .hero-sub {
    font-family: var(--sans); font-size: 12px;
    letter-spacing: 0.15em; color: var(--ash);
    line-height: 2; max-width: 360px; margin-bottom: 48px;
    opacity: 0; animation: fadeUp 1s 0.9s forwards;
  }
  .hero-cta {
    display: flex; align-items: center; gap: 32px;
    opacity: 0; animation: fadeUp 1s 1.2s forwards;
  }
  .btn-primary {
    font-family: var(--sans); font-size: 11px; letter-spacing: 0.25em; text-transform: uppercase;
    color: var(--matte-black); background: var(--beige); border: none;
    padding: 16px 40px; cursor: none; transition: all 0.4s;
    display: inline-block; text-decoration: none;
    position: relative; overflow: hidden;
  }
  .btn-primary::before {
    content: ''; position: absolute; inset: 0;
    background: var(--gold); transform: translateX(-101%);
    transition: transform 0.4s cubic-bezier(0.23,1,0.32,1);
  }
  .btn-primary:hover::before { transform: translateX(0); }
  .btn-primary span { position: relative; z-index: 1; }
  .btn-ghost {
    font-family: var(--sans); font-size: 11px; letter-spacing: 0.25em; text-transform: uppercase;
    color: var(--sand); background: transparent; border: none;
    cursor: none; display: flex; align-items: center; gap: 12px; text-decoration: none;
    transition: color 0.3s;
  }
  .btn-ghost:hover { color: var(--beige); }
  .btn-ghost-arrow {
    width: 36px; height: 1px; background: var(--sand);
    position: relative; transition: width 0.4s;
  }
  .btn-ghost:hover .btn-ghost-arrow { width: 56px; background: var(--beige); }
  .btn-ghost-arrow::after {
    content: ''; position: absolute; right: 0; top: -3px;
    width: 6px; height: 6px; border-right: 1px solid currentColor;
    border-top: 1px solid currentColor; transform: rotate(45deg);
  }
  .hero-scroll-hint {
    position: absolute; bottom: 40px; right: 52px; z-index: 10;
    font-family: var(--sans); font-size: 9px; letter-spacing: 0.3em;
    color: var(--ash); text-transform: uppercase; writing-mode: vertical-rl;
    opacity: 0; animation: fadeIn 1s 2s forwards;
    display: flex; align-items: center; gap: 12px;
  }
  .scroll-line {
    width: 1px; height: 60px; background: linear-gradient(to bottom, transparent, var(--gold));
    animation: scrollPulse 2s 2s infinite;
  }
  @keyframes scrollPulse { 0%,100%{opacity:0.4} 50%{opacity:1} }

  /* === MARQUEE === */
  .marquee-strip {
    background: var(--gold);
    padding: 14px 0; overflow: hidden;
    display: flex;
  }
  .marquee-track {
    display: flex; gap: 0; white-space: nowrap;
    animation: marqueeScroll 20s linear infinite;
  }
  .marquee-item {
    font-family: var(--display); font-size: 11px; letter-spacing: 0.3em;
    color: var(--matte-black); text-transform: uppercase;
    padding: 0 36px; display: flex; align-items: center; gap: 36px;
  }
  .marquee-item::after { content: '◆'; font-size: 6px; color: rgba(14,13,12,0.4); }
  @keyframes marqueeScroll { 0%{transform:translateX(0)} 100%{transform:translateX(-50%)} }

  /* === SECTIONS COMMON === */
  section { position: relative; }

  /* === EDITORIAL INTRO === */
  .editorial {
    background: var(--charcoal);
    padding: 120px 8%;
    display: grid; grid-template-columns: 1fr 1fr; gap: 80px; align-items: center;
  }
  .editorial-label {
    font-family: var(--sans); font-size: 9px; letter-spacing: 0.5em;
    color: var(--gold); text-transform: uppercase; margin-bottom: 24px;
    display: flex; align-items: center; gap: 16px;
  }
  .editorial-label::after { content: ''; flex: 1; height: 1px; background: rgba(184,152,90,0.3); }
  .editorial-title {
    font-family: var(--serif); font-size: clamp(42px, 5vw, 64px);
    font-weight: 300; line-height: 1.1; color: var(--beige); margin-bottom: 28px;
  }
  .editorial-title em { font-style: italic; color: var(--sand); }
  .editorial-body {
    font-family: var(--sans); font-size: 13px; letter-spacing: 0.06em;
    color: var(--ash); line-height: 2.2; margin-bottom: 40px;
  }
  .editorial-visual {
    position: relative; aspect-ratio: 3/4; overflow: hidden;
  }
  .editorial-visual-bg {
    position: absolute; inset: 0;
    background: linear-gradient(135deg, #2A2520 0%, #1A1612 50%, #252018 100%);
  }
  .editorial-visual-accent {
    position: absolute; bottom: 0; right: 0; width: 70%; height: 60%;
    background: linear-gradient(135deg, var(--sand), var(--beige-mid));
    opacity: 0.15;
  }
  .editorial-visual-number {
    position: absolute; top: 24px; right: 24px;
    font-family: var(--serif); font-size: 120px; font-weight: 300;
    color: rgba(245,240,232,0.04); line-height: 1; user-select: none;
  }
  .editorial-visual-cross {
    position: absolute; top: 50%; left: 50%; transform: translate(-50%,-50%);
    width: 80px; height: 80px; opacity: 0.2;
  }
  .editorial-visual-cross::before, .editorial-visual-cross::after {
    content: ''; position: absolute; background: var(--gold);
  }
  .editorial-visual-cross::before { top: 50%; left: 0; right: 0; height: 1px; transform: translateY(-50%); }
  .editorial-visual-cross::after { left: 50%; top: 0; bottom: 0; width: 1px; transform: translateX(-50%); }
  .editorial-visual-tag {
    position: absolute; bottom: 32px; left: 32px;
    font-family: var(--sans); font-size: 9px; letter-spacing: 0.3em;
    color: var(--sand); text-transform: uppercase;
    border: 1px solid rgba(196,180,154,0.3); padding: 8px 16px;
  }

  /* === PARALLAX COLLECTION === */
  .collection {
    background: var(--beige);
    padding: 120px 8%;
  }
  .collection-header {
    display: flex; align-items: flex-end; justify-content: space-between;
    margin-bottom: 72px;
  }
  .collection-title {
    font-family: var(--serif); font-size: clamp(48px, 5.5vw, 72px);
    font-weight: 300; line-height: 0.95; color: var(--matte-black);
  }
  .collection-title em { font-style: italic; display: block; }
  .collection-meta {
    font-family: var(--sans); font-size: 10px; letter-spacing: 0.3em;
    color: var(--ash); text-transform: uppercase; text-align: right;
    line-height: 2;
  }
  .products-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 2px;
  }
  .product-card {
    position: relative; cursor: none;
    background: var(--charcoal);
    overflow: hidden;
    aspect-ratio: 2/3;
  }
  .product-card:nth-child(2) { margin-top: 60px; }
  .product-card:nth-child(3) { margin-top: 120px; }
  .product-bg {
    position: absolute; inset: 0;
    transition: transform 0.8s cubic-bezier(0.23,1,0.32,1);
  }
  .product-card:hover .product-bg { transform: scale(1.06); }
  .product-bg-1 { background: linear-gradient(160deg, #2E2820 0%, #1A1510 40%, #252015 100%); }
  .product-bg-2 { background: linear-gradient(160deg, #1E1C18 0%, #2A2520 50%, #1C1A15 100%); }
  .product-bg-3 { background: linear-gradient(160deg, #251E18 0%, #1E1815 50%, #2A2218 100%); }
  .product-shape {
    position: absolute; inset: 0; display: flex; align-items: center; justify-content: center;
  }
  .product-shape svg { width: 55%; height: 55%; opacity: 0.25; }
  .product-overlay {
    position: absolute; inset: 0;
    background: linear-gradient(to top, rgba(14,13,12,0.9) 0%, transparent 50%);
  }
  .product-hover-reveal {
    position: absolute; inset: 0;
    background: rgba(14,13,12,0.4);
    opacity: 0; transition: opacity 0.4s;
  }
  .product-card:hover .product-hover-reveal { opacity: 1; }
  .product-info {
    position: absolute; bottom: 0; left: 0; right: 0;
    padding: 32px;
    transform: translateY(0); transition: transform 0.4s cubic-bezier(0.23,1,0.32,1);
  }
  .product-category {
    font-family: var(--sans); font-size: 9px; letter-spacing: 0.4em;
    color: var(--gold); text-transform: uppercase; margin-bottom: 8px;
  }
  .product-name {
    font-family: var(--serif); font-size: 26px; font-weight: 300;
    color: var(--beige); line-height: 1.2; margin-bottom: 4px;
  }
  .product-name em { font-style: italic; }
  .product-price {
    font-family: var(--sans); font-size: 12px; letter-spacing: 0.1em;
    color: var(--sand); margin-bottom: 16px;
  }
  .product-action {
    font-family: var(--sans); font-size: 9px; letter-spacing: 0.3em;
    text-transform: uppercase; color: var(--beige);
    display: flex; align-items: center; gap: 10px;
    opacity: 0; transform: translateY(8px);
    transition: opacity 0.4s, transform 0.4s;
    transition-delay: 0.05s;
    text-decoration: none;
  }
  .product-action-line {
    width: 24px; height: 1px; background: var(--gold); transition: width 0.4s;
  }
  .product-card:hover .product-action { opacity: 1; transform: translateY(0); }
  .product-card:hover .product-action-line { width: 40px; }
  .product-number {
    position: absolute; top: 24px; right: 24px;
    font-family: var(--serif); font-size: 64px; font-weight: 300;
    color: rgba(245,240,232,0.06); line-height: 1; user-select: none;
  }

  /* === FULL BLEED LOOKBOOK === */
  .lookbook {
    height: 90vh; position: relative; overflow: hidden;
    display: flex; align-items: center;
  }
  .lookbook-bg {
    position: absolute; inset: 0;
    background: linear-gradient(135deg, #1A1410 0%, #0E0D0C 35%, #161310 60%, #201A12 100%);
  }
  .lookbook-geometric {
    position: absolute; right: 0; top: 0; width: 50%; height: 100%;
    background: var(--beige-dark);
    clip-path: polygon(20% 0%, 100% 0%, 100% 100%, 0% 100%);
    opacity: 0.07;
  }
  .lookbook-lines {
    position: absolute; inset: 0; overflow: hidden; opacity: 0.05;
  }
  .lookbook-content {
    position: relative; z-index: 10; padding: 0 8%;
    max-width: 580px;
  }
  .lookbook-season {
    font-family: var(--display); font-size: 9px; letter-spacing: 0.5em;
    color: var(--gold); text-transform: uppercase; margin-bottom: 32px;
  }
  .lookbook-title {
    font-family: var(--serif); font-size: clamp(56px, 7vw, 88px);
    font-weight: 300; line-height: 0.9; color: var(--beige); margin-bottom: 40px;
  }
  .lookbook-title em { font-style: italic; color: var(--sand); }
  .lookbook-divider {
    width: 60px; height: 1px; background: var(--gold); margin-bottom: 32px;
  }
  .lookbook-desc {
    font-family: var(--sans); font-size: 12px; letter-spacing: 0.12em;
    color: var(--ash); line-height: 2.2; margin-bottom: 48px;
  }
  .lookbook-grid-overlay {
    position: absolute; right: 8%; top: 50%; transform: translateY(-50%);
    display: grid; grid-template-columns: 1fr 1fr; gap: 3px; width: 360px;
  }
  .lookbook-thumb {
    aspect-ratio: 2/3; position: relative; overflow: hidden; cursor: none;
  }
  .lookbook-thumb-bg {
    position: absolute; inset: 0;
    transition: transform 0.6s cubic-bezier(0.23,1,0.32,1);
  }
  .lookbook-thumb:hover .lookbook-thumb-bg { transform: scale(1.08); }
  .lt-1 { background: linear-gradient(135deg, #2A2318 0%, #1E1A12 100%); }
  .lt-2 { background: linear-gradient(135deg, #1E1C18 0%, #2E2820 100%); margin-top: 30px; }
  .lt-3 { background: linear-gradient(135deg, #251E15 0%, #1A1610 100%); margin-top: -30px; }
  .lt-4 { background: linear-gradient(135deg, #221D18 0%, #2A2318 100%); }
  .lt-overlay { position: absolute; inset: 0; background: linear-gradient(to top, rgba(0,0,0,0.6) 0%, transparent 60%); }
  .lt-label {
    position: absolute; bottom: 12px; left: 12px;
    font-family: var(--sans); font-size: 8px; letter-spacing: 0.3em;
    color: var(--sand); text-transform: uppercase;
  }

  /* === FEATURED PRODUCT === */
  .featured {
    background: var(--beige);
    padding: 120px 8%;
    display: grid; grid-template-columns: 1.2fr 1fr; gap: 80px; align-items: center;
  }
  .featured-visual {
    position: relative; aspect-ratio: 3/4; background: var(--charcoal); overflow: hidden;
  }
  .featured-visual-inner {
    position: absolute; inset: 0;
    background: linear-gradient(160deg, #2A2520 0%, #1E1A16 50%, #252018 100%);
  }
  .featured-badge {
    position: absolute; top: 32px; left: 32px; z-index: 10;
    font-family: var(--sans); font-size: 8px; letter-spacing: 0.4em;
    text-transform: uppercase; color: var(--gold);
    border: 1px solid rgba(184,152,90,0.5); padding: 8px 14px;
    background: rgba(14,13,12,0.6);
  }
  .featured-visual-shape {
    position: absolute; inset: 0; display: flex; align-items: center; justify-content: center;
  }
  .featured-info { padding: 20px 0; }
  .featured-label {
    font-family: var(--sans); font-size: 9px; letter-spacing: 0.5em;
    color: var(--ash); text-transform: uppercase; margin-bottom: 20px;
  }
  .featured-name {
    font-family: var(--serif); font-size: clamp(40px, 4vw, 56px);
    font-weight: 300; line-height: 1.05; color: var(--matte-black); margin-bottom: 12px;
  }
  .featured-name em { font-style: italic; }
  .featured-subname {
    font-family: var(--serif); font-size: 20px; font-weight: 300; font-style: italic;
    color: var(--ash); margin-bottom: 32px;
  }
  .featured-divider { width: 40px; height: 1px; background: var(--gold); margin-bottom: 32px; }
  .featured-desc {
    font-family: var(--sans); font-size: 12px; letter-spacing: 0.08em;
    color: var(--graphite); line-height: 2.2; margin-bottom: 40px;
  }
  .featured-price-row {
    display: flex; align-items: baseline; gap: 16px; margin-bottom: 40px;
  }
  .featured-price {
    font-family: var(--serif); font-size: 32px; font-weight: 300; color: var(--matte-black);
  }
  .featured-price-label {
    font-family: var(--sans); font-size: 10px; letter-spacing: 0.2em;
    color: var(--ash); text-transform: uppercase;
  }
  .featured-sizes {
    display: flex; gap: 8px; margin-bottom: 40px;
  }
  .size-chip {
    font-family: var(--sans); font-size: 10px; letter-spacing: 0.15em;
    color: var(--graphite); border: 1px solid rgba(46,44,42,0.2);
    padding: 8px 16px; cursor: none; transition: all 0.3s;
  }
  .size-chip:hover, .size-chip.active {
    background: var(--matte-black); color: var(--beige); border-color: var(--matte-black);
  }
  .featured-actions { display: flex; gap: 16px; }
  .btn-dark {
    font-family: var(--sans); font-size: 11px; letter-spacing: 0.2em; text-transform: uppercase;
    color: var(--beige); background: var(--matte-black); border: none;
    padding: 16px 40px; cursor: none; transition: all 0.4s; flex: 1; text-align: center;
    position: relative; overflow: hidden;
  }
  .btn-dark::before {
    content: ''; position: absolute; inset: 0;
    background: var(--graphite); transform: translateX(-101%);
    transition: transform 0.4s cubic-bezier(0.23,1,0.32,1);
  }
  .btn-dark:hover::before { transform: translateX(0); }
  .btn-dark span { position: relative; z-index: 1; }
  .btn-outline-dark {
    font-family: var(--sans); font-size: 11px; letter-spacing: 0.2em; text-transform: uppercase;
    color: var(--matte-black); background: transparent;
    border: 1px solid rgba(46,44,42,0.4); padding: 16px 24px; cursor: none;
    transition: all 0.3s; display: flex; align-items: center; justify-content: center;
  }
  .btn-outline-dark:hover { border-color: var(--matte-black); }

  /* === PHILOSOPHY SECTION === */
  .philosophy {
    background: var(--matte-black); padding: 140px 8%;
    text-align: center; position: relative; overflow: hidden;
  }
  .philosophy-bg-text {
    position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%);
    font-family: var(--serif); font-size: 300px; font-weight: 300;
    color: rgba(245,240,232,0.015); white-space: nowrap; pointer-events: none;
    user-select: none; letter-spacing: -0.05em;
  }
  .philosophy-quote {
    font-family: var(--serif); font-size: clamp(28px, 3.5vw, 44px);
    font-weight: 300; font-style: italic; line-height: 1.5;
    color: var(--beige); max-width: 760px; margin: 0 auto 32px;
    position: relative; z-index: 1;
  }
  .philosophy-attr {
    font-family: var(--sans); font-size: 10px; letter-spacing: 0.4em;
    color: var(--gold); text-transform: uppercase; position: relative; z-index: 1;
  }

  /* === NEWSLETTER === */
  .newsletter {
    background: var(--charcoal);
    padding: 100px 8%;
    display: grid; grid-template-columns: 1fr 1fr; gap: 80px; align-items: center;
    border-top: 1px solid rgba(184,152,90,0.15);
  }
  .newsletter-title {
    font-family: var(--serif); font-size: clamp(36px, 4vw, 52px);
    font-weight: 300; line-height: 1.1; color: var(--beige);
  }
  .newsletter-title em { font-style: italic; color: var(--sand); }
  .newsletter-desc {
    font-family: var(--sans); font-size: 12px; letter-spacing: 0.08em;
    color: var(--ash); line-height: 2; margin-top: 20px;
  }
  .newsletter-form { display: flex; gap: 0; }
  .newsletter-input {
    flex: 1; background: transparent;
    border: 1px solid rgba(184,152,90,0.3); border-right: none;
    padding: 16px 24px; font-family: var(--sans); font-size: 12px;
    letter-spacing: 0.1em; color: var(--beige); outline: none;
    transition: border-color 0.3s;
  }
  .newsletter-input::placeholder { color: var(--ash); }
  .newsletter-input:focus { border-color: var(--gold); }
  .newsletter-submit {
    font-family: var(--sans); font-size: 10px; letter-spacing: 0.3em; text-transform: uppercase;
    color: var(--matte-black); background: var(--gold); border: none;
    padding: 16px 32px; cursor: none; transition: background 0.3s;
  }
  .newsletter-submit:hover { background: var(--gold-light); }

  /* === FOOTER === */
  footer {
    background: var(--matte-black);
    padding: 80px 8% 40px;
    border-top: 1px solid rgba(184,152,90,0.1);
  }
  .footer-top {
    display: grid; grid-template-columns: 2fr 1fr 1fr 1fr; gap: 60px; margin-bottom: 60px;
  }
  .footer-logo {
    font-family: var(--display); font-size: 22px; letter-spacing: 0.35em;
    color: var(--beige); margin-bottom: 20px; font-weight: 600;
  }
  .footer-tagline {
    font-family: var(--serif); font-size: 15px; font-style: italic;
    color: var(--ash); line-height: 1.8; max-width: 280px;
  }
  .footer-col-title {
    font-family: var(--sans); font-size: 9px; letter-spacing: 0.4em;
    color: var(--gold); text-transform: uppercase; margin-bottom: 24px;
  }
  .footer-links { list-style: none; display: flex; flex-direction: column; gap: 12px; }
  .footer-links a {
    font-family: var(--sans); font-size: 12px; letter-spacing: 0.08em;
    color: var(--ash); text-decoration: none; transition: color 0.3s;
  }
  .footer-links a:hover { color: var(--sand); }
  .footer-bottom {
    border-top: 1px solid rgba(184,152,90,0.1); padding-top: 32px;
    display: flex; justify-content: space-between; align-items: center;
  }
  .footer-copy {
    font-family: var(--sans); font-size: 10px; letter-spacing: 0.15em; color: var(--graphite);
  }
  .footer-legal {
    display: flex; gap: 32px;
  }
  .footer-legal a {
    font-family: var(--sans); font-size: 10px; letter-spacing: 0.1em;
    color: var(--graphite); text-decoration: none; transition: color 0.3s;
  }
  .footer-legal a:hover { color: var(--sand); }

  /* === ANIMATIONS === */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(30px); }
    to { opacity: 1; transform: translateY(0); }
  }
  @keyframes fadeIn {
    from { opacity: 0; } to { opacity: 1; }
  }
  .reveal {
    opacity: 0; transform: translateY(40px);
    transition: opacity 0.9s cubic-bezier(0.23,1,0.32,1), transform 0.9s cubic-bezier(0.23,1,0.32,1);
  }
  .reveal.visible { opacity: 1; transform: translateY(0); }
  .reveal-delay-1 { transition-delay: 0.1s; }
  .reveal-delay-2 { transition-delay: 0.2s; }
  .reveal-delay-3 { transition-delay: 0.3s; }
  .reveal-delay-4 { transition-delay: 0.4s; }

  /* Gold accent lines */
  .gold-line {
    display: inline-flex; align-items: center; gap: 16px;
  }
  .gold-line::before { content: ''; width: 30px; height: 1px; background: var(--gold); }
</style>
</head>
<body>

<!-- Custom Cursor -->
<div id="cursor-dot"></div>
<div id="cursor-ring"></div>

<!-- Navigation -->
<nav id="navbar">
  <a href="#" class="nav-logo">MAISON NOIR</a>
  <ul class="nav-links">
    <li><a href="#collection">Collection</a></li>
    <li><a href="#lookbook">Lookbook</a></li>
    <li><a href="#about">Atelier</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
  <div class="nav-actions">
    <button class="nav-btn">Boutique</button>
  </div>
</nav>

<!-- Hero -->
<section class="hero">
  <div class="hero-bg"></div>
  <div class="hero-texture"></div>
  <div class="hero-accent">
    <div class="hero-accent-img"></div>
    <div class="hero-accent-overlay"></div>
    <div class="hero-figure">
      <svg viewBox="0 0 300 600" fill="none" xmlns="http://www.w3.org/2000/svg">
        <ellipse cx="150" cy="80" rx="45" ry="55" fill="rgba(196,180,154,0.15)"/>
        <path d="M105 135 Q90 200 80 320 Q75 400 85 520 L100 520 L108 380 Q115 300 150 270 Q185 300 192 380 L200 520 L215 520 Q225 400 220 320 Q210 200 195 135 Z" fill="rgba(196,180,154,0.12)"/>
        <path d="M80 200 Q50 220 40 280 Q45 300 65 295 Q75 260 90 240 Z" fill="rgba(196,180,154,0.08)"/>
        <path d="M220 200 Q250 220 260 280 Q255 300 235 295 Q225 260 210 240 Z" fill="rgba(196,180,154,0.08)"/>
        <line x1="150" y1="0" x2="150" y2="600" stroke="rgba(184,152,90,0.08)" stroke-width="1"/>
      </svg>
    </div>
  </div>
  <div class="hero-content">
    <div class="hero-eyebrow">Autumn / Winter 2024</div>
    <h1 class="hero-title">The Art<br>of <em>Shadows</em></h1>
    <p class="hero-sub">Where darkness becomes poetry. A collection born from the tension between restraint and desire.</p>
    <div class="hero-cta">
      <a href="#collection" class="btn-primary"><span>Explore Collection</span></a>
      <a href="#lookbook" class="btn-ghost">
        <span class="btn-ghost-arrow"></span>
        View Lookbook
      </a>
    </div>
  </div>
  <div class="hero-scroll-hint">
    <div class="scroll-line"></div>
    Scroll
  </div>
</section>

<!-- Marquee -->
<div class="marquee-strip">
  <div class="marquee-track">
    <div class="marquee-item">Maison Noir</div>
    <div class="marquee-item">Aw/24 Collection</div>
    <div class="marquee-item">Paris · Milan · Tokyo</div>
    <div class="marquee-item">Haute Couture</div>
    <div class="marquee-item">The Art of Shadows</div>
    <div class="marquee-item">Maison Noir</div>
    <div class="marquee-item">Aw/24 Collection</div>
    <div class="marquee-item">Paris · Milan · Tokyo</div>
    <div class="marquee-item">Haute Couture</div>
    <div class="marquee-item">The Art of Shadows</div>
    <div class="marquee-item">Maison Noir</div>
    <div class="marquee-item">Aw/24 Collection</div>
    <div class="marquee-item">Paris · Milan · Tokyo</div>
    <div class="marquee-item">Haute Couture</div>
    <div class="marquee-item">The Art of Shadows</div>
  </div>
</div>

<!-- Editorial Intro -->
<section class="editorial" id="about">
  <div>
    <div class="editorial-label reveal">The House</div>
    <h2 class="editorial-title reveal reveal-delay-1">A Language<br>of <em>Pure</em><br>Elegance</h2>
    <p class="editorial-body reveal reveal-delay-2">Founded in the ateliers of Paris, Maison Noir was born from a single conviction: that true luxury exists in the space between what is said and what is felt. Each garment is a meditation on form, a dialogue between the body and the void.</p>
    <a href="#" class="btn-ghost reveal reveal-delay-3" style="display:inline-flex;">
      <span class="btn-ghost-arrow" style="background:var(--sand)"></span>
      Our Story
    </a>
  </div>
  <div class="editorial-visual reveal reveal-delay-2">
    <div class="editorial-visual-bg"></div>
    <div class="editorial-visual-accent"></div>
    <div class="editorial-visual-number">I</div>
    <div class="editorial-visual-cross"></div>
    <div style="position:absolute;inset:0;display:flex;align-items:center;justify-content:center;">
      <svg width="120" height="200" viewBox="0 0 120 200" fill="none" opacity="0.15">
        <rect x="20" y="10" width="80" height="180" rx="2" stroke="#B8985A" stroke-width="0.5"/>
        <line x1="60" y1="10" x2="60" y2="190" stroke="#B8985A" stroke-width="0.5" opacity="0.5"/>
        <ellipse cx="60" cy="35" rx="22" ry="26" stroke="#B8985A" stroke-width="0.5"/>
        <path d="M38 62 Q30 100 28 150 Q30 170 40 175 L80 175 Q90 170 92 150 Q90 100 82 62 Z" stroke="#B8985A" stroke-width="0.5" fill="none"/>
      </svg>
    </div>
    <div class="editorial-visual-tag">Atelier, Paris XVI</div>
  </div>
</section>

<!-- Products Collection -->
<section class="collection" id="collection">
  <div class="collection-header">
    <div class="collection-title reveal">
      <em>Selected</em>
      Pieces
    </div>
    <div class="collection-meta reveal">
      Autumn / Winter 2024<br>
      16 Exclusive Pieces
    </div>
  </div>
  <div class="products-grid">

    <!-- Product 1 -->
    <div class="product-card reveal">
      <div class="product-bg product-bg-1"></div>
      <div class="product-shape">
        <svg viewBox="0 0 200 300" fill="none">
          <path d="M60 20 Q40 60 35 120 Q32 180 40 260 L80 260 L85 180 Q90 150 100 140 Q110 150 115 180 L120 260 L160 260 Q168 180 165 120 Q160 60 140 20 Z" stroke="rgba(196,180,154,0.4)" stroke-width="1" fill="rgba(196,180,154,0.04)"/>
          <ellipse cx="100" cy="15" rx="28" ry="20" stroke="rgba(196,180,154,0.3)" stroke-width="1" fill="none"/>
        </svg>
      </div>
      <div class="product-overlay"></div>
      <div class="product-hover-reveal"></div>
      <div class="product-number">01</div>
      <div class="product-info">
        <div class="product-category">Ready to Wear</div>
        <div class="product-name">Le Manteau <em>Nocturne</em></div>
        <div class="product-price">€ 4,850</div>
        <a href="#" class="product-action">
          <div class="product-action-line"></div>
          Discover
        </a>
      </div>
    </div>

    <!-- Product 2 -->
    <div class="product-card reveal reveal-delay-1">
      <div class="product-bg product-bg-2"></div>
      <div class="product-shape">
        <svg viewBox="0 0 200 300" fill="none">
          <path d="M70 10 L130 10 L150 80 L140 260 L60 260 L50 80 Z" stroke="rgba(196,180,154,0.35)" stroke-width="1" fill="rgba(196,180,154,0.03)"/>
          <line x1="100" y1="10" x2="100" y2="260" stroke="rgba(184,152,90,0.15)" stroke-width="0.5"/>
          <rect x="75" y="40" width="50" height="60" rx="2" stroke="rgba(196,180,154,0.2)" stroke-width="0.5" fill="none"/>
        </svg>
      </div>
      <div class="product-overlay"></div>
      <div class="product-hover-reveal"></div>
      <div class="product-number">02</div>
      <div class="product-info">
        <div class="product-category">Accessories</div>
        <div class="product-name">Sac <em>Minuit</em></div>
        <div class="product-price">€ 2,200</div>
        <a href="#" class="product-action">
          <div class="product-action-line"></div>
          Discover
        </a>
      </div>
    </div>

    <!-- Product 3 -->
    <div class="product-card reveal reveal-delay-2">
      <div class="product-bg product-bg-3"></div>
      <div class="product-shape">
        <svg viewBox="0 0 200 300" fill="none">
          <path d="M100 20 Q60 40 50 100 L50 200 Q50 240 100 255 Q150 240 150 200 L150 100 Q140 40 100 20 Z" stroke="rgba(196,180,154,0.3)" stroke-width="1" fill="rgba(196,180,154,0.04)"/>
          <path d="M100 20 Q120 50 125 100" stroke="rgba(184,152,90,0.2)" stroke-width="0.5" fill="none"/>
          <circle cx="100" cy="140" r="30" stroke="rgba(196,180,154,0.15)" stroke-width="0.5" fill="none"/>
        </svg>
      </div>
      <div class="product-overlay"></div>
      <div class="product-hover-reveal"></div>
      <div class="product-number">03</div>
      <div class="product-info">
        <div class="product-category">Haute Couture</div>
        <div class="product-name">La Robe <em>Éclipse</em></div>
        <div class="product-price">€ 12,500</div>
        <a href="#" class="product-action">
          <div class="product-action-line"></div>
          Discover
        </a>
      </div>
    </div>

  </div>
</section>

<!-- Lookbook -->
<section class="lookbook" id="lookbook">
  <div class="lookbook-bg"></div>
  <div class="lookbook-geometric"></div>
  <div class="lookbook-content">
    <div class="lookbook-season reveal">AW/24 — The Lookbook</div>
    <h2 class="lookbook-title reveal reveal-delay-1">
      Between<br>
      <em>Night</em><br>
      & Form
    </h2>
    <div class="lookbook-divider reveal reveal-delay-2"></div>
    <p class="lookbook-desc reveal reveal-delay-2">A visual narrative exploring duality — the tension between the structured and the fluid, the visible and the concealed. Shot in the abandoned salons of the 16th arrondissement.</p>
    <a href="#" class="btn-primary reveal reveal-delay-3"><span>View Full Lookbook</span></a>
  </div>
  <div class="lookbook-grid-overlay reveal reveal-delay-2">
    <div class="lookbook-thumb">
      <div class="lookbook-thumb-bg lt-1"></div>
      <div class="lt-overlay"></div>
      <div class="lt-label">Look 01</div>
    </div>
    <div class="lookbook-thumb">
      <div class="lookbook-thumb-bg lt-2"></div>
      <div class="lt-overlay"></div>
      <div class="lt-label">Look 02</div>
    </div>
    <div class="lookbook-thumb">
      <div class="lookbook-thumb-bg lt-3"></div>
      <div class="lt-overlay"></div>
      <div class="lt-label">Look 03</div>
    </div>
    <div class="lookbook-thumb">
      <div class="lookbook-thumb-bg lt-4"></div>
      <div class="lt-overlay"></div>
      <div class="lt-label">Look 04</div>
    </div>
  </div>
</section>

<!-- Featured Product -->
<section class="featured">
  <div class="featured-visual reveal">
    <div class="featured-visual-inner"></div>
    <div class="featured-badge">New Arrival</div>
    <div class="featured-visual-shape">
      <svg width="55%" height="55%" viewBox="0 0 240 320" fill="none" opacity="0.2">
        <path d="M120 20 Q75 45 65 110 L60 220 Q60 280 120 295 Q180 280 180 220 L175 110 Q165 45 120 20 Z" stroke="#B8985A" stroke-width="1"/>
        <ellipse cx="120" cy="20" rx="30" ry="18" stroke="#B8985A" stroke-width="1"/>
        <line x1="60" y1="150" x2="180" y2="150" stroke="#B8985A" stroke-width="0.5" opacity="0.5"/>
        <line x1="120" y1="20" x2="120" y2="295" stroke="#B8985A" stroke-width="0.5" opacity="0.5"/>
        <circle cx="120" cy="155" r="20" stroke="#B8985A" stroke-width="0.5"/>
      </svg>
    </div>
  </div>
  <div class="featured-info">
    <div class="featured-label reveal">Featured Piece</div>
    <h2 class="featured-name reveal reveal-delay-1">Le Blazer<br><em>Ombré Noir</em></h2>
    <p class="featured-subname reveal reveal-delay-1">The Signature Piece</p>
    <div class="featured-divider reveal reveal-delay-2"></div>
    <p class="featured-desc reveal reveal-delay-2">Crafted from double-faced cashmere sourced exclusively from the highlands of Mongolia. A structured silhouette that dissolves at its edges, as if the garment itself is dissolving into light.</p>
    <div class="featured-price-row reveal reveal-delay-2">
      <div class="featured-price">€ 6,400</div>
      <div class="featured-price-label">Incl. Duties & Tax</div>
    </div>
    <div class="featured-sizes reveal reveal-delay-3">
      <div class="size-chip">34</div>
      <div class="size-chip active">36</div>
      <div class="size-chip">38</div>
      <div class="size-chip">40</div>
      <div class="size-chip">42</div>
    </div>
    <div class="featured-actions reveal reveal-delay-3">
      <button class="btn-dark"><span>Add to Cart</span></button>
      <button class="btn-outline-dark">♡</button>
    </div>
  </div>
</section>

<!-- Philosophy -->
<section class="philosophy">
  <div class="philosophy-bg-text">NOIR</div>
  <p class="philosophy-quote reveal">"Luxury is not the abundance of things. It is the absence of everything superfluous."</p>
  <div class="philosophy-attr reveal reveal-delay-1">— Maison Noir, Paris, Est. 1987</div>
</section>

<!-- Newsletter -->
<section class="newsletter">
  <div>
    <h2 class="newsletter-title reveal">Enter <em>Our</em><br>Inner Circle</h2>
    <p class="newsletter-desc reveal reveal-delay-1">Private access to new collections, exclusive events, and the world of Maison Noir. By invitation only.</p>
  </div>
  <div class="reveal reveal-delay-2">
    <div class="newsletter-form">
      <input type="email" class="newsletter-input" placeholder="Your email address">
      <button class="newsletter-submit">Request Access</button>
    </div>
  </div>
</section>

<!-- Footer -->
<footer>
  <div class="footer-top">
    <div>
      <div class="footer-logo">MAISON NOIR</div>
      <p class="footer-tagline">Crafting silence into wearable form since 1987. Atelier at 14 Rue du Faubourg Saint-Honoré, Paris.</p>
    </div>
    <div>
      <div class="footer-col-title">Collections</div>
      <ul class="footer-links">
        <li><a href="#">Autumn / Winter</a></li>
        <li><a href="#">Haute Couture</a></li>
        <li><a href="#">Accessories</a></li>
        <li><a href="#">Archive</a></li>
      </ul>
    </div>
    <div>
      <div class="footer-col-title">Maison</div>
      <ul class="footer-links">
        <li><a href="#">Our Story</a></li>
        <li><a href="#">Atelier</a></li>
        <li><a href="#">Sustainability</a></li>
        <li><a href="#">Careers</a></li>
      </ul>
    </div>
    <div>
      <div class="footer-col-title">Client Services</div>
      <ul class="footer-links">
        <li><a href="#">Personal Shopping</a></li>
        <li><a href="#">Alterations</a></li>
        <li><a href="#">Boutiques</a></li>
        <li><a href="#">Care Guide</a></li>
      </ul>
    </div>
  </div>
  <div class="footer-bottom">
    <div class="footer-copy">© 2024 Maison Noir. All Rights Reserved.</div>
    <div class="footer-legal">
      <a href="#">Privacy Policy</a>
      <a href="#">Terms of Use</a>
      <a href="#">Cookies</a>
    </div>
  </div>
</footer>

<script>
  // Custom cursor
  const dot = document.getElementById('cursor-dot');
  const ring = document.getElementById('cursor-ring');
  let mx = 0, my = 0, rx = 0, ry = 0;

  document.addEventListener('mousemove', e => {
    mx = e.clientX; my = e.clientY;
    dot.style.left = mx + 'px';
    dot.style.top = my + 'px';
  });

  function animateRing() {
    rx += (mx - rx) * 0.12;
    ry += (my - ry) * 0.12;
    ring.style.left = rx + 'px';
    ring.style.top = ry + 'px';
    requestAnimationFrame(animateRing);
  }
  animateRing();

  document.querySelectorAll('a, button, .product-card, .size-chip, .lookbook-thumb, .nav-btn, .btn-primary, .btn-ghost, .btn-dark, .newsletter-submit').forEach(el => {
    el.addEventListener('mouseenter', () => document.body.classList.add('hovering'));
    el.addEventListener('mouseleave', () => document.body.classList.remove('hovering'));
  });

  // Navbar scroll
  const navbar = document.getElementById('navbar');
  window.addEventListener('scroll', () => {
    navbar.classList.toggle('scrolled', window.scrollY > 60);
  });

  // Scroll reveal
  const reveals = document.querySelectorAll('.reveal');
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(e => { if (e.isIntersecting) { e.target.classList.add('visible'); } });
  }, { threshold: 0.12 });
  reveals.forEach(el => observer.observe(el));

  // Size selector
  document.querySelectorAll('.size-chip').forEach(chip => {
    chip.addEventListener('click', () => {
      document.querySelectorAll('.size-chip').forEach(c => c.classList.remove('active'));
      chip.classList.add('active');
    });
  });

  // Parallax hero accent
  window.addEventListener('scroll', () => {
    const scrollY = window.scrollY;
    const heroAccent = document.querySelector('.hero-accent');
    if (heroAccent) {
      heroAccent.style.transform = `translateY(${scrollY * 0.15}px)`;
    }
    const heroBg = document.querySelector('.hero-bg');
    if (heroBg) {
      heroBg.style.transform = `translateY(${scrollY * 0.08}px)`;
    }
  });
</script>
</body>
</html>
