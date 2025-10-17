
# Project Launchpad - Landing Page Architecture Analysis & Recommendations

## Executive Summary

This document provides a comprehensive analysis of the Project Launchpad landing page development, comparing the architectural requirements with existing implementations and providing actionable recommendations.

---

## 1. Current State Analysis

### 1.1 Existing Assets Review

**Current [`index.html`](index.html:1)**
- ✅ Strong hero section with clear value proposition
- ✅ Effective stats bar showing ROI metrics
- ✅ Six outcome pillars well-implemented
- ✅ Membership comparison (Launchpad Lite vs Lift-Off)
- ✅ Typeform integration for signups
- ✅ Purple/coral gradient branding established
- ⚠️ Missing: Full navigation structure
- ⚠️ Missing: About, Support, Insights sections
- ⚠️ Missing: Footer with comprehensive links

**Reference Design [`join-plp- (1).html`](../../../Users/jaryd/Downloads/join-plp- (1).html:1)**
- ✅ Excellent animation system (fade-in, slide-up, scale-up)
- ✅ Professional navigation with dropdowns
- ✅ Video hero section with play button
- ✅ Auto-scrolling partner logos
- ✅ Multiple feature presentation styles
- ✅ Testimonials section
- ✅ Newsletter signup
- ✅ Comprehensive footer structure
- ⚠️ Content is generic "changemaker" focused (needs PLP-specific content)

**Architecture Document [`project-launchpad-architecture.md`](../../../Users/jaryd/Downloads/project-launchpad-architecture.md:1)**
- Comprehensive 1,103-line specification
- Detailed page hierarchy and navigation structure
- Complete design system specifications
- Technical requirements and SEO guidelines
- Content strategy and tone guidelines

---

## 2. Gap Analysis

### 2.1 Critical Missing Components

#### Navigation & Structure
- **Primary Navigation**: Need full nav with HOME, JOIN PLP, INSIGHTS, ABOUT ▼, SUPPORT ▼
- **Dropdown Menus**: About and Support sections need dropdown navigation
- **Login Button**: Portal access button needed
- **Mobile Menu**: Hamburger menu for responsive design

#### Page Structure
- **Homepage**: Mostly complete, needs navigation integration
- **Join PLP Page** ([`joinplp.html`](joinplp.html:1)): Currently empty, needs full implementation
- **About Section**: [`about.html`](about.html:1) is placeholder only
  - Our Story/Mission/Vision
  - Meet the Team
  - Impact Network
  - Fuel Our Mission
- **Support Section**: Not yet created
  - Contact Us
  - FAQs
  - Help Center
- **Governance Section**: Not yet created
- **Insights/Blog**: Not yet created

#### Design Elements
- **Animations**: Current site lacks scroll animations from reference design
- **Video Placeholders**: No video integration yet
- **Partner Logos**: Auto-scrolling section not implemented
- **Testimonials**: Not present on current homepage
- **Newsletter Signup**: Missing from current implementation

---

## 3. Recommended Site Architecture

### 3.1 File Structure

```
project-launchpad/
├── index.html                    # Homepage (build from scratch)
├── joinplp.html                  # Join PLP page (leave untouched)
├── about.html                    # About overview (rebuild)
├── insights.html                 # Blog listing (new)
├── about/
│   ├── story.html               # Our Story/Mission/Vision
│   ├── team.html                # Meet the Team
│   ├── network.html             # Impact Network
│   └── support-us.html          # Fuel Our Mission
├── support/
│   ├── index.html               # Support Hub
│   ├── contact.html             # Contact Us
│   ├── faqs.html                # FAQs
│   └── help.html                # Help Center
├── governance/
│   ├── index.html               # Governance Overview
│   ├── policies.html            # Policies
│   ├── terms.html               # Terms & Conditions
│   └── land-acknowledgement.html
├── assets/
│   ├── css/
│   │   ├── main.css             # Core styles
│   │   ├── components.css       # Reusable components
│   │   └── animations.css       # Animation library
│   ├── js/
│   │   ├── main.js              # Core functionality
│   │   ├── navigation.js        # Nav & mobile menu
│   │   └── animations.js        # Scroll animations
│   └── images/
│       ├── logo/
│       ├── team/
│       └── partners/
└── components/
    ├── header.html              # Reusable header
    └── footer.html              # Reusable footer
```

