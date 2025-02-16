# Apache Tika PDF Extraction

This implementation uses Apache Tika 3.1.0 with OCR capabilities for PDF text extraction.

## Features

- Text extraction from both text-based and scanned PDFs
- OCR support using Tesseract (Dutch + English)
- JPEG2000 image support
- Multiple output formats:
  - HTML output (primary format)
  - Plain text
  - Basic Markdown (converted from HTML)
- Metadata extraction
- Configurable OCR settings

## Technical Details

### Docker Configuration
- Base image: `apache/tika:3.1.0.0-full`
- Custom configuration for OCR and JPEG2000 support
- Memory allocation: 4GB heap, 6GB container limit
- Health checks enabled

### OCR Configuration
- Languages: Dutch (nld) and English (eng)
- Image processing:
  - DPI: 300
  - Format: PNG
  - Quality: 0.85
- Configurable size limits for OCR processing

### Output Processing
- Primary HTML output
- HTML to Markdown conversion using html2text
- Limited formatting preservation in Markdown
- Basic table conversion
- Unicode character support
- Link preservation

## Usage

1. Start the Tika server:
```bash
docker compose up -d
```

2. Process PDF files:
```bash
python parse_pdf.py
```

The script will:
1. Process all PDFs from the `../../documents/` directory
2. Generate output files in `../../results/tika/`:
   - `{filename}.md` - Markdown version
   - `{filename}.html` - HTML version
   - `{filename}_text.txt` - Plain text version
   - `{filename}_metadata.json` - Extracted metadata

## Configuration

### OCR Settings
Edit `tika-config.xml` to modify:
- OCR language support
- Image processing parameters
- File size limits
- Parser timeouts

### Docker Resources
Edit `docker-compose.yml` to adjust:
- Memory allocation
- Port mapping
- Volume mounts
- Environment variables

## Limitations

- OCR processing can be memory-intensive
- Large PDFs may require increased timeout settings
- Some complex PDF layouts may not preserve formatting perfectly
- No native Markdown output, conversion from HTML loses some formatting
- Table structures often break in Markdown conversion
- Complex formatting (columns, footnotes) may be lost in Markdown

## Evaluation Results

### 1. Cost and Scalability
- ✅ Free, open-source solution
- ✅ Self-hosted with no per-document costs
- ⚠️ Resource intensive for OCR (4GB heap minimum recommended)
- ⚠️ Processing speed varies significantly with OCR enabled

### 2. Accuracy and Quality
- ✅ Excellent for text-based PDFs
- ✅ Good OCR quality with Tesseract
- ✅ Multi-language support (configurable)
- ⚠️ Table structure preservation needs improvement

### 3. Output Formats
- ⚠️ No native Markdown support (requires HTML conversion)
- ⚠️ Markdown conversion loses complex formatting
- ✅ Clean HTML output
- ✅ Rich metadata extraction
- ⚠️ Table formatting often breaks in Markdown
- ⚠️ Limited control over Markdown output quality

### 4. Real-world Performance
- ✅ Handles complex layouts well in HTML
- ✅ Good image extraction
- ⚠️ Form field detection is basic
- ⚠️ May struggle with heavily formatted documents
- ⚠️ Markdown conversion reduces formatting quality

### 5. Production Readiness
- ✅ Official Docker container available
- ✅ REST API built-in
- ✅ Extensive documentation
- ✅ Health checks and monitoring
- ✅ Production-grade error handling

### 6. Project Activity
- ✅ Very active development (Apache Foundation)
- ✅ Regular releases
- ✅ Large community
- ✅ Quick security patch responses

### 7. Licensing
- ✅ Apache License 2.0
- ✅ Permissive for commercial use
- ✅ No royalty requirements
- ✅ Clear patent provisions

### 8. Privacy and Security
- ✅ Fully on-premises deployment
- ✅ No data leaves your infrastructure
- ✅ No data retention
- ✅ Regular security updates 