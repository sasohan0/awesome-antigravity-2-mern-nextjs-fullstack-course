# Module 5: Figma-to-Code Workflow — From Design to React/Tailwind Implementation

**File Name:** `06-module-05-figma-to-code-workflow.md`  
**Module Type:** Core Module  
**Target Learners:** Junior MERN Stack Developers  
**Estimated Time:** 5–7 hours  
**Recommended After:** Module 4: `SKILL.md` Mastery  
**Main Goal:** Learn how to convert a Figma design or design screenshot into clean React + TypeScript + Tailwind UI using Antigravity, while keeping design accuracy, responsiveness, and developer control.

---

## Module purpose

In real company assignments, you may not receive a vague idea only.

You may receive:

- A Figma file
- A Figma frame link
- A landing page design
- A dashboard design
- A mobile screen design
- A website reference
- A screenshot
- A Figma community template
- A design handoff document

Your task as a frontend or MERN developer is to convert that design into working UI.

This module teaches you how to do that with Antigravity.

You will learn:

- How to inspect Figma designs
- How to extract design tokens
- How to create a UI specification
- How to create a component map
- How to plan responsive behavior
- How to use Figma MCP when available
- How to work manually when MCP is unavailable
- How to guide Antigravity to implement one section at a time
- How to verify visual accuracy in the browser
- How to avoid messy AI-generated UI

This module is not about blindly asking:

```txt
Make this Figma design in React.
```

This module teaches a controlled workflow:

```txt
Design inspect → Token extraction → Component map → Implementation plan → Section-by-section build → Browser verification → Visual QA
```

---

## Why this module matters

Many junior developers can build UI from imagination.

Fewer junior developers can accurately convert a real design into clean code.

This skill is valuable because companies often evaluate developers using:

- Figma-to-code assignments
- Landing page replication tasks
- Dashboard UI tasks
- Pixel-matching tasks
- Responsive design tasks
- Frontend implementation challenges

If you can show that you can take a design and convert it into a professional UI, your portfolio becomes stronger.

---

## Figma-to-code mindset

Do not treat Figma as just an image.

A Figma design contains information:

- Layout
- Spacing
- Typography
- Colors
- Components
- Variants
- Assets
- Icons
- States
- Responsive clues
- Design system patterns

Your job is to extract that information and translate it into code.

---

## Two workflows in this module

You will learn two workflows.

| Workflow | When to use |
|---|---|
| Figma MCP workflow | When Figma MCP is available and connected to your AI tool/agent |
| Manual Figma handoff workflow | When MCP is unavailable, limited, confusing, or not allowed |

Both are useful.

Do not depend on MCP only.

A strong developer can still implement a design manually.

---

## What is Figma MCP?

Figma MCP allows supported AI agents and coding tools to access design context from Figma.

This can help agents understand:

- Design structure
- Styles
- Layout details
- Component hierarchy
- Design values
- Dev Mode context

This can make design-to-code more accurate than only giving screenshots.

But MCP is not magic.

You still need to:

- Review the output
- Check browser results
- Compare against the design
- Fix spacing
- Fix responsiveness
- Check accessibility
- Clean component structure

---

## When Figma MCP is useful

Use Figma MCP when:

- You have access to the Figma file
- The Figma file is organized
- The frame names are clear
- The design system is consistent
- Your agent/tool supports MCP
- You want better design context for implementation

---

## When manual workflow is better

Use manual workflow when:

- Figma MCP is not available
- You only have a screenshot
- The Figma file is messy
- The design has too many frames
- You want to teach yourself design inspection
- You need full control over implementation
- MCP output is inaccurate

Manual workflow is slower but builds stronger understanding.

---

# Part 1: Figma inspection basics

Before coding, inspect the design.

Look for:

```txt
1. Page/frame name
2. Layout structure
3. Section boundaries
4. Width and max-width
5. Grid/columns
6. Spacing
7. Typography
8. Colors
9. Border radius
10. Shadows
11. Buttons
12. Cards
13. Forms
14. Icons/images
15. Reusable components
16. Hover/active states if available
17. Mobile/tablet frames if available
```

---

## Inspect layout

Ask these questions:

