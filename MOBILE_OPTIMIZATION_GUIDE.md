
# Mobile Optimization Guide for Project Launchpad Website

## Executive Summary
This guide provides a comprehensive, step-by-step approach to optimize the Project Launchpad website for mobile devices. Currently, the site has minimal mobile optimization with only basic responsive breakpoints at 768px and 480px.

---

## Current State Analysis

### Existing Mobile Support
- ✅ Basic viewport meta tag present in index.html
- ✅ Some responsive grid adjustments at 768px
- ✅ Navigation hidden on mobile (768px)
- ⚠️ Limited touch-friendly interactions
- ❌ No mobile-first approach
- ❌ Inconsistent mobile breakpoints across pages
- ❌ Large text sizes not optimized for small screens
- ❌ No hamburger menu implementation
- ❌ Images not optimized for mobile bandwidth

### Critical Issues Found
1. **Missing viewport meta tags** in joinplp.html, support.html, and about/*.html files
2. **Navigation disappears** on mobile with no replacement menu
3. **Typography too large** for small screens (hero h1: 56px on mobile)
4. **No touch optimization** - buttons and links may be too small
5. **Tables not responsive** (joinplp.html value table)
6. **Forms not optimized** for mobile input

---

## Phase 1: Foundation - Critical Mobile Fixes

### 1.1 Add Viewport Meta Tag to ALL Pages
**Priority: CRITICAL** | **Effort: 5 minutes**

**Files Missing Viewport Tag:**
- joinplp.html
- support.html
- about/fuel-our-mission.html
- about/meet-the-founders.html
- about/our-story.html
- about/plp-impact-network.html
- All support/*.html files

**Add this to `<head>` section:**
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

### 1.2 Implement Mobile Navigation Menu
**Priority: CRITICAL** | **Effort: 2 hours**

**Current Issue:** Navigation simply disappears on mobile (display: none at 768px)

**Solution: Add Hamburger Menu**

**Step 1: Add CSS to styles.css**
```css
/* Mobile Menu Toggle Button */
.mobile-menu-toggle {
    display: none;
    background: none;
    border: none;
    font-size: 1.75rem;
    color: #6b7280;
    cursor: pointer;
    padding: 8px;
    transition: color 0.2s;
}

.mobile-menu-toggle:hover {
    color: #8c52ff;
}

@media (max-width: 768px) {
    .mobile-menu-toggle {
        display: block;
        z-index: 1001;
    }
    
    .nav-links {
        display: none;
        position: fixed;
        top: 81px; /* Height of header */
        left: 0;
        right: 0;
        bottom: 0;
        background: white;
        flex-direction: column;
        padding: 20px;
        gap: 0;
        overflow-y: auto;
        z-index: 999;
    }
    
    .nav-links.active {
        display: flex;
    }
    
    .nav-links li {
        width: 100%;
        border-bottom: 1px solid #f3f4f6;
    }
    
    .nav-links > li > a {
        display: block;
        padding: 16px 0;
        font-size: 1.125rem;
    }
    
    .dropdown-content {
        position: static;
        box-shadow: none;
        border: none;
        padding-left: 20px;
        background: #f8fafc;
        margin-top: 8px;
        border-radius: 8px;
    }
    
    .dropdown > a:after {
        float: right;
    }
    
    .dropdown:hover .dropdown-content {
        display: none; /* Disable hover on mobile */
    }
    
    .dropdown.active .dropdown-content {
        display: block;
    }
}
```

**Step 2: Add JavaScript (create mobile-nav.js or add to each page)**
```javascript
document.addEventListener('DOMContentLoaded', function() {
    // Create mobile menu toggle button
    const menuToggle = document.createElement('button');
    menuToggle.className = 'mobile-menu-toggle';
    menuToggle.innerHTML = '☰';
    menuToggle.setAttribute('aria-label', 'Toggle navigation menu');
    menuToggle.setAttribute('aria-expanded', 'false');
    
    const nav = document.querySelector('.nav');
    const navLinks = document.querySelector('.nav-links');
    const headerButtons = document.querySelector('.header-buttons');
    
    if (nav && navLinks) {
        // Insert toggle button before header buttons
        if (headerButtons) {
            headerButtons.parentNode.insertBefore(menuToggle, headerButtons);
        }
        
        // Toggle menu
        menuToggle.addEventListener('click', function() {
            const isActive = navLinks.classList.toggle('active');
            menuToggle.innerHTML = isActive ? '✕' : '☰';
            menuToggle.setAttribute('aria-expanded', isActive);
            document.body.style.overflow = isActive ? 'hidden' : '';
        });
        
        // Handle dropdown clicks on mobile
        const dropdowns = document.querySelectorAll('.dropdown');
        dropdowns.forEach(dropdown => {
            const link = dropdown.querySelector('a');
            link.addEventListener('click', function(e) {
                if (window.innerWidth <= 768) {
                    e.preventDefault();
                    dropdown.classList.toggle('active');
                }
            });
        });
        
        // Close menu when clicking outside
        document.addEventListener('click', function(e) {
            if (window.innerWidth <= 768 && 
                !nav.contains(e.target) && 
                navLinks.classList.contains('active')) {
                navLinks.classList.remove('active');
                menuToggle.innerHTML = '☰';
                menuToggle.setAttribute('aria-expanded', 'false');
                document.body.style.overflow = '';
            }
        });
    }
});
```

**Step 3: Add script tag to all HTML files before closing `</body>`**
```html
<script src="mobile-nav.js"></script>
```

### 1.3 Fix Typography for Mobile Screens
**Priority: HIGH** | **Effort: 30 minutes**

**Add to styles.css:**
```css
/* ===== MOBILE TYPOGRAPHY OPTIMIZATION ===== */

