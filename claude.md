# Claude Instructions for Digital Garden Repository

## Repository Overview

This is a Jekyll-based digital garden for personal knowledge management. It uses a static site generator to create interconnected notes with automatic backlinks and link previews.

## Project Structure

```
digital-garden/
├── _notes/           # All note content goes here (Markdown files)
├── _config.yml       # Jekyll configuration
├── _layouts/         # HTML templates for rendering
├── _includes/        # Reusable HTML components
├── _plugins/         # Custom Jekyll plugins (bidirectional links)
├── _sass/            # Styling
├── assets/           # Images, media, CSS, JS
└── _pages/           # Static pages (non-note content)
```

## Working with Notes

### Note Files
- All notes are stored as Markdown files in the `_notes/` directory
- Notes can be organized in subdirectories within `_notes/`
- Each note should have YAML front matter with at minimum a `title` field:

```markdown
---
title: Note Title
---

# Content here
```

### Link Syntax
Notes use Roam-style double bracket notation for internal linking:

- `[[note-title]]` - Links using the note's title
- `[[filename]]` - Links using the filename (without .md extension)
- `[[note-title|custom label]]` - Links with custom display text

The Jekyll plugin automatically creates bidirectional links between notes.

### Creating New Notes
1. Create a new `.md` file in `_notes/` (or a subdirectory)
2. Add YAML front matter with a title
3. Write content using standard Markdown
4. Use `[[double-bracket]]` syntax to link to other notes

### Editing Existing Notes
- Read the note file from `_notes/` first
- Make changes while preserving the YAML front matter
- Maintain the link syntax format when modifying links

## Configuration

Key settings in `_config.yml`:
- `title`: Site title (currently "My digital garden")
- `baseurl`: Base URL for deployment
- `use_html_extension`: Set to true if host requires .html extensions
- `open_external_links_in_new_tab`: Controls external link behavior
- `embed_tweets`: Enable/disable Twitter embeds

## Development

- The site uses Jekyll for static site generation
- Ruby dependencies are managed via Bundler (see Gemfile)
- Custom plugin: `bidirectional_links_generator.rb` creates the notes graph
- The site can be deployed to Netlify or built locally with Jekyll

## Important Guidelines

### Style Preferences
- **DO NOT use emojis** in any text, documentation, or notes
- Keep content professional and text-based
- Use clear, concise language

### File Operations
- Always read existing note files before editing
- Preserve YAML front matter structure
- Maintain consistent Markdown formatting
- Don't create unnecessary files

### Link Management
- Use double-bracket syntax for internal note links
- Verify linked notes exist or will be created
- Use descriptive link text when using custom labels

## Testing Changes

To preview changes locally:
1. Ensure Ruby and Bundler are installed
2. Run `bundle install` to install dependencies
3. Run `bundle exec jekyll serve` to start local server
4. View site at http://localhost:4000

## Deployment

The site is configured for deployment via Netlify (see netlify.toml).
The main branch is deployed automatically on push.
