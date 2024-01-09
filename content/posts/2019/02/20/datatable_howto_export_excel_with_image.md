---
title: "Datatable: howto export excel with image"
date: 2019-02-20T16:17:29-06:00
draft: flase
toc: true
tags:
  - Development
  - Backend
categories:
  - Engineer
languages:
  - en
---

At some point the project I was working on requieres to export excel from datatable with the logo of the company, here I describe my path to get an image when export data from tables usign datatable.

First of all, there's no click download button with the file or code you need, and I'm not a JS experienced programmer so maybe I'm breaking some JS rules of code.

## Show me the code

The file we need to modify is `buttons.html5.js`, this file `Copy to clipboard and create Excel, PDF and CSV files from the table's data.` and stuff.

The basic structure for a valid excel file .xlsx is this:

```javascript
var xlsx = {
  _rels: {
    ".rels": getXml('_rels/.rels')
  },
  xl: {
    _rels: {
      "workbook.xml.rels": getXml('xl/_rels/workbook.xml.rels')
    },
    "workbook.xml": getXml('xl/workbook.xml'),
    "styles.xml": getXml('xl/styles.xml'),
    "worksheets": {
      "sheet1.xml": rels
    }

  },
  "[Content_Types].xml": getXml('[Content_Types].xml')
};
```

And yes! The .xlsx file is a bunch of other files (yeah! like a zip file), some xml and .rels files. But for images we need to zip other files with the rigth estructure, at this point we start to open all our .xlsx files with winrar or zip insteand of excel. (A lot of try-error comes...)

### New Basic structure .xlsx

we need something like this:

```javascript
var xlsx = {
  _rels: {
    ".rels": getXml('_rels/.rels')
  },
  "docProps": {
    "app.xml": getXml('docProps/app.xml'),
    "core.xml": getXml('docProps/core.xml')
  },
  xl: {
    _rels: {
      "workbook.xml.rels": getXml('xl/_rels/workbook.xml.rels')
    },
    "workbook.xml": getXml('xl/workbook.xml'),
    "styles.xml": getXml('xl/styles.xml'),
    "sharedStrings.xml": getXml('xl/sharedStrings.xml'),
    "theme": {
      "theme1.xml": getXml('xl/theme/theme1.xml')
    },
    "worksheets": {
      "sheet1.xml": rels,
      "_rels": {
          "sheet1.xml.rels": getXml('xl/worksheets/_rels/sheet1.xml.rels')
        }
    },
      "drawings": {
        "drawing1.xml" :  getXml('xl/drawings/drawing1.xml'),
        "_rels": {
          "drawing1.xml.rels": getXml('xl/drawings/_rels/drawing1.xml.rels')
        },
      },
      media: {

      }
  },
  "[Content_Types].xml": getXml('[Content_Types].xml')
};
```

Important changes, the `drawings` and `media` dirs, other new files added are requiered to support office365. `media` contains the images and `drawings` contains the xml files with especifications of where, how and what.

Time to open another bunch of excel files and extract the content from the xml needed, find the var `excelStrings` where the content of every file zipped in the xlsx are listed, like this

