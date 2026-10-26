<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Microsoft Word Simulator</title>
  <link href="https://cdn.jsdelivr.net/gh/rastikerdar/vazirmatn@v33.003/Vazirmatn-font-face.css" rel="stylesheet" type="text/css" />
  
  <style>
    :root {
      --word-blue: #2b579a;
      --word-blue-dark: #1b3d6d;
      --ribbon-bg: #f3f2f1;
      --border-color: #d2d0ce;
      --hover-bg: #e1dfdd;
      --active-bg: #c8c6c4;
      --page-shadow: 0 4px 15px rgba(0, 0, 0, 0.15);
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Segoe UI', Tahoma, Vazirmatn, Arial, sans-serif;
      user-select: none;
    }

    body {
      background-color: #edebe9;
      display: flex;
      flex-direction: column;
      height: 100vh;
      overflow: hidden;
      direction: ltr;
    }

    .title-bar {
      background-color: var(--word-blue);
      color: white;
      height: 38px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 0 12px;
      font-size: 13px;
    }
    .title-text {
      font-weight: 600;
      letter-spacing: 0.5px;
    }

    .tabs-bar {
      background-color: var(--word-blue);
      display: flex;
      align-items: flex-end;
      padding-left: 8px;
      height: 34px;
    }
    .tab-btn {
      background: transparent;
      border: none;
      color: #ffffff;
      padding: 7px 16px;
      font-size: 12.5px;
      cursor: pointer;
      border-top-left-radius: 4px;
      border-top-right-radius: 4px;
      outline: none;
    }
    .tab-btn:hover {
      background-color: rgba(255, 255, 255, 0.15);
    }
    .tab-btn.file-btn {
      background-color: var(--word-blue-dark);
      font-weight: 600;
      padding: 7px 18px;
    }
    .tab-btn.file-btn:hover {
      background-color: #122b4f;
    }
    .tab-btn.active {
      background-color: var(--ribbon-bg);
      color: var(--word-blue);
      font-weight: 600;
    }

    .ribbon-container {
      background-color: var(--ribbon-bg);
      border-bottom: 1px solid var(--border-color);
      min-height: 98px;
      display: flex;
      align-items: stretch;
      padding: 4px 6px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.04);
      overflow-x: auto;
    }
    .tab-panel {
      display: none;
      width: 100%;
      height: 100%;
    }
    .tab-panel.active {
      display: flex;
      align-items: stretch;
      gap: 6px;
    }

    .ribbon-group {
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      border-right: 1px solid #e1dfdd;
      padding: 0 6px 2px 6px;
      min-width: max-content;
    }
    .group-content {
      display: flex;
      align-items: center;
      gap: 3px;
      flex: 1;
    }
    .group-title {
      font-size: 10px;
      color: #605e5c;
      text-align: center;
      padding-top: 2px;
      border-top: 1px solid #f0f0f0;
    }

    .ribbon-btn {
      background: transparent;
      border: 1px solid transparent;
      border-radius: 3px;
      padding: 4px 6px;
      font-size: 12px;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      min-height: 26px;
      color: #323130;
      outline: none;
    }
    .ribbon-btn:hover {
      background-color: var(--hover-bg);
      border-color: #c8c6c4;
    }
    .ribbon-btn:active, .ribbon-btn.active {
      background-color: var(--active-bg);
    }
    .ribbon-btn-large {
      flex-direction: column;
      padding: 6px 8px;
      gap: 4px;
      font-size: 11px;
    }
    .ribbon-btn-large .icon {
      font-size: 20px;
    }
    .ribbon-btn-row {
      display: flex;
      align-items: center;
      gap: 2px;
    }
    .select-tool {
      height: 24px;
      border: 1px solid var(--border-color);
      border-radius: 2px;
      font-size: 11.5px;
      padding: 0 4px;
      background: white;
      outline: none;
    }

    .styles-gallery {
      display: flex;
      gap: 4px;
      overflow-x: auto;
      max-width: 320px;
      padding: 2px 0;
    }
    .style-tile {
      border: 1px solid #e1dfdd;
      background: white;
      border-radius: 3px;
      padding: 4px 8px;
      min-width: 68px;
      text-align: center;
      cursor: pointer;
      display: flex;
      flex-direction: column;
      justify-content: center;
    }
    .style-tile:hover {
      border-color: var(--word-blue);
      background-color: #f8f9fa;
    }
    .style-preview {
      font-size: 13px;
      margin-bottom: 2px;
    }
    .style-name {
      font-size: 9.5px;
      color: #605e5c;
    }

    .table-picker-popup {
      display: none;
      position: absolute;
      background: white;
      border: 1px solid var(--border-color);
      box-shadow: 0 4px 10px rgba(0,0,0,0.15);
      padding: 8px;
      z-index: 100;
      top: 130px;
    }
    .grid-container {
      display: grid;
      grid-template-columns: repeat(5, 18px);
      gap: 3px;
      margin-bottom: 4px;
    }
    .grid-cell {
      width: 18px;
      height: 18px;
      border: 1px solid #b8b8b8;
      cursor: pointer;
    }
    .grid-cell.highlight {
      background-color: #c7d8ed;
      border-color: var(--word-blue);
    }
    .grid-label {
      font-size: 11px;
      text-align: center;
      color: #605e5c;
    }

    .workspace {
      flex: 1;
      overflow: auto;
      display: flex;
      justify-content: center;
      padding: 30px 15px;
      background-color: #edebe9;
    }
    .page-a4 {
      position: relative;
      background: white;
      width: 210mm;
      min-height: 297mm;
      padding: 25.4mm;
      box-shadow: var(--page-shadow);
      direction: rtl;
      outline: none;
      font-size: 14pt;
      line-height: 1.6;
      font-family: 'Vazirmatn', Tahoma, sans-serif;
      user-select: text;
    }
    .page-a4 p {
      margin-bottom: 8px;
    }
    .page-a4 table {
      width: 100%;
      border-collapse: collapse;
      margin: 10px 0;
    }
    .page-a4 table, .page-a4 th, .page-a4 td {
      border: 1px solid #666;
    }
    .page-a4 td, .page-a4 th {
      padding: 6px 10px;
      min-width: 20px;
    }

    .status-bar {
      background-color: #f3f2f1;
      border-top: 1px solid var(--border-color);
      height: 24px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 0 16px;
      font-size: 11px;
      color: #605e5c;
    }

    .backstage-overlay {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background: white;
      z-index: 200;
      flex-direction: row;
    }
    .backstage-sidebar {
      width: 220px;
      background: var(--word-blue);
      color: white;
      padding-top: 20px;
      display: flex;
      flex-direction: column;
    }
    .backstage-item {
      padding: 12px 24px;
      font-size: 14px;
      cursor: pointer;
      display: flex;
      align-items: center;
      gap: 12px;
    }
    .backstage-item:hover {
      background: rgba(255,255,255,0.12);
    }
    .backstage-back-btn {
      width: 38px;
      height: 38px;
      border-radius: 50%;
      border: 1px solid rgba(255,255,255,0.4);
      margin: 0 0 20px 20px;
      background: transparent;
      color: white;
      font-size: 18px;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    .backstage-content {
      flex: 1;
      padding: 40px;
      overflow-y: auto;
    }

    .page-a4 { transition: width .2s ease, min-height .2s ease; }
    .page-a4 h1 { color:#2b579a; font-size:24pt; }
    .page-a4 h2 { font-size:19pt; }
    .page-a4 img { max-width:100%; }
    .page-a4 [data-comment] { background:#fff2cc; border-bottom:2px dotted #b8860b; }
    .tabs-bar { overflow-x:auto; flex-shrink:0; }
    .ribbon-container { flex-shrink:0; }
    .workspace { min-height:0; }
    .ruler { display:none; height:18px; background:repeating-linear-gradient(90deg,#aaa 0,#aaa 1px,transparent 1px,transparent 10px); border-bottom:1px solid #aaa; margin:0 auto; width:min(210mm,95%); }
    .ruler.visible { display:block; }
    .navigation-pane { display:none; position:fixed; z-index:150; top:170px; left:12px; width:260px; max-height:60vh; overflow:auto; background:#fff; border:1px solid #aaa; padding:12px; box-shadow:0 3px 12px #0002; }
    .navigation-pane.visible { display:block; }
    .focus-mode .title-bar, .focus-mode .tabs-bar, .focus-mode .ribbon-container, .focus-mode .status-bar { display:none; }
    .focus-mode .workspace { padding:20px; }
    @media print { body { height:auto; overflow:visible; background:white; } .title-bar,.tabs-bar,.ribbon-container,.status-bar,.backstage-overlay,.ruler,.navigation-pane {display:none!important} .workspace{display:block;padding:0;overflow:visible;background:white} .page-a4{box-shadow:none;margin:0;width:auto;min-height:0;padding:20mm;border:none!important} }
    @media(max-width:700px) { .page-a4 { width:100%; min-height:100%; padding:12mm; } .workspace { padding:10px 4px; } .backstage-sidebar {width:150px} .backstage-content {padding:18px} }

  </style>
</head>
<body>

  <!-- نوار عنوان -->
  <div class="title-bar">
    <div>
      <span>💾</span>
      <span style="margin-left: 8px;">↩️</span>
      <span style="margin-left: 4px;">↪️</span>
    </div>
    <div class="title-text">Document1 - Word Simulator</div>
    <div>— ▢ ✕</div>
  </div>

  <!-- نوار زبانه‌ها (Tabs) -->
  <div class="tabs-bar">
    <button class="tab-btn file-btn" id="btn-file">File</button>
    <button class="tab-btn active" data-tab="home">Home</button>
    <button class="tab-btn" data-tab="insert">Insert</button>
    <button class="tab-btn" data-tab="design">Design</button>
    <button class="tab-btn" data-tab="layout">Layout</button>
    <button class="tab-btn" data-tab="references">References</button>
    <button class="tab-btn" data-tab="mailings">Mailings</button>
    <button class="tab-btn" data-tab="review">Review</button>
    <button class="tab-btn" data-tab="view">View</button>
  </div>

  <!-- محفظه ابزارهای ریبون -->
  <div class="ribbon-container">

    <!-- تب HOME -->
    <div class="tab-panel active" id="tab-home">
      <!-- Clipboard -->
      <div class="ribbon-group">
        <div class="group-content">
          <button class="ribbon-btn ribbon-btn-large" onclick="execCmd('paste')">
            <span class="icon">📋</span>
            <span>Paste</span>
          </button>
          <div style="display:flex; flex-direction:column; gap:2px;">
            <button class="ribbon-btn" title="Cut" onclick="execCmd('cut')">✂️ Cut</button>
            <button class="ribbon-btn" title="Copy" onclick="execCmd('copy')">📄 Copy</button>
            <button class="ribbon-btn" title="Format Painter" onclick="applyFormatPainter()">🖌️ Format Painter</button>
          </div>
        </div>
        <div class="group-title">Clipboard</div>
      </div>

      <!-- Font -->
      <div class="ribbon-group">
        <div class="group-content" style="flex-direction: column; align-items: flex-start; gap: 4px;">
          <div class="ribbon-btn-row">
            <select class="select-tool" onchange="execCmd('fontName', this.value)">
              <option value="Vazirmatn">Vazirmatn</option>
              <option value="Tahoma">Tahoma</option>
              <option value="Arial">Arial</option>
              <option value="Times New Roman">Times New Roman</option>
            </select>
            <select class="select-tool" style="width: 48px;" onchange="execCmd('fontSize', this.value)">
              <option value="2">10</option>
              <option value="3">12</option>
              <option value="4" selected>14</option>
              <option value="5">18</option>
              <option value="6">24</option>
              <option value="7">36</option>
            </select>
            <button class="ribbon-btn" title="Clear All Formatting" onclick="execCmd('removeFormat')">🧹</button>
          </div>
          <div class="ribbon-btn-row">
            <button class="ribbon-btn" title="Bold (Ctrl+B)" onclick="execCmd('bold')"><b>B</b></button>
            <button class="ribbon-btn" title="Italic (Ctrl+I)" onclick="execCmd('italic')"><i>I</i></button>
            <button class="ribbon-btn" title="Underline (Ctrl+U)" onclick="execCmd('underline')"><u>U</u></button>
            <button class="ribbon-btn" title="Strikethrough" onclick="execCmd('strikeThrough')"><s>S</s></button>
            <input type="color" title="Font Color" onchange="execCmd('foreColor', this.value)" style="width:22px; height:22px; padding:0; border:none; cursor:pointer;" value="#000000">
            <input type="color" title="Highlight Color" onchange="execCmd('hiliteColor', this.value)" style="width:22px; height:22px; padding:0; border:none; cursor:pointer;" value="#ffff00">
          </div>
        </div>
        <div class="group-title">Font</div>
      </div>

      <!-- Paragraph -->
      <div class="ribbon-group">
        <div class="group-content" style="flex-direction: column; align-items: flex-start; gap: 4px;">
          <div class="ribbon-btn-row">
            <button class="ribbon-btn" title="Bullets" onclick="execCmd('insertUnorderedList')">•≡</button>
            <button class="ribbon-btn" title="Numbering" onclick="execCmd('insertOrderedList')">1≡</button>
            <button class="ribbon-btn" title="Decrease Indent" onclick="execCmd('outdent')">⇤</button>
            <button class="ribbon-btn" title="Increase Indent" onclick="execCmd('indent')">⇥</button>
            <button class="ribbon-btn" title="LTR" onclick="setDocDirection('ltr')">LTR</button>
            <button class="ribbon-btn" title="RTL" onclick="setDocDirection('rtl')">RTL</button>
          </div>
          <div class="ribbon-btn-row">
            <button class="ribbon-btn" title="Align Left" onclick="execCmd('justifyLeft')">⫷</button>
            <button class="ribbon-btn" title="Center" onclick="execCmd('justifyCenter')">≡</button>
            <button class="ribbon-btn" title="Align Right" onclick="execCmd('justifyRight')">⫸</button>
            <button class="ribbon-btn" title="Justify" onclick="execCmd('justifyFull')">≣</button>
          </div>
        </div>
        <div class="group-title">Paragraph</div>
      </div>

      <!-- Styles -->
      <div class="ribbon-group">
        <div class="group-content">
          <div class="styles-gallery">
            <div class="style-tile" onclick="applyStyle('p')">
              <span class="style-preview">AaBbCc</span>
              <span class="style-name">Normal</span>
            </div>
            <div class="style-tile" onclick="applyStyle('h1')">
              <span class="style-preview" style="color:#2b579a; font-weight:bold;">AaBb</span>
              <span class="style-name">Heading 1</span>
            </div>
            <div class="style-tile" onclick="applyStyle('h2')">
              <span class="style-preview" style="color:#1b3d6d;">AaBb</span>
              <span class="style-name">Heading 2</span>
            </div>
            <div class="style-tile" onclick="applyStyle('title')">
              <span class="style-preview" style="font-size:16px; font-weight:bold;">Title</span>
              <span class="style-name">Title</span>
            </div>
          </div>
        </div>
        <div class="group-title">Styles</div>
      </div>

      <!-- Editing -->
      <div class="ribbon-group">
        <div class="group-content" style="flex-direction: column; gap: 2px;">
          <button class="ribbon-btn" onclick="openFind()">🔍 Find</button>
          <button class="ribbon-btn" onclick="openReplace()">🔄 Replace</button>
          <button class="ribbon-btn" onclick="execCmd('selectAll')">Select All</button>
        </div>
        <div class="group-title">Editing</div>
      </div>
    </div>

    <!-- تب INSERT -->
    <div class="tab-panel" id="tab-insert">
      <!-- Pages -->
      <div class="ribbon-group">
        <div class="group-content">
          <button class="ribbon-btn ribbon-btn-large" onclick="insertPageBreak()">
            <span class="icon">📃</span>
            <span>Blank Page</span>
          </button>
          <button class="ribbon-btn ribbon-btn-large" onclick="insertPageBreak()">
            <span class="icon">✂️</span>
            <span>Page Break</span>
          </button>
        </div>
        <div class="group-title">Pages</div>
      </div>

      <!-- Tables -->
      <div class="ribbon-group">
        <div class="group-content">
          <button class="ribbon-btn ribbon-btn-large" onclick="toggleTablePicker()">
            <span class="icon">田</span>
            <span>Table ▾</span>
          </button>
        </div>
        <div class="group-title">Tables</div>
      </div>

      <!-- Illustrations -->
      <div class="ribbon-group">
        <div class="group-content">
          <label class="ribbon-btn ribbon-btn-large" style="margin-bottom:0;">
            <span class="icon">🖼️</span>
            <span>Pictures</span>
            <input type="file" accept="image/*" style="display:none;" onchange="insertPicture(this)">
          </label>
          <div style="display:flex; flex-direction:column; gap:2px;">
            <button class="ribbon-btn" onclick="insertShape('rectangle')">▭ Rectangle</button>
            <button class="ribbon-btn" onclick="insertShape('circle')">◯ Circle</button>
          </div>
        </div>
        <div class="group-title">Illustrations</div>
      </div>

      <!-- Header & Footer -->
      <div class="ribbon-group">
        <div class="group-content" style="flex-direction: column; gap: 2px;">
          <button class="ribbon-btn" onclick="insertHeader()">🏷️ Header</button>
          <button class="ribbon-btn" onclick="insertFooter()">🏷️ Footer</button>
          <button class="ribbon-btn" onclick="insertPageNumber()"># Page Number</button>
        </div>
        <div class="group-title">Header & Footer</div>
      </div>

      <!-- Text & Symbols -->
      <div class="ribbon-group">
        <div class="group-content">
          <button class="ribbon-btn ribbon-btn-large" onclick="insertTextBox()">
            <span class="icon">🗚</span>
            <span>Text Box</span>
          </button>
          <div style="display:flex; flex-direction:column; gap:2px;">
            <button class="ribbon-btn" onclick="insertSymbol('©')">© Symbol</button>
            <button class="ribbon-btn" onclick="insertSymbol('∑')">∑ Math</button>
            <button class="ribbon-btn" onclick="execCmd('insertHorizontalRule')">― Line</button>
          </div>
        </div>
        <div class="group-title">Text & Symbols</div>
      </div>
    </div>

    <!-- تب DESIGN -->
    <div class="tab-panel" id="tab-design">
      <!-- Document Formatting -->
      <div class="ribbon-group">
        <div class="group-content">
          <div style="display:flex; flex-direction:column; gap:4px;">
            <div class="ribbon-btn-row">
              <span style="font-size:11px;">Theme Color:</span>
              <select class="select-tool" onchange="applyThemeColor(this.value)">
                <option value="#2b579a">Default Blue</option>
                <option value="#107c41">Emerald Green</option>
                <option value="#b4009e">Purple</option>
                <option value="#d83b01">Warm Red</option>
              </select>
            </div>
          </div>
        </div>
        <div class="group-title">Document Formatting</div>
      </div>

      <!-- Page Background -->
      <div class="ribbon-group">
        <div class="group-content">
          <button class="ribbon-btn ribbon-btn-large" onclick="setWatermark()">
            <span class="icon">🌊</span>
            <span>Watermark</span>
          </button>

          <label class="ribbon-btn ribbon-btn-large" style="margin:0; cursor:pointer;" title="Page Color">
            <span class="icon">🎨</span>
            <span>Page Color</span>
            <input type="color" value="#ffffff" onchange="setPageColor(this.value)" style="display:none;">
          </label>

          <div style="display:flex; flex-direction:column; gap:2px;">
            <button class="ribbon-btn" onclick="setPageBorder('solid')">▢ Box Border</button>
            <button class="ribbon-btn" onclick="setPageBorder('double')">▣ Double Border</button>
            <button class="ribbon-btn" onclick="setPageBorder('none')">✕ No Border</button>
          </div>
        </div>
        <div class="group-title">Page Background</div>
      </div>
    </div>


    <div class="tab-panel" id="tab-layout">
      <div class="ribbon-group"><div class="group-content" style="flex-direction:column;align-items:flex-start;gap:4px">
        <div class="ribbon-btn-row"><button class="ribbon-btn" onclick="setPageOrientation('portrait')">↕ Portrait</button><button class="ribbon-btn" onclick="setPageOrientation('landscape')">↔ Landscape</button></div>
        <div class="ribbon-btn-row"><label>Margins <select class="select-tool" onchange="setMargins(this.value)"><option value="25.4">Normal</option><option value="12.7">Narrow</option><option value="38.1">Wide</option></select></label>
        <label>Size <select class="select-tool" onchange="setPaperSize(this.value)"><option value="A4">A4</option><option value="Letter">Letter</option><option value="A3">A3</option></select></label></div>
      </div><div class="group-title">Page Setup</div></div>
      <div class="ribbon-group"><div class="group-content" style="flex-direction:column;align-items:flex-start;gap:4px">
        <div class="ribbon-btn-row"><button class="ribbon-btn" onclick="setColumns(1)">One</button><button class="ribbon-btn" onclick="setColumns(2)">Two Columns</button><button class="ribbon-btn" onclick="setColumns(3)">Three Columns</button></div>
        <div class="ribbon-btn-row"><label>Spacing <select class="select-tool" onchange="setLineSpacing(this.value)"><option value="1">Single</option><option value="1.15">1.15</option><option value="1.5">1.5</option><option value="2">Double</option></select></label>
        <button class="ribbon-btn" onclick="setParagraphSpacing()">Paragraph Spacing</button></div>
      </div><div class="group-title">Paragraph</div></div>
    </div>
    <div class="tab-panel" id="tab-references">
      <div class="ribbon-group"><div class="group-content" style="flex-direction:column;gap:4px">
        <button class="ribbon-btn" onclick="insertTableOfContents()">📑 Table of Contents</button>
        <button class="ribbon-btn" onclick="insertFootnote()">¹ Insert Footnote</button>
        <button class="ribbon-btn" onclick="insertCaption()">Figure Caption</button>
      </div><div class="group-title">Table of Contents</div></div>
      <div class="ribbon-group"><div class="group-content" style="flex-direction:column;gap:4px">
        <button class="ribbon-btn" onclick="insertCitation()">📚 Insert Citation</button>
        <button class="ribbon-btn" onclick="insertBibliography()">Bibliography</button>
      </div><div class="group-title">Citations & Bibliography</div></div>
    </div>
    <div class="tab-panel" id="tab-mailings">
      <div class="ribbon-group"><div class="group-content" style="flex-direction:column;gap:4px">
        <button class="ribbon-btn" onclick="insertMergeField('نام')">Insert «نام»</button>
        <button class="ribbon-btn" onclick="insertMergeField('نام خانوادگی')">Insert «نام خانوادگی»</button>
        <button class="ribbon-btn" onclick="insertMergeField('آدرس')">Insert «آدرس»</button>
      </div><div class="group-title">Write & Insert Fields</div></div>
      <div class="ribbon-group"><div class="group-content" style="flex-direction:column;gap:4px">
        <button class="ribbon-btn" onclick="previewMerge()">👁 Preview Results</button>
        <button class="ribbon-btn" onclick="finishMerge()">Finish & Merge</button>
      </div><div class="group-title">Mail Merge Practice</div></div>
    </div>
    <div class="tab-panel" id="tab-review">
      <div class="ribbon-group"><div class="group-content" style="flex-direction:column;gap:4px">
        <button class="ribbon-btn" onclick="runSpellingCheck()">✓ Spelling & Grammar</button>
        <button class="ribbon-btn" onclick="showWordCount()">🔢 Word Count</button>
        <button class="ribbon-btn" onclick="toggleReadOnly()">🔒 Protect / Edit</button>
      </div><div class="group-title">Proofing</div></div>
      <div class="ribbon-group"><div class="group-content" style="flex-direction:column;gap:4px">
        <button class="ribbon-btn" onclick="insertComment()">💬 New Comment</button>
        <button class="ribbon-btn" onclick="toggleTrackChanges()">Track Changes</button>
        <button class="ribbon-btn" onclick="acceptReviewMarks()">Accept Review Marks</button>
      </div><div class="group-title">Comments & Tracking</div></div>
    </div>
    <div class="tab-panel" id="tab-view">
      <div class="ribbon-group"><div class="group-content" style="flex-direction:column;gap:4px">
        <div class="ribbon-btn-row"><button class="ribbon-btn" onclick="setZoom(80)">80%</button><button class="ribbon-btn" onclick="setZoom(100)">100%</button><button class="ribbon-btn" onclick="setZoom(125)">125%</button></div>
        <button class="ribbon-btn" onclick="toggleRuler()">☷ Toggle Ruler</button>
      </div><div class="group-title">Zoom & Display</div></div>
      <div class="ribbon-group"><div class="group-content" style="flex-direction:column;gap:4px">
        <button class="ribbon-btn" onclick="toggleNavigation()">🔍 Navigation Pane</button>
        <button class="ribbon-btn" onclick="toggleFocusMode()">Focus Mode</button>
        <button class="ribbon-btn" onclick="window.print()">Print Layout / Print</button>
      </div><div class="group-title">Views</div></div>
    </div>
  </div>

  <!-- پاپ‌آپ گرید انتخاب جدول -->
  <div class="table-picker-popup" id="tablePickerPopup">
    <div class="grid-label" id="gridLabel">Insert Table: 1x1</div>
    <div class="grid-container" id="gridContainer"></div>
  </div>

  <div id="ruler" class="ruler" aria-hidden="true"></div>
  <aside id="navigationPane" class="navigation-pane"><strong>ناوبری سند</strong><button style="float:left" onclick="toggleNavigation()">✕</button><input id="navSearch" placeholder="جستجو در سند..." style="width:100%;margin:10px 0;padding:6px" oninput="searchNavigation(this.value)"><div id="navResults"></div></aside>
  <!-- محیط سند (A4 Paper) -->
  <div class="workspace" onclick="hideTablePicker()">
    <div class="page-a4" id="editor" contenteditable="true" spellcheck="false">
      <h2 style="color: #2b579a; margin-bottom: 12px;">شبیه‌ساز کار با مایکروسافت ورد (Microsoft Word)</h2>
      <p>هنرجویان گرامی؛ می‌توانید تمرین‌های عملی پودمان اول ارائه دهنده خدمات رایانه‌ای را در این محیط به‌صورت آنلاین انجام دهید.</p>
      <p>از زبانه <b>Home</b> برای تنظیم فونت‌ها، ترازبندی پاراگراف و استایل‌ها، و از زبانه <b>Insert</b> برای درج جدول، تصویر، اشکال هندسی و نمادها استفاده فرمایید.</p>
    </div>
  </div>

  <!-- نوار وضعیت پایین -->
  <div class="status-bar">
    <div id="statusWords">Page 1 of 1 | Words: 40</div>
    <div>100% —————🔘— +</div>
  </div>

  <!-- نمای پشت‌صحنه File (Backstage) -->
  <div class="backstage-overlay" id="backstageOverlay">
    <div class="backstage-sidebar">
      <button class="backstage-back-btn" onclick="closeBackstage()" title="Back">←</button>
      <div class="backstage-item" onclick="newDocument()">📄 New</div>
      <div class="backstage-item" onclick="saveDocument()">💾 Save</div>
      <div class="backstage-item" onclick="saveAsHtml()">🌐 Save As HTML</div>
      <div class="backstage-item" onclick="printDoc()">🖨️ Print</div>
      <div class="backstage-item" onclick="closeBackstage()">❌ Close</div>
    </div>
    <div class="backstage-content">
      <h2 style="color:var(--word-blue); margin-bottom: 20px;">Document Information</h2>
      <p><strong>Name:</strong> Document1.docx</p>
      <p><strong>Status:</strong> Ready for editing</p>
      <p style="margin-top: 15px; color:#666;">This simulator helps students practice Microsoft Office Word ribbons and tools without requiring Office installation.</p>
    </div>
  </div>

  <script>
    // --- تعویض تب‌ها کاملاً مستقل و تضمین‌شده ---
    document.addEventListener("DOMContentLoaded", function() {
      const tabButtons = document.querySelectorAll('.tab-btn[data-tab]');
      
      tabButtons.forEach(btn => {
        btn.addEventListener('click', function(e) {
          e.stopPropagation();
          const targetTab = this.getAttribute('data-tab');

          // غیرفعال کردن همه
          document.querySelectorAll('.tab-btn:not(.file-btn)').forEach(b => b.classList.remove('active'));
          document.querySelectorAll('.tab-panel').forEach(p => p.classList.remove('active'));

          // فعال‌سازی تب موردنظر
          this.classList.add('active');
          const panel = document.getElementById('tab-' + targetTab);
          if (panel) panel.classList.add('active');
        });
      });

      // دکمه File
      const fileBtn = document.getElementById('btn-file');
      if (fileBtn) {
        fileBtn.addEventListener('click', openBackstage);
      }

      // ساخت امن گرید جدول
      initTablePicker();
    });

    // --- اجرای دستورات ویرایشگر ---
    function execCmd(command, value = null) {
      document.execCommand(command, false, value);
      const editor = document.getElementById('editor');
      if (editor) editor.focus();
      updateStatus();
    }

    function setDocDirection(dir) {
      const editor = document.getElementById('editor');
      if (editor) {
        editor.setAttribute('dir', dir);
        editor.focus();
      }
    }

    function applyStyle(tag) {
      if (tag === 'p') execCmd('formatBlock', '<p>');
      if (tag === 'h1') execCmd('formatBlock', '<h1>');
      if (tag === 'h2') execCmd('formatBlock', '<h2>');
      if (tag === 'title') {
        execCmd('formatBlock', '<h1>');
        execCmd('fontSize', '6');
      }
    }

    let copiedStyle = null;
    function applyFormatPainter() {
      const selection = window.getSelection();
      if (!selection.rangeCount) return;
      const parent = selection.anchorNode.parentElement;
      if (!copiedStyle) {
        copiedStyle = {
          color: window.getComputedStyle(parent).color,
          fontSize: window.getComputedStyle(parent).fontSize,
          fontWeight: window.getComputedStyle(parent).fontWeight
        };
        alert('فرمت متن کپی شد. متن مقصد را انتخاب کنید و مجدداً روی Format Painter بزنید.');
      } else {
        execCmd('foreColor', copiedStyle.color);
        copiedStyle = null;
      }
    }

    // --- ابزارهای تب Insert ---
    function insertPageBreak() {
      execCmd('insertHTML', '<hr style="border:none; border-top:2px dashed #999; margin:30px 0; page-break-after:always;"><br>');
    }

    function insertPicture(input) {
      if (input.files && input.files[0]) {
        const reader = new FileReader();
        reader.onload = function(e) {
          execCmd('insertHTML', `<img src="${e.target.result}" style="max-width:100%; height:auto; margin:10px 0; border:1px solid #ddd; border-radius:4px;" />`);
        };
        reader.readAsDataURL(input.files[0]);
      }
    }

    function insertShape(type) {
      let shapeHtml = '';
      if (type === 'rectangle') {
        shapeHtml = '<div style="width:140px; height:80px; background:#2b579a; border:2px solid #1b3d6d; display:inline-block; margin:5px;"></div>';
      } else if (type === 'circle') {
        shapeHtml = '<div style="width:90px; height:90px; background:#e81123; border-radius:50%; display:inline-block; margin:5px;"></div>';
      }
      execCmd('insertHTML', shapeHtml);
    }

    function insertTextBox() {
      const box = '<div style="border:1.5px solid #2b579a; padding:10px; width:220px; min-height:60px; display:inline-block; background:#fcfcfc; margin:10px;">متن کادر متنی...</div>';
      execCmd('insertHTML', box);
    }

    function insertHeader() {
      const header = '<div style="border-bottom:1px solid #aaa; color:#777; font-size:10pt; margin-bottom:15px; padding-bottom:4px;">سربرگ سند (Header)</div>';
      const ed = document.getElementById('editor');
      if (ed) ed.innerHTML = header + ed.innerHTML;
    }

    function insertFooter() {
      const footer = '<div style="border-top:1px solid #aaa; color:#777; font-size:10pt; margin-top:25px; padding-top:4px;">پاورقی سند (Footer)</div>';
      const ed = document.getElementById('editor');
      if (ed) ed.innerHTML = ed.innerHTML + footer;
    }

    function insertPageNumber() {
      execCmd('insertHTML', '<span style="font-weight:bold; padding:2px 8px; border:1px solid #ccc; background:#eee;">صفحه ۱</span>');
    }

    function insertSymbol(sym) {
      execCmd('insertHTML', sym);
    }

    // --- ساخت گرید جدول بدون خطا ---
    function initTablePicker() {
      const gridContainer = document.getElementById('gridContainer');
      if (!gridContainer) return;
      gridContainer.innerHTML = '';
      for (let r = 1; r <= 5; r++) {
        for (let c = 1; c <= 5; c++) {
          const cell = document.createElement('div');
          cell.className = 'grid-cell';
          cell.dataset.row = r;
          cell.dataset.col = c;
          cell.onmouseover = () => highlightCells(r, c);
          cell.onclick = () => insertTable(r, c);
          gridContainer.appendChild(cell);
        }
      }
    }

    function toggleTablePicker() {
      const popup = document.getElementById('tablePickerPopup');
      if (popup) {
        popup.style.display = popup.style.display === 'block' ? 'none' : 'block';
      }
    }

    function hideTablePicker() {
      const popup = document.getElementById('tablePickerPopup');
      if (popup) popup.style.display = 'none';
    }

    function highlightCells(maxR, maxC) {
      const gridLabel = document.getElementById('gridLabel');
      if (gridLabel) gridLabel.innerText = `Insert Table: ${maxR} x ${maxC}`;
      document.querySelectorAll('.grid-cell').forEach(c => {
        const r = parseInt(c.dataset.row);
        const col = parseInt(c.dataset.col);
        if (r <= maxR && col <= maxC) {
          c.classList.add('highlight');
        } else {
          c.classList.remove('highlight');
        }
      });
    }

    function insertTable(rows, cols) {
      let html = '<table style="width:100%; border-collapse:collapse; margin:10px 0;"><tbody>';
      for (let i = 0; i < rows; i++) {
        html += '<tr>';
        for (let j = 0; j < cols; j++) {
          html += '<td style="border:1px solid #666; padding:8px;">متن</td>';
        }
        html += '</tr>';
      }
      html += '</tbody></table><br>';
      execCmd('insertHTML', html);
      hideTablePicker();
    }

    // --- ابزارهای تب Design ---
    function applyThemeColor(color) {
      const editor = document.getElementById('editor');
      if (editor) {
        const headings = editor.querySelectorAll('h1, h2, h3');
        headings.forEach(h => h.style.color = color);
      }
    }

    function setPageColor(color) {
      const editor = document.getElementById('editor');
      if (editor) editor.style.backgroundColor = color;
    }

    function setPageBorder(borderType) {
      const editor = document.getElementById('editor');
      if (!editor) return;
      if (borderType === 'none') {
        editor.style.border = 'none';
      } else if (borderType === 'solid') {
        editor.style.border = '2px solid #2b579a';
      } else if (borderType === 'double') {
        editor.style.border = '4px double #2b579a';
      }
    }

    function setWatermark() {
      const wmText = prompt('متن واترمارک را وارد فرمایید (مثال: محرمانه یا پیش‌نویس):', 'محرمانه');
      if (wmText) {
        let wm = document.getElementById('docWatermark');
        const editor = document.getElementById('editor');
        if (!wm && editor) {
          wm = document.createElement('div');
          wm.id = 'docWatermark';
          wm.style.cssText = 'position:absolute; top:40%; left:15%; transform:rotate(-40deg); font-size:60pt; color:rgba(0,0,0,0.08); pointer-events:none; font-weight:bold; white-space:nowrap;';
          editor.appendChild(wm);
        }
        if (wm) wm.innerText = wmText;
      }
    }

    // --- جستجو و جایگزینی ---
    function openFind() {
      const term = prompt('متن مورد جستجو را وارد کنید:');
      if (!term) return;
      const editor = document.getElementById('editor');
      if (!editor) return;
      if (window.find) {
        window.find(term);
      } else {
        const found = editor.innerText.includes(term);
        alert(found ? 'متن پیدا شد.' : 'متن یافت نشد.');
      }
    }

    function openReplace() {
      const term = prompt('متن مورد جستجو:');
      if (term === null || term === '') return;
      const repl = prompt('متن جایگزین:');
      if (repl === null) return;
      const editor = document.getElementById('editor');
      const walker = document.createTreeWalker(editor, NodeFilter.SHOW_TEXT);
      const nodes = []; while (walker.nextNode()) nodes.push(walker.currentNode);
      let count = 0;
      nodes.forEach(node => { if (node.parentElement.closest('script,style')) return;
        if (node.nodeValue.includes(term)) { count += node.nodeValue.split(term).length - 1; node.nodeValue = node.nodeValue.split(term).join(repl); }
      });
      updateStatus(); alert(count ? `${count} مورد جایگزین شد.` : 'متنی پیدا نشد.');
    }

    // --- File / Backstage ---
    function openBackstage() {
      const ov = document.getElementById('backstageOverlay');
      if (ov) ov.style.display = 'flex';
    }

    function closeBackstage() {
      const ov = document.getElementById('backstageOverlay');
      if (ov) ov.style.display = 'none';
    }

    function newDocument() {
      if (confirm('سند جدید ایجاد شود؟ محتوای فعلی از بین می‌رود.')) {
        const editor = document.getElementById('editor');
        if (editor) editor.innerHTML = '<p><br></p>';
        closeBackstage();
        updateStatus();
      }
    }

    function saveDocument() {
      const editor = document.getElementById('editor');
      if (!editor) return;
      const html = '<!DOCTYPE html><html lang="fa" dir="rtl"><head><meta charset="UTF-8"><title>Document1</title><style>body{font-family:Tahoma,Arial;direction:rtl;line-height:1.7}table,td,th{border:1px solid #666;border-collapse:collapse;padding:6px}img{max-width:100%}</style></head><body>' + editor.innerHTML + '</body></html>';
      const blob = new Blob(['\\ufeff', html], { type: 'application/msword;charset=utf-8' });
      const a = document.createElement('a'); const url = URL.createObjectURL(blob);
      a.href = url; a.download = 'Document1.doc'; a.click();
      setTimeout(() => URL.revokeObjectURL(url), 1000);
      closeBackstage();
    }

    function saveAsHtml() {
      const editor = document.getElementById('editor');
      if (!editor) return;
      const html = '<!DOCTYPE html><html lang="fa" dir="rtl"><head><meta charset="UTF-8"><title>Document1</title></head><body>' + editor.innerHTML + '</body></html>';
      const blob = new Blob([html], { type: 'text/html;charset=utf-8' });
      const a = document.createElement('a');
      a.href = URL.createObjectURL(blob);
      a.download = 'Document1.html';
      a.click();
      URL.revokeObjectURL(a.href);
      closeBackstage();
    }

    function printDoc() {
      closeBackstage();
      window.print();
    }

    // --- نوار وضعیت: شمارش کلمات ---
    function updateStatus() {
      const editor = document.getElementById('editor');
      const status = document.getElementById('statusWords');
      if (!editor || !status) return;
      const text = editor.innerText.trim();
      const words = text ? text.split(/\s+/).length : 0;
      status.innerText = 'Page 1 of 1 | Words: ' + words;
    }

    // به‌روزرسانی وضعیت هنگام تایپ
    document.addEventListener('input', updateStatus);
    document.addEventListener('keyup', updateStatus);

    // ابزارهای تکمیلی زبانه‌ها
    function setPageOrientation(mode) {
      const e=document.getElementById('editor'); if(!e)return;
      e.style.width=mode==='landscape'?'297mm':'210mm';
      e.style.minHeight=mode==='landscape'?'210mm':'297mm';
    }
    function setMargins(mm) { document.getElementById('editor').style.padding=mm+'mm'; }
    function setPaperSize(size) {
      const e=document.getElementById('editor');
      const dims={A4:['210mm','297mm'],Letter:['8.5in','11in'],A3:['297mm','420mm']};
      e.style.width=dims[size][0]; e.style.minHeight=dims[size][1];
    }
    function setColumns(n) {
      const e=document.getElementById('editor'); e.style.columnCount=String(n); e.style.columnGap='24px';
    }
    function setLineSpacing(v) { document.getElementById('editor').style.lineHeight=v; }
    function setParagraphSpacing() {
      const v=prompt('فاصله پایین پاراگراف به پیکسل (مثلاً 12):','12');
      if(v!==null && Number.isFinite(Number(v)) && Number(v)>=0) {
        const sel=window.getSelection(); if(sel && sel.rangeCount && !sel.isCollapsed) {
          let n=sel.anchorNode.nodeType===1?sel.anchorNode:sel.anchorNode.parentElement;
          const p=n.closest('p,div,li,h1,h2,h3'); if(p)p.style.marginBottom=Number(v)+'px';
        } else alert('ابتدا مکان‌نما را داخل پاراگراف موردنظر قرار دهید.');
      }
    }
    function insertTableOfContents() {
      const e=document.getElementById('editor'), hs=[...e.querySelectorAll('h1,h2,h3')];
      if(!hs.length){alert('ابتدا از ابزار Styles عنوان‌های Heading ایجاد کنید.');return;}
      const box=document.createElement('div'); box.contentEditable='false'; box.style.cssText='border:1px solid #aaa;padding:10px;margin:10px 0;background:#fafafa';
      const title=document.createElement('strong'); title.textContent='فهرست مطالب'; box.appendChild(title);
      const ul=document.createElement('ul');
      hs.forEach((h,i)=>{if(!h.id)h.id='heading-'+(i+1);const li=document.createElement('li');li.style.marginRight=(parseInt(h.tagName[1])-1)*14+'px';const a=document.createElement('a');a.href='#'+h.id;a.textContent=h.innerText;li.appendChild(a);ul.appendChild(li);});
      box.appendChild(ul); insertNodeAtCaret(box);
    }
    function insertNodeAtCaret(node) {
      const sel=window.getSelection(); const e=document.getElementById('editor');
      if(sel&&sel.rangeCount&&e.contains(sel.anchorNode)){const r=sel.getRangeAt(0);r.deleteContents();r.insertNode(node);r.setStartAfter(node);r.collapse(true);sel.removeAllRanges();sel.addRange(r);}
      else e.appendChild(node); e.focus(); updateStatus();
    }
    function insertFootnote() {
      const t=prompt('متن پاورقی را وارد کنید:'); if(t===null)return;
      const sup=document.createElement('sup');sup.textContent='['+(document.querySelectorAll('.footnote').length+1)+']';
      const note=document.createElement('span');note.className='footnote';note.style.cssText='font-size:10pt;color:#555';note.textContent=' پاورقی: '+t;
      const frag=document.createDocumentFragment();frag.append(sup,note);insertNodeAtCaret(frag);
    }
    function insertCaption() { const t=prompt('عنوان شکل یا جدول:','شکل ۱: ');if(t!==null){const p=document.createElement('p');p.style.cssText='text-align:center;font-size:11pt;color:#555';p.textContent=t;insertNodeAtCaret(p);} }
    function insertCitation() { const t=prompt('منبع (نام نویسنده، عنوان، سال):');if(t!==null&&t.trim()){const span=document.createElement('span');span.textContent=' ('+t.trim()+')';insertNodeAtCaret(span);} }
    function insertBibliography() { const t=prompt('منابع را وارد کنید (هر منبع در یک خط):');if(t===null)return;const h=document.createElement('h2');h.textContent='منابع';const ul=document.createElement('ul');t.split(/\n/).filter(x=>x.trim()).forEach(x=>{const li=document.createElement('li');li.textContent=x;ul.appendChild(li)});const d=document.createDocumentFragment();d.append(h,ul);insertNodeAtCaret(d); }
    function insertMergeField(name) { const s=document.createElement('span');s.textContent='«'+name+'»';s.style.cssText='background:#fff2cc;border:1px dashed #b8860b;padding:2px';s.dataset.mergeField=name;insertNodeAtCaret(s); }
    function previewMerge() { const e=document.getElementById('editor');e.querySelectorAll('[data-merge-field]').forEach(n=>{if(!n.dataset.originalText)n.dataset.originalText=n.textContent;const demo={'نام':'علی','نام خانوادگی':'احمدی','آدرس':'تهران'};n.textContent=demo[n.dataset.mergeField]||n.dataset.originalText;}); }
    function finishMerge() { previewMerge();alert('پیش‌نمایش ادغام انجام شد. این نسخه آموزشی به فهرست گیرندگان واقعی متصل نیست.'); }
    function runSpellingCheck() { alert('بررسی خودکار املای فارسی در این شبیه‌ساز فعال نیست. برای تمرین، متن را بازخوانی کنید یا از غلط‌یاب مرورگر استفاده کنید.'); }
    function showWordCount() { const e=document.getElementById('editor'),t=e.innerText.trim();const words=t?t.split(/\s+/).length:0;const chars=t.length;alert('تعداد کلمات: '+words+'\nتعداد نویسه‌ها: '+chars+'\nتعداد پاراگراف‌ها: '+e.querySelectorAll('p').length); }
    let editorLocked=false, trackChanges=false;
    function toggleReadOnly() { editorLocked=!editorLocked;document.getElementById('editor').contentEditable=String(!editorLocked);alert(editorLocked?'ویرایش قفل شد.':'ویرایش فعال شد.'); }
    function insertComment() { const t=prompt('یادداشت آموزشی:');if(t===null)return;const s=document.createElement('span');s.dataset.comment='true';s.title=t;s.textContent='[یادداشت: '+t+']';insertNodeAtCaret(s); }
    function toggleTrackChanges() { trackChanges=!trackChanges;const e=document.getElementById('editor');e.dataset.trackChanges=String(trackChanges);alert(trackChanges?'حالت تمرینی پیگیری تغییرات روشن شد؛ تغییرات واقعی به‌صورت کامل ثبت نمی‌شوند.':'حالت پیگیری تغییرات خاموش شد.'); }
    function acceptReviewMarks() { document.querySelectorAll('#editor [data-comment]').forEach(n=>{const t=document.createTextNode(n.textContent);n.replaceWith(t)});document.getElementById('editor').removeAttribute('data-track-changes');trackChanges=false; }
    function setZoom(n) { const e=document.getElementById('editor');e.style.zoom=(n/100);document.querySelector('.status-bar div:last-child').textContent=n+'%'; }
    function toggleRuler() { document.getElementById('ruler').classList.toggle('visible'); }
    function toggleNavigation() { document.getElementById('navigationPane').classList.toggle('visible'); }
    function toggleFocusMode() { document.body.classList.toggle('focus-mode'); }
    function searchNavigation(q) { const out=document.getElementById('navResults');out.innerHTML='';if(!q)return;const e=document.getElementById('editor');const nodes=[...e.querySelectorAll('h1,h2,h3,p,li')];let hits=0;nodes.forEach(n=>{if(n.innerText.toLowerCase().includes(q.toLowerCase())){const b=document.createElement('button');b.style.cssText='display:block;width:100%;text-align:right;padding:6px;margin:3px 0';b.textContent=n.innerText.slice(0,100);b.onclick=()=>{n.scrollIntoView({behavior:'smooth',block:'center'});};out.appendChild(b);hits++;}});if(!hits)out.textContent='موردی پیدا نشد.';}
    // نگه‌داشتن متن انتخاب‌شده هنگام استفاده از ابزارها و میانبرهای رایج
    document.addEventListener('keydown',e=>{
      if((e.ctrlKey||e.metaKey)&&e.key.toLowerCase()==='s'){e.preventDefault();saveDocument();}
      if((e.ctrlKey||e.metaKey)&&e.key.toLowerCase()==='b'){e.preventDefault();execCmd('bold');}
      if((e.ctrlKey||e.metaKey)&&e.key.toLowerCase()==='i'){e.preventDefault();execCmd('italic');}
      if((e.ctrlKey||e.metaKey)&&e.key.toLowerCase()==='u'){e.preventDefault();execCmd('underline');}
    });
    // شمارش وضعیت در شروع و بازیابی ایمن متن تمرینی از همین نشست
    document.addEventListener('DOMContentLoaded',()=>{updateStatus();});

  </script>
</body>
</html>