@media (max-width: 768px) {
    /* Hero Sections */
    .hero-text h1,
    .video-hero .hero-text h1 {
        font-size: 2rem !important; /* Down from 3.5rem */
        line-height: 1.2;
        margin-bottom: 16px;
    }
    
    .hero-text p,
    .video-hero .hero-text p {
        font-size: 1rem !important; /* Down from 1.25rem */
        margin-bottom: 24px;
    }
    
    /* Section Titles */
    .section-title {
        font-size: 1.75rem !important; /* Down from 2.5rem */
        line-height: 1.2;
        margin-bottom: 16px;
    }
    
    .section-subtitle {
        font-size: 1rem !important; /* Down from 1.25rem */
        line-height: 1.5;
    }
    
    /* Content Headings */
    h1 {
        font-size: 2rem !important;
    }
    
    h2 {
        font-size: 1.5rem !important;
    }
    
    h3 {
        font-size: 1.25rem !important;
    }
    
    /* Body Text */
    body {
        font-size: 16px;
    }
    
    p {
        font-size: 1rem;
        line-height: 1.6;
    }
    
    /* Buttons */
    .btn-primary,
    .btn-secondary,
    .btn-white,
    .btn-outline-white,
    .btn-login {
        padding: 12px 24px;
        font-size: 1rem;
    }
}

@media (max-width: 480px) {
    .hero-text h1,
    .video-hero .hero-text h1 {
        font-size: 1.75rem !important;
    }
    
    .section-title {
        font-size: 1.5rem !important;
    }
    
    h1 {
        font-size: 1.75rem !important;
    }
    
    h2 {
        font-size: 1.375rem !important;
    }
}
```

---

## Phase 2: Layout & Spacing Optimization

### 2.1 Optimize Grid Layouts for Mobile
**Priority: HIGH** | **Effort: 1 hour**

**Add to styles.css:**
```css
/* ===== MOBILE GRID OPTIMIZATION ===== */

@media (max-width: 768px) {
    /* All feature grids to single column */
    .features-icons,
    .features-grid,
    .outcomes-grid,
    .engagement-grid,
    .value-cards-grid,
    .value-proof-grid {
        grid-template-columns: 1fr !important;
        gap: 24px;
    }
    
    /* Stats grid to single column */
    .stats-grid {
        grid-template-columns: 1fr !important;
        gap: 24px;
    }
    
    /* Two-column layouts */
    .two-column,
    .newsletter-content {
        grid-template-columns: 1fr !important;
        gap: 32px;
    }
    
    /* Testimonials */
    .testimonials-grid {
        grid-template-columns: 1fr !important;
        gap: 24px;
    }
    
    /* Membership cards */
    .membership-grid {
        grid-template-columns: 1fr !important;
        gap: 24px;
    }
    
    /* Footer grid */
    .footer-grid {
        grid-template-columns: 1fr !important;
        gap: 32px;
        text-align: center;
    }
    
    /* Allies grid */
    .allies-grid {
        grid-template-columns: 1fr !important;
        gap: 20px;
    }
}
```

### 2.2 Optimize Section Spacing
**Priority: MEDIUM** | **Effort: 30 minutes**

```css
/* ===== MOBILE SPACING OPTIMIZATION ===== */

