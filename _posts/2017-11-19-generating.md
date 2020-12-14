---
title: Generating a PDF
author: PipisCrew
date: 2017-11-19
categories: [php]
toc: true
---

> Office Style

<span style="color: #ff0000;">**Office Document Converter (ODC)**</span>
Is an online convertor for office document which runs as a web service. Its aim is to provide the facility of converting almost all office documents into image which make office documents viewable even without any office suite software installed on your machines.
ps: edit resources/config.php, the server must have at php.ini the *allow_url_fopen* true
[http://github.com/chellem/Office-Document-Converter](http://github.com/chellem/Office-Document-Converter)

<span style="color: #ff0000;">**PHPWord (2014)**</span>
Is a library written in pure PHP that provides a set of classes to write to and read from different document file formats. The current version of PHPWord supports Microsoft Office Open XML (OOXML or OpenXML), OASIS Open Document Format for Office Applications (OpenDocument or ODF), Rich Text Format (RTF), HTML, and PDF.
[http://github.com/PHPOffice/PHPWord](http://github.com/PHPOffice/PHPWord)

<span style="color: #ff0000;">**PHPExcel (2014)**</span>
Read, Write and Create Excel documents in PHP - Spreadsheet engine
[http://phpexcel.codeplex.com/](http://phpexcel.codeplex.com/)

<span style="color: #ff0000;">**PHPPowerPoint (2014)**</span>
Is a library written in pure PHP that provides a set of classes to write to different presentation file formats, i.e. Microsoft Office Open XML (OOXML or OpenXML) or OASIS Open Document Format for Office Applications (OpenDocument or ODF).
[http://github.com/PHPOffice/PHPPowerPoint](https://github.com/PHPOffice/PHPPowerPoint)

<span style="color: #ff0000;">**PHPWord (2011)**</span>
Is a library written in PHP that create word documents. No Windows operating system is needed for usage because the result are docx files (Office Open XML) that can be opened by all major office software.
[http://phpword.codeplex.com/](http://phpword.codeplex.com/)

> PDF

<span style="color: #ff0000;">**Digital Format Conversion tools**</span> enable conversion from Microsoft Word (2007+) DOCX format or HTML to EPUB, Kindle and PDF in PHP.

The tools are constructed from a range of Open Source elements, including:

*   EPub PHP class (http://www.phpclasses.org/package/6115)

*   phpMobi (https://github.com/raiju/phpMobi)

*   mPDF (http://www.mpdf1.com/mpdf/)

*   PHPDOCX (http://www.phpdocx.com/)

*   Twitter Bootstrap (http://twitter.github.com/bootstrap/)

A copy of the source code for these elements are available in /library

[http://github.com/benskay/PHP-Digital-Format-Convert-Epub-Mobi-PDF](http://github.com/benskay/PHP-Digital-Format-Convert-Epub-Mobi-PDF)

<span style="color: #ff0000;">**mPDF**</span> is a PHP class which generates PDF files from UTF-8 encoded HTML

[http://www.mpdf1.com/mpdf/index.php](http://www.mpdf1.com/mpdf/index.php)

<span style="color: #ff0000;">**FPDFF**</span> is a PHP class which allows to generate PDF files with pure PHP, that is to say without using the PDFlib library

[http://www.fpdf.org/](http://www.fpdf.org/)
<span style="color: #ff0000;">**TCPDF**</span> PHP class for generating PDF documents

[http://www.tcpdf.org/](http://www.tcpdf.org/)

<span style="color: #ff0000;">**unoconv** </span>convert between any document format supported by OpenOffice. Is written in **p**ytho**n**. It **needs** a recent LibreOffice or OpenOffice with UNO bindings.

[http://dag.wiee.rs/home-made/unoconv/](http://dag.wiee.rs/home-made/unoconv/)

<span style="color: #ff0000;">**Zend_Service_LiveDocx_MailMerge** </span>is a SOAP service (aka **<span style="color: #ff9900;">http://api.livedocx.com</span>**) that allows developers to generate word processing documents by combining structured data from PHP with a template, created in a word processor.

Template File Formats (input) : doc / docx / rtf / txd
Document File Formats (output): doc / docx / rtf / txd / html / txt / pdf

[http://framework.zend.com/manual/1.12/en/zend.service.livedocx.html](http://framework.zend.com/manual/1.12/en/zend.service.livedocx.html)

talk direct to <span style="color: #ff9900;">**http://api.livedocx.com**</span> without the Zend -> [http://www.phplivedocx.org/articles/using-livedocx-without-the-zend-framework/](http://www.phplivedocx.org/articles/using-livedocx-without-the-zend-framework/)

stripped down version of sample#1
a test.docx must be near php file, with fields applied aka 
![](https://www.pipiscrew.com/wp-content/uploads/2014/11/snap169.png "snap169")
```js
<?php turn="" up="" error="" reporting="" error_reporting="" (e_all|e_strict);="" turn="" off="" wsdl="" caching="" ini_set="" ('soap.wsdl_cache_enabled',="" 0);="" define="" credentials="" for="" ld="" dsefine="" ('username',="" 'x');="" your="" username="" define="" ('password',="" 'x');="" your="" password=""?><- register="" to="" their="" portal="" first="" www.livedocx.com="" soap="" wsdl="" endpoint="" define="" ('endpoint',="" 'https://api.livedocx.com/1.2/mailmerge.asmx?wsdl');="" define="" timezone="" date_default_timezone_set('europe/berlin');="" print('starting="" sample="" #1="" (license-agreement)...');="" instantiate="" soap="" object="" and="" log="" into="" livedocx="" $soap="new" soapclient(endpoint);="" $soap-="">LogIn(
    array(
        'username' => USERNAME,
        'password' => PASSWORD
    )
);

// Upload template

$data = file_get_contents('test.doc');
//license-agreement-template.docx');

$soap->SetLocalTemplate(
    array(
        'template' => base64_encode($data),
        'format'   => 'docx'
    )
);

// Assign data to template

$fieldValues = array (
    'software' => 'x',
    'licensee' => 'x',
    'company'  => 'x Co-Operation',
    'date'     => date('F d, Y'),
    'time'     => date('H:i:s'),
    'city'     => 'x',
    'country'  => 'x'
);

$soap->SetFieldValues(
    array (
        'fieldValues' => assocArrayToArrayOfArrayOfString($fieldValues)
    )
);

// Build the document

$soap->CreateDocument();

// Get document as PDF

$result = $soap->RetrieveDocument(
    array(
        'format' => 'pdf'
    )
);

$data = $result->RetrieveDocumentResult;
 //echo $result;

//write near test.docx 
file_put_contents('test.pdf', base64_decode($data));
?>
```

<span style="color: #ff0000;">**jsPDF** </span>a HTML5 client-side solution for generating PDFs. Perfect for event tickets, reports, certificates, you name it!
[https://parall.ax/products/jspdf](https://parall.ax/products/jspdf)

<span style="color: #ff0000;">**flip.swf**</span>
http://bit.ly/1vv5Cn0
http://www.boxoft.com/pdf-to-flash/
Provides a quick and easy way to batch convert ordinary PDF files into stunning Flash & HTML5 - See more at: http://www.flipbuilder.com/flip-pdf/

<span style="color: #ff0000;">**iPaper**</span>

homepage - [http://www.ipaper-cms.com/](http://www.ipaper-cms.com/)
sample - [http://tupperware.ipapercms.dk/Tupperware/Greece/2014/TW14AWGR/](http://tupperware.ipapercms.dk/Tupperware/Greece/2014/TW14AWGR/)</->

origin - http://www.pipiscrew.com/?p=1832 php-pdf