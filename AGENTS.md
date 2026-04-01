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
categories: [auto-detect 2-4 categories - space separated]
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
```

**Step A2 - Orient (if needed):**
```bash
# Check dimensions - if image appears wrong on phone, rotate to match phone view
# For iPhone HEIC: rotate -90 degrees (270) to make it portrait as seen on phone
sips -r -90 /tmp/original.png --out /tmp/rotated.png
```
Note: HEIC files from iPhones often need rotation to match how they appear on the device. If the image appears correctly after conversion, skip this step and use `/tmp/original.png` in subsequent steps. If rotated, use `/tmp/rotated.png` instead.

**Step B - Crop:**
```bash
sips -c 1500 3000 /tmp/rotated.png --out /tmp/cropped.png
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

#### 3. Categorization Rules

**Detect and assign from this taxonomy:**

**Categories** (pick 2-4):
- `technology` - for AI, tools, infrastructure posts
- `security` - for privacy, data protection, risk posts  
- `ai` - for LLM, machine learning, automation posts
- `engineering-leadership` - for management, teams, culture posts
- `product-management` - for roadmap, features, product posts

**Tags** (generate 8-12):  
Include specific terms mentioned in content + these standards:
- Tool names (e.g., opencode, jekyll, docker)
- Technology terms (e.g., llm, ai-agents, infrastructure)
- Concept tags (e.g., privacy, risk-management, data-security)
- Action tags (e.g., free-tier, hidden-costs, due-diligence)

#### 4. Image Naming & Caption Format

**Filename Pattern:**
```
[location]-[description]-[month]-[year].png
```
- All lowercase
- Use hyphens as separators
- Month and year from image metadata creation date

**Examples:**
- `outdoor-cafe-amsterdam-november-2025.png`
- `charles-bridge-museum-prague-january-2026.png`
- `cathedrale-de-la-major-april-2024.png`

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

**For deployment:**
- Only commit files in `_posts/` and `public/images/`
- Never commit .DS_Store, Gemfile.lock, or other system files