@media (max-width: 768px) {
    /* Reduce section padding */
    .section {
        padding: 60px 0 !important;
    }
    
    /* Large sections */
    .video-hero,
    .outcomes-section,
    .cta-section,
    .everything-section {
        padding: 50px 0 !important;
    }
    
    /* Medium sections */
    .stats-section,
    .membership-section,
    .engagement-section,
    .value-section {
        padding: 50px 0 !important;
    }
    
    /* Small sections */
    .partners-section,
    .testimonials-section {
        padding: 40px 0 !important;
    }
    
    /* Container padding */
    .container {
        padding: 0 16px;
    }
    
    /* Card padding */
    .feature-card,
    .outcome-card,
    .membership-card,
    .engagement-card,
    .value-card {
        padding: 24px 20px;
    }
    
    /* Content wrappers */
    .content-wrapper,
    .support-content {
        padding: 32px 20px;
    }
    
    /* Section headers */
    .section-header {
        margin-bottom: 40px;
    }
}

@media (max-width: 480px) {
    .section {
        padding: 40px 0 !important;
    }
    
    .container {
        padding: 0 12px;
    }
}
```

### 2.3 Optimize Hero Section
**Priority: HIGH** | **Effort: 30 minutes**

```css
/* ===== MOBILE HERO OPTIMIZATION ===== */

@media (max-width: 768px) {
    .video-hero {
        padding: 60px 0 !important;
    }
    
    .hero-content {
        max-width: 100%;
    }
    
    .hero-text-container {
        padding: 24px;
        border-radius: 12px;
    }
    
    .hero-buttons {
        flex-direction: column;
        gap: 12px;
        width: 100%;
    }
    
    .hero-buttons .btn-primary,
    .hero-buttons .btn-secondary {
        width: 100%;
        text-align: center;
        padding: 14px 24px;
        font-size: 1rem;
    }
    
    /* Stats bar in hero */
    .stats-bar {
        flex-direction: column;
        gap: 20px;
        padding: 20px 16px;
    }
    
    .stat {
        padding: 0;
    }
    
    .stat-number {
        font-size: 2rem;
    }
}

@media (max-width: 480px) {
    .video-hero {
        padding: 40px 0 !important;
    }
    
    .hero-text-container {
        padding: 20px;
    }
}
```

---

## Phase 3: Touch & Interaction Optimization

### 3.1 Ensure Minimum Touch Target Sizes
**Priority: HIGH** | **Effort: 45 minutes**

**Minimum Requirements:**
- Apple: 44x44px
- Google: 48x48px
- We'll use 44px minimum

```css
/* ===== TOUCH TARGET OPTIMIZATION ===== */

@media (max-width: 768px) {
    /* All buttons */
    .btn-primary,
    .btn-secondary,
    .btn-login,
    .btn-white,
    .btn-outline-white,
    .btn-grant-connect,
    .btn-subscribe,
    .btn-toggle-tools,
    .join-button,
    .cta-button {
        min-height: 44px;
        padding: 12px 24px;
        display: inline-flex;
        align-items: center;
        justify-content: center;
    }
    
    /* Navigation links */
    .nav-links a {
        min-height: 44px;
        display: flex;
        align-items: center;
        padding: 12px 16px;
    }
    
    /* Dropdown items */
    .dropdown-content a {
        min-height: 44px;
        padding: 12px 20px;
        display: flex;
        align-items: center;
    }
    
    /* Footer links */
    .footer-links a {
        min-height: 44px;
        display: inline-flex;
        align-items: center;
        padding: 8px 0;
    }
    
    /* Social media icons */
    .footer-social a {
        min-width: 44px;
        min-height: 44px;
        display: inline-flex;
        align-items: center;
        justify-content: center;
    }
    
    /* Carousel controls */
    .carousel-prev,
    .carousel-next {
        min-width: 44px;
        min-height: 44px;
    }
    
    /* Tab buttons */
    .preview-tab {
        min-height: 44px;
        padding: 12px 24px;
    }
}
```

### 3.2 Optimize Forms for Mobile
**Priority: HIGH** | **Effort: 30 minutes**

```css
/* ===== MOBILE FORM OPTIMIZATION ===== */

