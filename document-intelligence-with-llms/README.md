# Document Intelligence with LLMs

A practical exploration of different approaches to extracting and understanding information from PDF documents using Large Language Models (LLMs).

PDF documents often contain a mixture of digital text, complex tables, and scanned images. Traditional extraction tools can handle some of these elements effectively, but they often struggle with scanned or visually complex content.

This project implements and compares three approaches to document intelligence:

1. Traditional PDF extraction.
2. Multimodal LLM-based extraction using page images.
3. Native PDF processing using an LLM API.

It also explores a hybrid pipeline that combines traditional extraction with vision-based processing.

## Project Objectives

- Understand how to interact with an LLM API.
- Extract text and tables from PDF documents using traditional Python libraries.
- Process PDF pages as images using multimodal LLMs.
- Explore native PDF processing capabilities.
- Compare different extraction approaches.
- Understand the trade-offs between accuracy, processing complexity, latency, and cost.
- Implement a hybrid extraction pipeline.

## Technologies Used

- Python
- OpenAI Python SDK
- AvalAI API
- GPT-4o
- GPT-4o-mini
- pdfplumber
- pdf2image
- Pillow
- Pandas

## Project Structure

```text
document-intelligence-with-llms/
│
├── README.md
├── document_intelligence.ipynb
├── sample_field_report.pdf
├── requirements.txt
└── .gitignore
```

## Implemented Approaches

### 1. Traditional PDF Extraction

Uses `pdfplumber` to extract digital text and tables from PDF pages.

This approach is useful for structured documents containing selectable text, but it may fail when dealing with scanned pages or image-based content.

### 2. Multimodal LLM Extraction

Converts individual PDF pages into images using `pdf2image` and sends them to a vision-capable LLM.

The model is instructed to:
- Transcribe visible text.
- Reconstruct tables in Markdown format.
- Recognize and transcribe scanned content.
- Preserve the original document structure as much as possible.

### 3. Native PDF Processing

Sends the complete PDF directly to the model through the API's native PDF input support.

Unlike the image-based approach, this method does not require manually rendering each page.

### 4. Hybrid Extraction Pipeline

Combines traditional PDF extraction with vision-based processing.

The pipeline:
- Uses traditional extraction as the default method.
- Checks whether the extracted text meets a minimum character threshold.
- Falls back to vision-based extraction when the extracted text is insufficient.

This approach aims to reduce unnecessary vision API calls while maintaining coverage of scanned pages.

## Installation

Clone the repository:

```bash
git clone <YOUR_REPOSITORY_URL>
cd document-intelligence-with-llms
```

Install the required Python packages:

```bash
pip install -r requirements.txt
```

**Additional requirement:** `pdf2image` requires Poppler to be installed on your system.

Install Poppler according to your operating system before running the notebook.

## API Configuration

This project uses the AvalAI API through the OpenAI Python SDK.

You need an AvalAI API key to run the LLM-based extraction sections.

The API key should be provided securely at runtime and should never be hardcoded or committed to GitHub.

## Usage

1. Install the required dependencies.
2. Install Poppler.
3. Open `document_intelligence.ipynb` in Jupyter Notebook or Google Colab.
4. Configure your API key when prompted.
5. Make sure `sample_field_report.pdf` is available in the expected location.
6. Run the notebook cells in order.

## Evaluation and Comparison

The project compares the implemented approaches based on:

- Extracted text content.
- Table extraction capabilities.
- Handling of scanned pages.
- Processing complexity.
- API usage and associated costs.
- Practical suitability for different document types.

The notebook also includes observations and reflections based on the results obtained from the sample PDF.

## Key Takeaways

- Traditional PDF extraction is effective for many digitally generated documents.
- Vision-based LLM extraction can handle scanned and visually complex pages.
- Native PDF processing simplifies the implementation by reducing manual preprocessing.
- Hybrid pipelines can help balance extraction quality and API usage.

## Limitations

- Extraction quality depends on the document structure and image quality.
- LLM-generated transcriptions may contain errors and should be validated when accuracy is critical.
- API-based approaches require network access and may introduce additional costs and latency.
- The hybrid pipeline uses a simple character-count threshold rather than a comprehensive document-quality evaluation.

## Future Improvements

- Implement quantitative extraction accuracy metrics.
- Add processing time and API cost measurements.
- Improve table extraction evaluation.
- Support batch processing of multiple PDF documents.
- Introduce configurable extraction thresholds.
- Add automated evaluation against manually verified ground truth.

## License

This project is available under the MIT License.