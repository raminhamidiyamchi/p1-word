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
    .title-actions { display:flex; align-items:center; gap:4px; }
    .title-actions button { border:1px solid transparent; background:transparent; color:#fff; border-radius:3px; padding:3px 6px; cursor:pointer; font-size:15px; }
    .title-actions button:hover { background:rgba(255,255,255,.18); border-color:rgba(255,255,255,.25); }
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

    #tab-practice .ribbon-group { align-items:stretch; }
    #tab-practice .group-content { min-height:64px; }
    #editor a { color:#0563c1; text-decoration:underline; }
    #editor .sim-bookmark { background:#fff2cc; border-bottom:1px dotted #b8860b; }
    #editor .sim-wordart { display:inline-block; font-size:24pt; font-weight:bold; color:#2b579a; text-shadow:2px 2px 2px #bbb; transform:rotate(-4deg); padding:5px; }
    #editor .sim-comment { background:#fff2cc; border-bottom:2px dotted #b8860b; }
    #editor .sim-section-break { border-top:2px dashed #7f7f7f; margin:24px 0; padding-top:8px; color:#777; font-size:10pt; }

    @media print { body { height:auto; overflow:visible; background:white; } .title-bar,.tabs-bar,.ribbon-container,.status-bar,.backstage-overlay,.ruler,.navigation-pane {display:none!important} .workspace{display:block;padding:0;overflow:visible;background:white} .page-a4{box-shadow:none;margin:0;width:auto;min-height:0;padding:20mm;border:none!important} }
    @media(max-width:700px) { .page-a4 { width:100%; min-height:100%; padding:12mm; } .workspace { padding:10px 4px; } .backstage-sidebar {width:150px} .backstage-content {padding:18px} }

  @media print {
      body { height:auto !important; overflow:visible !important; background:#fff !important; }
      .title-bar, .tabs-bar, .ribbon-container, .status-bar, .backstage-overlay, #navigationPane, #ruler { display:none !important; }
      .workspace { display:block !important; overflow:visible !important; padding:0 !important; background:#fff !important; }
      .page-a4 { box-shadow:none !important; margin:0 auto !important; }
    }
    </style>
</head>
<body>

  <!-- نوار عنوان -->
  <div class="title-bar">
    <div class="title-actions">
      <button type="button" title="ذخیره (Ctrl+S)" onclick="saveDocument()">💾</button>
      <button type="button" title="واگرد (Ctrl+Z)" onclick="execCmd('undo')">↩️</button>
      <button type="button" title="انجام دوباره (Ctrl+Y)" onclick="execCmd('redo')">↪️</button>
    </div>
    <div class="title-text" id="documentTitle">Document1 - Word Simulator</div>
    <div aria-hidden="true">Word Simulator</div>
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
    <button class="tab-btn" data-tab="practice">تمرین‌های کتاب</button>
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
          <button class="ribbon-btn" onclick="startDictation()">🎙 Dictate</button>
          <button class="ribbon-btn" onclick="openAIWritingPractice()">✨ AI Writing Practice</button>
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
        <div class="group-content" style="flex-direction:column;align-items:flex-start;gap:3px">
          <button class="ribbon-btn ribbon-btn-large" onclick="toggleTablePicker()">
            <span class="icon">田</span>
            <span>Table ▾</span>
          </button>
          <button class="ribbon-btn" onclick="addTableRow()">＋ Add Row</button>
          <button class="ribbon-btn" onclick="deleteTableRow()">－ Delete Row</button>
          <button class="ribbon-btn" onclick="mergeTableCells()">⇔ Merge Cells</button>
          <button class="ribbon-btn" onclick="splitTableCell()">▦ Split Cell</button>
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
            <button class="ribbon-btn" onclick="insertSymbol('∑')">∑ Symbol</button>
            <button class="ribbon-btn" onclick="insertEquation()">x² Equation</button>
            <button class="ribbon-btn" onclick="insertWordArt()">WordArt</button>
            <button class="ribbon-btn" onclick="insertHyperlink()">🔗 Link</button>
            <button class="ribbon-btn" onclick="insertBookmark()">🔖 Bookmark</button>
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
            <button class="ribbon-btn" onclick="setPageBorder('art')">✿ Art Border</button>
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
        <label>Size <select class="select-tool" onchange="setPaperSize(this.value)"><option value="A4">A4</option><option value="Letter">Letter</option><option value="A3">A3</option><option value="Vaziri">وزیری (تقریبی)</option><option value="Raghi">رقعی (تقریبی)</option><option value="Khesti">خشتی (تقریبی)</option><option value="Pocket">جیبی (تقریبی)</option></select></label></div>
      </div><div class="group-title">Page Setup</div></div>
      <div class="ribbon-group"><div class="group-content" style="flex-direction:column;align-items:flex-start;gap:4px">
        <div class="ribbon-btn-row"><button class="ribbon-btn" onclick="setColumns(1)">One</button><button class="ribbon-btn" onclick="setColumns(2)">Two Columns</button><button class="ribbon-btn" onclick="setColumns(3)">Three Columns</button></div>
        <div class="ribbon-btn-row"><label>Spacing <select class="select-tool" onchange="setLineSpacing(this.value)"><option value="1">Single</option><option value="1.15">1.15</option><option value="1.5">1.5</option><option value="2">Double</option></select></label>
        <button class="ribbon-btn" onclick="setParagraphSpacing()">Paragraph Spacing</button>
        <button class="ribbon-btn" onclick="insertSectionBreak()">Section Break</button></div>
      </div><div class="group-title">Paragraph</div></div>
    </div>
    <div class="tab-panel" id="tab-references">
      <div class="ribbon-group"><div class="group-content" style="flex-direction:column;gap:4px">
        <button class="ribbon-btn" onclick="insertTableOfContents()">📑 Table of Contents</button>
        <button class="ribbon-btn" onclick="insertFootnote()">¹ Insert Footnote</button>
        <button class="ribbon-btn" onclick="updateTableOfContents()">Update TOC</button>
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
        <button class="ribbon-btn" onclick="manageMailingList()">قائمة گیرندگان</button>
        <button class="ribbon-btn" onclick="createLabels()">Labels</button>
        <button class="ribbon-btn" onclick="createEnvelope()">Envelope</button>
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
    <div class="tab-panel" id="tab-practice">
      <div class="ribbon-group"><div class="group-content" style="flex-direction:column;gap:5px;align-items:stretch">
        <select id="practiceSelect" class="select-tool" style="min-width:220px">
          <option value="format">تمرین ۱: قالب‌بندی متن</option>
          <option value="paragraph">تمرین ۲: پاراگراف و فهرست</option>
          <option value="table">تمرین ۳: جدول هنرجویان</option>
          <option value="picture">تمرین ۴: تصویر و شکل</option>
          <option value="page">تمرین ۵: صفحه‌آرایی</option>
          <option value="review">تمرین ۶: بازبینی و نظر</option>
          <option value="toc">تمرین ۷: عنوان‌ها و فهرست مطالب</option>
          <option value="mail">تمرین ۸: ادغام پستی</option>
        </select>
        <button class="ribbon-btn" onclick="loadPractice()">نمایش دستور تمرین</button>
        <button class="ribbon-btn" onclick="checkPractice()">بررسی عملکرد من</button>
      </div><div class="group-title">تمرین عملی</div></div>
      <div class="ribbon-group" style="min-width:320px;max-width:520px">
        <div class="group-content" style="display:block;width:100%">
          <div id="practiceInstructions" style="font-size:12px;line-height:1.8;max-width:480px">یک تمرین انتخاب کنید و «نمایش دستور تمرین» را بزنید. بررسی خودکار، نشانه‌های قابل‌تشخیص در سند را می‌سنجد و جایگزین ارزیابی کامل معلم نیست.</div>
          <div id="practiceFeedback" role="status" style="margin-top:5px;font-weight:bold;color:#2b579a"></div>
        </div><div class="group-title">راهنما و بازخورد</div>
      </div>
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
      <div class="backstage-item" onclick="document.getElementById('openDocumentInput').click()">📂 Open HTML/TXT</div>
      <div class="backstage-item" onclick="saveDocument()">💾 Save</div>
      <div class="backstage-item" onclick="saveAsHtml()">🌐 Save As HTML</div>
      <div class="backstage-item" onclick="printDoc()">🖨️ Print</div>
      <div class="backstage-item" onclick="closeBackstage()">❌ Close</div>
    </div>
    <input type="file" id="openDocumentInput" accept=".html,.htm,.txt,text/html,text/plain" hidden onchange="openDocumentFile(this)">
    <div class="backstage-content">
      <h2 style="color:var(--word-blue); margin-bottom: 20px;">Document Information</h2>
      <p><strong>Name:</strong> Document1</p>
      <p><strong>Status:</strong> Ready for editing</p>
      <p style="margin-top: 15px; color:#666;">This simulator helps students practice Microsoft Office Word ribbons and tools without requiring Office installation.</p><p style="margin-top:10px;color:#8a4b08;font-size:12px;">Save creates a Word-compatible HTML .doc file, not a native .docx file. Open supports HTML and TXT.</p>
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

    let savedEditorRange = null;
    let documentDirty = false;

    function setDirty(value) {
      documentDirty = !!value;
      const title = document.getElementById('documentTitle');
      if (!title) return;
      const base = title.textContent.replace(/^●\s*/, '').replace(/\s*\*$/, '').replace(/\s*-\s*Word Simulator$/i, '');
      title.textContent = (documentDirty ? '● ' : '') + (base || 'Document1') + ' - Word Simulator';
    }

    function saveEditorSelection() {
      const editor = document.getElementById('editor');
      const sel = window.getSelection();
      if (!editor || !sel || !sel.rangeCount) return;
      const range = sel.getRangeAt(0);
      if (editor.contains(range.commonAncestorContainer)) savedEditorRange = range.cloneRange();
    }

    function restoreEditorSelection() {
      const editor = document.getElementById('editor');
      if (!editor) return;
      editor.focus();
      const sel = window.getSelection();
      if (savedEditorRange && editor.contains(savedEditorRange.commonAncestorContainer)) {
        sel.removeAllRanges();
        sel.addRange(savedEditorRange);
      }
    }

    document.addEventListener('selectionchange', saveEditorSelection);
    document.addEventListener('DOMContentLoaded', () => {
      const ribbon = document.querySelector('.ribbon-container');
      if (ribbon) ribbon.addEventListener('mousedown', saveEditorSelection);
      const editor = document.getElementById('editor');
      if (editor) editor.addEventListener('input', () => setDirty(true));
    });

    // --- اجرای دستورات ویرایشگر ---
    function execCmd(command, value = null) {
      restoreEditorSelection();
      try { document.execCommand(command, false, value); }
      catch (err) { console.warn('دستور اجرا نشد:', command, err); }
      const editor = document.getElementById('editor');
      if (editor) editor.focus();
      saveEditorSelection();
      setDirty(true);
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
      } else if (borderType === 'art') {
        editor.style.border = '8px ridge #2b579a';
        editor.style.outline = '2px dotted #7fba00';
        editor.style.outlineOffset = '-12px';
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
      if (!confirm(documentDirty ? 'تغییرات ذخیره‌نشده از بین می‌روند. سند جدید ایجاد شود؟' : 'سند جدید ایجاد شود؟')) return;
      const editor = document.getElementById('editor');
      if (editor) { editor.innerHTML = '<p><br></p>'; editor.style.cssText = ''; editor.setAttribute('dir', 'rtl'); }
      const title = document.getElementById('documentTitle');
      if (title) title.textContent = 'Document1 - Word Simulator';
      closeBackstage();
      setDirty(false);
      updateStatus();
    }

    function getExportHtml() {
      const editor = document.getElementById('editor');
      const title = (document.getElementById('documentTitle')?.textContent || 'Document1')
        .replace(/\s*-\s*Word Simulator\s*$/i, '').replace(/^●\s*/, '').trim() || 'Document1';
      const clone = editor.cloneNode(true);
      clone.removeAttribute('contenteditable');
      clone.removeAttribute('spellcheck');
      clone.removeAttribute('id');
      const css = 'body{font-family:Tahoma,Arial,sans-serif;direction:rtl;line-height:1.7}table{border-collapse:collapse;width:100%}table,td,th{border:1px solid #666}td,th{padding:6px}img{max-width:100%;height:auto}';
      return '<!DOCTYPE html><html lang="fa" dir="rtl"><head><meta charset="UTF-8"><title>' +
        escapeHtml(title) + '</title><style>' + css + '</style></head><body>' + clone.innerHTML + '</body></html>';
    }

    function escapeHtml(value) {
      return String(value).replace(/[&<>"']/g, ch => ({
        '&':'&amp;', '<':'&lt;', '>':'&gt;', '"':'&quot;', "'":'&#39;'
      })[ch]);
    }

    function downloadBlob(blob, filename) {
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.href = url;
      a.download = filename;
      document.body.appendChild(a);
      a.click();
      a.remove();
      setTimeout(() => URL.revokeObjectURL(url), 1500);
    }

    function saveDocument() {
      // خروجی DOC، HTML سازگار با Word است؛ این فایل DOCX باینری واقعی نیست.
      const blob = new Blob(['\ufeff', getExportHtml()], { type: 'application/msword;charset=utf-8' });
      downloadBlob(blob, 'Document1.doc');
      closeBackstage();
      setDirty(false);
    }

    function saveAsHtml() {
      const blob = new Blob(['\ufeff', getExportHtml()], { type: 'text/html;charset=utf-8' });
      downloadBlob(blob, 'Document1.html');
      closeBackstage();
      setDirty(false);
    }

    function openDocumentFile(input) {
      const file = input.files && input.files[0];
      if (!file) return;
      const ext = file.name.split('.').pop().toLowerCase();
      if (!['html','htm','txt'].includes(ext)) {
        alert('در این نسخه فقط فایل‌های HTML و TXT باز می‌شوند؛ DOCX واقعی هنوز پشتیبانی نمی‌شود.');
        input.value = '';
        return;
      }
      const reader = new FileReader();
      reader.onload = () => {
        const editor = document.getElementById('editor');
        if (!editor) return;
        if (ext === 'txt') {
          editor.textContent = String(reader.result || '');
          editor.innerHTML = editor.innerHTML.replace(/\n/g, '<br>');
        } else {
          const parsed = new DOMParser().parseFromString(String(reader.result || ''), 'text/html');
          parsed.body.querySelectorAll('script,style,iframe,object,embed,link,meta').forEach(n => n.remove());
          editor.innerHTML = parsed.body.innerHTML || '<p><br></p>';
          editor.querySelectorAll('*').forEach(el => {
            [...el.attributes].forEach(attr => { if (/^on/i.test(attr.name)) el.removeAttribute(attr.name); });
          });
        }
        const title = document.getElementById('documentTitle');
        if (title) title.textContent = file.name.replace(/\.(html?|txt)$/i, '') + ' - Word Simulator';
        closeBackstage();
        setDirty(false);
        updateStatus();
        input.value = '';
      };
      reader.onerror = () => alert('خواندن فایل ناموفق بود.');
      reader.readAsText(file, 'UTF-8');
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
      const text = (editor.innerText || '').replace(/\u00a0/g, ' ').trim();
      const words = text ? text.split(/\s+/u).filter(Boolean).length : 0;
      status.innerText = 'Editing area | Words: ' + words;
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
      const dims={
        A4:['210mm','297mm'], Letter:['8.5in','11in'], A3:['297mm','420mm'],
        Vaziri:['165mm','235mm'], Raghi:['140mm','210mm'], Khesti:['215mm','215mm'], Pocket:['100mm','190mm']
      };
      if(!e || !dims[size]) return;
      e.style.width=dims[size][0]; e.style.minHeight=dims[size][1];
      e.dataset.paperSize=size;
      setDirty(true);
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
      if(!e) return;
      if(sel&&sel.rangeCount&&e.contains(sel.anchorNode)){
        const r=sel.getRangeAt(0); r.deleteContents();
        let lastInserted = node;
        if(node && node.nodeType === Node.DOCUMENT_FRAGMENT_NODE) lastInserted = node.lastChild;
        r.insertNode(node);
        if(lastInserted && lastInserted.parentNode) { r.setStartAfter(lastInserted); r.collapse(true); sel.removeAllRanges(); sel.addRange(r); }
      } else e.appendChild(node);
      e.focus(); updateStatus();
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

    // --- ابزارهای تکمیلی همسو با پودمان کتاب ---
    function startDictation() {
      const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
      if (!SpeechRecognition) {
        alert('مرورگر فعلی از تبدیل گفتار به متن پشتیبانی نمی‌کند. در نسخه دسکتاپ Chrome یا Edge امتحان کنید.');
        return;
      }
      const recognition = new SpeechRecognition();
      recognition.lang = 'fa-IR';
      recognition.interimResults = false;
      recognition.maxAlternatives = 1;
      recognition.onresult = event => {
        const spoken = event.results?.[0]?.[0]?.transcript || '';
        if (spoken) { insertNodeAtCaret(document.createTextNode(spoken + ' ')); setDirty(true); }
      };
      recognition.onerror = event => alert('تشخیص گفتار متوقف شد: ' + (event.error || 'خطای نامشخص'));
      recognition.start();
      alert('حالا صحبت کنید. برای استفاده از میکروفون، اجازه مرورگر را تأیید کنید.');
    }

    function openAIWritingPractice() {
      const task = prompt('تمرین هوش مصنوعی: موضوع یا دستور نوشتن را وارد کنید. این نسخه مستقل به سرویس هوش مصنوعی متصل نیست و فقط محیط تمرین را فراهم می‌کند:', 'یک نامه رسمی به معلم درباره غیبت بنویس');
      if (task === null || !task.trim()) return;
      const draft = prompt('متن پیشنهادی خود را بنویسید تا به‌عنوان پیش‌نویس تمرینی وارد سند شود. برای تولید واقعی متن با هوش مصنوعی، باید سرویس جداگانه‌ای متصل شود:', 'موضوع: ' + task + '\nبا سلام و احترام،\n\nمتن نامه را اینجا تکمیل کنید.\n\nبا تشکر');
      if (draft === null) return;
      const box = document.createElement('div');
      box.style.cssText = 'border:1px solid #8a8886;background:#f8f8f8;padding:10px;margin:8px 0;white-space:pre-wrap';
      const label = document.createElement('strong'); label.textContent = 'پیش‌نویس تمرینی (AI Practice):\n';
      const body = document.createElement('div'); body.textContent = draft;
      box.append(label, body); insertNodeAtCaret(box); setDirty(true);
    }

    function insertEquation() {
      const expr = prompt('فرمول را به صورت متنی وارد کنید (مثال: y = x² + 5x + 4):', 'y = x² + 5x + 4');
      if (expr === null || !expr.trim()) return;
      const span = document.createElement('span');
      span.textContent = expr;
      span.style.cssText = 'display:inline-block;direction:ltr;font-family:Cambria,serif;font-size:16pt;padding:3px 8px;border:1px solid #ddd;background:#fafafa';
      span.setAttribute('aria-label', 'فرمول آموزشی');
      insertNodeAtCaret(span);
      setDirty(true);
    }

    function insertWordArt() {
      const t = prompt('متن هنری را وارد کنید:', 'مهارت');
      if (t === null || !t.trim()) return;
      const span = document.createElement('span');
      span.className = 'sim-wordart';
      span.textContent = t;
      insertNodeAtCaret(span);
      setDirty(true);
    }

    function insertHyperlink() {
      const url = prompt('آدرس کامل پیوند را وارد کنید (مثال: https://www.google.com):', 'https://www.google.com');
      if (!url) return;
      let safeUrl;
      try { safeUrl = new URL(url); } catch (_) { alert('آدرس معتبر نیست. آدرس را با https:// وارد کنید.'); return; }
      if (!['http:', 'https:', 'mailto:'].includes(safeUrl.protocol)) { alert('این نوع پیوند مجاز نیست.'); return; }
      restoreEditorSelection();
      const sel = window.getSelection();
      const text = sel && !sel.isCollapsed ? sel.toString() : (prompt('متن نمایشی پیوند:', safeUrl.hostname) || safeUrl.hostname);
      const a = document.createElement('a');
      a.href = safeUrl.href;
      a.textContent = text;
      a.target = '_blank';
      a.rel = 'noopener noreferrer';
      insertNodeAtCaret(a);
      setDirty(true);
    }

    function insertBookmark() {
      const name = prompt('نام نشانک (بدون فاصله):', 'بخش_مهم');
      if (!name) return;
      const id = name.trim().replace(/[^a-zA-Z0-9_\-\u0600-\u06FF]/g, '_');
      if (!id) return;
      const span = document.createElement('span');
      span.id = 'bookmark-' + id;
      span.className = 'sim-bookmark';
      span.textContent = '🔖 ' + name.trim();
      span.title = 'نشانک آموزشی؛ برای تمرین مدیریت سند';
      insertNodeAtCaret(span);
      setDirty(true);
      alert('نشانک درج شد. در این نسخه، نشانک به‌صورت علامت قابل مشاهده در متن تمرین می‌شود.');
    }

    function updateTableOfContents() {
      const e = document.getElementById('editor');
      const old = e.querySelector('[data-sim-toc="true"]');
      if (old) old.remove();
      const hs = [...e.querySelectorAll('h1,h2,h3')];
      if (!hs.length) { alert('ابتدا چند عنوان با Heading 1 یا Heading 2 ایجاد کنید.'); return; }
      const box = document.createElement('div');
      box.dataset.simToc = 'true';
      box.style.cssText = 'border:1px solid #aaa;padding:10px;margin:10px 0;background:#fafafa';
      const title = document.createElement('strong');
      title.textContent = 'فهرست مطالب (قابل به‌روزرسانی در شبیه‌ساز)';
      box.appendChild(title);
      const ol = document.createElement('ol');
      hs.forEach((h, i) => {
        if (!h.id) h.id = 'heading-' + (i + 1);
        const li = document.createElement('li');
        li.style.marginRight = (parseInt(h.tagName[1]) - 1) * 14 + 'px';
        const a = document.createElement('a');
        a.href = '#' + h.id;
        a.textContent = h.innerText;
        li.appendChild(a); ol.appendChild(li);
      });
      box.appendChild(ol);
      const prior = old;
      if (prior) prior.remove();
      insertNodeAtCaret(box);
      setDirty(true);
    }

    function insertSectionBreak() {
      const div = document.createElement('div');
      div.className = 'sim-section-break';
      div.contentEditable = 'true';
      div.textContent = 'شکست بخش (Section Break — شبیه‌سازی آموزشی)';
      insertNodeAtCaret(div);
      setDirty(true);
      alert('نشانه شکست بخش اضافه شد. این نسخه هنوز رفتار کامل Section Break در Word را شبیه‌سازی نمی‌کند.');
    }

    function getCurrentCell() {
      const sel = window.getSelection();
      if (!sel || !sel.rangeCount) return null;
      let node = sel.anchorNode;
      if (node && node.nodeType === Node.TEXT_NODE) node = node.parentElement;
      return node && node.closest ? node.closest('#editor td, #editor th') : null;
    }

    function addTableRow() {
      const cell = getCurrentCell();
      if (!cell) { alert('ابتدا داخل یکی از سلول‌های جدول کلیک کنید.'); return; }
      const row = cell.parentElement;
      const table = row.closest('table');
      const newRow = row.cloneNode(true);
      newRow.querySelectorAll('td,th').forEach(c => c.textContent = 'متن');
      row.parentElement.insertBefore(newRow, row.nextSibling);
      setDirty(true);
    }

    function deleteTableRow() {
      const cell = getCurrentCell();
      if (!cell) { alert('ابتدا داخل یکی از سلول‌های جدول کلیک کنید.'); return; }
      const row = cell.parentElement, table = row.closest('table');
      if (table.rows.length <= 1) { alert('جدول باید دست‌کم یک سطر داشته باشد.'); return; }
      row.remove(); setDirty(true);
    }

    function mergeTableCells() {
      const cell = getCurrentCell();
      if (!cell) { alert('داخل جدول کلیک کنید. برای تمرین ادغام، دو سلول مجاور یک سطر را انتخاب کنید.'); return; }
      const row = cell.parentElement;
      const cells = [...row.cells];
      const idx = cells.indexOf(cell);
      if (idx < 0 || idx + 1 >= cells.length) { alert('سلول انتخاب‌شده، سلول مجاور برای ادغام ندارد.'); return; }
      const next = cells[idx + 1];
      cell.colSpan = (cell.colSpan || 1) + (next.colSpan || 1);
      cell.textContent = (cell.textContent + ' ' + next.textContent).trim();
      next.remove(); setDirty(true);
    }

    function splitTableCell() {
      const cell = getCurrentCell();
      if (!cell) { alert('ابتدا داخل سلول جدول کلیک کنید.'); return; }
      const row = cell.parentElement;
      const newCell = cell.cloneNode(false);
      newCell.textContent = 'متن';
      cell.colSpan = 1;
      row.insertBefore(newCell, cell.nextSibling);
      setDirty(true);
    }

    const textbookPractices = {
      format: {
        title: 'قالب‌بندی متن',
        instruction: 'این جمله را در سند بنویسید: «ساختن محصولاتی که مردم دوست دارند». عبارت را ضخیم (Bold)، مورب (Italic) و زیرخط‌دار کنید؛ سپس رنگ متن را تغییر دهید.',
        check: e => ({ ok: /ساختن محصولات|ساختن محصولاتی/.test(e.innerText) && !!e.querySelector('b,strong') && !!e.querySelector('i,em') && !!e.querySelector('u'), msg: 'بررسی: متن نمونه و قالب‌های Bold، Italic و Underline در سند جست‌وجو شد.' })
      },
      paragraph: {
        title: 'پاراگراف و فهرست',
        instruction: 'یک پاراگراف فارسی وارد کنید، راست‌چین یا Justify کنید و یک فهرست حداقل سه‌موردی بولت‌دار یا شماره‌دار بسازید.',
        check: e => ({ ok: !!e.querySelector('ul li,ol li') && !!e.querySelector('p[style*="text-align"],div[style*="text-align"]'), msg: 'بررسی: وجود فهرست و نشانه تراز پاراگراف بررسی شد. ترازبندی بصری ممکن است در همه مرورگرها به‌طور کامل قابل تشخیص نباشد.' })
      },
      table: {
        title: 'جدول هنرجویان',
        instruction: 'یک جدول حداقل ۳ ستونی و ۳ سطری بسازید و عنوان ستون‌ها را «ردیف»، «نام و نام خانوادگی» و «کد هنرجویی» قرار دهید. سپس یک سطر اضافه کنید.',
        check: e => ({ ok: [...e.querySelectorAll('table')].some(t => t.rows.length >= 3 && t.rows[0].cells.length >= 3), msg: 'بررسی: حداقل یک جدول با ۳ سطر و ۳ ستون جست‌وجو شد.' })
      },
      picture: {
        title: 'تصویر و شکل',
        instruction: 'از زبانه Insert یک تصویر از رایانه درج کنید و سپس یک شکل مستطیل یا دایره اضافه کنید.',
        check: e => ({ ok: !!e.querySelector('img') && !![...e.querySelectorAll('div,span')].find(n => /background:\s*#2b579a|border-radius:\s*50%/i.test(n.getAttribute('style') || '')), msg: 'بررسی: وجود تصویر و یک شکل گرافیکی در سند جست‌وجو شد.' })
      },
      page: {
        title: 'صفحه‌آرایی',
        instruction: 'اندازه کاغذ را روی وزیری یا رقعی بگذارید، حاشیه صفحه را تغییر دهید، واترمارک «سؤالات آزمون عملی» درج کنید و شماره صفحه را اضافه کنید.',
        check: e => ({ ok: ['Vaziri','Raghi'].includes(e.dataset.paperSize) && !!e.querySelector('#docWatermark') && /صفحه/.test(e.innerText), msg: 'بررسی: اندازه کاغذ انتخاب‌شده، واترمارک و نشانه شماره صفحه بررسی شد.' })
      },
      review: {
        title: 'بازبینی و نظر',
        instruction: 'یک جمله وارد کنید، بخشی از آن را انتخاب کنید و از Review گزینه New Comment را بزنید. سپس حالت Track Changes را روشن و خاموش کنید.',
        check: e => ({ ok: !!e.querySelector('[data-comment],.sim-comment') && !!e.dataset.trackChanges, msg: 'بررسی: وجود یادداشت و وضعیت Track Changes بررسی شد؛ خاموش‌کردن آن ممکن است وضعیت را از بین ببرد.' })
      },
      toc: {
        title: 'عنوان‌ها و فهرست مطالب',
        instruction: 'با Heading 1 و Heading 2 حداقل دو عنوان بسازید؛ سپس References > Table of Contents را اجرا کنید و فهرست را به‌روزرسانی کنید.',
        check: e => ({ ok: e.querySelectorAll('h1,h2,h3').length >= 2 && !!e.querySelector('[data-sim-toc="true"],a[href^="#heading-"]'), msg: 'بررسی: دو عنوان و نشانه فهرست مطالب جست‌وجو شد.' })
      },
      mail: {
        title: 'ادغام پستی',
        instruction: 'از زبانه Mailings فیلدهای «نام» و «نام خانوادگی» را وارد کنید و پیش‌نمایش نتایج را ببینید. این نسخه داده‌های نمونه دارد و به فایل Excel واقعی متصل نیست.',
        check: e => ({ ok: e.querySelectorAll('[data-merge-field]').length >= 2, msg: 'بررسی: حداقل دو فیلد ادغام پستی در سند جست‌وجو شد.' })
      }
    };

    function loadPractice() {
      const key = document.getElementById('practiceSelect').value;
      const p = textbookPractices[key];
      document.getElementById('practiceInstructions').innerHTML = '<strong>' + p.title + '</strong><br>' + p.instruction;
      document.getElementById('practiceFeedback').textContent = '';
    }

    function checkPractice() {
      const key = document.getElementById('practiceSelect').value;
      const p = textbookPractices[key];
      const result = p.check(document.getElementById('editor'));
      const feedback = document.getElementById('practiceFeedback');
      feedback.textContent = (result.ok ? '✓ انجام شد — ' : '△ نیاز به تکمیل — ') + result.msg;
      feedback.style.color = result.ok ? '#107c41' : '#a4262c';
    }

    function manageMailingList() {
      const raw = prompt('اطلاعات نمونه گیرندگان را هر نفر در یک خط وارد کنید؛ نام و نام خانوادگی را با ویرگول جدا کنید:', 'علی,احمدی\\nسارا,محمدی');
      if (raw === null) return;
      window.simMailingList = raw.split(/\\n/).map(line => line.split(',').map(x => x.trim())).filter(row => row.some(Boolean));
      alert('فهرست نمونه گیرندگان ذخیره شد: ' + window.simMailingList.length + ' نفر. اتصال به Excel/Access در این نسخه وجود ندارد.');
    }

    function createLabels() {
      const t = prompt('متن برچسب را وارد کنید:', 'نام: علی احمدی\\nنشانی: تهران');
      if (t === null) return;
      const grid = document.createElement('table');
      grid.style.cssText = 'width:100%;border-collapse:collapse;margin:10px 0';
      for (let r=0;r<4;r++) {
        const tr=document.createElement('tr');
        for(let c=0;c<2;c++) {
          const td=document.createElement('td');
          td.style.cssText='border:1px dashed #888;width:50%;height:55px;padding:8px;vertical-align:top';
          td.textContent=t;
          tr.appendChild(td);
        }
        grid.appendChild(tr);
      }
      insertNodeAtCaret(grid); setDirty(true);
    }

    function createEnvelope() {
      const to = prompt('نشانی گیرنده پاکت:', '');
      if (to === null) return;
      const from = prompt('نشانی فرستنده:', '');
      if (from === null) return;
      const d=document.createElement('div');
      d.style.cssText='border:1px solid #888;width:240mm;max-width:100%;min-height:100mm;padding:15mm;box-sizing:border-box;margin:12px auto;position:relative';
      const sender=document.createElement('div');sender.textContent='فرستنده: '+from;sender.style.cssText='font-size:10pt;color:#666';
      const recipient=document.createElement('div');recipient.textContent='گیرنده: '+to;recipient.style.cssText='margin:25mm 0 0 30mm;font-size:14pt';
      d.append(sender,recipient);insertNodeAtCaret(d);setDirty(true);
    }

    // افزودن نشانه نظر به شکل قابل تشخیص برای تمرین
    const originalInsertComment = insertComment;
    insertComment = function() {
      const t = prompt('نظر آموزشی برای متن انتخاب‌شده:');
      if (t === null) return;
      const sel = window.getSelection();
      if (sel && !sel.isCollapsed && sel.rangeCount) {
        const span = document.createElement('span');
        span.className = 'sim-comment';
        span.dataset.comment = 'true';
        span.title = t;
        span.textContent = sel.toString();
        const range = sel.getRangeAt(0);
        range.deleteContents(); range.insertNode(span);
        insertNodeAtCaret(document.createTextNode(''));
      } else {
        const span = document.createElement('span');
        span.className = 'sim-comment'; span.dataset.comment = 'true';
        span.textContent = '[نظر: ' + t + ']'; span.title = t;
        insertNodeAtCaret(span);
      }
      setDirty(true);
    };


    // نگه‌داشتن متن انتخاب‌شده هنگام استفاده از ابزارها و میانبرهای رایج
    document.addEventListener('keydown',e=>{
      const mod = e.ctrlKey || e.metaKey;
      if(mod && e.key.toLowerCase()==='s'){e.preventDefault();saveDocument();}
      if(mod && e.key.toLowerCase()==='z'){e.preventDefault();execCmd('undo');}
      if(mod && e.key.toLowerCase()==='y'){e.preventDefault();execCmd('redo');}
      if(mod && e.key.toLowerCase()==='b'){e.preventDefault();execCmd('bold');}
      if(mod && e.key.toLowerCase()==='i'){e.preventDefault();execCmd('italic');}
      if(mod && e.key.toLowerCase()==='u'){e.preventDefault();execCmd('underline');}
      if(e.key==='Escape'){closeBackstage();hideTablePicker();}
    });
    // شمارش وضعیت در شروع و بازیابی ایمن متن تمرینی از همین نشست
    document.addEventListener('DOMContentLoaded',()=>{updateStatus();});

  </script>
</body>
</html>
