---
description: Scrape and extract structured data from a web page
argument-hint: <url>
allowed-tools: [WebFetch, Read, Write]
---

# Web Scraper

Fetch and extract structured data from the URL provided: $ARGUMENTS

## Process

1. Fetch the page content using WebFetch
2. Parse and organize the content into structured sections
3. Present the results in clean markdown format

## Extract the following

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

## Error handling

- If the URL is unreachable, report the error clearly
- If the page requires authentication, note what type (401, login form, etc.)
- If the content is mostly JavaScript-rendered, note that static fetching may miss dynamic content

## Output format

Present everything in well-organized markdown with clear section headers. At the end, offer: "Would you like me to save this data to a file? If so, suggest a filename or I'll use `scraped-[domain].md`."
