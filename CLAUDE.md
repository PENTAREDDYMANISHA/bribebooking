# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Single-file static bridal photography booking website. Everything â€” HTML, CSS, and JavaScript â€” lives in one file: `index.html`. There is no build step, no package manager, and no framework.

## Serving Locally

No Python or Node.js is available in this environment. Use PowerShell's built-in .NET HTTP listener:

```powershell
$listener = New-Object System.Net.HttpListener
$listener.Prefixes.Add("http://localhost:8080/")
$listener.Start()
Start-Process "http://localhost:8080/"
while ($listener.IsListening) {
    $ctx = $listener.GetContext()
    $bytes = [System.IO.File]::ReadAllBytes("C:\Users\ManishaPentareddy\Downloads\BRIBEBOOKING\index.html")
    $ctx.Response.ContentType = "text/html; charset=utf-8"
    $ctx.Response.OutputStream.Write($bytes, 0, $bytes.Length)
    $ctx.Response.OutputStream.Close()
}
```

## Architecture

`index.html` is organized top-to-bottom as one linear document:

1. **`<head>`** â€” Google Fonts (`Playfair Display`, `Lato`), all CSS in a single `<style>` block
2. **`<body>`** â€” seven sections in DOM order: Nav â†’ Hero â†’ About â†’ Packages â†’ Gallery â†’ Booking Form â†’ Contact/Footer
3. **`<script>`** at end of `<body>` â€” all JavaScript inline (no modules, no libraries)

### CSS

- Design tokens defined as CSS custom properties on `:root` (`--blush-*`, `--gold`, `--gold-dark`, `--text-*`, `--white`, `--nav-h`)
- Single responsive breakpoint at `768px`
- Scroll anchoring via `scroll-margin-top: var(--nav-h)` on each section

### JavaScript

Three responsibilities, all in one `<script>` block:
- **Nav**: scroll-based class toggle (`scrolled`), mobile hamburger open/close
- **Packages**: `choosePackage(name)` â€” scrolls to `#booking` and pre-selects the Package dropdown
- **Form submission**: `fetch` POST (JSON) to `https://formsubmit.co/ajax/manisha_p@i-mxms.com`; handles three response states â€” JSON success, HTML body (FormSubmit first-time activation), and network error

### FormSubmit Activation

The FormSubmit AJAX endpoint requires one-time email confirmation. On the very first POST it returns an HTML page (not JSON). The form submission code checks `Content-Type` before calling `res.json()` and shows an activation prompt if HTML is returned. Once confirmed via the link in the inbox, subsequent submissions return JSON normally.