### 3.2 Priority Implementation Phases

#### Phase 1: Foundation (Priority: HIGH)
1. **Navigation System**
   - Implement full navigation bar with dropdowns
   - Add mobile hamburger menu
   - Create sticky header behavior
   - Add login button

2. **Component Library**
   - Extract reusable header component
   - Extract reusable footer component
   - Create CSS component library
   - Implement animation system

3. **Homepage Enhancements**
   - Add scroll animations
   - Integrate video placeholders
   - Add partner logo section
   - Add testimonials section
   - Add newsletter signup

#### Phase 2: Core Pages (Priority: HIGH)
4. **Join PLP Page** ([`joinplp.html`](joinplp.html:1))
   - Hero section with tier comparison
   - Detailed feature comparison table
   - FAQ accordion
   - Testimonials/social proof
   - Final CTA section

5. **About Section**
   - About overview page
   - Our Story page with timeline
   - Team page with member cards
   - Impact Network page

6. **Support Section**
   - Support hub landing
   - Contact form (Typeform integration)
   - FAQ page with accordion
   - Help center structure

#### Phase 3: Content & Polish (Priority: MEDIUM)
7. **Insights/Blog**
   - Blog listing page
   - Post template
   - Category filtering

8. **Governance**
   - Policies page
   - Terms & Conditions
   - Land Acknowledgement

9. **SEO & Performance**
   - Meta tags optimization
   - Image optimization
   - Performance testing
   - Accessibility audit

---

## 4. Design System Specifications

### 4.1 Color Palette

```css
/* Primary Colors */
:root {
    --purple-primary: #8B5CF6;
    --coral-primary: #FF6B9D;
    
    /* Gradient */
    --gradient-primary: linear-gradient(135deg, #FF6B9D 0%, #8B5CF6 100%);
    
    /* Neutral Colors */
    --dark-gray: #1F2937;
    --medium-gray: #6B7280;
    --light-gray: #F3F4F6;
    --white: #FFFFFF;
    
    /* Semantic Colors */
    --success: #10B981;
    --warning: #F59E0B;
    --error: #EF4444;
    --info: #3B82F6;
}
```

### 4.2 Typography System

```css
/* Font Family */
body {
    font-family: 'Poppins', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
}

/* Type Scale */
h1 { font-size: 3rem; line-height: 1.2; font-weight: 800; }      /* 48px - Hero headlines */
h2 { font-size: 2.25rem; line-height: 1.2; font-weight: 700; }   /* 36px - Section titles */
h3 { font-size: 1.75rem; line-height: 1.2; font-weight: 600; }   /* 28px - Subsection titles */
h4 { font-size: 1.5rem; line-height: 1.2; font-weight: 600; }    /* 24px - Card titles */
.body-large { font-size: 1.125rem; line-height: 1.6; }           /* 18px - Intro paragraphs */
body { font-size: 1rem; line-height: 1.6; }                      /* 16px - Standard text */
.body-small { font-size: 0.875rem; line-height: 1.4; }           /* 14px - Captions, labels */
```

### 4.3 Spacing System

```css
:root {
    /* Base Unit: 4px */
    --space-xs: 4px;
    --space-sm: 8px;
    --space-md: 16px;
    --space-lg: 24px;
    --space-xl: 32px;
    --space-2xl: 48px;
    --space-3xl: 64px;
    --space-4xl: 96px;
    
    /* Container Widths */
    --container-max: 1280px;
    --container-content: 1024px;
    --container-narrow: 768px;
}
```

### 4.4 Component Library

#### Buttons

```css
/* Primary Button */
.btn-primary {
    background: linear-gradient(135deg, #FF6B9D 0%, #8B5CF6 100%);
    color: white;
    padding: 12px 24px;
    border: none;
    border-radius: 8px;
    font-weight: 600;
    font-size: 1rem;
    cursor: pointer;
    transition: all 0.3s ease;
    text-decoration: none;
    display: inline-block;
}

.btn-primary:hover {
    transform: translateY(-2px);
    box-shadow: 0 10px 25px rgba(139, 92, 246, 0.3);
}

/* Secondary Button */
.btn-secondary {
    background: transparent;
    border: 2px solid #8B5CF6;
    color: #8B5CF6;
    padding: 12px 24px;
    border-radius: 8px;
    font-weight: 600;
    transition: all 0.3s ease;
}

.btn-secondary:hover {
    background: #8B5CF6;
    color: white;
}

/* Login Button */
.btn-login {
    background: transparent;
    color: #6B7280;
    padding: 12px 20px;
    border: 2px solid #E5E7EB;
    border-radius: 8px;
    font-weight: 600;
    transition: all 0.2s;
}

.btn-login:hover {
    border-color: #8B5CF6;
    color: #8B5CF6;
}
```

