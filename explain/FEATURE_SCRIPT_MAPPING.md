# RAG-Anything 功能與腳本對應表

本文件整理 RAG-Anything 專案中各功能模組與其對應腳本的映射關係。

---

## 📁 核心模組 (`raganything/`)

| 檔案 | 功能說明 | 主要類別/函式 |
|------|----------|--------------|
| `raganything.py` | **主入口點** - 整合所有功能的統一介面 | `RAGAnything` |
| `config.py` | **配置管理** - 系統參數與環境變數設定 | `RAGAnythingConfig` |
| `parser.py` | **文件解析** - PDF/Office/圖片文件解析 | `Parser`, `MineruParser`, `DoclingParser` |
| `processor.py` | **文件處理** - 多模態內容分類與處理管線 | `ProcessorMixin` |
| `query.py` | **查詢功能** - 文字/多模態/VLM 增強查詢 | `QueryMixin` |
| `modalprocessors.py` | **模態處理器** - 圖片/表格/公式專門處理 | `ImageModalProcessor`, `TableModalProcessor`, `EquationModalProcessor`, `GenericModalProcessor`, `ContextExtractor` |
| `batch.py` | **批次處理** - 多文件並行處理 | `BatchMixin` |
| `batch_parser.py` | **批次解析** - 多文件並行解析與進度追蹤 | `BatchParser`, `BatchProcessingResult` |
| `utils.py` | **工具函式** - 內容分離、文字插入等輔助功能 | `separate_content()`, `insert_text_content()`, `encode_image_to_base64()` |
| `prompt.py` | **提示模板** - 多模態內容分析的 prompt 模板 | `PROMPTS` 字典 |
| `enhanced_markdown.py` | **Markdown 轉換** - Markdown 轉 PDF 功能 | `EnhancedMarkdownConverter`, `MarkdownConfig` |

---

## 🎯 功能詳細對應

### 1. 文件解析 (Document Parsing)

| 功能 | 腳本位置 | 關鍵函式 |
|------|----------|----------|
| PDF 解析 | `parser.py` | `MineruParser.parse_pdf()`, `DoclingParser.parse_pdf()` |
| 圖片解析 | `parser.py` | `MineruParser.parse_image()`, `DoclingParser.parse_image()` |
| Office 文件轉 PDF | `parser.py` | `Parser.convert_office_to_pdf()` |
| 文字檔轉 PDF | `parser.py` | `Parser.convert_text_to_pdf()` |
| 通用文件解析 | `parser.py` | `Parser.parse_document()` |
| 解析器安裝檢查 | `parser.py` | `Parser.check_installation()` |

### 2. 多模態處理 (Multimodal Processing)

| 功能 | 腳本位置 | 關鍵類別 |
|------|----------|----------|
| 圖片分析 | `modalprocessors.py` | `ImageModalProcessor` |
| 表格分析 | `modalprocessors.py` | `TableModalProcessor` |
| 公式分析 | `modalprocessors.py` | `EquationModalProcessor` |
| 通用內容分析 | `modalprocessors.py` | `GenericModalProcessor` |
| 上下文提取 | `modalprocessors.py` | `ContextExtractor` |
| 內容分離 | `utils.py` | `separate_content()` |

### 3. 查詢功能 (Query)

| 功能 | 腳本位置 | 關鍵函式 |
|------|----------|----------|
| 純文字查詢 | `query.py` | `QueryMixin.aquery()` |
| 多模態查詢 | `query.py` | `QueryMixin.aquery_with_multimodal()` |
| VLM 增強查詢 | `query.py` | `QueryMixin.aquery_vlm_enhanced()` |
| 查詢內容處理 | `query.py` | `QueryMixin._process_multimodal_query_content()` |

### 4. 批次處理 (Batch Processing)

| 功能 | 腳本位置 | 關鍵函式 |
|------|----------|----------|
| 資料夾批次處理 | `batch.py` | `BatchMixin.process_folder_complete()` |
| 文件批次處理 | `batch.py` | `BatchMixin.process_documents_batch()` |
| 非同步批次處理 | `batch.py` | `BatchMixin.process_documents_batch_async()` |
| 並行文件解析 | `batch_parser.py` | `BatchParser.process_batch()` |

### 5. 文件處理管線 (Document Processing Pipeline)

| 功能 | 腳本位置 | 關鍵函式 |
|------|----------|----------|
| 完整文件處理 | `processor.py` | `ProcessorMixin.parse_document()` |
| 多模態內容處理 | `processor.py` | `ProcessorMixin._process_multimodal_content()` |
| 批次類型感知處理 | `processor.py` | `ProcessorMixin._process_multimodal_content_batch_type_aware()` |
| 快取管理 | `processor.py` | `ProcessorMixin._get_cached_result()`, `ProcessorMixin._store_cached_result()` |

### 6. 配置管理 (Configuration)

| 功能 | 腳本位置 | 關鍵參數 |
|------|----------|----------|
| 工作目錄設定 | `config.py` | `working_dir` |
| 解析方法設定 | `config.py` | `parse_method`, `parser` |
| 多模態處理開關 | `config.py` | `enable_image_processing`, `enable_table_processing`, `enable_equation_processing` |
| 上下文提取設定 | `config.py` | `context_window`, `context_mode`, `max_context_tokens` |
| 批次處理設定 | `config.py` | `max_concurrent_files`, `supported_file_extensions` |

---

## 📚 範例腳本 (`examples/`)

| 範例檔案 | 功能說明 |
|----------|----------|
| `raganything_example.py` | 基本使用範例 - 端到端文件處理與查詢 |
| `modalprocessors_example.py` | 模態處理器使用範例 |
| `batch_processing_example.py` | 批次處理範例 |
| `batch_dry_run_example.py` | 批次處理乾跑測試範例 |
| `insert_content_list_example.py` | 直接插入內容列表範例 |
| `enhanced_markdown_example.py` | Markdown 轉換範例 |
| `lmstudio_integration_example.py` | LM Studio 整合範例 |
| `image_format_test.py` | 圖片格式測試 |
| `text_format_test.py` | 文字格式測試 |
| `office_document_test.py` | Office 文件測試 |

---

## 🔗 模組依賴關係

```
RAGAnything (raganything.py)
    ├── RAGAnythingConfig (config.py)
    ├── ProcessorMixin (processor.py)
    │   └── Parser/MineruParser/DoclingParser (parser.py)
    ├── QueryMixin (query.py)
    ├── BatchMixin (batch.py)
    │   └── BatchParser (batch_parser.py)
    └── Modal Processors (modalprocessors.py)
        ├── ImageModalProcessor
        ├── TableModalProcessor
        ├── EquationModalProcessor
        ├── GenericModalProcessor
        └── ContextExtractor
```

---

## 🛠️ 工具與輔助模組

| 模組 | 功能 |
|------|------|
| `utils.py` | 內容分離、Base64 編碼、圖片驗證 |
| `prompt.py` | 視覺分析、表格分析、公式分析的提示模板 |
| `enhanced_markdown.py` | Markdown 轉 PDF (支援 WeasyPrint/Pandoc) |
| `base.py` | 基礎類別定義 |
