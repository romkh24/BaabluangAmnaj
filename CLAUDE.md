# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Always Do First
- **Invoke the `frontend-design` skill** before writing any frontend code, every session, no exceptions.

## Project Overview
This is a static website for **บ้านหลวงอำนาจจีนนิกร** (Ban Luang Amnaj Chinnakorn), a historic Thai house in Chonburi, Thailand. The site is in **Thai language**. Content covers the house's history, its founder (หลวงอำนาจจีนนิกร / Luang Amnaj Chinnakorn, a Teochew Chinese immigrant), related novels by author ปิยะพร ศักดิ์เกษม, and the conservation award it received.

## Content Structure
All content assets live in Thai-named folders at the project root:

| Folder | Contents |
|---|---|
| `HomepagePhotos/` | Hero/homepage photos of the house and its owners |
| `Drawing_Render/` | Architectural drawings (`drawing-01` to `drawing-06`) and 3D renders (`Render01` to `Render08`) |
| `บ้านหลวงอำนาจ/` | Interior/exterior house photos + article HTML (Cocoa HTML Writer export) |
| `มองภาพเก่า เล่าเรื่องคุณก๋ง/` | Old photos and two article HTMLs about the great-grandfather |
| `นิยายที่มีจุดกำเนิดมาจากบ้านหลังนี้/` | Book cover images for 3 novels inspired by the house |
| `ความหมายของป้าย/` | Photos of ancestral plaques/signs and their translations |
| `รางวัลอนุรักษ์จากสมาคม/` | Conservation award photos from the Thai Architects Association |

The `.html` files inside content folders are **source text exports** (macOS TextEdit/Cocoa HTML Writer) — not styled pages. Read them to extract article text when building pages.

## Local Server
- **Always serve on localhost** — never screenshot a `file:///` URL.
- Start the dev server: `node serve.mjs` (serves the project root at `http://localhost:3000`)
- `serve.mjs` lives in the project root. Start it in the background before taking any screenshots.
- If the server is already running, do not start a second instance.
- **`serve.mjs` and `screenshot.mjs` do not exist yet** — create them if needed before first use.

## Screenshot Workflow
- **Always screenshot from localhost:** `node screenshot.mjs http://localhost:3000`
- Screenshots are saved automatically to `./temporary screenshots/screenshot-N.png` (auto-incremented, never overwritten).
- Optional label suffix: `node screenshot.mjs http://localhost:3000 label` → saves as `screenshot-N-label.png`
- `screenshot.mjs` lives in the project root. Use it as-is once created.
- After screenshotting, read the PNG from `temporary screenshots/` with the Read tool — Claude can see and analyze the image directly.
- When comparing, be specific: "heading is 32px but reference shows ~24px", "card gap is 16px but should be 24px"
- Check: spacing/padding, font size/weight/line-height, colors (exact hex), alignment, border-radius, shadows, image sizing

## Reference Images
- If a reference image is provided: match layout, spacing, typography, and color exactly. Swap in placeholder content (images via `https://placehold.co/`, generic copy). Do not improve or add to the design.
- If no reference image: design from scratch with high craft (see guardrails below).
- Screenshot your output, compare against reference, fix mismatches, re-screenshot. Do at least 2 comparison rounds. Stop only when no visible differences remain or user says so.

## Output Defaults
- Single `index.html` file, all styles inline, unless user says otherwise
- Tailwind CSS via CDN: `<script src="https://cdn.tailwindcss.com"></script>`
- Placeholder images: `https://placehold.co/WIDTHxHEIGHT`
- Mobile-first responsive
- Thai language: use a Thai-compatible web font (e.g. Sarabun or Noto Sans Thai from Google Fonts)

## Brand Assets
- Always check the `brand_assets/` folder before designing (it may not exist yet).
- If assets exist there, use them. Do not use placeholders where real assets are available.
- Real photos are available in the content folders above — use them instead of placeholders when building actual pages.

## Anti-Generic Guardrails
- **Colors:** Never use default Tailwind palette (indigo-500, blue-600, etc.). Pick a custom brand color and derive from it.
- **Shadows:** Never use flat `shadow-md`. Use layered, color-tinted shadows with low opacity.
- **Typography:** Never use the same font for headings and body. Pair a display/serif with a clean sans. Apply tight tracking (`-0.03em`) on large headings, generous line-height (`1.7`) on body.
- **Gradients:** Layer multiple radial gradients. Add grain/texture via SVG noise filter for depth.
- **Animations:** Only animate `transform` and `opacity`. Never `transition-all`. Use spring-style easing.
- **Interactive states:** Every clickable element needs hover, focus-visible, and active states. No exceptions.
- **Images:** Add a gradient overlay (`bg-gradient-to-t from-black/60`) and a color treatment layer with `mix-blend-multiply`.
- **Spacing:** Use intentional, consistent spacing tokens — not random Tailwind steps.
- **Depth:** Surfaces should have a layering system (base → elevated → floating), not all sit at the same z-plane.

## Hard Rules
- Do not add sections, features, or content not in the reference
- Do not "improve" a reference design — match it
- Do not stop after one screenshot pass
- Do not use `transition-all`
- Do not use default Tailwind blue/indigo as primary color