#### Cards

```css
/* Standard Card */
.card {
    background: white;
    border: 1px solid #F3F4F6;
    border-radius: 12px;
    padding: 24px;
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    transition: all 0.3s ease;
}

.card:hover {
    transform: translateY(-4px);
    box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.15);
}

/* Gradient Border Card (for outcome pillars) */
.card-gradient {
    background: white;
    border-radius: 12px;
    padding: 24px;
    position: relative;
    overflow: hidden;
}

.card-gradient::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 5px;
    background: linear-gradient(90deg, #FF6B9D, #8B5CF6);
}

/* Pricing Card */
.pricing-card {
    background: white;
    border: 2px solid #F3F4F6;
    border-radius: 16px;
    padding: 32px;
    text-align: center;
    transition: all 0.3s;
}

.pricing-card.featured {
    border-color: #8B5CF6;
    transform: scale(1.05);
}

.pricing-card.featured::before {
    content: 'Best Value for Charities';
    position: absolute;
    top: -15px;
    left: 50%;
    transform: translateX(-50%);
    background: linear-gradient(90deg, #FF6B9D, #8B5CF6);
    color: white;
    padding: 5px 20px;
    border-radius: 20px;
    font-size: 0.8em;
    font-weight: bold;
}
```

### 4.5 Animation System

```css
/* Fade In Animation */
.fade-in {
    opacity: 0;
    transform: translateY(30px);
    transition: all 0.8s ease-out;
}

.fade-in.animate {
    opacity: 1;
    transform: translateY(0);
}

/* Slide Up Animation */
.slide-up {
    opacity: 0;
    transform: translateY(50px);
    transition: all 0.6s ease-out;
}

.slide-up.animate {
    opacity: 1;
    transform: translateY(0);
}

/* Slide Left Animation */
.slide-left {
    opacity: 0;
    transform: translateX(-50px);
    transition: all 0.8s ease-out;
}

.slide-left.animate {
    opacity: 1;
    transform: translateX(0);
}

/* Slide Right Animation */
.slide-right {
    opacity: 0;
    transform: translateX(50px);
    transition: all 0.8s ease-out;
}

.slide-right.animate {
    opacity: 1;
    transform: translateX(0);
}

/* Scale Up Animation */
.scale-up {
    opacity: 0;
    transform: scale(0.9);
    transition: all 0.6s ease-out;
}

.scale-up.animate {
    opacity: 1;
    transform: scale(1);
}

/* Stagger Animation Delays */
.stagger-1 { transition-delay: 0.1s; }
.stagger-2 { transition-delay: 0.2s; }
.stagger-3 { transition-delay: 0.3s; }
.stagger-4 { transition-delay: 0.4s; }
```

---

## 5. Navigation Architecture

### 5.1 Primary Navigation Structure

```html
<header class="header">
    <div class="container">
        <nav class="nav">
            <!-- Logo -->
            <a href="index.html" class="logo">
                <div class="logo-icon">PL</div>
                <span>Project Launchpad</span>
            </a>
            
            <!-- Center Navigation -->
            <ul class="nav-links">
                <li><a href="index.html">HOME</a></li>
                <li><a href="joinplp.html">JOIN PLP</a></li>
                <li><a href="insights.html">INSIGHTS</a></li>
                
                <!-- About Dropdown -->
                <li class="dropdown">
                    <a href="about.html">ABOUT</a>
                    <div class="dropdown-content">
                        <a href="about/story.html">Our Story/Mission/Vision</a>
                        <a href="about/team.html">Meet PLP Team</a>
                        <a href="about/network.html">PLP Impact Network</a>
                        <a href="about/support-us.html">Fuel Our Mission</a>
                    </div>
                </li>
                
                <!-- Support Dropdown -->
                <li class="dropdown">
                    <a href="support/index.html">SUPPORT</a>
                    <div class="dropdown-content">
                        <a href="support/contact.html">Contact Us</a>
                        <a href="support/faqs.html">FAQs</a>
                        <a href="support/help.html">Help Center</a>
                        <a href="governance/index.html">Governance</a>
                    </div>
                </li>
            </ul>
            
            <!-- Right Buttons -->
            <div class="header-buttons">
                <a href="#login" class="btn-login">Login</a>
                <a href="joinplp.html" class="btn-primary">Join PLP</a>
            </div>
            
            <!-- Mobile Menu Toggle -->
            <button class="mobile-menu-toggle" aria-label="Toggle menu">
                <span></span>
                <span></span>
                <span></span>
            </button>
        </nav>
    </div>
</header>
```

