---
name: scrape-web
description: Fetch a web page and extract structured data including metadata, heading hierarchy, text content, links, and images. Outputs clean markdown. Use for content extraction, research, or competitive analysis.
---

# Web Scraper

Fetch and extract structured data from the URL provided by the user.

## Process

1. Fetch the page content
2. Parse and organize into structured sections
3. Present results in clean markdown

## Extract the Following

### Metadata
- Page title
- Meta description
- Meta keywords
- Author
- Open Graph tags (og:title, og:description, og:image, og:type)
- Canonical URL

### Content Structure
- Heading hierarchy (H1 through H4, indented to show structure)
- Main text content (paragraphs, stripped of boilerplate nav/footer)

### Links
- Internal links (same domain) — anchor text + URL
- External links — anchor text + URL
- Limit to first 50 links if there are many

### Images
- Image URLs with alt text
- Limit to first 20 images if there are many

### Technical Details
- Response status code
- Content-Type header
- Any notable response headers (caching, security, etc.)

## Error Handling

- If the URL is unreachable, report the error clearly
- If the page requires authentication, note what type (401, login form, etc.)
- If the content is mostly JavaScript-rendered, note that static fetching may miss dynamic content

## Output Format

Present everything in well-organized markdown with clear section headers. At the end, offer to save the extracted data to a file if the user wants.
