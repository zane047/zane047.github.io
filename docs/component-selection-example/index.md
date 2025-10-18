<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Your Document Title</title>
  <meta name="description" content="Describe this page for SEO." />
  <style>
    :root {
      --bg: #ffffff; --fg: #0f172a;
      --muted: #475569; --border: #e2e8f0; --link: #2563eb;
      --code-bg: #0b1020; --code-fg: #e5e7eb;
      --maxw: 820px;
    }
    * { box-sizing: border-box; }
    html,body { margin:0; padding:0; }
    body {
      font-family: system-ui, -apple-system, Segoe UI, Roboto, Inter, Arial, sans-serif;
      line-height: 1.6; color: var(--fg); background: var(--bg);
    }
    header, main, footer { width: 100%; }
    .container { max-width: var(--maxw); margin: 0 auto; padding: 2rem 1rem; }
    header h1 { margin: 0 0 0.25rem; line-height: 1.2; }
    header p { margin: 0; color: var(--muted); }
    h1, h2, h3, h4 { line-height: 1.25; margin: 2rem 0 0.75rem; }
    p { margin: 1rem 0; }
    ul, ol { padding-left: 1.5rem; margin: 1rem 0; }
    li + li { margin-top: 0.25rem; }
    a { color: var(--link); text-decoration: none; }
    a:hover { text-decoration: underline; }
    hr { border: 0; border-top: 1px solid var(--border); margin: 2rem 0; }
    blockquote {
      margin: 1.25rem 0; padding: 0.75rem 1rem;
      border-left: 4px solid var(--border); background: #f8fafc;
    }
    img, video { max-width: 100%; height: auto; }
    figure { margin: 1.25rem 0; }
    figcaption { color: var(--muted); font-size: 0.925rem; margin-top: 0.25rem; }
    table { width:100%; border-collapse: collapse; margin: 1.25rem 0; }
    th, td { border:1px solid var(--border); padding: 0.625rem; text-align:left; }
    thead th { background:#f8fafc; }
    code, pre { font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, monospace; }
    pre {
      background: var(--code-bg); color: var(--code-fg); padding: 1rem;
      border-radius: 8px; overflow:auto; margin: 1rem 0;
    }
    .lead { font-size: 1.125rem; color: var(--muted); }
    .small { font-size: 0.925rem; color: var(--muted); }
    footer { border-top: 1px solid var(--border); }
    @media print {
      .container { padding: 0; }
      a[href^="http"]:after { content: " (" attr(href) ")"; font-size: 0.85em; }
    }
  </style>
</head>
<body>
  <header>
    <div class="container">
      <h1>Your Document Title</h1>
      <p class="lead">Optional subtitle or summary goes here.</p>
    </div>
  </header>

  <main>
    <div class="container">
      <!-- ======= Start pasting your content below ======= -->
      <h2>Section Heading</h2>
      <p>Paragraph text from your Google Doc. You can keep <strong>bold</strong>, <em>italic</em>, and <a href="#">links</a>.</p>

      <h3>Bulleted list</h3>
      <ul>
        <li>First point</li>
        <li>Second point</li>
        <li>Third point</li>
      </ul>

      <h3>Numbered steps</h3>
      <ol>
        <li>Do this</li>
        <li>Then this</li>
        <li>Finally this</li>
      </ol>

      <h3>Image example</h3>
      <figure>
        <img src="images/your-image.png" alt="Describe the image">
        <figcaption>Optional caption for accessibility and context.</figcaption>
      </figure>

      <h3>Table example</h3>
      <table>
        <thead>
          <tr><th>Column A</th><th>Column B</th><th>Column C</th></tr>
        </thead>
        <tbody>
          <tr><td>Row 1</td><td>Data</td><td>More</td></tr>
          <tr><td>Row 2</td><td>Data</td><td>More</td></tr>
        </tbody>
      </table>

      <h3>Code block</h3>
      <pre><code>// Example code snippet
function hello() {
  console.log("Hello world");
}
</code></pre>
      <!-- ======= End paste area ======= -->
    </div>
  </main>

  <footer>
    <div class="container">
      <p class="small">© <span id="year"></span> Your Name or Org</p>
    </div>
  </footer>

  <script>
    document.getElementById("year").textContent = new Date().getFullYear();
  </script>
</body>
</html>