### 5.2 Footer Structure

```html
<footer class="footer">
    <div class="container">
        <div class="footer-content">
            <!-- Brand Section -->
            <div class="footer-brand">
                <a href="index.html" class="footer-logo">
                    <div class="logo-icon">PL</div>
                    <span>PROJECT LAUNCHPAD</span>
                </a>
                <p class="footer-description">
                    Built for impact, not profit.<br>
                    Designed exclusively for Canada's smaller charities.
                </p>
            </div>
            
            <!-- Links Grid -->
            <div class="footer-links">
                <div class="footer-column">
                    <h4>About</h4>
                    <ul>
                        <li><a href="about/story.html">Our Story</a></li>
                        <li><a href="about/team.html">Meet the Team</a></li>
                        <li><a href="about/network.html">Impact Network</a></li>
                        <li><a href="about/support-us.html">Support Us</a></li>
                    </ul>
                </div>
                
                <div class="footer-column">
                    <h4>Support</h4>
                    <ul>
                        <li><a href="support/contact.html">Contact Us</a></li>
                        <li><a href="support/faqs.html">FAQs</a></li>
                        <li><a href="support/help.html">Help Center</a></li>
                    </ul>
                </div>
                
                <div class="footer-column">
                    <h4>Legal</h4>
                    <ul>
                        <li><a href="governance/policies.html">Privacy Policy</a></li>
                        <li><a href="governance/terms.html">Terms & Conditions</a></li>
                        <li><a href="governance/land-acknowledgement.html">Land Acknowledgement</a></li>
                    </ul>
                </div>
                
                <div class="footer-column">
                    <h4>Connect</h4>
                    <ul>
                        <li><a href="mailto:hello@projectlaunchpad.ca">📧 hello@projectlaunchpad.ca</a></li>
                        <li><a href="https://www.linkedin.com/company/projectlaunchpad/">🔗 LinkedIn</a></li>
                    </ul>
                </div>
            </div>
        </div>
        
        <!-- Bottom Bar -->
        <div class="footer-bottom">
            <p>© 2025 Project Launchpad. All rights reserved.</p>
            <p>A collaboration between <a href="https://harmoniaphilanthropy.ca/">Harmonia Philanthropy</a> and <a href="https://telos.one/">Telos One</a></p>
        </div>
    </div>
</footer>
```

---

## 6. Page-Specific Architecture

### 6.1 Homepage ([`index.html`](index.html:1)) - Enhancement Plan

**Current Sections (Keep & Enhance):**
1. ✅ Hero Section - Add animations
2. ✅ Stats Bar - Add rolling counter animations
3. ✅ Membership Comparison - Add scroll animations
4. ✅ Six Outcome Pillars - Add hover effects and animations
5. ✅ Footer CTA - Keep existing

**New Sections to Add:**

**A. Partner Logos Section** (Insert after Hero)
```html
<section class="partners-section">
    <div class="partners-scroll">
        <div class="partner-logo">Harmonia Philanthropy</div>
        <div class="partner-logo">Telos One</div>
        <div class="partner-logo">Imagine Canada</div>
        <div class="partner-logo">Partner 4</div>
        <div class="partner-logo">Partner 5</div>
        <!-- Duplicate for seamless scroll -->
    </div>
</section>
```

**B. Video/Demo Section** (Insert before Membership)
```html
<section class="video-section">
    <div class="container">
        <h2 class="section-title">See Project Launchpad in Action</h2>
        <p class="section-subtitle">Discover how our platform transforms charity operations</p>
        <div class="video-container">
            <div class="video-placeholder">
                <div class="play-button">▶</div>
            </div>
        </div>
    </div>
</section>
```

