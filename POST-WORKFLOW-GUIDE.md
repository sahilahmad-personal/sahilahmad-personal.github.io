# Post Workflow Guide
## Complete Step-by-Step Process for Every Post

---

## 1. Folder and File Structure

Your complete blog structure for posts and media:

```
sahilahmad-personal.github.io/
│
├── _posts/                          ← ALL posts go here
│   ├── 2026-06-10-first-post.md
│   ├── 2026-07-01-second-post.md
│   └── 2026-08-01-third-post.md
│
├── assets/
│   └── img/
│       ├── avatar.jpg               ← your profile photo
│       ├── social-preview.png       ← site-wide social preview
│       ├── favicons/                ← favicon files
│       └── posts/                   ← ALL post images go here
│           ├── identity-governance/
│           │   ├── cover.jpg        ← cover image (1200x630)
│           │   ├── screenshot-1.png
│           │   └── diagram.png
│           ├── htb-lame/
│           │   ├── cover.jpg
│           │   ├── nmap-scan.png
│           │   └── user-flag.png
│           └── sql-injection/
│               ├── cover.jpg
│               └── burp-request.png
│
├── _drafts/                         ← work in progress posts
│   └── draft-post-title.md          ← no date prefix needed
│
├── POST-WRITING-GUIDE.md            ← your writing reference
└── POST-WORKFLOW-GUIDE.md           ← this file
```

---

## 2. File Naming Convention

### Published Posts

Format: `YYYY-MM-DD-title-in-lowercase-with-hyphens.md`

```
Rules:
├── Date must match the date in front matter
├── Title part: lowercase only
├── Spaces replaced with hyphens
├── No special characters (no apostrophes, commas, etc.)
├── Keep it short but descriptive
└── This becomes your post URL
```

Examples:
```
2026-06-10-what-is-identity-governance-and-why-i-am-learning-sailpoint.md
2026-07-01-htb-lame-writeup.md
2026-07-15-sql-injection-root-cause-to-remediation.md
2026-08-01-tls-handshake-analysed-in-wireshark.md
2026-09-01-active-directory-attack-lab-on-a-budget.md
```

The filename `2026-07-01-htb-lame-writeup.md` produces URL:
```
sahilahmad-personal.github.io/posts/htb-lame-writeup/
```

### Draft Posts (Work in Progress)

Format: `draft-title-here.md` (no date, lives in `_drafts/`)

```
_drafts/
├── draft-kerberoasting-explained.md
├── draft-burp-suite-complete-guide.md
└── draft-htb-blue-writeup.md
```

Drafts never publish — they build locally only.

---

## 3. Image Requirements

### Cover Image

| Property | Requirement |
|---|---|
| Dimensions | Exactly 1200 x 630 pixels |
| File size | Under 300KB ideally, maximum 500KB |
| Format | JPG preferred (smaller than PNG) |
| Filename | cover.jpg always |
| Location | /assets/img/posts/post-folder-name/ |

### In-Post Images (Screenshots, Diagrams)

| Property | Requirement |
|---|---|
| Dimensions | Maximum 1200px wide |
| File size | Under 500KB each |
| Format | PNG for screenshots, JPG for photos |
| Filename | descriptive-name.png (no spaces) |
| Location | Same folder as cover image |

---

## 4. Image Preparation Workflow

### Step 1: Get Your Images

**For cover images:**
- Download from unsplash.com (free, no attribution required for blog use)
- Or generate with AI image tools
- Or create in Canva (free) at 1200x630px custom size

**For screenshots:**
- Take screenshots with: `Prt Sc` key or `flameshot gui` on Kali
- Install flameshot: `sudo apt install -y flameshot`
- Flameshot lets you annotate, highlight, and crop before saving

### Step 2: Resize and Optimise

**Resize cover image to exactly 1200x630:**
```bash
convert input-image.jpg \
  -resize 1200x630^ \
  -gravity center \
  -extent 1200x630 \
  cover.jpg
```

**Resize in-post screenshots to max 1200px wide:**
```bash
convert screenshot.png \
  -resize 1200x \
  screenshot.png
```

**Compress JPG quality (reduce file size):**
```bash
convert cover.jpg \
  -quality 85 \
  cover.jpg
```

