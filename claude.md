# Erlin AI Documentation Repository

## About this project
This is the official Mintlify documentation repository for **Erlin AI** - an AI-powered content generation and brand analytics SaaS platform.

**Product overview:**
Erlin AI is a SaaS platform that combines AI-powered content generation with brand analytics. The platform supports 7 article types (product reviews, comparisons, how-to guides, blog posts, press releases, guest posts, how-to product guides) and provides real-time brand monitoring and analytics through an interactive dashboard.

**Technical stack:**
- Platform: Mintlify (modern documentation framework)
- Format: MDX (Markdown + JSX components)
- Theme: `palm` (provides full-width layout with sidebar navigation)
- Deployment: Auto-deploys from main branch when pushed
- Local development: `mint dev` command for live preview

**Brand identity:**
- Primary color: `#0d37fd` (Erlin blue)
- Secondary colors: Light `#3d5ffe`, Dark `#0827c4`
- Logo: Custom SVG with "ERLIN AI" text and sparkle icon
- Dark mode: White text with blue sparkle
- Light mode: Black text (#231f20) with blue sparkle
- Logo aspect ratio: 2.6:1 (viewBox: 600.12 x 230)

**URLs:**
- Marketing site: https://erlin.ai
- Application: https://app.erlin.ai/onboarding
- Documentation: (Mintlify deployment URL)

## Quick reference

### Logo sizing solution (CRITICAL)
Logo sizing was a complex issue that required multiple iterations to solve. The final working solution uses three components:

1. **custom.css** (PRIMARY CONTROL) - Mintlify auto-detects this file in repo root. This CSS rule has final control over logo size:
   - Target selectors: `.logo img` and `img[src*="/logo/"]`
   - Current value: `max-height: 50px !important;`
   - Adjust this single value to change logo size (increase for bigger, decrease for smaller)
   - The `!important` flag ensures it overrides Mintlify's default theme CSS

2. **SVG dimensions** (SUPPORTING) - Both dark.svg and light.svg include extreme dimensions:
   - Attributes: `width="2500" height="960"`
   - ViewBox: `viewBox="0 0 600.12 230"` (defines coordinate system and aspect ratio)
   - These large dimensions help push against CSS max-width constraints

3. **docs.json logo object** (EXPERIMENTAL) - Includes undocumented properties:
   - Properties: `"height": 80, "width": 208`
   - These are NOT officially documented in Mintlify schema
   - May or may not have effect, but kept for compatibility

**What didn't work:**
- ViewBox-only approach (removing width/height) made logo SMALLER
- Multiple SVG dimension increases without CSS had no effect
- docs.json properties alone don't control sizing

**Bottom line:** Modify `custom.css` max-height value to adjust logo size. This is the reliable control mechanism.

### Navigation structure
The documentation uses a 4-tab layout with hierarchical organization:

**Tab 1: Introduction**
- Group: Getting Started
  - index.mdx (homepage - not in navigation but referenced)
  - introduction/overview.mdx
  - introduction/quickstart.mdx
- Group: Core Concepts
  - introduction/how-it-works.mdx
  - introduction/key-features.mdx

**Tab 2: Features**
- Group: Content Generation
  - features/content-generation/overview.mdx
  - features/content-generation/article-types.mdx
  - features/content-generation/workflow.mdx
- Group: Brand Analytics
  - features/analytics/overview.mdx

**Tab 3: Platform**
- Group: Dashboard
  - platform/dashboard/overview.mdx

**Tab 4: Changelog**
- Group: Updates
  - changelog/index.mdx

**Key patterns:**
- Structure in docs.json: `navigation.tabs[].groups[].pages[]`
- Page paths are relative to repo root, without .mdx extension
- Homepage (index.mdx) is referenced in "Getting Started" group
- All MDX files MUST have frontmatter with `title` and `description`
- Paths in docs.json must match actual file locations exactly

### Key files and their purposes

**Configuration files:**
- **docs.json** - Central Mintlify configuration controlling theme, colors, navigation, navbar, footer
- **custom.css** - Custom CSS for logo sizing and other style overrides (auto-detected by Mintlify)
- **claude.md** - This file (project context and documentation guidelines for AI agents)

**Brand assets:**
- **logo/dark.svg** - Logo for dark mode (white #fff text, blue #0d37fd sparkle, extreme 2500x960 dimensions)
- **logo/light.svg** - Logo for light mode (black #231f20 text, blue #0d37fd sparkle, extreme 2500x960 dimensions)
- **favicon.ico** - Browser favicon (4286 bytes, ICO format)
- **favicon.svg** - SVG version of favicon (kept for reference)

**Documentation content:**
- **index.mdx** - Homepage with CardGroup showcasing 4 main features, uses Note component
- **introduction/** - Getting started content, overview, quickstart, core concepts
- **features/** - Product features documentation (content generation, analytics)
- **platform/** - Platform guides (dashboard documentation)
- **changelog/** - Release notes and updates

**Reference materials:**
- **references/** - Contains reference screenshots (e.g., Thena AI sidebar layout example)
- **README.md** - Repository readme
- **LICENSE** - License file

### Directory structure
```
/home/user/docs/
├── docs.json                           # Mintlify configuration
├── custom.css                          # Logo sizing CSS
├── claude.md                           # AI agent project context
├── index.mdx                           # Homepage
├── favicon.ico                         # Favicon
├── favicon.svg                         # SVG favicon
├── README.md                           # Repo readme
├── LICENSE                             # License
├── logo/
│   ├── dark.svg                        # Dark mode logo
│   └── light.svg                       # Light mode logo
├── references/
│   └── Screenshot 2025-11-17...png     # Reference images
├── introduction/
│   ├── overview.mdx
│   ├── quickstart.mdx
│   ├── how-it-works.mdx
│   └── key-features.mdx
├── features/
│   ├── content-generation/
│   │   ├── overview.mdx                # Uses Steps component
│   │   ├── article-types.mdx
│   │   └── workflow.mdx
│   └── analytics/
│       └── overview.mdx
├── platform/
│   └── dashboard/
│       └── overview.mdx
└── changelog/
    └── index.mdx
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

### How Mintlify works
- **Framework**: React-based documentation platform optimized for modern docs
- **Build process**: Mintlify compiles MDX → React components → static site
- **Live preview**: `mint dev` runs local dev server with hot reload
- **Auto-detection**: CSS/JS files in repo root are automatically included
- **Deployment**: Pushes to main branch trigger automatic rebuild and deploy
- **Validation**: docs.json schema validation happens at build time
- **Theme system**: Pre-built themes (mint, palm, maple, etc.) control layout and styling

### Palm theme specifics
- **Layout**: Full-width content area with collapsible sidebar navigation
- **Purpose**: Designed for documentation with extensive navigation needs
- **Sidebar**: Automatically generated from navigation.tabs structure
- **Width**: Wider content area compared to other themes like "mint"
- **Navigation**: Tabs appear in top navbar, clicking tab shows groups in sidebar
- **Current theme**: `"theme": "palm"` in docs.json

### Common docs.json validation errors (CRITICAL)
These errors will prevent Mintlify from building:

1. **Invalid navbar.primary.href** - Error: "#.navbar.primary.href: Must be a valid url"
   - Fix: Use full URL (https://...) not relative path (/path)
   - Example: `"href": "https://app.erlin.ai/onboarding"` ✓ not `"href": "/quickstart"` ✗

2. **Missing theme property** - Error: "#.theme: Invalid discriminator value..."
   - Fix: Must include one of: `mint`, `maple`, `palm`, `willow`, `linden`, `almond`, `aspen`
   - Example: `"theme": "palm"` ✓

3. **Wrong property names** - Error: "Property X is not allowed"
   - OLD (wrong): `topbarLinks`, `topbarCtaButton`, `footerSocials`
   - NEW (correct): `navbar.links`, `navbar.primary`, `footer.socials`
   - These property names changed in recent Mintlify versions

4. **Invalid navigation structure** - Tabs must be inside navigation object
   - Wrong: `"tabs": [...]` at root level ✗
   - Correct: `"navigation": { "tabs": [...] }` ✓
   - Structure: tabs contain groups, groups contain pages

5. **Page path mismatches** - Pages in docs.json must match actual file paths
   - Paths are relative to repo root
   - Omit .mdx extension
   - Example: `"introduction/overview"` for file at `/introduction/overview.mdx`

### Logo and branding implementation details
**docs.json logo object:**
- Officially documented properties: `dark`, `light`, `href` (optional)
- Undocumented properties: `height`, `width` (we include them but effect uncertain)
- Path format: Paths are relative to repo root with leading slash
- Example: `"dark": "/logo/dark.svg"` refers to `/logo/dark.svg` file

**SVG structure:**
- viewBox defines coordinate system and aspect ratio (don't modify)
- width/height attributes are rendering size hints (we use extreme values: 2500x960)
- CSS has final control over rendered size (this is why custom.css is needed)
- SVG optimization: Don't optimize/minify - keep readable for potential edits

**CSS precedence:**
- Mintlify theme CSS applies default logo sizing
- custom.css with `!important` overrides theme defaults
- Browser DevTools can inspect actual rendered size
- Test in both light and dark modes

### Mintlify components used in this project
**Current usage:**
- `<Card>` + `<CardGroup>` - Used extensively in index.mdx and feature pages for showcasing features
- `<Note>` - Used in index.mdx for callout to quickstart guide
- `<Steps>` + `<Step>` - Used in features/content-generation/overview.mdx for process flow
- Icons - Font Awesome icons via `icon` prop (e.g., `icon="rocket"`, `icon="sparkles"`)

**Available but not yet used:**
- `<Warning>` - Important warnings and cautions
- `<Tip>` - Helpful tips and best practices
- `<Accordion>` + `<AccordionGroup>` - Collapsible FAQ sections
- `<Tabs>` + `<Tab>` - Tabbed content within pages
- `<CodeGroup>` - Multi-language code examples with tabs
- `<Frame>` - Image/video containers with captions
- `<ParamField>` - API parameter documentation

**Component documentation:** https://docs.mintlify.com (use WebFetch to access when needed)

### Validation and testing workflow
1. Make changes to MDX files or docs.json
2. Run `mint dev` locally to preview
3. Check terminal for validation errors
4. Fix any schema violations in docs.json
5. Verify navigation works correctly in browser
6. Test both light and dark modes
7. Commit and push to deploy

## Troubleshooting guide

### Logo appears too small or too large
**Solution:** Modify `custom.css` max-height value
- File location: `/home/user/docs/custom.css`
- Current value: `max-height: 50px !important;`
- Increase value for larger logo (e.g., 60px, 80px, 100px)
- Decrease value for smaller logo (e.g., 40px, 35px)
- Test in both light and dark modes

### Sidebar not showing
**Check these:**
1. Theme is set to one that supports sidebar (`palm`, `willow`, `aspen`)
2. Navigation structure uses `navigation.tabs[].groups[]` format
3. Groups array is not empty
4. Page paths in docs.json match actual files

### Full-width layout not applied
**Solutions:**
- Verify theme is `palm` (designed for full-width)
- Check if custom CSS is conflicting
- Clear browser cache and hard reload

### docs.json validation errors
**Process:**
1. Read the exact error message from `mint dev` output
2. Check "Common docs.json validation errors" section above
3. Validate property names match current Mintlify schema
4. Ensure all required properties are present
5. Test with `mint dev` after each fix

### Page not appearing in navigation
**Check:**
1. File path in docs.json matches actual file location (without .mdx)
2. File has valid frontmatter with title and description
3. File is in correct group array in docs.json
4. No typos in page path
5. Run `mint dev` to see if build errors occur

### Changes not reflected after deployment
**Steps:**
1. Verify changes were committed and pushed to main branch
2. Check deployment status (Mintlify dashboard or hosting platform)
3. Clear browser cache
4. Wait for CDN propagation (can take minutes)
5. Check if build succeeded without errors

### Custom CSS not being applied
**Verify:**
1. File is named `custom.css` (exact name)
2. File is in repo root directory (/home/user/docs/)
3. CSS selectors are specific enough
4. Using `!important` flag if needed to override theme CSS
5. No syntax errors in CSS file

## Git workflow
- NEVER use --no-verify when committing
- Ask how to handle uncommitted changes before starting
- Create a new branch when no clear branch exists for changes
- Commit frequently throughout development with descriptive messages
- NEVER skip or disable pre-commit hooks
- Branch naming: `claude/` prefix for Claude Code branches
- Push to correct branch: `git push -u origin <branch-name>`
- Pull before making changes: `git pull origin <branch-name>`

## Do not - Lessons learned from implementation

**Repository and content:**
- Skip frontmatter on any MDX file (breaks Mintlify navigation)
- Use absolute URLs for internal links (use relative paths like `/features/overview`)
- Include untested code examples (verify all code actually works)
- Make assumptions - always ask for clarification
- Remove Mintlify starter content without replacing with actual content

**Configuration mistakes:**
- Remove the theme property from docs.json (causes validation error)
- Use invalid property names in docs.json (use navbar.*, not topbar*)
- Use relative paths for navbar.primary.href (must be full URL)
- Put tabs at root level (must be inside navigation object)
- Modify docs.json without testing with `mint dev`

**Styling and branding:**
- Try to control logo size through SVG dimensions alone (CSS has final say)
- Use ViewBox-only approach for logo sizing (makes logo smaller)
- Add custom CSS without testing impact on Mintlify's built-in styles
- Optimize/minify SVG logos (keep readable for future edits)
- Forget to test in both light and dark modes

**Process mistakes:**
- Make multiple changes without committing incrementally
- Push to wrong branch
- Skip validation testing with `mint dev`
- Assume docs.json properties work without checking schema
- Hard reset without communicating (can cause confusion)

## Implementation history and current state

### What was accomplished
1. **Repository setup** - Cleaned Mintlify starter kit, removed all example content
2. **Branding** - Updated to Erlin AI brand (name, colors, logo, favicon)
3. **Navigation** - Set up 4-tab structure with proper hierarchy (Introduction, Features, Platform, Changelog)
4. **Content structure** - Created modular directory structure with 11 MDX pages
5. **Theme configuration** - Switched from mint → almond → palm for full-width layout
6. **Logo sizing** - Solved complex logo sizing issue with custom.css approach
7. **Validation fixes** - Corrected all docs.json schema violations (navbar properties, navigation structure)

### Key technical decisions made
- **Theme choice:** `palm` - Chosen for full-width layout and robust sidebar support
- **Logo solution:** custom.css with `!important` flags - Only reliable way to control logo size
- **SVG approach:** Extreme dimensions (2500x960) combined with viewBox - Helps push against CSS constraints
- **Navigation pattern:** Tabs → Groups → Pages - Mintlify's recommended structure for multi-section docs
- **Component usage:** Card, CardGroup, Note, Steps - Provides visual hierarchy and engagement

### What's working
- All 11 MDX pages exist with proper frontmatter
- Navigation displays correctly in 4 tabs
- Logo renders at adjustable size via custom.css
- Brand colors applied throughout (Erlin blue #0d37fd)
- Palm theme provides full-width layout
- Sidebar navigation functions properly
- Both light and dark modes supported

### What needs future work
- Remaining pages need actual Erlin AI content (currently have placeholder/starter content)
- Analytics features documentation may need expansion
- Platform section only has dashboard overview (could add more guides)
- Changelog needs to be populated with actual releases
- Consider adding FAQ section using Accordion components
- May need additional brand monitoring documentation
- Competitor analysis features may need documentation

### Critical files to preserve
- **custom.css** - Contains the working logo sizing solution
- **docs.json** - Carefully configured navigation and theme settings
- **logo/dark.svg & logo/light.svg** - Custom brand logos with specific dimensions
- **claude.md** - This comprehensive project context file

### For the next session
When starting work on this repository:
1. Read this claude.md file completely first
2. Pull latest changes from the branch
3. Understand current navigation structure in docs.json
4. Review existing MDX files to understand content patterns
5. Test with `mint dev` before making major changes
6. Commit frequently with descriptive messages
7. If modifying logo, only adjust custom.css max-height value
8. If adding pages, add to docs.json navigation AND create MDX file
9. Validate all docs.json changes to avoid schema errors
10. Remember: custom.css is the SOURCE OF TRUTH for logo sizing
