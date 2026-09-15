---
name: html-media-design
description: "Create posters, feature graphics, announcement images, social cards, promotional headers, and other designed raster media as editable HTML/CSS rendered in a browser. Use when exact typography, brand consistency, reusable layout, or platform dimensions matter. Use image generation only for visual ingredients; do not use ImageMagick or similar raster tools for creative composition."
---

# HTML Media Design

Build designed media from an editable HTML/CSS source, render it in a real browser, and export the approved canvas at its exact target dimensions.

## Choose the production method

- Use HTML/CSS for final typography, layout, spacing, logos, screenshots, charts, badges, frames, and geometric motifs.
- Use the environment's available image-generation capability only when the work benefits from an original background, illustration, texture, or other raster ingredient. When such a capability is available, generate that ingredient without final copy or exact UI, then place it in the HTML composition.
- Reuse exact supplied or canonical brand assets. Do not ask image generation to redraw a logo, screenshot, interface, or wordmark.
- Do not use ImageMagick, PIL, or another raster compositor to design the layout or render text. They may be used only for mechanical validation or delivery operations such as inspecting dimensions, checking opacity and color space, lossless cropping, format conversion, or compression when the browser export cannot satisfy a platform constraint directly.
- Skip image generation when CSS gradients, shapes, shadows, or existing imagery can produce the intended result cleanly.

## Establish the design

Before composing, identify the destination, exact pixel dimensions, safe areas, required copy, factual claims, and available brand references. Inspect an existing brand template when one applies. Preserve recognizable visual language across surfaces while allowing each surface to have a layout suited to its purpose.

Treat platform requirements as constraints, not decoration. Do not invent product features, interface states, metrics, testimonials, awards, or promotional claims. Prefer one clear message and one supporting visual idea over a collage.

## Compose in HTML

Create a self-contained HTML source with a fixed-size canvas matching the requested output. Keep reusable design values as CSS custom properties for color, typography, spacing, radii, and shadows. Use semantic structure where practical, local or bundled assets, and deterministic line breaks when headline wrapping is part of the design.

The HTML file is the canonical editable source. Keep text as text and structural motifs as HTML/CSS rather than flattening them prematurely. Avoid remote runtime dependencies that could make a later render drift or fail.

## Render and iterate

Render the HTML through the environment's available real-browser or browser-equivalent workflow at the target dimensions; do not depend on a particular browser vendor. Inspect the actual render rather than approving from source code alone. Iterate until the composition has:

- clear hierarchy at normal and thumbnail size;
- balanced spacing and deliberate alignment;
- legible copy with no accidental wrapping or clipping;
- faithful colors, logos, screenshots, and geometry;
- adequate contrast and safe margins;
- no browser chrome, scrollbars, loading artifacts, or unintended transparency.

Do not present the first technically valid render as final when visible design issues remain. Record the reason for each meaningful iteration in concise progress updates.

## Export and verify

Capture only the canvas, not the surrounding browser viewport. If the browser's clipped capture applies an incorrect device scale, capture the full browser render and make one mechanical crop using the measured canvas bounds; do not redesign through the raster tool.

Verify the exported file's exact dimensions, format, opacity or alpha requirement, color space, and size limit. Visually inspect the final exported file again at full size and thumbnail size. Return both the editable HTML source and the final raster asset unless the user requests only one.

Uploading, publishing, replacing a live asset, or deleting an existing asset remains a separate action requiring the user's applicable approval.