**Compress PNG (reduce file size):**
```bash
sudo apt install -y pngquant
pngquant --quality=65-80 screenshot.png
# Creates screenshot-fs8.png (compressed version)
mv screenshot-fs8.png screenshot.png
```

**Check file size:**
```bash
ls -lh assets/img/posts/post-folder/
```

**Check dimensions:**
```bash
python3 -c "
from PIL import Image
img = Image.open('cover.jpg')
print(f'{img.width}x{img.height}px')
"
```

### Step 3: Create Post Image Folder

```bash
mkdir -p assets/img/posts/your-post-folder-name
```

Naming rule: folder name should match your post filename (without date and .md)

Example:
- Post file: `2026-07-15-sql-injection-explained.md`
- Image folder: `assets/img/posts/sql-injection-explained/`

### Step 4: Copy Images to Folder

```bash
cp ~/Downloads/cover.jpg \
   assets/img/posts/your-post-folder/cover.jpg

cp ~/Pictures/screenshot.png \
   assets/img/posts/your-post-folder/screenshot-1.png
```

---

## 5. Complete Post Creation Workflow

Follow these exact steps for every post:

### Step 1: Plan

Before opening any file, answer these:
```
- What is the main topic?
- Who is this for? (beginner, intermediate, expert)
- What will the reader know after reading this?
- What category and tags will I use?
- Do I have hands-on content to include?
- What cover image will I use?
```

Write a quick outline:
```
## Section 1
## Section 2
## Section 3
## Conclusion
```

### Step 2: Write in Draft First

```bash
# Create draft
vim _drafts/draft-your-post-title.md
```

Start with the front matter template, then write freely.
Don't worry about perfection in draft stage — just get the content out.

### Step 3: Prepare Images

```bash
# Create image folder
mkdir -p assets/img/posts/your-post-folder

# Get cover image, resize it
convert downloaded-image.jpg \
  -resize 1200x630^ \
  -gravity center \
  -extent 1200x630 \
  assets/img/posts/your-post-folder/cover.jpg

# Verify dimensions
python3 -c "
from PIL import Image
img = Image.open('assets/img/posts/your-post-folder/cover.jpg')
print(f'{img.width}x{img.height}px')
"
```

### Step 4: Create the Published Post File

```bash
# Get today's date
date +%Y-%m-%d

# Create post file with correct date
vim _posts/2026-07-01-your-post-title.md
```

Copy content from your draft. Add front matter at top.

### Step 5: Review Checklist

Before committing — go through the checklist from POST-WRITING-GUIDE.md

### Step 6: Commit and Push

```bash
# Add everything
gaa

# Commit with descriptive message
gcmsg "post: your post title here"

# Push
gp
```

### Step 7: Verify Live

After build completes (2-3 minutes):
```
1. Visit your blog homepage — post appears ✓
2. Click the post — renders correctly ✓
3. Check cover image loads ✓
4. Check table of contents works ✓
5. Check share buttons work ✓
6. Check mobile view ✓
```

### Step 8: Share

```
LinkedIn:
- Write 3-4 lines about the post
- Include the link
- Add 3-5 hashtags
- Post

Twitter/X:
- One punchy line
- Link
- 2-3 hashtags

Reddit:
- Post to relevant subreddit (r/netsec, r/cybersecurity)
- Write genuine post description
- Include link

Medium (cross-post):
- Copy entire post content
- Paste into Medium editor
- Add canonical URL pointing to your blog
  (Settings → Advanced → Canonical URL)
- Publish
```

---

## 6. Where to Write

### Primary: Vim in Terminal

```bash
cd ~/personal/sahilahmad-personal.github.io
vim _posts/2026-07-01-your-post-title.md
```

Best for: quick posts, edits, technical content

### Alternative: VS Code

```bash
cd ~/personal/sahilahmad-personal.github.io
code .
```

Navigate to `_posts/` and create/edit your file.
VS Code gives you:
- Markdown preview (Ctrl+Shift+V)
- Spell check (install Code Spell Checker extension)
- Better for long-form writing

### For Long Writing Sessions

Write in Obsidian first:
```
Obsidian vault → drafts folder → write freely
→ When done → copy to _posts/ file
→ Add front matter
→ Push
```

