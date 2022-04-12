# ✨ PDFSegmenter

PDFSegmenter is an Executor used for extracting images and text as chunks from PDF data. It stores each images and text of each page as chunks separately, with their respective mime types. It uses the [pdfplumber](https://github.com/jsvine/pdfplumber) library.

## Loading data

The `PDFSegmenter` expects data to be found in the `Document`'s `.tensor` attribute. This can be loaded from a PDF file like so

```python
from docarray import DocumentArray, Document
from jina import Flow

doc = DocumentArray([Document(uri='/home/cristian/Downloads/cats_are_awesome.pdf')])
doc[0].load_uri_to_blob()
print(doc[0])

f = Flow().add(
    uses='jinahub+docker://PDFSegmenter',
)
with f:
    resp = f.post(on='/craft', inputs=doc)
    print(f'{[c.mime_type for c in resp[0].chunks]}')
```


```
>> ['image/*', 'image/*', 'text/plain']
```