@media (max-width: 768px) {
    /* Newsletter form */
    .newsletter-form {
        flex-direction: column;
        gap: 12px;
    }
    
    /* All input fields */
    .email-input,
    input[type="text"],
    input[type="email"],
    input[type="tel"],
    input[type="search"],
    textarea,
    select {
        width: 100%;
        font-size: 16px !important; /* Prevents iOS zoom */
        padding: 14px 16px;
        border-radius: 8px;
        -webkit-appearance: none;
        appearance: none;
    }
    
    /* Submit buttons */
    .btn-subscribe,
    button[type="submit"],
    input[type="submit"] {
        width: 100%;
        padding: 14px;
        font-size: 1rem;
    }
    
    /* Prevent iOS zoom on focus */
    input:focus,
    textarea:focus,
    select:focus {
        font-size: 16px !important;
    }
}
```

### 3.3 Improve Card Interactions
**Priority: MEDIUM** | **Effort: 20 minutes**

```css
/* ===== MOBILE CARD INTERACTIONS ===== */

@media (max-width: 768px) {
    /* Reduce hover effects on mobile (use tap instead) */
    .feature-card:hover,
    .outcome-card:hover,
    .membership-card:hover,
    .testimonial-card:hover {
        transform: none;
    }
    
    /* Add active state for touch */
    .feature-card:active,
    .outcome-card:active,
    .membership-card:active {
        transform: scale(0.98);
        transition: transform 0.1s;
    }
    
    /* Ensure cards are tappable */
    .feature-card,
    .outcome-card,
    .membership-card,
    .section-card {
        cursor: pointer;
        -webkit-tap-highlight-color: rgba(140, 82, 255, 0.1);
    }
}
```

---

## Phase 4: Content-Specific Optimizations

### 4.1 Make Tables Responsive
**Priority: HIGH** | **Effort: 1 hour**

**For joinplp.html value table:**

```css
/* ===== MOBILE TABLE OPTIMIZATION ===== */

@media (max-width: 768px) {
    .value-table-wrapper {
        overflow-x: auto;
        -webkit-overflow-scrolling: touch;
        margin: 0 -16px;
        padding: 0 16px;
    }
    
    .value-table {
        min-width: 500px;
        font-size: 0.875rem;
    }
    
    .value-table th,
    .value-table td {
        padding: 10px 12px;
    }
}

@media (max-width: 480px) {
    /* Stack table on very small screens */
    .value-table,
    .value-table thead,
    .value-table tbody,
    .value-table tr,
    .value-table th,
    .value-table td {
        display: block;
        width: 100%;
    }
    
    .value-table thead {
        display: none;
    }
    
    .value-table tr {
        margin-bottom: 16px;
        border: 1px solid #e5e7eb;
        border-radius: 8px;
        padding: 12px;
        background: white;
    }
    
    .value-table td {
        text-align: left;
        padding: 8px 0;
        border: none;
        position: relative;
        padding-left: 50%;
    }
    
    .value-table td:before {
        content: attr(data-label);
        position: absolute;
        left: 0;
        width: 45%;
        font-weight: 600;
        color: #8c52ff;
    }
    
    .value-table .total-row,
    .value-table .investment-row {
        background: #f8fafc;
    }
}
```

**Update HTML in joinplp.html - add data-label attributes:**
```html
<tr>
    <td data-label="What You Get">18+ professional development courses</td>
    <td data-label="Market Value">$200-500 each</td>
</tr>
```

### 4.2 Optimize Sneak Preview Carousel
**Priority: MEDIUM** | **Effort: 45 minutes**

```css
/* ===== MOBILE CAROUSEL OPTIMIZATION ===== */