**C. Testimonials Section** (Insert after Outcomes)
```html
<section class="testimonials-section">
    <div class="container">
        <h2 class="section-title">What Charities Are Saying</h2>
        <div class="testimonials-grid">
            <div class="testimonial-card">
                <div class="stars">★★★★★</div>
                <p class="testimonial-text">"Quote from charity leader..."</p>
                <div class="testimonial-author">
                    <div class="author-avatar"></div>
                    <div class="author-info">
                        <h4>Name</h4>
                        <p>Title, Organization</p>
                    </div>
                </div>
            </div>
            <!-- More testimonials -->
        </div>
    </div>
</section>
```

**D. Newsletter Section** (Insert before Footer)
```html
<section class="newsletter-section">
    <div class="container">
        <div class="newsletter-content">
            <div class="newsletter-text">
                <h2>Stay Updated on PLP Launch</h2>
                <p>Get exclusive updates, resources, and early access opportunities</p>
            </div>
            <div class="newsletter-form">
                <input type="email" placeholder="Your email address" class="email-input">
                <button type="submit" class="btn-subscribe">Subscribe</button>
            </div>
        </div>
    </div>
</section>
```

### 6.2 Join PLP Page ([`joinplp.html`](joinplp.html:1)) - Complete Structure

**Section 1: Hero**
```html
<section class="join-hero">
    <div class="container">
        <h1>Choose Your Launchpad</h1>
        <p>Start free or unlock full potential—both designed exclusively for smaller Canadian charities</p>
    </div>
</section>
```

**Section 2: Detailed Tier Comparison**
```html
<section class="tier-comparison">
    <div class="container">
        <div class="comparison-table">
            <!-- Detailed feature-by-feature comparison -->
            <!-- Sticky CTAs -->
        </div>
    </div>
</section>
```

**Section 3: Social Proof**
```html
<section class="social-proof">
    <div class="container">
        <h2>Trusted by Canadian Charities</h2>
        <!-- Partner logos -->
        <!-- Impact statistics -->
        <!-- Testimonials -->
    </div>
</section>
```

**Section 4: FAQ Accordion**
```html
<section class="faq-section">
    <div class="container">
        <h2>Frequently Asked Questions</h2>
        <div class="faq-accordion">
            <!-- Expandable Q&A items -->
        </div>
    </div>
</section>
```

**Section 5: Final CTA**
```html
<section class="final-cta">
    <div class="container">
        <h2>Ready to Transform Your Charity?</h2>
        <p>Join the waitlist for Fall 2025 launch</p>
        <div class="cta-buttons">
            <a href="#" class="btn-primary">Join Waitlist - Free Tier</a>
            <a href="#" class="btn-primary">Join Waitlist - Lift-Off Tier</a>
        </div>
        <div class="trust-badges">
            <!-- Security, Privacy, Canadian badges -->
        </div>
    </div>
</section>
```

### 6.3 About Section Pages

#### [`about/story.html`](about/story.html)
**Required Sections:**
- Hero with mission statement
- Origin story narrative
- Vision for impact
- Core values grid
- Visual timeline of milestones
- Founder photos/videos
- CTA to join or support

#### [`about/team.html`](about/team.html)
**Required Sections:**
- Hero introducing the team
- Leadership team cards
- Advisory board cards
- Core team cards
- Partner organizations
- Join the team CTA

#### [`about/network.html`](about/network.html)
**Required Sections:**
- Hero explaining the network
- Sector Allies section with logo grid
- Founding Members section with success stories
- Interactive filters (sector, region)
- Case study spotlights
- Become a partner CTA

#### [`about/support-us.html`](about/support-us.html)
**Required Sections:**
- Hero explaining ways to support
- Donate section with form/link
- Partner inquiry section
- Volunteer application section
- Spread the word section with social sharing
- Feedback form section

### 6.4 Support Section Pages

#### [`support/index.html`](support/index.html)
**Required Sections:**
- Hero with search bar
- Card-based navigation (Contact, FAQs, Help, Community)
- Quick links section
- Popular articles
- Contact information

#### [`support/contact.html`](support/contact.html)
**Required Sections:**
- Hero with contact information
- Typeform embedded contact form
- Alternative contact methods
- Response time expectations
- Office hours (if applicable)