Obsidian gives you:
- Distraction-free writing
- Word count
- Linked notes for research
- Works offline

---

## 7. Draft Management

### View All Drafts

```bash
ls _drafts/
```

### Preview Draft Locally

To see how a draft looks before publishing:

```bash
# Install Jekyll locally if not done
gem install jekyll bundler
bundle install

# Serve with drafts included
bundle exec jekyll serve --drafts

# Visit: http://localhost:4000
```

### Promote Draft to Published

```bash
# Rename from draft to published post
mv _drafts/draft-post-title.md \
   _posts/2026-07-01-post-title.md

# Add correct date to filename and front matter
# Then commit and push
```

---

## 8. Commit Message Convention

Use consistent commit messages:

```bash
# New post
gcmsg "post: title of your post"

# Edit existing post
gcmsg "edit: fix typo in sql injection post"

# Add image
gcmsg "add: cover image for htb lame post"

# Fix something
gcmsg "fix: correct broken link in first post"

# Add new feature or file
gcmsg "feat: add post workflow guide"

# Configuration change
gcmsg "config: update social links"
```

---

## 9. Post Organisation by Category

Keep this naming consistent across all posts:

### Security / HTB Posts
```
_posts/YYYY-MM-DD-htb-machinename-writeup.md
assets/img/posts/htb-machinename/
  ├── cover.jpg
  ├── nmap-scan.png
  ├── exploitation.png
  └── root-flag.png
```

### Security / Web Posts
```
_posts/YYYY-MM-DD-vulnerability-name-explained.md
assets/img/posts/vulnerability-name/
  ├── cover.jpg
  ├── burp-request.png
  └── payload-result.png
```

### IAM / SailPoint Posts
```
_posts/YYYY-MM-DD-sailpoint-topic.md
assets/img/posts/sailpoint-topic/
  ├── cover.jpg
  └── diagram.png
```

### Journey / Learning Posts
```
_posts/YYYY-MM-DD-monthly-reflection.md
assets/img/posts/monthly-reflection/
  └── cover.jpg
```

---

## 10. Content Calendar

Plan your posts in advance. Suggested schedule:

```
Month 1:
└── Post 1: What Is Identity Governance ✓ (published)

Month 2:
└── Post 2: TLS Handshake Analysed in Wireshark

Month 3:
└── Post 3: My First HTB Machines — What Nobody Tells You

Month 4:
└── Post 4: SQL Injection Root Cause to Remediation

Month 5:
└── Post 5: Active Directory Attack Lab on a Budget

Month 6:
└── Post 6: 6 Months Into Cybersecurity — Honest Reflection
```

Plus: HTB writeup for every retired machine you solve.

---

## 11. Quick Reference Card

Print this or pin it somewhere visible:
```
NEW POST CHECKLIST:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[ ] Write draft in _drafts/ or Obsidian
[ ] Create image folder: assets/img/posts/folder-name/
[ ] Get cover image from unsplash.com
[ ] Resize cover to 1200x630: convert img -resize 1200x630^ -gravity center -extent 1200x630 cover.jpg
[ ] Verify size under 500KB: ls -lh
[ ] Create post file: _posts/YYYY-MM-DD-title.md
[ ] Write complete front matter
[ ] Add content from draft
[ ] Run through writing checklist
[ ] Commit: gcmsg "post: title"
[ ] Push: gp
[ ] Wait for build (2-3 min)
[ ] Verify on live blog
[ ] Share on LinkedIn
[ ] Share on Twitter
[ ] Share on Reddit
[ ] Cross-post to Medium
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

IMAGE SIZES:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Cover image:      1200 x 630px  JPG  <300KB
In-post images:   max 1200px wide  PNG  <500KB
Avatar:           square  any size  JPG
Social preview:   1200 x 630px  PNG/JPG
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

RESIZE COMMAND:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
convert input.jpg -resize 1200x630^ -gravity center -extent 1200x630 cover.jpg
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

COMMIT MESSAGES:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
New post:    gcmsg "post: title here"
Edit post:   gcmsg "edit: what you changed"
Add image:   gcmsg "add: image description"
Fix:         gcmsg "fix: what you fixed"
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