```javascript
// Excel - Pre-defined strings to build a basic XLSX file
var excelStrings = {
  "_rels/.rels":
    '<?xml version="1.0" encoding="UTF-8" standalone="yes"?>'+
    '<Relationships xmlns="http://schemas.openxmlformats.org/package/2006/relationships">'+
    '<Relationship Id="rId3" Type="http://schemas.openxmlformats.org/officeDocument/2006/relationships/extended-properties" Target="docProps/app.xml" />'+
    '<Relationship Id="rId2" Type="http://schemas.openxmlformats.org/package/2006/relationships/metadata/core-properties" Target="docProps/core.xml" />'+
    '<Relationship Id="rId1" Type="http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument" Target="xl/workbook.xml" />'+
    '</Relationships>',

  "xl/_rels/workbook.xml.rels":
    '<?xml version="1.0" encoding="UTF-8" standalone="yes"?>'+
    '<Relationships xmlns="http://schemas.openxmlformats.org/package/2006/relationships">'+
      '<Relationship Id="rId3" Type="http://schemas.openxmlformats.org/officeDocument/2006/relationships/styles" Target="styles.xml"/>'+
      '<Relationship Id="rId2" Type="http://schemas.openxmlformats.org/officeDocument/2006/relationships/theme" Target="theme/theme1.xml"/>'+
      '<Relationship Id="rId1" Type="http://schemas.openxmlformats.org/officeDocument/2006/relationships/worksheet" Target="worksheets/sheet1.xml"/>'+
      '<Relationship Id="rId4" Type="http://schemas.openxmlformats.org/officeDocument/2006/relationships/sharedStrings" Target="sharedStrings.xml"/>'+
    '</Relationships>',

  "[Content_Types].xml":
    '<?xml version="1.0" encoding="UTF-8" standalone="yes"?>'+
    '<Types xmlns="http://schemas.openxmlformats.org/package/2006/content-types">'+
      '<Default Extension="jpg" ContentType="image/jpeg" />'+
      '<Default  Extension="wmf" ContentType="image/x-wmf"/>'+
      '<Default  Extension="png" ContentType="image/png"/>'+
      '<Default Extension="rels" ContentType="application/vnd.openxmlformats-package.relationships+xml" />'+
      '<Default Extension="xml" ContentType="application/xml" />'+
      '<Override PartName="/docProps/app.xml" ContentType="application/vnd.openxmlformats-officedocument.extended-properties+xml"/>'+
      '<Override PartName="/docProps/core.xml" ContentType="application/vnd.openxmlformats-package.core-properties+xml"/>'+
      '<Override PartName="/xl/sharedStrings.xml" ContentType="application/vnd.openxmlformats-officedocument.spreadsheetml.sharedStrings+xml"/>'+
      '<Override PartName="/xl/worksheets/sheet1.xml" ContentType="application/vnd.openxmlformats-officedocument.spreadsheetml.worksheet+xml" />'+
      '<Override PartName="/xl/drawings/drawing1.xml" ContentType="application/vnd.openxmlformats-officedocument.drawing+xml"/>'+
      '<Override PartName="/xl/theme/theme1.xml" ContentType="application/vnd.openxmlformats-officedocument.theme+xml"/>'+
      '<Override PartName="/xl/styles.xml" ContentType="application/vnd.openxmlformats-officedocument.spreadsheetml.styles+xml" />'+
      '<Override PartName="/xl/workbook.xml" ContentType="application/vnd.openxmlformats-officedocument.spreadsheetml.sheet.main+xml" />'+
    '</Types>',
  
  "xl/sharedStrings.xml":
    '<?xml version="1.0" encoding="UTF-8" standalone="yes"?>'+
    '<sst xmlns="http://schemas.openxmlformats.org/spreadsheetml/2006/main" count="3" uniqueCount="3">'+
    '<si>'+
    '<t>'+
    '</t>'+
    '</si>'+
    '</sst>',

  "xl/workbook.xml":
    '<?xml version="1.0" encoding="UTF-8" standalone="yes"?>'+
    '<workbook xmlns="http://schemas.openxmlformats.org/spreadsheetml/2006/main" xmlns:r="http://schemas.openxmlformats.org/officeDocument/2006/relationships">'+
      '<fileVersion appName="xl" lastEdited="5" lowestEdited="5" rupBuild="24816"/>'+
      '<workbookPr showInkAnnotation="0" autoCompressPictures="0"/>'+
      '<bookViews>'+
        '<workbookView xWindow="0" yWindow="0" windowWidth="25600" windowHeight="19020" tabRatio="500"/>'+
      '</bookViews>'+
      '<sheets>'+
        '<sheet name="" sheetId="1" r:id="rId1"/>'+
      '</sheets>'+
    '</workbook>',

  "xl/worksheets/sheet1.xml":
    '<?xml version="1.0" encoding="UTF-8" standalone="yes"?>'+
    '<worksheet xmlns="http://schemas.openxmlformats.org/spreadsheetml/2006/main" xmlns:r="http://schemas.openxmlformats.org/officeDocument/2006/relationships" xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006" mc:Ignorable="x14ac" xmlns:x14ac="http://schemas.microsoft.com/office/spreadsheetml/2009/9/ac">'+
      '<sheetData/>'+
      '<mergeCells count="0"/>'+
      '<drawing r:id="rId1"/>'+
    '</worksheet>',

  "xl/styles.xml":
    '<?xml version="1.0" encoding="UTF-8"?>'+
    '<styleSheet xmlns="http://schemas.openxmlformats.org/spreadsheetml/2006/main" xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006" mc:Ignorable="x14ac" xmlns:x14ac="http://schemas.microsoft.com/office/spreadsheetml/2009/9/ac">'+
      '<numFmts count="6">'+
        '<numFmt numFmtId="164" formatCode="#,##0.00_-\ [$$-45C]"/>'+
        '<numFmt numFmtId="165" formatCode="&quot;£&quot;#,##0.00"/>'+
        '<numFmt numFmtId="166" formatCode="[$€-2]\ #,##0.00"/>'+
        '<numFmt numFmtId="167" formatCode="0.0%"/>'+
        '<numFmt numFmtId="168" formatCode="#,##0;(#,##0)"/>'+
        '<numFmt numFmtId="169" formatCode="#,##0.00;(#,##0.00)"/>'+
      '</numFmts>'+
      '<fonts count="5" x14ac:knownFonts="1">'+
        '<font>'+
          '<sz val="11" />'+
          '<name val="Calibri" />'+
        '</font>'+
        '<font>'+
          '<sz val="11" />'+
          '<name val="Calibri" />'+
          '<color rgb="FFFFFFFF" />'+
        '</font>'+
        '<font>'+
          '<sz val="11" />'+
          '<name val="Calibri" />'+
          '<b />'+
        '</font>'+
        '<font>'+
          '<sz val="11" />'+
          '<name val="Calibri" />'+
          '<i />'+
        '</font>'+
        '<font>'+
          '<sz val="11" />'+
          '<name val="Calibri" />'+
          '<u />'+
        '</font>'+
      '</fonts>'+
      '<fills count="6">'+
        '<fill>'+
          '<patternFill patternType="none" />'+
        '</fill>'+
        '<fill>'+ // Excel appears to use this as a dotted background regardless of values but
          '<patternFill patternType="none" />'+ // to be valid to the schema, use a patternFill
        '</fill>'+
        '<fill>'+
          '<patternFill patternType="solid">'+
            '<fgColor rgb="FFD9D9D9" />'+
            '<bgColor indexed="64" />'+
          '</patternFill>'+
        '</fill>'+
        '<fill>'+
          '<patternFill patternType="solid">'+
            '<fgColor rgb="FFD99795" />'+
            '<bgColor indexed="64" />'+
          '</patternFill>'+
        '</fill>'+
        '<fill>'+
          '<patternFill patternType="solid">'+
            '<fgColor rgb="ffc6efce" />'+
            '<bgColor indexed="64" />'+
          '</patternFill>'+
        '</fill>'+
        '<fill>'+
          '<patternFill patternType="solid">'+
            '<fgColor rgb="ffc6cfef" />'+
            '<bgColor indexed="64" />'+
          '</patternFill>'+
        '</fill>'+
      '</fills>'+
      '<borders count="2">'+
        '<border>'+
          '<left />'+
          '<right />'+
          '<top />'+
          '<bottom />'+
          '<diagonal />'+
        '</border>'+
        '<border diagonalUp="false" diagonalDown="false">'+
          '<left style="thin">'+
            '<color auto="1" />'+
          '</left>'+
          '<right style="thin">'+
            '<color auto="1" />'+
          '</right>'+
          '<top style="thin">'+
            '<color auto="1" />'+
          '</top>'+
          '<bottom style="thin">'+
            '<color auto="1" />'+
          '</bottom>'+
          '<diagonal />'+
        '</border>'+
      '</borders>'+
      '<cellStyleXfs count="1">'+
        '<xf numFmtId="0" fontId="0" fillId="0" borderId="0" />'+
      '</cellStyleXfs>'+
      '<cellXfs count="67">'+
        '<xf numFmtId="0" fontId="0" fillId="0" borderId="0" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="1" fillId="0" borderId="0" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="2" fillId="0" borderId="0" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="3" fillId="0" borderId="0" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="4" fillId="0" borderId="0" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="0" fillId="2" borderId="0" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="1" fillId="2" borderId="0" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="2" fillId="2" borderId="0" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="3" fillId="2" borderId="0" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="4" fillId="2" borderId="0" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="0" fillId="3" borderId="0" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="1" fillId="3" borderId="0" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="2" fillId="3" borderId="0" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="3" fillId="3" borderId="0" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="4" fillId="3" borderId="0" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="0" fillId="4" borderId="0" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="1" fillId="4" borderId="0" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="2" fillId="4" borderId="0" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="3" fillId="4" borderId="0" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="4" fillId="4" borderId="0" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="0" fillId="5" borderId="0" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="1" fillId="5" borderId="0" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="2" fillId="5" borderId="0" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="3" fillId="5" borderId="0" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="4" fillId="5" borderId="0" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="0" fillId="0" borderId="1" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="1" fillId="0" borderId="1" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="2" fillId="0" borderId="1" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="3" fillId="0" borderId="1" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="4" fillId="0" borderId="1" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="0" fillId="2" borderId="1" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="1" fillId="2" borderId="1" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="2" fillId="2" borderId="1" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="3" fillId="2" borderId="1" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="4" fillId="2" borderId="1" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="0" fillId="3" borderId="1" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="1" fillId="3" borderId="1" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="2" fillId="3" borderId="1" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="3" fillId="3" borderId="1" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="4" fillId="3" borderId="1" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="0" fillId="4" borderId="1" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="1" fillId="4" borderId="1" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="2" fillId="4" borderId="1" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="3" fillId="4" borderId="1" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="4" fillId="4" borderId="1" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="0" fillId="5" borderId="1" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="1" fillId="5" borderId="1" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="2" fillId="5" borderId="1" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="3" fillId="5" borderId="1" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="4" fillId="5" borderId="1" applyFont="1" applyFill="1" applyBorder="1"/>'+
        '<xf numFmtId="0" fontId="0" fillId="0" borderId="0" applyFont="1" applyFill="1" applyBorder="1" xfId="0" applyAlignment="1">'+
          '<alignment horizontal="left"/>'+
        '</xf>'+
        '<xf numFmtId="0" fontId="0" fillId="0" borderId="0" applyFont="1" applyFill="1" applyBorder="1" xfId="0" applyAlignment="1">'+
          '<alignment horizontal="center"/>'+
        '</xf>'+
        '<xf numFmtId="0" fontId="0" fillId="0" borderId="0" applyFont="1" applyFill="1" applyBorder="1" xfId="0" applyAlignment="1">'+
          '<alignment horizontal="right"/>'+
        '</xf>'+
        '<xf numFmtId="0" fontId="0" fillId="0" borderId="0" applyFont="1" applyFill="1" applyBorder="1" xfId="0" applyAlignment="1">'+
          '<alignment horizontal="fill"/>'+
        '</xf>'+
        '<xf numFmtId="0" fontId="0" fillId="0" borderId="0" applyFont="1" applyFill="1" applyBorder="1" xfId="0" applyAlignment="1">'+
          '<alignment textRotation="90"/>'+
        '</xf>'+
        '<xf numFmtId="0" fontId="0" fillId="0" borderId="0" applyFont="1" applyFill="1" applyBorder="1" xfId="0" applyAlignment="1">'+
          '<alignment wrapText="1"/>'+
        '</xf>'+
        '<xf numFmtId="9"   fontId="0" fillId="0" borderId="0" applyFont="1" applyFill="1" applyBorder="1" xfId="0" applyNumberFormat="1"/>'+
        '<xf numFmtId="164" fontId="0" fillId="0" borderId="0" applyFont="1" applyFill="1" applyBorder="1" xfId="0" applyNumberFormat="1"/>'+
        '<xf numFmtId="165" fontId="0" fillId="0" borderId="0" applyFont="1" applyFill="1" applyBorder="1" xfId="0" applyNumberFormat="1"/>'+
        '<xf numFmtId="166" fontId="0" fillId="0" borderId="0" applyFont="1" applyFill="1" applyBorder="1" xfId="0" applyNumberFormat="1"/>'+
        '<xf numFmtId="167" fontId="0" fillId="0" borderId="0" applyFont="1" applyFill="1" applyBorder="1" xfId="0" applyNumberFormat="1"/>'+
        '<xf numFmtId="168" fontId="0" fillId="0" borderId="0" applyFont="1" applyFill="1" applyBorder="1" xfId="0" applyNumberFormat="1"/>'+
        '<xf numFmtId="169" fontId="0" fillId="0" borderId="0" applyFont="1" applyFill="1" applyBorder="1" xfId="0" applyNumberFormat="1"/>'+
        '<xf numFmtId="3" fontId="0" fillId="0" borderId="0" applyFont="1" applyFill="1" applyBorder="1" xfId="0" applyNumberFormat="1"/>'+
        '<xf numFmtId="4" fontId="0" fillId="0" borderId="0" applyFont="1" applyFill="1" applyBorder="1" xfId="0" applyNumberFormat="1"/>'+
        '<xf numFmtId="1" fontId="0" fillId="0" borderId="0" applyFont="1" applyFill="1" applyBorder="1" xfId="0" applyNumberFormat="1"/>'+
        '<xf numFmtId="2" fontId="0" fillId="0" borderId="0" applyFont="1" applyFill="1" applyBorder="1" xfId="0" applyNumberFormat="1"/>'+
      '</cellXfs>'+
      '<cellStyles count="1">'+
        '<cellStyle name="Normal" xfId="0" builtinId="0" />'+
      '</cellStyles>'+
      '<dxfs count="0" />'+
      '<tableStyles count="0" defaultTableStyle="TableStyleMedium9" defaultPivotStyle="PivotStyleMedium4" />'+
    '</styleSheet>',

  "xl/theme/theme1.xml":
    '<?xml version="1.0" encoding="UTF-8" standalone="yes"?>'+
    '<a:theme xmlns:a="http://schemas.openxmlformats.org/drawingml/2006/main" name="Office Theme">'+
    '<a:themeElements>'+
    '<a:clrScheme name="Office">'+
    '<a:dk1>'+
    '<a:sysClr val="windowText" lastClr="000000"/>'+
    '</a:dk1>'+
    '<a:lt1>'+
    '<a:sysClr val="window" lastClr="FFFFFF"/>'+
    '</a:lt1>'+
    '<a:dk2>'+
    '<a:srgbClr val="44546A"/>'+
    '</a:dk2>'+
    '<a:lt2>'+
    '<a:srgbClr val="E7E6E6"/>'+
    '</a:lt2>'+
    '<a:accent1>'+
    '<a:srgbClr val="5B9BD5"/>'+
    '</a:accent1>'+
    '<a:accent2>'+
    '<a:srgbClr val="ED7D31"/>'+
    '</a:accent2>'+
    '<a:accent3>'+
    '<a:srgbClr val="A5A5A5"/>'+
    '</a:accent3>'+
    '<a:accent4>'+
    '<a:srgbClr val="FFC000"/>'+
    '</a:accent4>'+
    '<a:accent5>'+
    '<a:srgbClr val="4472C4"/>'+
    '</a:accent5>'+
    '<a:accent6>'+
    '<a:srgbClr val="70AD47"/>'+
    '</a:accent6>'+
    '<a:hlink>'+
    '<a:srgbClr val="0563C1"/>'+
    '</a:hlink>'+
    '<a:folHlink>'+
    '<a:srgbClr val="954F72"/>'+
    '</a:folHlink>'+
    '</a:clrScheme>'+
    '<a:fontScheme name="Office">'+
    '<a:majorFont>'+
    '<a:latin typeface="Calibri Light" panose="020F0302020204030204"/>'+
    '<a:ea typeface=""/>'+
    '<a:cs typeface=""/>'+
    '<a:font script="Jpan" typeface="Yu Gothic Light"/>'+
    '<a:font script="Hang" typeface="맑은 고딕"/>'+
    '<a:font script="Hans" typeface="DengXian Light"/>'+
    '<a:font script="Hant" typeface="新細明體"/>'+
    '<a:font script="Arab" typeface="Times New Roman"/>'+
    '<a:font script="Hebr" typeface="Times New Roman"/>'+
    '<a:font script="Thai" typeface="Tahoma"/>'+
    '<a:font script="Ethi" typeface="Nyala"/>'+
    '<a:font script="Beng" typeface="Vrinda"/>'+
    '<a:font script="Gujr" typeface="Shruti"/>'+
    '<a:font script="Khmr" typeface="MoolBoran"/>'+
    '<a:font script="Knda" typeface="Tunga"/>'+
    '<a:font script="Guru" typeface="Raavi"/>'+
    '<a:font script="Cans" typeface="Euphemia"/>'+
    '<a:font script="Cher" typeface="Plantagenet Cherokee"/>'+
    '<a:font script="Yiii" typeface="Microsoft Yi Baiti"/>'+
    '<a:font script="Tibt" typeface="Microsoft Himalaya"/>'+
    '<a:font script="Thaa" typeface="MV Boli"/>'+
    '<a:font script="Deva" typeface="Mangal"/>'+
    '<a:font script="Telu" typeface="Gautami"/>'+
    '<a:font script="Taml" typeface="Latha"/>'+
    '<a:font script="Syrc" typeface="Estrangelo Edessa"/>'+
    '<a:font script="Orya" typeface="Kalinga"/>'+
    '<a:font script="Mlym" typeface="Kartika"/>'+
    '<a:font script="Laoo" typeface="DokChampa"/>'+
    '<a:font script="Sinh" typeface="Iskoola Pota"/>'+
    '<a:font script="Mong" typeface="Mongolian Baiti"/>'+
    '<a:font script="Viet" typeface="Times New Roman"/>'+
    '<a:font script="Uigh" typeface="Microsoft Uighur"/>'+
    '<a:font script="Geor" typeface="Sylfaen"/>'+
    '</a:majorFont>'+
    '<a:minorFont>'+
    '<a:latin typeface="Calibri" panose="020F0502020204030204"/>'+
    '<a:ea typeface=""/>'+
    '<a:cs typeface=""/>'+
    '<a:font script="Jpan" typeface="Yu Gothic"/>'+
    '<a:font script="Hang" typeface="맑은 고딕"/>'+
    '<a:font script="Hans" typeface="DengXian"/>'+
    '<a:font script="Hant" typeface="新細明體"/>'+
    '<a:font script="Arab" typeface="Arial"/>'+
    '<a:font script="Hebr" typeface="Arial"/>'+
    '<a:font script="Thai" typeface="Tahoma"/>'+
    '<a:font script="Ethi" typeface="Nyala"/>'+
    '<a:font script="Beng" typeface="Vrinda"/>'+
    '<a:font script="Gujr" typeface="Shruti"/>'+
    '<a:font script="Khmr" typeface="DaunPenh"/>'+
    '<a:font script="Knda" typeface="Tunga"/>'+
    '<a:font script="Guru" typeface="Raavi"/>'+
    '<a:font script="Cans" typeface="Euphemia"/>'+
    '<a:font script="Cher" typeface="Plantagenet Cherokee"/>'+
    '<a:font script="Yiii" typeface="Microsoft Yi Baiti"/>'+
    '<a:font script="Tibt" typeface="Microsoft Himalaya"/>'+
    '<a:font script="Thaa" typeface="MV Boli"/>'+
    '<a:font script="Deva" typeface="Mangal"/>'+
    '<a:font script="Telu" typeface="Gautami"/>'+
    '<a:font script="Taml" typeface="Latha"/>'+
    '<a:font script="Syrc" typeface="Estrangelo Edessa"/>'+
    '<a:font script="Orya" typeface="Kalinga"/>'+
    '<a:font script="Mlym" typeface="Kartika"/>'+
    '<a:font script="Laoo" typeface="DokChampa"/>'+
    '<a:font script="Sinh" typeface="Iskoola Pota"/>'+
    '<a:font script="Mong" typeface="Mongolian Baiti"/>'+
    '<a:font script="Viet" typeface="Arial"/>'+
    '<a:font script="Uigh" typeface="Microsoft Uighur"/>'+
    '<a:font script="Geor" typeface="Sylfaen"/>'+
    '</a:minorFont>'+
    '</a:fontScheme>'+
    '<a:fmtScheme name="Office">'+
    '<a:fillStyleLst>'+
    '<a:solidFill>'+
    '<a:schemeClr val="phClr"/>'+
    '</a:solidFill>'+
    '<a:gradFill rotWithShape="1">'+
    '<a:gsLst>'+
    '<a:gs pos="0">'+
    '<a:schemeClr val="phClr">'+
    '<a:lumMod val="110000"/>'+
    '<a:satMod val="105000"/>'+
    '<a:tint val="67000"/>'+
    '</a:schemeClr>'+
    '</a:gs>'+
    '<a:gs pos="50000">'+
    '<a:schemeClr val="phClr">'+
    '<a:lumMod val="105000"/>'+
    '<a:satMod val="103000"/>'+
    '<a:tint val="73000"/>'+
    '</a:schemeClr>'+
    '</a:gs>'+
    '<a:gs pos="100000">'+
    '<a:schemeClr val="phClr">'+
    '<a:lumMod val="105000"/>'+
    '<a:satMod val="109000"/>'+
    '<a:tint val="81000"/>'+
    '</a:schemeClr>'+
    '</a:gs>'+
    '</a:gsLst>'+
    '<a:lin ang="5400000" scaled="0"/>'+
    '</a:gradFill>'+
    '<a:gradFill rotWithShape="1">'+
    '<a:gsLst>'+
    '<a:gs pos="0">'+
    '<a:schemeClr val="phClr">'+
    '<a:satMod val="103000"/>'+
    '<a:lumMod val="102000"/>'+
    '<a:tint val="94000"/>'+
    '</a:schemeClr>'+
    '</a:gs>'+
    '<a:gs pos="50000">'+
    '<a:schemeClr val="phClr">'+
    '<a:satMod val="110000"/>'+
    '<a:lumMod val="100000"/>'+
    '<a:shade val="100000"/>'+
    '</a:schemeClr>'+
    '</a:gs>'+
    '<a:gs pos="100000">'+
    '<a:schemeClr val="phClr">'+
    '<a:lumMod val="99000"/>'+
    '<a:satMod val="120000"/>'+
    '<a:shade val="78000"/>'+
    '</a:schemeClr>'+
    '</a:gs>'+
    '</a:gsLst>'+
    '<a:lin ang="5400000" scaled="0"/>'+
    '</a:gradFill>'+
    '</a:fillStyleLst>'+
    '<a:lnStyleLst>'+
    '<a:ln w="6350" cap="flat" cmpd="sng" algn="ctr">'+
    '<a:solidFill>'+
    '<a:schemeClr val="phClr"/>'+
    '</a:solidFill>'+
    '<a:prstDash val="solid"/>'+
    '<a:miter lim="800000"/>'+
    '</a:ln>'+
    '<a:ln w="12700" cap="flat" cmpd="sng" algn="ctr">'+
    '<a:solidFill>'+
    '<a:schemeClr val="phClr"/>'+
    '</a:solidFill>'+
    '<a:prstDash val="solid"/>'+
    '<a:miter lim="800000"/>'+
    '</a:ln>'+
    '<a:ln w="19050" cap="flat" cmpd="sng" algn="ctr">'+
    '<a:solidFill>'+
    '<a:schemeClr val="phClr"/>'+
    '</a:solidFill>'+
    '<a:prstDash val="solid"/>'+
    '<a:miter lim="800000"/>'+
    '</a:ln>'+
    '</a:lnStyleLst>'+
    '<a:effectStyleLst>'+
    '<a:effectStyle>'+
    '<a:effectLst/>'+
    '</a:effectStyle>'+
    '<a:effectStyle>'+
    '<a:effectLst/>'+
    '</a:effectStyle>'+
    '<a:effectStyle>'+
    '<a:effectLst>'+
    '<a:outerShdw blurRad="57150" dist="19050" dir="5400000" algn="ctr" rotWithShape="0">'+
    '<a:srgbClr val="000000">'+
    '<a:alpha val="63000"/>'+
    '</a:srgbClr>'+
    '</a:outerShdw>'+
    '</a:effectLst>'+
    '</a:effectStyle>'+
    '</a:effectStyleLst>'+
    '<a:bgFillStyleLst>'+
    '<a:solidFill>'+
    '<a:schemeClr val="phClr"/>'+
    '</a:solidFill>'+
    '<a:solidFill>'+
    '<a:schemeClr val="phClr">'+
    '<a:tint val="95000"/>'+
    '<a:satMod val="170000"/>'+
    '</a:schemeClr>'+
    '</a:solidFill>'+
    '<a:gradFill rotWithShape="1">'+
    '<a:gsLst>'+
    '<a:gs pos="0">'+
    '<a:schemeClr val="phClr">'+
    '<a:tint val="93000"/>'+
    '<a:satMod val="150000"/>'+
    '<a:shade val="98000"/>'+
    '<a:lumMod val="102000"/>'+
    '</a:schemeClr>'+
    '</a:gs>'+
    '<a:gs pos="50000">'+
    '<a:schemeClr val="phClr">'+
    '<a:tint val="98000"/>'+
    '<a:satMod val="130000"/>'+
    '<a:shade val="90000"/>'+
    '<a:lumMod val="103000"/>'+
    '</a:schemeClr>'+
    '</a:gs>'+
    '<a:gs pos="100000">'+
    '<a:schemeClr val="phClr">'+
    '<a:shade val="63000"/>'+
    '<a:satMod val="120000"/>'+
    '</a:schemeClr>'+
    '</a:gs>'+
    '</a:gsLst>'+
    '<a:lin ang="5400000" scaled="0"/>'+
    '</a:gradFill>'+
    '</a:bgFillStyleLst>'+
    '</a:fmtScheme>'+
    '</a:themeElements>'+
    '<a:objectDefaults/>'+
    '<a:extraClrSchemeLst/>'+
    '<a:extLst>'+
    '<a:ext uri="{05A4C25C-085E-4340-85A3-A5531E510DB2}">'+
    '<thm15:themeFamily xmlns:thm15="http://schemas.microsoft.com/office/thememl/2012/main" name="Office Theme" id="{62F939B6-93AF-4DB8-9C6B-D6C7DFDC589F}" vid="{4A3C46E8-61CC-4603-A589-7422A47A8E4A}"/>'+
    '</a:ext>'+
    '</a:extLst>'+
    '</a:theme>',

  "xl/drawings/drawing1.xml":
    '<?xml version="1.0" encoding="UTF-8" standalone="yes"?>'+
    '<xdr:wsDr xmlns:xdr="http://schemas.openxmlformats.org/drawingml/2006/spreadsheetDrawing" xmlns:a="http://schemas.openxmlformats.org/drawingml/2006/main">'+
    '<xdr:twoCellAnchor editAs="oneCell">'+
    '<xdr:from>'+
    '<xdr:col>0</xdr:col>'+
    '<xdr:colOff>0</xdr:colOff>'+
    '<xdr:row>0</xdr:row>'+
    '<xdr:rowOff>0</xdr:rowOff>'+
    '</xdr:from>'+
    '<xdr:to>'+
    '<xdr:col>3</xdr:col>'+
    '<xdr:colOff>822000</xdr:colOff>'+
    '<xdr:row>5</xdr:row>'+
    '<xdr:rowOff>292000</xdr:rowOff>'+
    '</xdr:to>'+
    '<xdr:pic>'+
    '<xdr:nvPicPr>'+
    '<xdr:cNvPr id="1" name="Logotipo"/>'+
    '<xdr:cNvPicPr>'+
    '<a:picLocks noChangeAspect="1"/>'+
    '</xdr:cNvPicPr>'+
    '</xdr:nvPicPr>'+
    '<xdr:blipFill>'+
    '<a:blip xmlns:r="http://schemas.openxmlformats.org/officeDocument/2006/relationships" r:embed="rId1"/>'+
    '<a:stretch>'+
    '<a:fillRect/>'+
    '</a:stretch>'+
    '</xdr:blipFill>'+
    '<xdr:spPr>'+
    '<a:xfrm>'+
    '<a:off x="0" y="0"/>'+
    '<a:ext cx="3238499" cy="1069515"/>'+
    '</a:xfrm>'+
    '<a:prstGeom prst="rect">'+
    '<a:avLst/>'+
    '</a:prstGeom>'+
    '</xdr:spPr>'+
    '</xdr:pic>'+
    '<xdr:clientData/>'+
    '</xdr:twoCellAnchor>'+
    '</xdr:wsDr>',

  "xl/drawings/_rels/drawing1.xml.rels":
    '<?xml version="1.0" encoding="UTF-8" standalone="yes"?>'+
    '<Relationships xmlns="http://schemas.openxmlformats.org/package/2006/relationships">'+
    '<Relationship Id="rId1" Type="http://schemas.openxmlformats.org/officeDocument/2006/relationships/image" Target="../media/image1.jpg"/>'+
    '</Relationships>',
  
  "xl/worksheets/_rels/sheet1.xml.rels":
    '<?xml version="1.0" encoding="UTF-8" standalone="yes"?>'+
    '<Relationships xmlns="http://schemas.openxmlformats.org/package/2006/relationships">'+
    '<Relationship Id="rId1" Type="http://schemas.openxmlformats.org/officeDocument/2006/relationships/drawing" Target="../drawings/drawing1.xml"/>'+
    '</Relationships>',

  "docProps/app.xml":
    '<?xml version="1.0" encoding="UTF-8" standalone="yes"?>'+
    '<Properties xmlns="http://schemas.openxmlformats.org/officeDocument/2006/extended-properties" xmlns:vt="http://schemas.openxmlformats.org/officeDocument/2006/docPropsVTypes">'+
    '<Application>Microsoft Excel</Application>'+
    '<DocSecurity>0</DocSecurity>'+
    '<ScaleCrop>false</ScaleCrop>'+
    '<HeadingPairs>'+
    '<vt:vector size="2" baseType="variant">'+
    '<vt:variant>'+
    '<vt:lpstr>Hojas de cálculo</vt:lpstr>'+
    '</vt:variant>'+
    '<vt:variant>'+
    '<vt:i4>1</vt:i4>'+
    '</vt:variant>'+
    '</vt:vector>'+
    '</HeadingPairs>'+
    '<TitlesOfParts>'+
    '<vt:vector size="1" baseType="lpstr">'+
    '<vt:lpstr>Hoja1</vt:lpstr>'+
    '</vt:vector>'+
    '</TitlesOfParts>'+
    '<Company>'+
    '</Company>'+
    '<LinksUpToDate>false</LinksUpToDate>'+
    '<SharedDoc>false</SharedDoc>'+
    '<HyperlinksChanged>false</HyperlinksChanged>'+
    '<AppVersion>16.0300</AppVersion>'+
    '</Properties>',
  
  "docProps/core.xml":
    '<?xml version="1.0" encoding="UTF-8" standalone="yes"?>'+
    '<cp:coreProperties xmlns:cp="http://schemas.openxmlformats.org/package/2006/metadata/core-properties" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:dcterms="http://purl.org/dc/terms/" xmlns:dcmitype="http://purl.org/dc/dcmitype/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">'+
    '<dc:creator>'+
    'novaSPP</dc:creator>'+
    '<cp:lastModifiedBy>'+
    'novaSPP</cp:lastModifiedBy>'+
    '<dcterms:created xsi:type="dcterms:W3CDTF">'+
    '2019-01-01T00:00:00Z</dcterms:created>'+
    '<dcterms:modified xsi:type="dcterms:W3CDTF">'+
    '2019-01-01T00:00:00Z</dcterms:modified>'+
    '</cp:coreProperties>'
};
```

Finally we need to add the image with the customize option

```javascript
var logo = new Image();
logo.src = 'image.jpg';
function getBase64Image(img) {
  var canvas = document.createElement("canvas");
  canvas.width = img.width;
  canvas.height = img.height;
  var ctx = canvas.getContext("2d");
  ctx.drawImage(img, 0, 0);
  return canvas.toDataURL("image/jpeg");
}
........
  buttons  : [{ extend     :'excelHtml5',
    customize: function( xlsx ) {
      xlsx.xl.media = [{
        name:"image1.jpg",
        data:getBase64Image(logo).split(',')[1]
      }];
    }
  }]
```

## Final note

I know is not the best solution, not dinamic for other images, etc, etc, but, I want to write down the process as a self documentation for future references.
