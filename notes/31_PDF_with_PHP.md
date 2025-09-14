# Chapter 31 – PDF with PHP

## Sections
1. Preparation  
2. TCPDF  
3. FPDF  
4. Haru  

---

## Summary
This chapter introduces ways to **generate and manipulate PDF documents with PHP**.  
PDF generation is important in web applications for invoices, reports, contracts, and downloadable documents.  

---

## Key Concepts

### 1. Preparation
- PHP does not natively support PDF generation.  
- Several libraries and extensions are available.  
- Key features often include:  
  - Text and image rendering.  
  - Tables, charts, and styled elements.  
  - Page headers, footers, and metadata.  
  - UTF-8 / Unicode support.  

---

### 2. TCPDF
- One of the most widely used **open-source PHP libraries** for PDF generation.  
- Actively maintained and feature-rich.  
- Supports:  
  - UTF-8 and right-to-left languages.  
  - HTML to PDF conversion (basic).  
  - Images, barcodes, QR codes.  

Example:  
```php
require_once('tcpdf.php');
$pdf = new TCPDF();
$pdf->AddPage();
$pdf->SetFont('helvetica', '', 12);
$pdf->Write(0, 'Hello from TCPDF!');
$pdf->Output('example.pdf', 'I');
```

---

### 3. FPDF

* Lightweight PHP class for PDF creation.
* Easier to learn, fewer dependencies.
* Basic features compared to TCPDF.
* Extensions exist (e.g., FPDI to import existing PDFs).

Example:

```php
require('fpdf.php');
$pdf = new FPDF();
$pdf->AddPage();
$pdf->SetFont('Arial', 'B', 16);
$pdf->Cell(40, 10, 'Hello FPDF!');
$pdf->Output();
```

---

### 4. Haru

* PHP binding for the **libHaru PDF library** (written in C).
* High performance and low-level PDF manipulation.
* Not as commonly used in web apps (fewer tutorials, less ecosystem).
* Good for projects needing fine-grained PDF control.

---

## Notes

* **TCPDF**: best choice for modern, complex PDF needs (reports, invoices).
* **FPDF**: good for lightweight, simple tasks.
* **Haru**: niche, powerful, but less community support.
* Consider Unicode and HTML support if working with multilingual documents.