1. Is the layout full-width or centered?
2. What is the max content width?
3. Is it grid, flex, or absolute positioned?
4. How many columns are used?
5. What is the section padding?
6. What is the gap between cards?
7. What is the gap between title and content?
8. What changes on mobile?

---

## Inspect typography

For each major text style, collect:

```txt
font family
font size
font weight
line height
letter spacing
text color
```

Example:

| Element | Font size | Weight | Line height | Color |
|---|---:|---:|---:|---|
| Hero title | 56px | 700 | 64px | #111827 |
| Section title | 36px | 700 | 44px | #111827 |
| Body text | 16px | 400 | 24px | #4B5563 |
| Button text | 16px | 600 | 24px | #FFFFFF |

---

## Inspect colors

Collect colors as tokens.

Example:

| Token | Value | Usage |
|---|---|---|
| `primary` | `#F97316` | CTA buttons |
| `primary-dark` | `#EA580C` | Button hover |
| `background` | `#FFFFFF` | Page background |
| `surface` | `#F9FAFB` | Cards/sections |
| `text-primary` | `#111827` | Headings |
| `text-muted` | `#6B7280` | Paragraphs |
| `border` | `#E5E7EB` | Card border |

Do not randomly choose similar colors if exact values are available.

---

## Inspect spacing

Spacing is what makes UI look professional.

Collect common spacing values:

| Use | Value |
|---|---:|
| Page horizontal padding | 24px |
| Section vertical padding | 80px |
| Card padding | 24px |
| Grid gap | 24px |
| Button padding | 12px 20px |
| Navbar height | 72px |

Then translate to Tailwind:

| Pixel | Tailwind |
|---:|---|
| 4px | `1` |
| 8px | `2` |
| 12px | `3` |
| 16px | `4` |
| 20px | `5` |
| 24px | `6` |
| 32px | `8` |
| 40px | `10` |
| 48px | `12` |
| 64px | `16` |
| 80px | `20` |

---

## Inspect components

Find repeated UI patterns:

- Navbar
- Hero section
- Button
- Card
- Badge
- Input
- Search bar
- Filter chip
- Dashboard card
- Table row
- Modal
- Sidebar
- Footer

Create reusable components when a pattern appears more than once.

---

# Part 2: Required design documentation

Before asking Antigravity to code, create these docs:

```txt
docs/DESIGN_SOURCE.md
docs/DESIGN_SYSTEM.md
docs/UI_SPEC.md
docs/COMPONENT_MAP.md
docs/RESPONSIVE_PLAN.md
docs/ASSET_PLAN.md
docs/FIGMA_TO_CODE_PLAN.md
docs/VISUAL_QA_CHECKLIST.md
```

These files help Antigravity understand the design without repeatedly asking you for context.

---

## `DESIGN_SOURCE.md`

Create:

```txt
docs/DESIGN_SOURCE.md
```

Template:

```md
# Design Source

## Design type
Figma file / Figma community file / Screenshot / Website reference

## Design link
-

## Frame/page name
-

## Screenshot path
-

## Target implementation
-

## Pages/sections to implement
1.
2.
3.

## Design access notes
-

## Known limitations
- Exact font may not be available
- Some images/icons may need replacement
- Mobile frame may be missing
- Some values may be approximate if not inspectable
```

---

## `DESIGN_SYSTEM.md`

Create:

```txt
docs/DESIGN_SYSTEM.md
```

Template:

```md
# Design System

## Colors

| Token | Value | Usage |
|---|---|---|
| primary | # | CTA/buttons |
| primary-hover | # | CTA hover |
| background | # | Page background |
| surface | # | Cards/sections |
| text-primary | # | Headings |
| text-secondary | # | Paragraphs |
| border | # | Borders |

## Typography

| Token | Font | Size | Weight | Line height | Usage |
|---|---|---:|---:|---:|---|
| heading-xl |  |  |  |  | Hero title |
| heading-lg |  |  |  |  | Section title |
| body |  |  |  |  | Paragraph |
| small |  |  |  |  | Captions |
| button |  |  |  |  | Buttons |

## Spacing

| Token | Value | Usage |
|---|---:|---|
| section-y |  | Section vertical padding |
| container-x |  | Page horizontal padding |
| card-padding |  | Card inner spacing |
| grid-gap |  | Card/list gap |

## Radius

| Token | Value | Usage |
|---|---:|---|
| sm |  | Small controls |
| md |  | Buttons |
| lg |  | Cards |
| xl |  | Hero cards/modals |

## Shadows

| Token | Value | Usage |
|---|---|---|
| card |  | Card shadow |
| dropdown |  | Menu/dropdown |
```

---

## `UI_SPEC.md`

Create:

```txt
docs/UI_SPEC.md
```

Template:

```md
# UI Specification

## Page/section name
-

## Purpose
-

## Layout
-

## Content structure
-

## Components
1.
2.
3.

## User actions
-

## Data needed
-

## States required
- Loading
- Empty
- Error
- Success

## Desktop behavior
-

## Tablet behavior
-

## Mobile behavior
-

## Accessibility notes
-

## Implementation notes
-
```

---

## `COMPONENT_MAP.md`

Create:

```txt
docs/COMPONENT_MAP.md
```

Template:

```md
# Component Map

## Page: Home

```txt
HomePage
  ├── Navbar
  ├── HeroSection
  ├── FeaturedItemsSection
  │     └── FoodCard
  ├── HowItWorksSection
  ├── TestimonialsSection
  └── Footer
```

## Component responsibilities

| Component | Responsibility | Props/Data |
|---|---|---|
| Navbar | Navigation and auth links | user optional |
| HeroSection | Main landing message and CTA | static text |
| FoodCard | Show food item summary | food |
| FeaturedItemsSection | Show selected foods | foods |
| Footer | Footer links/info | static text |
```

---

## `RESPONSIVE_PLAN.md`

Create:

```txt
docs/RESPONSIVE_PLAN.md
```

Template:

```md
# Responsive Plan

## Breakpoints

| Breakpoint | Width | Behavior |
|---|---:|---|
| Mobile | < 640px | Single column, compact spacing |
| Tablet | 640–1024px | Two columns where possible |
| Desktop | > 1024px | Full layout/grid |

## Navigation

| Device | Behavior |
|---|---|
| Mobile | Hamburger/stacked menu |
| Tablet | Compact nav |
| Desktop | Full nav |

## Grid behavior

| Section | Mobile | Tablet | Desktop |
|---|---|---|---|
| Food cards | 1 column | 2 columns | 3 columns |
| Dashboard cards | 1 column | 2 columns | 4 columns |
| Hero | Stacked | Stacked/2 column | 2 column |

## Spacing adjustments

| Element | Mobile | Desktop |
|---|---:|---:|
| Section padding | 48px | 80px |
| Container padding | 16px | 24px/32px |
| Card padding | 16px | 24px |
```

---

## `ASSET_PLAN.md`

Create:

```txt
docs/ASSET_PLAN.md
```

Template:

```md
# Asset Plan

## Images

| Asset | Source | Usage | Replacement allowed? |
|---|---|---|---|
| Hero image | Figma/Unsplash/custom | Hero section | Yes |
| Food images | Placeholder/stock | Food cards | Yes |
| Logo | Custom text/logo | Navbar | Yes |

## Icons

| Icon | Source | Usage |
|---|---|---|
| Search | Lucide/react-icons | Search bar |
| Cart | Lucide/react-icons | Cart button |
| User | Lucide/react-icons | Profile/auth |

## Asset rules
- Do not use copyrighted images without permission.
- Use placeholders if assets are unavailable.
- Optimize image sizes.
- Add alt text.
- Keep naming consistent.
```

---

## `FIGMA_TO_CODE_PLAN.md`

Create:

```txt
docs/FIGMA_TO_CODE_PLAN.md
```

Template:

```md
# Figma-to-Code Plan

## Target
-

## Implementation order
1. Extract design tokens
2. Create layout shell
3. Create reusable components
4. Implement first section
5. Verify in browser
6. Implement next section
7. Add responsive behavior
8. Run visual QA

## Files to create/edit

| File | Purpose |
|---|---|
| src/pages/HomePage.tsx | Home page |
| src/components/layout/Navbar.tsx | Navigation |
| src/components/home/HeroSection.tsx | Hero |
| src/components/common/Button.tsx | Reusable button |
| src/components/common/Card.tsx | Reusable card |

## Rules for Antigravity
- Implement one section at a time.
- Do not edit backend.
- Do not install packages unless approved.
- Do not guess design values if provided.
- After implementation, provide changed files and verification steps.

## Verification
- Compare desktop screenshot
- Compare mobile screenshot
- Check spacing
- Check typography
- Check colors
- Check console errors
```

---

## `VISUAL_QA_CHECKLIST.md`

Create:

```txt
docs/VISUAL_QA_CHECKLIST.md
```

Template:

```md
# Visual QA Checklist

## Layout
- [ ] Page width matches design
- [ ] Container alignment is correct
- [ ] Sections are in correct order
- [ ] Grid columns match design
- [ ] Cards align consistently

## Spacing
- [ ] Section padding is close to design
- [ ] Card padding is consistent
- [ ] Gap between elements is correct
- [ ] Mobile spacing is not too large/small

## Typography
- [ ] Heading size is close to design
- [ ] Font weight matches design
- [ ] Line height is readable
- [ ] Text colors match design

## Colors
- [ ] Primary color matches design
- [ ] Background color matches design
- [ ] Card color matches design
- [ ] Border color matches design

## Responsiveness
- [ ] Mobile layout works
- [ ] Tablet layout works
- [ ] Desktop layout works
- [ ] No horizontal scroll

## Interaction
- [ ] Buttons are clickable
- [ ] Links work
- [ ] Hover states are acceptable
- [ ] Forms are usable

## Technical
- [ ] No console errors
- [ ] No broken images
- [ ] Build passes
```

---

# Part 3: Manual Figma handoff workflow

Use this workflow when you have Figma access but no MCP.

## Step 1: Choose target frame

Pick one page or one section.

Do not start with the entire design.

Good first targets:

```txt
Navbar + Hero
Food card
Menu grid
Login form
Dashboard card
Admin table
Footer
```

---

## Step 2: Screenshot the frame

Save screenshot in:

```txt
design/screenshots/
```

Example:

```txt
design/screenshots/home-hero-desktop.png
design/screenshots/home-hero-mobile.png
```

---

## Step 3: Extract design tokens

Use Figma inspect panel or visual inspection.

Save values into:

```txt
docs/DESIGN_SYSTEM.md
```

---

## Step 4: Create component map

Break the design into components.

Example:

```txt
HeroSection
  ├── Badge
  ├── Heading
  ├── Subheading
  ├── CTAButtons
  └── HeroImageCard
```

---

## Step 5: Create implementation prompt

Use Antigravity like this:

```txt
Read:
- docs/DESIGN_SYSTEM.md
- docs/UI_SPEC.md
- docs/COMPONENT_MAP.md
- docs/RESPONSIVE_PLAN.md

Task:
Implement only the Home page hero section.

Use:
- React
- TypeScript
- Tailwind CSS

Rules:
- Do not edit backend.
- Do not implement other sections.
- Do not install packages.
- Follow the design tokens.
- Keep components reusable.
- After implementation, list changed files and browser verification steps.
```

---

## Step 6: Verify browser output

Open the app and compare:

- Design screenshot
- Browser output desktop
- Browser output mobile

Document issues in:

```txt
docs/VISUAL_QA_REPORT.md
```

---

# Part 4: Figma MCP workflow

Use this workflow when your coding tool/agent can access Figma MCP.

## Step 1: Confirm MCP availability

Check:

```txt
1. Is Figma MCP connected?
2. Does the agent have access to the frame?
3. Can it read design context?
4. Can it identify components/styles?
5. Does your account/seat allow it?
```

---

## Step 2: Give exact Figma frame

Do not give the whole file if the target is one section.

Prompt:

```txt
Use the Figma MCP context for this frame:

[Paste Figma frame link]

Task:
Analyze the design only.

Return:
1. Layout structure
2. Design tokens
3. Component map
4. Responsive assumptions
5. Assets needed
6. Implementation risks

Do not write code yet.
```

---

## Step 3: Save MCP analysis

Create:

```txt
docs/FIGMA_MCP_ANALYSIS.md
```

Include:

```md
# Figma MCP Analysis

## Frame
-

## Layout structure
-

## Design tokens
-

## Component map
-

## Assets
-

## Responsive assumptions
-

## Implementation risks
-
```

---

## Step 4: Implement one section

Prompt:

```txt
Use:
- docs/FIGMA_MCP_ANALYSIS.md
- docs/DESIGN_SYSTEM.md
- docs/COMPONENT_MAP.md

Implement only:
[Section name]

Rules:
- Use React + TypeScript + Tailwind.
- Do not edit unrelated files.
- Do not implement other sections.
- Do not install packages without approval.
- Keep components reusable.
- After implementation, summarize changed files.
```

---

## Step 5: Verify with browser

Prompt:

```txt
Use browser verification.

Compare the implemented section with the Figma frame.

Check:
1. Layout
2. Spacing
3. Typography
4. Colors
5. Responsiveness
6. Console errors
7. Broken images

Do not edit files yet.

Return a visual QA report.
```

---

# Part 5: Antigravity prompts for this module

## Prompt 1: Create design docs

```txt
I am doing Module 5: Figma-to-Code Workflow.

Create these files:
1. docs/DESIGN_SOURCE.md
2. docs/DESIGN_SYSTEM.md
3. docs/UI_SPEC.md
4. docs/COMPONENT_MAP.md
5. docs/RESPONSIVE_PLAN.md
6. docs/ASSET_PLAN.md
7. docs/FIGMA_TO_CODE_PLAN.md
8. docs/VISUAL_QA_CHECKLIST.md

Rules:
- Do not create React code yet.
- Do not install packages.
- Keep the docs beginner-friendly.
- Use React, TypeScript, and Tailwind CSS as implementation stack.
- Include sections for both Figma MCP and manual workflow.
```

---

## Prompt 2: Analyze a Figma design manually

```txt
I have a Figma design/screenshot for a MERN project page.

Analyze this design manually.

Return:
1. Layout structure
2. Section breakdown
3. Design tokens
4. Typography notes
5. Color notes
6. Component map
7. Responsive behavior assumptions
8. Assets needed
9. Implementation order
10. Risks

Do not write code yet.
```

---

## Prompt 3: Convert analysis into implementation plan

```txt
Read:
- docs/DESIGN_SYSTEM.md
- docs/UI_SPEC.md
- docs/COMPONENT_MAP.md
- docs/RESPONSIVE_PLAN.md
- docs/ASSET_PLAN.md

Create docs/SECTION_IMPLEMENTATION_PLAN.md.

Target section:
[Section name]

Include:
1. Component tree
2. Props/types needed
3. Files to create/edit
4. Tailwind layout approach
5. Responsive behavior
6. Data/mock data needed
7. Browser verification checklist

Do not write code.
```

---

## Prompt 4: Implement one section only

```txt
Read:
- docs/SECTION_IMPLEMENTATION_PLAN.md
- docs/DESIGN_SYSTEM.md
- docs/UI_SPEC.md

Implement only:
[Section name]

Rules:
- Use React + TypeScript + Tailwind.
- Do not edit backend.
- Do not implement other sections.
- Do not install packages.
- Keep components reusable.
- Use semantic HTML where possible.
- Add alt text for images.
- After implementation, list changed files and verification steps.
```

---

## Prompt 5: Visual QA review

```txt
Review the implemented section against the design reference.

Check:
1. Layout
2. Spacing
3. Typography
4. Colors
5. Buttons
6. Cards
7. Images
8. Responsiveness
9. Console errors
10. Accessibility basics

Do not edit yet.

Return:
- What matches
- What differs
- Critical fixes
- Nice-to-have improvements
- Final verdict
```

---

## Prompt 6: Fix only visual issues

```txt
Fix only the visual issues listed in docs/VISUAL_QA_REPORT.md.

Scope:
[Write exact files allowed]

Rules:
- Do not change business logic.
- Do not edit backend.
- Do not add new features.
- Do not install packages.
- Keep changes minimal.
- After fixing, summarize what changed.
```

---

# Part 6: NotebookLM workflow for this module

Create or open:

```txt
Antigravity 2.0 MERN Bootcamp
```

Add these sources:

```txt
1. 06-module-05-figma-to-code-workflow.md
2. Figma Dev Mode guide
3. Figma MCP server guide
4. Figma MCP developer docs
5. Your Figma design link or screenshots
6. DESIGN_SYSTEM.md
7. UI_SPEC.md
8. COMPONENT_MAP.md
9. RESPONSIVE_PLAN.md
10. FIGMA_TO_CODE_PLAN.md
```

---

## NotebookLM Prompt 1: Study Guide

```txt
Create a beginner-friendly study guide for Figma-to-code workflow.

Audience:
Junior MERN developers using Antigravity.

Explain:
1. What Figma-to-code means
2. How to inspect a design
3. How to extract design tokens
4. How to create a component map
5. How to plan responsive behavior
6. How to use Figma MCP when available
7. How to work manually when MCP is unavailable
8. How to prompt Antigravity for one section at a time
9. How to verify visual quality
10. Common mistakes
11. Practice checklist
```

---

## NotebookLM Prompt 2: Design analysis

```txt
Analyze my design sources and create a UI implementation guide.

Output:
1. Page/section summary
2. Layout structure
3. Design tokens
4. Component tree
5. Responsive behavior
6. Assets needed
7. Implementation order
8. Risk list
9. Antigravity prompts for implementation
```

---

## NotebookLM Prompt 3: Visual QA checklist

```txt
Create a visual QA checklist for my Figma-to-code implementation.

Check:
1. Layout
2. Spacing
3. Typography
4. Colors
5. Cards
6. Buttons
7. Forms
8. Images/icons
9. Mobile responsiveness
10. Accessibility basics
11. Console errors
12. Build errors
```

---

## NotebookLM Prompt 4: Interview explanation

```txt
Help me explain my Figma-to-code workflow in an interview.

Create:
1. 30-second answer
2. 1-minute answer
3. Technical explanation
4. Example from my project
5. Mistakes I avoided
6. How I used Antigravity safely
```

---

# Part 7: Required video resources

Watch at least two videos.

Search YouTube:

```txt
Figma Dev Mode for developers tutorial
Figma to React Tailwind tutorial
Figma MCP server tutorial
Figma to code workflow React
Convert Figma design to React Tailwind
```

Recommended official/product sources:

- Figma official YouTube channel
- Figma Dev Mode tutorials
- Figma MCP server introduction videos
- High-quality Figma-to-React/Tailwind walkthroughs

---

## Video learning notes

Create:

```txt
docs/notebooklm/module-05-video-learning-notes.md
```

Use this format:

```md
# Module 5 Video Learning Notes

## Video 1
Title:
Link:

### 5 lessons learned
1.
2.
3.
4.
5.

### How I will apply this to my project
1.
2.
3.

### Mistakes to avoid
1.
2.

---

## Video 2
Title:
Link:

### 5 lessons learned
1.
2.
3.
4.
5.

### How I will apply this to my project
1.
2.
3.

### Mistakes to avoid
1.
2.
```

---

# Part 8: Practice tasks

## Practice Task 1: Select a design source

Choose one:

```txt
1. Figma community landing page
2. Figma community dashboard
3. Figma file provided by mentor
4. Public website screenshot
5. Your own simple Figma design
```

Recommended beginner target:

```txt
Navbar + Hero + 1 card section
```

Do not start with a huge dashboard.

---

## Practice Task 2: Create design docs

Create:

```txt
docs/DESIGN_SOURCE.md
docs/DESIGN_SYSTEM.md
docs/UI_SPEC.md
docs/COMPONENT_MAP.md
docs/RESPONSIVE_PLAN.md
docs/ASSET_PLAN.md
docs/FIGMA_TO_CODE_PLAN.md
docs/VISUAL_QA_CHECKLIST.md
```

---

## Practice Task 3: Extract tokens manually

From your design, extract at least:

```txt
5 colors
5 typography styles
5 spacing values
3 border radius values
2 shadow values if available
```

Save them in:

```txt
docs/DESIGN_SYSTEM.md
```

---

## Practice Task 4: Create component map

Break the design into components.

Example:

```txt
HomePage
  ├── Navbar
  ├── HeroSection
  ├── FeaturedCards
  │     └── FeatureCard
  └── Footer
```

Save in:

```txt
docs/COMPONENT_MAP.md
```

---

## Practice Task 5: Create section implementation plan

Choose one section.

Create:

```txt
docs/SECTION_IMPLEMENTATION_PLAN.md
```

Include:

- Target section
- Component tree
- Props/types
- Files to create/edit
- Tailwind plan
- Responsive plan
- Verification checklist

---

## Practice Task 6: Implement one section with Antigravity

Use Prompt 4.

Rules:

```txt
1. Implement one section only.
2. Do not implement full project.
3. Do not edit backend.
4. Do not add unnecessary packages.
5. Verify in browser.
```

---

## Practice Task 7: Create visual QA report

Create:

```txt
docs/VISUAL_QA_REPORT.md
```

Use this format:

```md
# Visual QA Report

## Target section
-

## Design reference
-

## Browser URL
-

## Desktop comparison

### What matches
-

### What differs
-

## Mobile comparison

### What matches
-

### What differs
-

## Console errors
-

## Critical fixes
-

## Nice-to-have improvements
-

## Final verdict
Pass / Conditional pass / Fail
```

---

## Practice Task 8: Fix only visual issues

After visual QA, ask Antigravity to fix only the listed visual issues.

Do not allow it to rewrite the whole page.

---

# Part 9: Common mistakes

Avoid these mistakes:

## Mistake 1: Asking for full design implementation at once

Bad:

```txt
Convert this Figma file into React.
```

Better:

```txt
Analyze the hero section first. Do not write code yet.
```

---

## Mistake 2: Not creating design tokens

Bad:

```txt
Use similar colors.
```

Better:

```txt
Use colors from docs/DESIGN_SYSTEM.md.
```

---

## Mistake 3: Ignoring mobile view

Bad:

```txt
Only desktop looks fine.
```

Better:

```txt
Check mobile, tablet, and desktop.
```

---

## Mistake 4: Building non-reusable components

Bad:

```txt
Put all UI inside HomePage.tsx.
```

Better:

```txt
Create reusable Navbar, HeroSection, Button, and Card components.
```

---

## Mistake 5: Trusting AI visual output blindly

Bad:

```txt
It generated code, so it is done.
```

Better:

```txt
Compare browser output with the design and create VISUAL_QA_REPORT.md.
```

---

## Mistake 6: Using copyrighted assets blindly

Bad:

```txt
Use all images from the design without checking rights.
```

Better:

```txt
Use provided assets, placeholder images, or properly licensed assets.
```

---

# Part 10: Quality bar

Your Figma-to-code work should meet this minimum standard:

```txt
1. Layout roughly matches design.
2. Colors are close or exact.
3. Typography is close or exact.
4. Spacing is consistent.
5. Components are reusable.
6. Mobile layout works.
7. No major console errors.
8. Browser verification completed.
9. Visual QA report created.
10. Student can explain implementation decisions.
```

For advanced students:

```txt
1. Pixel-level alignment is improved.
2. Motion/hover states added carefully.
3. Accessibility basics checked.
4. Lighthouse issues reviewed.
5. Components are clean and scalable.
6. Storybook or component preview added optional.
```

---

# Required deliverables for this module

Submit:

```txt
1. Figma/design source link or screenshot
2. docs/DESIGN_SOURCE.md
3. docs/DESIGN_SYSTEM.md
4. docs/UI_SPEC.md
5. docs/COMPONENT_MAP.md
6. docs/RESPONSIVE_PLAN.md
7. docs/ASSET_PLAN.md
8. docs/FIGMA_TO_CODE_PLAN.md
9. docs/VISUAL_QA_CHECKLIST.md
10. docs/SECTION_IMPLEMENTATION_PLAN.md
11. Implemented React/Tailwind section
12. Desktop screenshot
13. Mobile screenshot
14. docs/VISUAL_QA_REPORT.md
15. NotebookLM Study Guide screenshot
16. NotebookLM design analysis screenshot
17. Video learning notes
18. Reflection file
```

---

# Reflection template

Create:

```txt
docs/reflections/06-module-05-figma-to-code-workflow-reflection.md
```

Use this format:

```md
# Reflection: Module 5 - Figma-to-Code Workflow

## Design source I used
-

## Section/page I implemented
-

## Design tokens I extracted
-

## Components I created
-

## What matched the design well
-

## What did not match perfectly
-

## What I learned about responsive design
-

## What Antigravity helped with
-

## What I had to fix manually
-

## How I will improve Figma-to-code work next time
-
```

---

# Quiz

## Multiple choice

**1. What is the first step before implementing a Figma design?**

A. Ask AI to build the full app  
B. Inspect and analyze the design  
C. Deploy immediately  
D. Create database models  

Correct answer: **B**

---

**2. What is a design token?**

A. A reusable design value like color, spacing, typography, radius, or shadow  
B. A MongoDB password  
C. A GitHub issue only  
D. A backend route  

Correct answer: **A**

---

**3. What should `COMPONENT_MAP.md` contain?**

A. A breakdown of page sections into reusable components  
B. Only API endpoints  
C. Only database collections  
D. Only deployment logs  

Correct answer: **A**

---

**4. What is the safest implementation approach with Antigravity?**

A. Implement the full Figma file at once  
B. Implement one section/component at a time  
C. Ignore design tokens  
D. Skip verification  

Correct answer: **B**

---

**5. What should you do after implementation?**

A. Push without checking  
B. Compare browser output with design and create a visual QA report  
C. Delete design docs  
D. Change backend randomly  

Correct answer: **B**

---

**6. What should you avoid if exact Figma values are available?**

A. Using exact design values  
B. Guessing random similar values  
C. Creating design docs  
D. Checking mobile view  

Correct answer: **B**

---

**7. What does `RESPONSIVE_PLAN.md` define?**

A. How layout changes across mobile, tablet, and desktop  
B. Backend schema only  
C. API response only  
D. GitHub license only  

Correct answer: **A**

---

**8. What is Figma MCP useful for?**

A. Giving AI agents structured design context  
B. Replacing all frontend knowledge  
C. Running MongoDB locally  
D. Deploying backend  

Correct answer: **A**

---

**9. What should be included in `VISUAL_QA_REPORT.md`?**

A. What matches, what differs, console errors, critical fixes, final verdict  
B. Only passwords  
C. Only package versions  
D. Only random comments  

Correct answer: **A**

---

**10. Why should components be reusable?**

A. To reduce duplication and improve maintainability  
B. To make code longer  
C. To avoid testing  
D. To hide UI issues  

Correct answer: **A**

---

## Short-answer questions

1. What is Figma-to-code workflow?
2. What is the difference between Figma MCP workflow and manual workflow?
3. Name five design tokens you should extract.
4. Why should you create a component map?
5. Why should you implement one section at a time?
6. What should be included in a responsive plan?
7. What is visual QA?
8. Why should you not blindly use copyrighted assets?
9. How can Antigravity help with Figma-to-code?
10. What will you check before saying the UI is complete?

---

# Mentor evaluation checklist

| Criteria | Pass condition |
|---|---|
| Design source | Figma/screenshot/reference clearly provided |
| Design system | Colors, typography, spacing, radius, shadows documented |
| UI spec | Page/section purpose, states, data, behavior documented |
| Component map | Page broken into reusable components |
| Responsive plan | Mobile/tablet/desktop behavior planned |
| Asset plan | Images/icons/assets listed with usage notes |
| Implementation plan | Section implementation planned before code |
| Code implementation | One section implemented cleanly |
| Visual QA | Browser output compared with design |
| Responsiveness | Mobile screenshot submitted |
| NotebookLM evidence | Study guide/design analysis submitted |
| Video evidence | Video notes submitted |
| Reflection | Student explains design-to-code decisions |

---

# Completion standard

You complete this module only when you can confidently say:

```txt
I can inspect a Figma design, extract design tokens, create a UI spec, map components, plan responsiveness, guide Antigravity to implement one section at a time, verify the result in the browser, and produce a visual QA report before moving to the next section.
```

After completing this file, continue to:

```txt
07-bonus-module-05-5-website-ui-replication-lab.md
```
