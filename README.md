# Bloom & Veil — Bridal Photography

A single-page bridal photography booking website for **Bloom & Veil**, a boutique studio specialising in elegant wedding and bridal portrait sessions. Visitors can browse packages, view the gallery, and submit a booking enquiry — all from one beautifully styled page.

## Live Site
[View live site](https://pentareddymanisha.github.io/bridebooking/)

## Tech Stack
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-222222?style=for-the-badge&logo=github&logoColor=white)

## File Structure

| File / Folder | Description |
|---|---|
| `index.html` | Entire site — HTML, CSS, and JavaScript in one file |
| `.github/workflows/deploy.yml` | GitHub Actions workflow that deploys to GitHub Pages on every push to `main` |
| `CLAUDE.md` | Instructions for the Claude Code AI assistant |
| `README.md` | This file |

## About the Project

Bloom & Veil is a static, single-file website built without any framework, build tool, or package manager. All styles live in a `<style>` block in `<head>`, and all interactivity is handled by a small inline `<script>` at the end of `<body>`. The design uses CSS custom properties (design tokens) for a consistent blush-and-gold colour palette, and a single `768px` breakpoint for responsive layout.

The site covers seven sections in order: navigation, hero, about, packages, gallery, booking form, and contact/footer. The booking form submits via the [FormSubmit](https://formsubmit.co) AJAX endpoint — no backend required. The first submission triggers a one-time email confirmation from FormSubmit; subsequent submissions return JSON and display an on-page success message.

Package cards include a "Book This Package" button that scrolls the user directly to the booking form and pre-selects the corresponding package in the dropdown, creating a smooth end-to-end booking flow.

## How to Use

### Running locally

No Node.js or Python needed. Use PowerShell's built-in .NET HTTP listener:

```powershell
$listener = New-Object System.Net.HttpListener
$listener.Prefixes.Add("http://localhost:8080/")
$listener.Start()
Start-Process "http://localhost:8080/"
while ($listener.IsListening) {
    $ctx = $listener.GetContext()
    $bytes = [System.IO.File]::ReadAllBytes("index.html")
    $ctx.Response.ContentType = "text/html; charset=utf-8"
    $ctx.Response.OutputStream.Write($bytes, 0, $bytes.Length)
    $ctx.Response.OutputStream.Close()
}
```

Or simply open `index.html` directly in a browser.

### Booking a session

1. Browse the **Packages** section and click **Book This Package** on your preferred option.
2. The page scrolls to the **Booking** form with that package pre-selected.
3. Fill in your name, email, preferred date, and any message, then click **Send Enquiry**.
4. You will see a confirmation message on the page once the enquiry is submitted.

## License
MIT