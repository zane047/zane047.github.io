<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Schematic Overview</title>

  <!-- Optional: MathJax (since the site path mentions it) -->
  <script>
    window.MathJax = { tex: { inlineMath: [['$', '$'], ['\\(', '\\)']] } };
  </script>
  <script defer src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>

  <style>
    :root {
      --ink: #1f2937;      /* slate-800 */
      --muted: #6b7280;    /* gray-500 */
      --accent: #2563eb;   /* blue-600 */
      --bg: #ffffff;
      --card: #fafafa;
      --border: #e5e7eb;   /* gray-200 */
    }
    html, body {
      margin: 0;
      background: var(--bg);
      color: var(--ink);
      font: 16px/1.6 system-ui, -apple-system, Segoe UI, Roboto, "Helvetica Neue", Arial, "Noto Sans", "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
    }
    .container {
      max-width: 980px;
      margin: 48px auto 96px;
      padding: 0 20px;
    }
    h1, h2 {
      line-height: 1.25;
      margin: 0 0 14px;
      font-weight: 700;
    }
    h1 { font-size: 2.125rem; margin-bottom: 12px; }
    h2 { font-size: 1.375rem; margin-top: 40px; }
    p {
      margin: 0 0 14px;
    }
    .lead {
      font-size: 1.05rem;
      color: var(--ink);
    }
    .figure {
      margin: 28px 0;
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: 6px;
      box-shadow: 0 1px 0 rgba(0,0,0,0.03);
      overflow: hidden;
    }
    .figure .frame {
      background: #fff;
      padding: 10px;
      border-bottom: 1px solid var(--border);
    }
    .figure img {
      width: 100%;
      height: auto;
      display: block;
      border: 1px solid var(--border);
    }
    .caption {
      font-size: 0.95rem;
      color: var(--muted);
      padding: 10px 14px 14px;
    }
    .caption strong { color: var(--muted); }
    .resources {
      margin-top: 8px;
      background: transparent;
    }
    .resources p {
      font-size: 1.02rem;
    }
    a {
      color: var(--accent);
      text-decoration: none;
      border-bottom: 1px solid rgba(37,99,235,0.35);
      padding-bottom: 1px;
    }
    a:hover { border-bottom-color: currentColor; }
    .mono { font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, "Liberation Mono", monospace; }
    footer {
      margin-top: 64px;
      color: var(--muted);
      font-size: 0.9rem;
    }
  </style>
</head>
<body>
  <main class="container">
    <h1>Overview</h1>
    <p class="lead">
      This schematic is designed to support … (highlight functionality, power, and controller).
    </p>

    <section class="figure">
      <div class="frame">
        <!-- Replace the src with your image path -->
        <img src="./assets/schematic.png" alt="Example KiCad schematic" />
      </div>
      <p class="caption">
        <strong>Figure ##:</strong> Showing a example schematic.
      </p>
    </section>

    <section class="resources">
      <h2>Resouces</h2> <!-- kept the original misspelling to match the screenshot -->
      <p>
        The schematic as a PDF download is available
        <a href="./assets/schematic.pdf" target="_blank" rel="noopener">here</a>,
        and the Zip folder of the project
        <a href="./assets/project.zip" target="_blank" rel="noopener">here</a>.
      </p>
    </section>

    <footer>
      <p>
        Built for GitHub Pages. Edit <span class="mono">index.html</span> in your repo
        to update links and text. Optional MathJax is enabled for equations like
        $V_{out} = 10\\,\\mathrm{mV}/^{\\circ}\\!\\mathrm{C} \\times T$.
      </p>
    </footer>
  </main>
</body>
</html>
