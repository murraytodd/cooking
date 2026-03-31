# Project Context: Recipe Archive Modernization

## 🎯 Overview
Migrating 11 hand-encoded XHTML recipe pages to modern HTML5 with structured data.

## 🛠 Tech Stack & Standards
- **Markup:** Semantic HTML5 (replace `<div>` soups with `<main>`, `<article>`, `<section>`).
- **Metadata:** Convert `hrecipe` microformats to `@type: Recipe` JSON-LD (Schema.org).
- **Styling:** Use plain, clean CSS that will render well on both laptops and mobile devices.
  - **Global Styles:** Place all general styles in a common `cooking.css` file. This file should be agnostic of individual recipes (i.e., no rules for specific recipe pages like `.carrot-soup-page`).
  - **Per-Recipe Styles:** For recipe-specific customizations like background colors, add a `<style>` block to the `<head>` of the individual HTML file. This keeps recipe-specific rules out of the global CSS file and avoids using inline `style` attributes on elements, which should be removed.
- **Character Encoding:** UTF-8.
- **Accessibility:** Ensure images have `alt` tags and instructions use ordered lists (`<ol>`).
- **Navigation:** Keep the navigation clean and simple with the same two "return to recipes" and "Murray's homepage" links.

## 📂 File Structure
- All recipe HTML files, the `cooking.css` file, and the `images` directory should reside at the same level.
- Example: `/recipes/carrot-soup.html`, `/recipes/cooking.css`, `/recipes/images/carrot-soup.jpg`

## 📋 Transformation Rules
1. **Schema Mapping:** - `fn` (item name) → `name`
   - `yield` → `recipeYield`
   - `duration` → `prepTime` / `cookTime` (Convert to ISO 8601, e.g., PT15M).
2. **Cleanup:** Remove inline `style="..."` attributes and deprecated tags (e.g., `<font>`). Replace presentational `<br />` tags with appropriate CSS margins. The self-closing slash in tags like `<br />` or `<img ... />` is optional in HTML5; you may remove it for consistency.
3. **Paths:** Update all internal links to remove the `.xhtml` extension if necessary. Also, the image paths were tied to a top (parent) level images directory, whereas now you should see them in an images sub-directory. Verify and fix those paths.
4. **Colors:** The pages' backgrounds had colors chosen to match the theme of the recipe: a cucumber soup was light green, whereas a carrot soup would be orange. Choose new colors for each recipe based on your own decision-making process, making sure that they are light enough so as not to impede readability.

## ✍️ Editorial Guidelines (The "Cleanup")
- **Tone:** These recipes were meant to represent my personality and excitement of sharing. I love to teach and to show people how things work, so want to be as educational as possible while also being to-the-point. (I hate authors who write endlessly long articles about a recipe just to strech out ad space!) If you see that I'm trying to teach something, help me make sure it's been taught clearly and is not distracting.
- **Sections:** Sections, in order, should be
  - Title
  - Image (optional)
  - Abstract
  - Description or Commentary (This section may be completely omitted if there's no original content)
  - Ingredients
  - "Before we cook" (an optional paragraph or two about important considerations, watch-outs, hints, etc.) THIS SECTION MAY BE OMITTED IF THERE'S NOTHING THAT REALLY CAN'T FIT INTO THE STEP-BY-STEP INSTRUCTIONS.
  - Step-by-step instructions (enumerated cooking instructions, which may include some duplication or notes tying to the previous section)
  - Notes (optional) If there are any additional notes that qualify as a quick "side-bar comment" rather than an important cooking consideration.
  - AI Notes: create a section at the very bottom where you can put anything I should review. This section will be wrapped in `<div class="ai-notes">...</div>`. The global `cooking.css` file will contain a rule (`.ai-notes { display: none; }`) to hide these notes by default. You can make them visible for review by temporarily changing this style in your browser's developer tools.
- **Formatting:** - Use "tbsp" for tablespoon and "tsp" for teaspoon.
  - Ingredients should be listed in the order they are used in the instructions.
  - Units should be consistent. There shouldn't be decimal (e.g. 1.5 tbsp) measurements next to fractional (e.g. 1 1/2 cups) measurements.
  - Sections do not need titles, with the exception of "Ingredients" and "Instructions" (or a similar heading like "Method"), which should have `<h2>` headings.
  - For readability of the code, wrap paragraph text at 120 columns.
- **Validation:** 
  - Flag any recipes where an ingredient is listed but never mentioned in the "Method" section. Also check to see if any critical information appears to be missing. (For example, oven temperature.) If missing, do some research to add the missing information but tag that addition with a written note that this was adadd by the editorial AI and needs to be validated.
  - Check to see if there are any cross-reference links that should be added. For example, the Krab Souffle is a special application of the basic souffle recipe, so they should be aware of each other.