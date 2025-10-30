# Mobile Navigation - Remaining Files to Update

## Overview
The mobile navigation system has been successfully implemented in the core files. The following support/*.html files still need the mobile navigation button and script added.

## Files Requiring Updates (11 files)

1. support/contact.html
2. support/code-of-conduct.html
3. support/data-security-policy.html
4. support/faq.html
5. support/governance.html
6. support/help-centre.html
7. support/member-feedback-complaints.html
8. support/policies.html
9. support/privacy-policy.html
10. support/refund-cancellation-policy.html
11. support/terms-of-service.html

## Required Changes for Each File

### Step 1: Add Mobile Menu Toggle Button
Find the navigation section (around line 436-440 for most files):
```html
<nav class="nav">
    <a href="../index.html" class="logo">
        <img src="../img/plp_logo.png" style="height: 50px; width: auto;"></img>
    </a>
    <div class="nav-center">
        <ul class="nav-links">
```

Add the mobile menu toggle button after the logo:
```html
<nav class="nav">
    <a href="../index.html" class="logo">
        <img src="../img/plp_logo.png" style="height: 50px; width: auto;"></img>
    </a>
    <button class="mobile-menu-toggle" aria-label="Toggle mobile menu" aria-expanded="false">☰</button>
    <div class="nav-center">
        <ul class="nav-links">
```

### Step 2: Add Mobile Navigation Script
Find the closing body tag at the end of each file:
```html
</body>
</html>
```

Add the script reference before the closing body tag:
```html
    <script src="../mobile-nav.js"></script>
</body>
</html>
```

## Automated Update Script (Optional)

If you prefer to update all files at once, you can use this pattern with search and replace:

### Search Pattern 1 (for nav button):
```
<nav class="nav">
                <a href="../index.html" class="logo">
                    <img src="../img/plp_logo.png" style="height: 50px; width: auto;"></img>
                </a>
                <div class="nav-center">
```

### Replace Pattern 1:
```
<nav class="nav">
                <a href="../index.html" class="logo">
                    <img src="../img/plp_logo.png" style="height: 50px; width: auto;"></img>
                </a>
                <button class="mobile-menu-toggle" aria-label="Toggle mobile menu" aria-expanded="false">☰</button>
                <div class="nav-center">
```

### Search Pattern 2 (for script):
```
</body>
</html>
```

### Replace Pattern 2:
```
    <script src="../mobile-nav.js"></script>
</body>
</html>
```

## Verification Checklist

After updating each file, verify:
- [ ] Mobile menu toggle button appears in the header
- [ ] Button has proper aria-label and aria-expanded attributes
- [ ] Script reference points to correct path (../mobile-nav.js)
- [ ] No syntax errors in HTML
- [ ] File saves successfully

## Testing

Once all files are updated, test on mobile devices or browser dev tools:
1. Open each page on mobile viewport (< 768px width)
2. Click hamburger menu (☰) - should open full-screen menu
3. Click menu items - should navigate correctly
4. Click outside menu - should close menu
5. Verify dropdown menus work on mobile
6. Test on actual mobile devices (iOS Safari, Chrome Mobile)

## Files Already Updated ✅

- index.html
- support.html
- joinplp.html
- about/our-story.html
- about/meet-the-founders.html
- about/fuel-our-mission.html
- about/plp-impact-network.html

## Mobile Navigation Features

The mobile navigation system includes:
- Hamburger menu toggle (☰/✕)
- Full-screen overlay menu
- Touch-friendly dropdown menus
- Click-outside-to-close functionality
- Automatic close on link click
- Window resize handling
- Accessibility support (ARIA attributes)
- Smooth animations

## Technical Details

### CSS Classes Used:
- `.mobile-menu-toggle` - Hamburger button
- `.nav-links.active` - Open menu state
- `.dropdown.active` - Open dropdown state

### JavaScript File:
- `mobile-nav.js` - Handles all mobile menu interactions

### Breakpoints:
- Mobile menu activates at: max-width: 768px
- Extra small adjustments at: max-width: 480px

## Support

If you encounter any issues:
1. Check browser console for JavaScript errors
2. Verify mobile-nav.js file exists in root directory
3. Ensure styles.css includes mobile navigation CSS
4. Test in different browsers and devices
5. Check that viewport meta tag is present in HTML head

## Next Steps

After completing these updates:
1. Add lazy loading to images (loading="lazy" attribute)
2. Optimize font loading (font-display: swap)
3. Conduct comprehensive mobile testing
4. Measure performance metrics
5. Gather user feedback on mobile experience