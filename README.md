# docling-indra-ocr

[Indra OCR](https://github.com/datalab-to/indra) plugin for Docling.

## Instalation

With [uv](https://docs.astral.sh/uv/), add to your project using:

``` sh
uv add docling-indra-ocr
```

Check available external plugins:

``` sh
docling --show-external-plugins
```

It should show indra-ocr:

``` text
            Available OCR engines
┏━━━━━━━━━━━┳━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━┓
┃      Name ┃ Plugin    ┃ Package           ┃
┡━━━━━━━━━━━╇━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━┩
│ indra-ocr │ indra-ocr │ docling_indra_ocr │
└───────────┴───────────┴───────────────────┘
```

## Usage

### CLI


``` sh
docling --allow-external-plugins --ocr-engine=indra-ocr <source>
```

### Python

``` python
from docling.datamodel.base_models import InputFormat
from docling.datamodel.pipeline_options import PdfPipelineOptions
from docling.document_converter import (
    DocumentConverter,
    ImageFormatOption,
    PdfFormatOption,
)

from docling_indra_ocr import IndraOcrOptions


pipeline_options = PdfPipelineOptions(
    allow_external_plugins=True,
    ocr_options=IndraOcrOptions(),
)

converter = DocumentConverter(
    format_options={
        InputFormat.PDF: PdfFormatOption(pipeline_options=pipeline_options),
        InputFormat.IMAGE: ImageFormatOption(pipeline_options=pipeline_options),
    }
)

result = converter.convert("path/to/document.pdf")
print(result.document.export_to_markdown())
```
