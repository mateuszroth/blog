---
title: "Frontend - printing documents"
tags:
  - Frontend
categories:
  - [Frontend, Other]
date: 2020-07-17 20:00:00
---

# Print `iframe`

JS:

```
window.frames["printf"].focus();
window.frames["printf"].print();
```

HTML:

```
<iframe id="printf" name="printf"></iframe>
```

JS:

```
document.getElementById("printf").contentWindow.print()​​​​​​;
```

More: https://stackoverflow.com/questions/9616426/javascript-print-iframe-contents-only

# Print `div`

```js
function printDiv(divName) {
  var printContents = document.getElementById(divName).innerHTML;
  var originalContents = document.body.innerHTML;

  document.body.innerHTML = printContents;

  window.print();

  document.body.innerHTML = originalContents;
}
```

# `jspdf` nie nadaje się do robienia plików HTML

More: https://cdn.rawgit.com/MrRio/jsPDF/master/examples/html2pdf/showcase_supported_html.html

# My implementation

```js
import replace from "lodash/replace";
import { getDataBase64String, MIME_HTML } from "../constants/mimeTypes";

export const REPLACE_SCRIPT = `
<script>
  window.loadPrint = function loadPrint() {
    window.print();
    setTimeout(function () { window.close(); document.clear(); document.close(); }, 100);
  }

  window.onload = function() { window.loadPrint(); }
</script>
`;
const HTML_TAG = "</html>";
const HTML_TAG_CAPITALIZED = "</HTML>";

function printHtmlDocument(dataBase64Source, iframeElement) {
  const dataBase64Prefix = getDataBase64String(MIME_HTML);
  const base64Source = dataBase64Source.slice(dataBase64Prefix.length);
  const source = atob(base64Source);

  const hasHtmlTag = source.indexOf(HTML_TAG) > -1;
  const hasCapitalizedHtmlTag = source.indexOf(HTML_TAG_CAPITALIZED) > -1;

  let processedHtml;

  if (hasHtmlTag && !hasCapitalizedHtmlTag) {
    processedHtml = replace(source, HTML_TAG, REPLACE_SCRIPT + HTML_TAG);
  } else if (!hasHtmlTag && hasCapitalizedHtmlTag) {
    processedHtml = replace(
      source,
      HTML_TAG_CAPITALIZED,
      REPLACE_SCRIPT + HTML_TAG_CAPITALIZED
    );
  }

  if (!processedHtml) {
    processedHtml = source + REPLACE_SCRIPT;
  }

  const processedBase64Source = btoa(processedHtml);
  const processedDataBase64Source = dataBase64Prefix + processedBase64Source;

  const iframe = iframeElement || document.createElement("iframe");
  iframe.src = processedDataBase64Source;
  iframe.height = "0";
  iframe.width = "0";
  iframe.title = "";
  document.body.appendChild(iframe);
  setTimeout(() => iframe.remove(), 1000);

  return {
    html: processedHtml,
    dataBase64: processedDataBase64Source,
    iframe: iframe,
  };
}

export default printHtmlDocument;
```

## Tests

```js
import printHtmlDocument, { REPLACE_SCRIPT } from "./printHtmlDocument";
import { DATA_MIME_HTML_BASE64 } from "../constants/mimeTypes";

describe("printHtmlDocument", () => {
  const HTML = "<html><body>Hello</body></html>";
  const HTML_EXPECTED = `<html><body>Hello</body>${REPLACE_SCRIPT}</html>`;
  const SOURCE = DATA_MIME_HTML_BASE64 + btoa(HTML);
  const SOURCE_EXPECTED = DATA_MIME_HTML_BASE64 + btoa(HTML_EXPECTED);

  test("it should return properly modified HTML with included REPLACE_SCRIPT script", () => {
    expect(printHtmlDocument(SOURCE).html).toEqual(HTML_EXPECTED);
  });

  test("it should return properly modified BASE64 source", () => {
    expect(printHtmlDocument(SOURCE).dataBase64).toEqual(SOURCE_EXPECTED);
  });

  test("it should create iframe element with proper attributes", () => {
    const result = printHtmlDocument(SOURCE);
    expect(result.iframe.src).toEqual(SOURCE_EXPECTED);
    expect(result.iframe.height).toEqual("0");
    expect(result.iframe.width).toEqual("0");
    expect(result.iframe.title).toEqual("");
  });
});
```