#### [`support/faqs.html`](support/faqs.html)
**Required Sections:**
- Hero with search functionality
- Category tabs/filters
- Accordion-style Q&A items
- "Still have questions?" CTA
- Related articles links

#### [`support/help.html`](support/help.html)
**Required Sections:**
- Hero with search
- Getting started guide
- Video tutorials section
- Feature documentation
- Best practices articles
- Troubleshooting guides
- Categorized navigation

---

## 7. Technical Implementation

### 7.1 JavaScript Requirements

```javascript
// animations.js - Intersection Observer for scroll animations
const observerOptions = {
    threshold: 0.1,
    rootMargin: '0px 0px -50px 0px'
};

const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
        if (entry.isIntersecting) {
            entry.target.classList.add('animate');
        }
    });
}, observerOptions);

// Observe all animated elements
document.addEventListener('DOMContentLoaded', () => {
    const animatedElements = document.querySelectorAll(
        '.fade-in, .slide-up, .slide-left, .slide-right, .scale-up'
    );
    animatedElements.forEach(el => observer.observe(el));
});

// navigation.js - Mobile menu toggle
function toggleMobileMenu() {
    const navLinks = document.querySelector('.nav-links');
    const menuToggle = document.querySelector('.mobile-menu-toggle');
    navLinks.classList.toggle('active');
    menuToggle.classList.toggle('active');
}

// Sticky header
window.addEventListener('scroll', () => {
    const header = document.querySelector('.header');
    if (window.scrollY > 100) {
        header.classList.add('sticky');
    } else {
        header.classList.remove('sticky');
    }
});

// Smooth scroll for anchor links
document.querySelectorAll('a[href^="#"]').forEach(anchor => {
    anchor.addEventListener('click', function (e) {
        e.preventDefault();
        const target = document.querySelector(this.getAttribute('href'));
        if (target) {
            target.scrollIntoView({ behavior: 'smooth', block: 'start' });
        }
    });
});

// FAQ accordion
document.querySelectorAll('.faq-item').forEach(item => {
    const question = item.querySelector('.faq-question');
    question.addEventListener('click', () => {
        item.classList.toggle('active');
    });
});
```

### 7.2 Responsive Design Breakpoints

```css
/* Mobile First Approach */

/* Mobile: 0-639px (default styles) */
body {
    font-size: 16px;
}

.container {
    padding: 0 20px;
}

/* Tablet: 640px-1023px */
@media (min-width: 640px) {
    .outcomes-grid {
        grid-template-columns: repeat(2, 1fr);
    }
    
    .membership-grid {
        grid-template-columns: repeat(2, 1fr);
    }
}

/* Desktop: 1024px+ */
@media (min-width: 1024px) {
    .nav-links {
        display: flex;
    }
    
    .mobile-menu-toggle {
        display: none;
    }
    
    .outcomes-grid {
        grid-template-columns: repeat(3, 1fr);
    }
    
    .two-column {
        grid-template-columns: 1fr 1fr;
    }
}

/* Large Desktop: 1280px+ */
@media (min-width: 1280px) {
    .container {
        max-width: 1280px;
    }
}
```

### 7.3 SEO Template

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    
    <!-- Primary Meta Tags -->
    <title>Page Title - Project Launchpad</title>
    <meta name="title" content="Page Title - Project Launchpad">
    <meta name="description" content="Page description (150-160 characters)">
    
    <!-- Open Graph / Facebook -->
    <meta property="og:type" content="website">
    <meta property="og:url" content="https://projectlaunchpad.ca/page">
    <meta property="og:title" content="Page Title - Project Launchpad">
    <meta property="og:description" content="Page description">
    <meta property="og:image" content="https://projectlaunchpad.ca/og-image.jpg">
    
    <!-- Twitter -->
    <meta property="twitter:card" content="summary_large_image">
    <meta property="twitter:url" content="https://projectlaunchpad.ca/page">
    <meta property="twitter:title" content="Page Title - Project Launchpad">
    <meta property="twitter:description" content="Page description">
    <meta property="twitter:image" content="https://projectlaunchpad.ca/twitter-image.jpg">
    
    <!-- Canonical URL -->
    <link rel="canonical" href="https://projectlaunchpad.ca/page">
    
    <!-- Favicon -->
    <link rel="icon" type="image/png" href="/favicon.png">
    
    <!-- Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic