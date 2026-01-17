# Lovable Presentation Prompt

Use this prompt in [Lovable](https://lovable.dev) to generate an interactive presentation deck for the VibeCheck session.

---

## Initial Prompt

```
Build an interactive presentation deck for a 60-minute workshop called "VibeCheck: Sip. Secure. Ship."

Design requirements:
- Dark theme with accent color #10B981 (emerald green)
- Clean, minimal design with lots of whitespace
- Smooth slide transitions using Framer Motion
- Keyboard navigation (arrow keys) and swipe support
- Progress indicator at bottom
- Mobile responsive

Slides needed:

1. TITLE SLIDE
   - "VibeCheck"
   - Tagline: "Sip. Secure. Ship."
   - Subtitle: "Build a secure project in one hour"
   - QR code placeholder for GitHub repo

2. WHAT YOU'LL LEAVE WITH (animated checklist)
   - ✅ Skills to vibe code a project from scratch
   - ✅ The security checklist that prevents 80% of disasters
   - ✅ This GitHub repo of resources
   - ✅ Your own project (if you bring one)

3. THE STAT (big number, dramatic)
   - "80%" large centered
   - "of AI-generated code contains vulnerabilities"
   - "This session helps you avoid them."

4. PICK YOUR LEVEL (3 columns, interactive hover)
   - 🌱 Beginner: Vibe Coding (Lovable, v0, Bolt)
   - 🔧 Intermediate: Spec Engineering (Kiro, Cursor)
   - 🚀 Advanced: Agentic Coding (Claude Code, Cline)
   Each column expands on hover to show tools

5. THE 7-POINT SECURITY CHECKLIST (animated list)
   1. Never commit secrets
   2. Review auth code
   3. Check .gitignore
   4. Scope API permissions
   5. Use secrets scanner
   6. Review DB queries
   7. Test error handling
   Items animate in one by one

6. BUILD TIME (countdown timer optional)
   - "30 minutes"
   - "Pick your project. Pick your tool. Start building."
   - Starter project suggestions in cards

7. DEMO: ZOMBIE BLASTER
   - Screenshot/video placeholder
   - "Built in 11 days with Claude Code"
   - "AI wrote 90% of the code"

8. SHARE
   - "What did you build?"
   - Space for audience interaction

9. RESOURCES (final slide)
   - GitHub repo QR code
   - Links: Kiro, Claude Code, MCP
   - "Sip. Secure. Ship."

Add a floating navigation menu that shows all slides as dots.
Include a "presenter mode" toggle that shows speaker notes.
```

---

## Knowledge File (Brand Colors)

Create a file called `brand.md` in Lovable and paste:

```markdown
# VibeCheck Brand

## Colors
- Primary: #10B981 (emerald green)
- Background: #0F172A (dark slate)
- Surface: #1E293B (slate)
- Text: #F8FAFC (white)
- Muted: #94A3B8 (gray)

## Typography
- Headings: Inter, bold
- Body: Inter, regular
- Code: JetBrains Mono

## Style
- Minimal, clean
- Lots of whitespace
- Subtle animations
- Dark theme
```

---

## Follow-Up Prompts

### Add slide transitions
```
Add smooth page transitions between slides using Framer Motion. 
Use a fade + slide effect. Duration 0.3s.
```

### Add keyboard navigation
```
Add keyboard navigation:
- Left/Right arrows to navigate slides
- Escape to show slide overview
- F for fullscreen
```

### Add presenter notes
```
Add a presenter mode (toggle with P key) that shows:
- Current slide
- Next slide preview
- Speaker notes
- Timer
```

### Make mobile responsive
```
Make the presentation fully responsive:
- Stack columns vertically on mobile
- Larger touch targets
- Swipe navigation
- Hide presenter controls on mobile
```

### Add QR code
```
Add a QR code component that links to:
https://github.com/vibecheck/vibecheck

Place it on the title slide and final slide.
```

---

## Slide-by-Slide Fix Prompts

After reviewing the live presentation at https://v1becheck.lovable.app, use these prompts to fix specific issues:

### CRITICAL: Slide 7 - Replace Demo Placeholder
```
On slide 7 (Demo: Zombie Blaster), replace the "Video / Screenshot Placeholder" with:

1. Add an actual image placeholder that I can replace with a screenshot
2. Use this placeholder image URL for now: https://placehold.co/800x450/1E293B/10B981?text=Zombie+Blaster+Demo
3. Add text below the image: "Demoed at AWS re:Invent — Jeff Barr stopped by!"
4. Keep the existing stats: "Built in 11 days" and "AI wrote 90% of the code"
5. Add a 🎮 emoji before "Zombie Blaster" in the title
```

### CRITICAL: Slide 8 - Fix Share Slide
```
On slide 8 (What did you build?), replace the "Audience interaction space" placeholder with:

1. Remove the empty placeholder box
2. Add 3 action cards in a row:
   - "🙋 Raise your hand" - "Share your screen with the group"
   - "💬 Drop in chat" - "Paste your project URL"
   - "📸 Screenshot it" - "We'll feature the best ones"
3. Add encouraging text below: "No project too small — even a button counts!"
4. Keep the people icon and "What did you build?" heading
```

### Slide 2 - Brand Color Fix
```
On slide 2 (What You'll Leave With), change the checkmark icons from blue to emerald green (#10B981) to match the brand colors.
```

### Slide 2 - Add Animation
```
On slide 2 (What You'll Leave With), add a staggered animation where each checklist item fades in one after another with a 0.2s delay between each.
```

### Slide 3 - Count-Up Animation
```
On slide 3 (the 80% stat), add a count-up animation that goes from 0% to 80% over 1.5 seconds when the slide appears. Use easing for a smooth effect.
```

### Slide 4 - Better Icons
```
On slide 4 (Pick Your Level), replace the current icons with emojis:
- Beginner: 🌱 (seedling)
- Intermediate: 🔧 (wrench)  
- Advanced: 🚀 (rocket)

Make them larger (48px) and centered above each card title.
```

### Slide 5 - Add Subtitle and Animation
```
On slide 5 (The 7-Point Security Checklist):
1. Add a subtitle below the heading: "These prevent 80% of vibe coding disasters"
2. Add staggered animation where items appear one by one (0.15s delay each)
3. Center the 7th item or make it span full width
```

### Slide 6 - Update Project Ideas
```
On slide 6 (Build Time), update the starter project cards to:
1. "Personal Portfolio" - "Your own site (20 min)" - 🌐 icon
2. "Landing Page" - "Marketing site with CTA (15 min)" - 📄 icon
3. "Todo App" - "Classic first project (30 min)" - ✅ icon

Add time estimates as badges on each card.
```

### Slide 9 - Add Thank You
```
On slide 9 (Resources):
1. Add "Thank You! 🙏" as a heading above "Resources"
2. Add "Questions?" as a subheading
3. Below the tagline, add small text: "This presentation was built with Lovable"
4. Optional: Add a Twitter/LinkedIn handle for follow-up
```

### Global - Improve Transitions
```
Add smooth slide transitions throughout:
- Use a fade + slight slide up effect
- Duration: 0.4s
- Easing: ease-out
- Apply to all slides consistently
```

### Global - Mobile Responsiveness
```
Ensure all slides work on mobile:
- Stack columns vertically on screens < 768px
- Increase touch targets to 44px minimum
- Hide "Hover over..." instructions on mobile (show expanded by default)
- Test swipe navigation works smoothly
```

---

## Export Options

Once built in Lovable:
1. **Deploy** — Get a shareable URL for the presentation
2. **Export** — Download the React code for self-hosting
3. **PDF** — Use browser print to PDF for backup

---

## Image Assets Needed

Before presenting, replace placeholder images:
- [ ] Zombie Blaster screenshot or GIF (slide 7)
- [ ] Verify QR codes scan correctly (slides 1 and 9)

---

*This presentation was built with Lovable. Practice what you preach.*