@media (max-width: 768px) {
    .preview-tabs {
        flex-direction: column;
        gap: 12px;
    }
    
    .preview-tab {
        width: 100%;
        padding: 12px 20px;
        font-size: 1rem;
    }
    
    .preview-slide {
        padding: 32px 20px;
        min-height: auto;
    }
    
    .slide-content {
        max-width: 100%;
    }
    
    .slide-content h3 {
        font-size: 1.5rem;
    }
    
    .slide-content p {
        font-size: 1rem;
    }
    
    .feature-checklist li {
        font-size: 0.9375rem;
    }
    
    .carousel-controls {
        gap: 16px;
        margin-top: 24px;
    }
    
    .carousel-prev,
    .carousel-next {
        width: 44px;
        height: 44px;
        font-size: 1.25rem;
    }
    
    /* Add swipe support */
    .preview-carousel {
        touch-action: pan-y;
        -webkit-overflow-scrolling: touch;
    }
}
```

### 4.3 Optimize Footer
**Priority: MEDIUM** | **Effort: 30 minutes**

```css
/* ===== MOBILE FOOTER OPTIMIZATION ===== */

@media (max-width: 768px) {
    .footer {
        padding: 40px 20px 20px;
    }
    
    .footer-grid {
        grid-template-columns: 1fr !important;
        gap: 32px;
        text-align: center;
    }
    
    .footer-column {
        text-align: center;
    }
    
    .footer-logo {
        display: flex;
        justify-content: center;
    }
    
    .footer-description {
        text-align: center;
    }
    
    .footer-links {
        text-align: center;
    }
    
    .footer-social {
        justify-content: center !important;
    }
    
    .footer-bottom {
        padding-top: 20px;
    }
    
    .footer-bottom p {
        font-size: 0.875rem;
        line-height: 1.6;
    }
    
    .limited-spots {
        padding: 24px 20px;
    }
    
    .spots-remaining {
        font-size: 2.5rem;
    }
}
```

---

## Phase 5: Performance Optimization

### 5.1 Optimize Images for Mobile
**Priority: HIGH** | **Effort: 2 hours**

**Step 1: Create mobile-optimized images**
```bash
# Recommended image sizes:
# Mobile: 480px width
# Tablet: 768px width
# Desktop: 1200px width

# Hero background:
- hero_bg_mobile.jpg (480x320, ~50KB)
- hero_bg_tablet.jpg (768x512, ~100KB)
- hero_bg.jpg (1920x1280, ~200KB)

# Logo images:
- Optimize all partner logos to max 200px width
- Use WebP format where possible
```

**Step 2: Implement responsive images**
```html
<!-- Replace hero background in index.html -->
<style>
@media (max-width: 480px) {
    .video-hero {
        background-image: 
            linear-gradient(135deg, rgba(140, 82, 255, 0.8) 0%, rgba(255, 87, 87, 0.75) 100%),
            url('img/hero_bg_mobile.jpg');
    }
}

@media (min-width: 481px) and (max-width: 768px) {
    .video-hero {
        background-image: 
            linear-gradient(135deg, rgba(140, 82, 255, 0.8) 0%, rgba(255, 87, 87, 0.75) 100%),
            url('img/hero_bg_tablet.jpg');
    }
}
</style>
```

**Step 3: Add lazy loading to all images**
```html
<!-- Add loading="lazy" to all images -->
<img src="img/plp_logo.png" alt="Project Launchpad" loading="lazy">
<img src="img/logos/harmonia_logo.png" alt="Harmonia" loading="lazy">
```

### 5.2 Reduce Animations on Mobile
**Priority: MEDIUM** | **Effort: 30 minutes**

```css
/* ===== MOBILE ANIMATION OPTIMIZATION ===== */

/* Respect user preferences */
@media (prefers-reduced-motion: reduce) {
    *,
    *::before,
    *::after {
        animation-duration: 0.01ms !important;
        animation-iteration-count: 1 !important;
        transition-duration: 0.01ms !important;
        scroll-behavior: auto !important;
    }
}

/* Simplify animations on mobile */
@media (max-width: 768px) {
    .fade-in,
    .slide-up,
    .slide-left,
    .slide-right,
    .scale-up {
        transition-duration: 0.3s;
    }
    
    /* Disable complex animations */
    @keyframes pulse-glow {
        0%, 100% { 
            box-shadow: 0 4px 14px rgba(140, 82, 255, 0.3);
        }
    }
    
    @keyframes float {
        0%, 100% { 
            transform: translate(0, 0);
        }
    }
    
    @keyframes pulse {
        0%, 100% { 
            transform: scale(1);
            opacity: 1;
        }
    }
    
    /* Disable scroll animations on mobile */
    .hero::before,
    .how-it-works-section::before,
    .how-it-works-section::after {
        animation: none;
    }
}
```

### 5.3 Optimize Font Loading
**Priority: MEDIUM** | **Effort: 15 minutes**

```html
<!-- Update font loading in all HTML files -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700;800&display=swap" rel="stylesheet">

