# Erlin AI Documentation Repository

## About this project
This is the official Mintlify documentation repository for **Erlin AI** - an AI-powered content generation and brand analytics SaaS platform.

**Key details:**
- Platform: Mintlify (mintlify.com)
- Theme: `palm` (full-width layout with sidebar support)
- Brand colors: Primary `#0d37fd`, Light `#3d5ffe`, Dark `#0827c4`
- Logo: Custom Erlin AI logo with sparkle icon (SVG format, dark/light modes)
- URL: https://erlin.ai
- App: https://app.erlin.ai/onboarding

## Quick reference

### Logo sizing solution
After testing multiple approaches, logo sizing is controlled via:
1. **custom.css** - Contains CSS rules targeting logo images. Adjust `max-height` value to control size:
   ```css
   .logo img, img[src*="/logo/"] {
     max-height: 80px !important; /* Increase/decrease this value */
   }
   ```
2. **SVG dimensions** - Both dark.svg and light.svg use `width="2500" height="960"` with `viewBox="0 0 600.12 230"`
3. **docs.json** - Logo object includes `height: 80, width: 208` properties (may be undocumented but kept for compatibility)

### Navigation structure
- 4 tabs: Introduction, Features, Platform, Changelog
- Each tab contains groups with pages
- Structure: `navigation.tabs[].groups[].pages[]`
- All pages are MDX files with required frontmatter (title, description)

### Key files
- **docs.json** - Central configuration (theme, navigation, colors, branding)
- **custom.css** - Custom styling (auto-detected by Mintlify)
- **logo/dark.svg** - Logo for dark mode (white text)
- **logo/light.svg** - Logo for light mode (black text, blue sparkle)
- **favicon.ico** - Browser favicon
- **index.mdx** - Homepage with feature cards
- **claude.md** - This file (documentation guidelines)

### Directory structure
```
docs/
├── introduction/          # Getting started, overview, quickstart, concepts
├── features/
│   ├── content-generation/  # Article types, workflow
│   └── analytics/           # Brand analytics
├── platform/
│   └── dashboard/           # Dashboard overview
├── changelog/             # Updates and releases
└── logo/                  # Brand assets
```

## Working relationship
- You can push back on ideas-this can lead to better documentation. Cite sources and explain your reasoning when you do so
- ALWAYS ask for clarification rather than making assumptions
- NEVER lie, guess, or make up information

## Project context
- Format: MDX files with YAML frontmatter
- Config: docs.json for navigation, theme, settings
- Components: Mintlify components

## Content strategy
- Document just enough for user success - not too much, not too little
- Prioritize accuracy and usability of information
- Make content evergreen when possible
- Search for existing information before adding new content. Avoid duplication unless it is done for a strategic reason
- Check existing patterns for consistency
- Start by making the smallest reasonable changes

## Frontmatter requirements for pages
- title: Clear, descriptive page title
- description: Concise summary for SEO/navigation

## Writing standards
- Second-person voice ("you")
- Prerequisites at start of procedural content
- Test all code examples before publishing
- Match style and formatting of existing pages
- Include both basic and advanced use cases
- Language tags on all code blocks
- Alt text on all images
- Relative paths for internal links

## Mintlify-specific technical details

### Validation and testing
- Test changes with `mint dev` locally before committing
- Watch for validation errors in docs.json (common issues below)
- Mintlify auto-detects CSS/JS files in repo root
- Changes deploy automatically when pushed to main branch

### Common docs.json validation errors
1. **Invalid navbar.primary.href** - Must be full URL, not relative path
2. **Missing theme property** - Required: `mint`, `maple`, `palm`, `willow`, `linden`, `almond`, `aspen`
3. **Wrong property names** - Use `navbar.links`, `navbar.primary`, `footer.socials` (not topbarLinks, topbarCtaButton, footerSocials)
4. **Invalid navigation structure** - Must be `navigation.tabs[].groups[].pages[]`

### Logo and branding quirks
- Mintlify's docs.json logo object officially supports: `dark`, `light`, `href` only
- `height` and `width` properties in logo object are undocumented but may work
- CSS has final say on logo size, not SVG dimensions
- Use custom.css to control logo sizing reliably
- SVG viewBox defines aspect ratio, width/height are rendering hints

### Mintlify components reference
- `<Card>`, `<CardGroup>` - Feature cards with icons
- `<Note>`, `<Warning>`, `<Tip>` - Callout boxes
- `<Accordion>`, `<AccordionGroup>` - Expandable sections
- `<Tabs>`, `<Tab>` - Tabbed content
- `<CodeGroup>` - Multi-language code examples
- All components documented at docs.mintlify.com

## Git workflow
- NEVER use --no-verify when committing
- Ask how to handle uncommitted changes before starting
- Create a new branch when no clear branch exists for changes
- Commit frequently throughout development
- NEVER skip or disable pre-commit hooks
- Branch naming: `claude/` prefix for Claude Code branches

## Do not
- Skip frontmatter on any MDX file
- Use absolute URLs for internal links
- Include untested code examples
- Make assumptions - always ask for clarification
- Add custom CSS without testing impact on Mintlify's built-in styles
- Remove the theme property from docs.json
- Use invalid property names in docs.json (validate against schema)
