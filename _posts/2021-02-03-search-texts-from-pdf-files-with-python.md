---
title: "Search Texts From PDF Files With Python"
date: 2021-02-03
tags: python pdf
---
> Disclaimer: Those two mehtods could not get exact all texts from the PDF file. You may need to try some other methods. This post is only a note to myself and is a working progress.  

<!--excerpt.start-->
I came across the need to search some texts from pdf files and return the page number of where the text is found. After some search, I found there are two popular methods with the help of three different Python packages could partially do the trick.   
<!--excerpt.end-->

One method is to use [PyPDF2](https://pypi.org/project/PyPDF2/) package. The other method is to use [pdfminer](https://pypi.org/project/pdfminer/) package, combined with [pdfminer.six](https://pypi.org/project/pdfminer.six/) package. I will summary each method below. 


Before using any of those packages, follow `pypi` to install each package respectively. It is also good practice to install inside a python virtual environment. 
# Using PyPDF2  
```sh
import PyPDF2

pdfFileObj = open('source.pdf', 'rb')
pdfReader = PyPDF2.PdfFileReader(pdfFileObj, strict=False)
pageObj = pdfReader.getPage(6)

# If this returns nothing, try the below method as a fallback. 
print(pageObj.extractText()
``` 

# Using pdfminer combined with pdfminer.six
```sh
from io import StringIO

from pdfminer.converter import TextConverter
from pdfminer.layout import LAParams
from pdfminer.pdfdocument import PDFDocument
from pdfminer.pdfinterp import PDFResourceManager, PDFPageInterpreter
from pdfminer.pdfpage import PDFPage
from pdfminer.pdfparser import PDFParser

output_string = StringIO()
with open('source.pdf', 'rb') as in_file:
    parser = PDFParser(in_file)
    doc = PDFDocument(parser)
    rsrcmgr = PDFResourceManager()
    device = TextConverter(rsrcmgr, output_string, laparams=LAParams())
    interpreter = PDFPageInterpreter(rsrcmgr, device)
    for page in PDFPage.create_pages(doc):
        interpreter.process_page(page)

print(output_string.getvalue())
```

***
Reference:  
1. [PyPDF2 Documentation](https://pythonhosted.org/PyPDF2/PageObject.html){:target="\_blank"}
2. [pdfminer Documentation](https://pdfminer-docs.readthedocs.io/index.html){:target="\_blank"}
3. [pdfminer.six Documentation](https://pdfminersix.readthedocs.io/en/latest/index.html){:target="\_blank"}




