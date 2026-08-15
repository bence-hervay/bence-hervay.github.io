---
layout: page
permalink: /cv/
title: cv
nav: true
nav_order: 1
# This page still lives and builds at /cv/ (a reverse proxy forwards
# cv.bence.io/* here); only the nav link target changes.
nav_external_url: https://cv.bence.io/
# SLOT — one line under the page title.
description:
---

<!--
  Deliberately minimal: an embedded PDF viewer and a download link, nothing
  else. The rendered Contact/Summary/Experience/etc. sections that used to be
  generated from _data/cv.yml have been removed on purpose (that file is kept
  around but is no longer rendered on this page).

  The src/href below are absolute (https://bence.io/cv.pdf), not a relative
  /cv.pdf: this page is reverse-proxied and served under cv.bence.io too, and
  a relative path would resolve against that host instead of the one true
  address of the PDF, which always stays bence.io/cv.pdf.
-->

<div class="cv">
  <div class="card mt-3 p-3">
    <p>
      <a
        href="https://bence.io/cv.pdf"
        class="btn btn-outline-primary"
        download
        target="_blank"
        rel="noopener noreferrer"
      >
        <i class="fa-solid fa-file-pdf"></i> Download the CV as a PDF
      </a>
    </p>
    <embed
      src="https://bence.io/cv.pdf"
      type="application/pdf"
      style="width: 100%; height: 85vh; border: 1px solid rgba(128, 128, 128, 0.3); border-radius: 4px;"
    />
    <p class="text-muted mt-2" style="font-size: 0.85em;">
      If the PDF does not display above (some mobile browsers cannot embed
      PDFs), use the download link.
    </p>
  </div>
</div>