<!-- Add font-display to CSS -->
<style>
@font-face {
    font-family: 'Poppins';
    font-display: swap; /* Prevents invisible text during load */
}
</style>
```

---

## Phase 6: Advanced Mobile Features

### 6.1 Add Mobile-Specific Utilities
**Priority: LOW** | **Effort: 15 minutes**

```css
/* ===== MOBILE UTILITY CLASSES ===== */

/* Visibility utilities */
.mobile-only {
    display: none;
}

.desktop-only {
    display: block;
}

@media (max-width: 768px) {
    .mobile-only {
        display: block;
    }
    
    .desktop-only {
        display: none !important;
    }
}

/* Text alignment utilities */
@media (max-width: 768px) {
    .mobile-text-center {
        text-align: center !important;
    }
    
    .mobile-text-left {
        text-align: left !important;
    }
    
    .mobile-full-width {
        width: 100% !important;
    }
}

/* Spacing utilities */
@media (max-width: 768px) {
    .mobile-mt-0 { margin-top: 0 !important; }
    .mobile-mb-0 { margin-bottom: 0 !important; }
    .mobile-p-0 { padding: 0 !important; }
}
```

### 6.2 Improve Scroll Behavior
**Priority: LOW** | **Effort: 20 minutes**

```css
/* ===== MOBILE SCROLL OPTIMIZATION ===== */

/* Smooth scrolling */
html {
    scroll-behavior: smooth;
}

@media (prefers-reduced-motion: reduce) {
    html {
        scroll-behavior: auto;
    }
}

/* Prevent overscroll bounce on iOS */
body {
    overscroll-behavior-y: contain;
}

/* Improve scrollbar on mobile */
@media (max-width: 768px) {
    ::-webkit-scrollbar {
        width: 4px;
    }
    
    ::-webkit-scrollbar-track {
        background: #f1f1f1;
    }
    
    ::-webkit-scrollbar-thumb {
        background: #8c52ff;
        border-radius: 2px;
    }
}
```

### 6.3 Add Safe Area Support for Notched Devices
**Priority: LOW** | **Effort: 15 minutes**

```css
/* ===== SAFE AREA SUPPORT ===== */

@media (max-width: 768px) {
    /* Header safe area */
    .header {
        padding-top: max(20px, env(safe-area-inset-top));
        padding-left: env(safe-area-inset-left);
        padding-right: env(safe-area-inset-right);
    }
    
    /* Footer safe area */
    .footer {
        padding-bottom: max(30px, env(safe-area-inset-bottom));
        padding-left: env(safe-area-inset-left);
        padding-right: env(safe-area-inset-right);
    }
    
    /* Fixed navigation safe area */
    .nav-links.active {
        padding-bottom: env(safe-area-inset-bottom);
    }
}
```

---

## Phase 7: Testing & Validation

### 7.1 Device Testing Checklist

**Test on these devices/viewports:**
- [ ] iPhone SE (375px width)
- [ ] iPhone 12/13/14 (390px width)
- [ ] iPhone 14 Pro Max (430px width)
- [ ] Samsung Galaxy S21 (360px width)
- [ ] iPad Mini (768px width)
- [ ] iPad Pro (1024px width)

**Test on these browsers:**
- [ ] Safari iOS (latest)
- [ ] Chrome Android (latest)
- [ ] Samsung Internet
- [ ] Firefox Mobile

### 7.2 Functionality Testing Checklist

**Navigation:**
- [ ] Hamburger menu opens/closes
- [ ] Dropdown menus work on mobile
- [ ] All links are tappable (44px minimum)
- [ ] Menu closes when clicking outside
- [ ] Menu scrolls if content is long

**Forms:**
- [ ] Newsletter signup works
- [ ] Input fields don't zoom on iOS
- [ ] Submit buttons are full-width
- [ ] Form validation displays properly

**Content:**
- [ ] All text is readable (not too small)
- [ ] Images load and scale properly
-