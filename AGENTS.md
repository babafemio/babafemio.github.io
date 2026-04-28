# Blog Post Creation Skill

## One-Shot Blog Post Workflow

This skill enables rapid, single-interaction blog post creation with standardized image processing.

### Inputs Required (Single Message)

User provides all three in one message:
1. **Post Title**: (e.g., "My New Post Title")
2. **Content**: Full blog post text  
3. **Image File Path**: (e.g., `~/Downloads/IMG_1234.HEIC`)

### Automatic Execution Steps

Upon receiving inputs, immediately execute:

#### 1. Create Blog Post File
- Generate filename: `YYYY-MM-DD-[slugified-title].md`
- Location: `_posts/`
- Template:
```yaml
---
layout: post
title: [Title]
tags: [auto-detect 8-12 tags - space separated]
image: /public/images/[processed-filename].png
description: [auto-generated 1-2 sentence summary]
image-caption: [auto-generated location + date + @babafemio]
---

[Content with excerpt separator <!--more--> after first paragraph]
```

#### 2. Process Image (Exact Sequence)

**Step A - Convert & Check Metadata:**
```bash
# Convert to PNG
sips -s format png [input] --out /tmp/original.png

# Get creation date from metadata (use this for filename and caption)
sips -g creation [input] | grep "creation:"
# Extract month and year from format: YYYY:MM:DD HH:MM:SS
# Example output: "creation: 2025:11:21 14:14:40" → "November 2025"

# Get GPS location data for filename and caption
mdls [input] | grep -E "kMDItemLatitude|kMDItemLongitude"
# Use coordinates to determine location (e.g., Prague, Amsterdam, etc.)
# If GPS data unavailable, ask user for location description
```

**Step A2 - Orient (Check Phone View):**
```bash
# Check current dimensions
file /tmp/original.png

# iPhone HEIC portrait photos often appear as landscape after conversion
# If the image shows as landscape (wider than tall) but should be portrait:
sips -r 90 /tmp/original.png --out /tmp/rotated.png

# Verify orientation matches phone view before proceeding
```
**Rotation Rule:** If image appears upside-down after +90°, use `-90` instead. Always verify orientation matches how it appears on the phone before cropping.

**Next step:** If rotated, use `/tmp/rotated.png` in subsequent steps. If not rotated, use `/tmp/original.png`.

**Step B - Crop:**
```bash
# Get image dimensions first to calculate 2:1 crop
# For portrait images (taller than wide), maintain full width, height = width/2
# For landscape images (wider than tall), maintain full height, width = height*2
sips -c 2142 4284 /tmp/rotated.png --out /tmp/cropped.png
```

**Step C - Resize:**
```bash
sips -z 800 1600 /tmp/cropped.png --out /tmp/resized.png
```

**Step D - Compress:**
```bash
pngquant --quality 80-95 --force --output /public/images/[filename].png /tmp/resized.png
```

**Step E - Cleanup:**
```bash
rm /tmp/original.png /tmp/rotated.png /tmp/cropped.png /tmp/resized.png
```

**Target Specs:**
- Dimensions: 1600x800 pixels
- File size: < 1MB (typically 700-900KB)
- Format: PNG (compressed with pngquant)

#### 3. Tag Rules

**Generate 8-12 relevant tags:**
Include specific terms mentioned in content + these standards:
- Tool names (e.g., opencode, jekyll, docker)
- Technology terms (e.g., llm, ai-agents, infrastructure)
- Concept tags (e.g., privacy, risk-management, data-security)
- Action tags (e.g., free-tier, hidden-costs, due-diligence)
- Category-equivalent tags (e.g., technology, security, ai, engineering-leadership, product-management)

#### 4. Image Naming & Caption Format

**Filename Pattern:**
```
[location]-[month]-[year].png
```
- All lowercase
- Use hyphens as separators
- Month and year from image metadata creation date
- Location from GPS metadata or user-provided description

**Examples:**
- `outdoor-cafe-amsterdam-november-2025.png`
- `charles-bridge-museum-prague-january-2026.png`
- `old-town-prague-january-2026.png`

**Caption Format:**
```
[Location Description], [Month] [Year] @babafemio
```
- Proper capitalization (title case for location/description)
- Use commas as separators
- Month and year MUST match the image creation date from metadata

**Examples:**
- "Outdoor Cafe, Amsterdam, November 2025 @babafemio"
- "Charles Bridge Museum, Prague, January 2026 @babafemio"
- "Cathedrale de la Major, April 2024 @babafemio"

### Review & Deploy Flow

**After creation, present:**

```
✅ Blog post created: _posts/YYYY-MM-DD-title.md
✅ Image processed: /public/images/[filename].png (XXXKB, 1600x800)

📋 Summary:
- Title: [Title]
- Categories: [list]
- Tags: [list]
- Image: [path]

🧪 Ready for review!

To test locally, run: bundle exec jekyll serve

When ready to deploy, reply: "deploy"
```

**Upon "deploy" command:**
```bash
git add _posts/YYYY-MM-DD-title.md public/images/[filename].png
git commit -m "Add new post: [Title]"
git push origin master
```

### Example User Input

```
Title: Innovate fast, manage risk faster

Content: [full blog post text here...]

Image: ~/Downloads/IMG_5111.HEIC
```

### Success Criteria

✓ One interaction to create
✓ Image automatically processed to <1MB
✓ Proper YAML front matter
✓ Auto-detected categories/tags
✓ Ready for immediate local testing
✓ One-command deploy

### Common Patterns

**For text content extraction:**
- Place `<!--more-->` after first substantial paragraph
- Auto-detect internal post links and format as: `{% link _posts/YYYY-MM-DD-title.md %}`

**For image processing:**
- Always maintain 2:1 aspect ratio (1600x800)
- Always compress with pngquant --quality 80-95
- Never skip the crop-then-resize sequence

**For link formatting:**
- Convert bare URLs to Markdown hyperlinks: `[anchor text](url)`
- Anchor text should describe the content being linked (not just "click here")
- For external links, add `{:target="_blank"}` attribute: `[text](url){:target="_blank"}`
- Example: `[opportunity cost of compute](https://stratechery.com/...){:target="_blank"}`

**For deployment:**
- Only commit files in `_posts/` and `public/images/`
- Never commit .DS_Store, Gemfile.lock, or other system files

**Pre-processing verification:**
Before executing image processing pipeline, verify:
1. Extract location from GPS metadata (use `mdls` if `exiftool` unavailable)
2. Confirm rotation direction by checking image orientation against expected phone view
3. Calculate crop dimensions based on actual image dimensions (not fixed values)
4. If GPS data is missing, pause and ask user for location description
