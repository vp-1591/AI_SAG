# Learn From PDF

**Learn From PDF** is an intelligent study companion that transforms your PDF documents into interactive learning experiences. Built with Streamlit and powered by Google's Gemini AI, it helps you master complex topics through AI-generated concept summaries and conversational learning.

> **Note:** This is an MVP (Minimum Viable Product) version currently under development. Feedback and suggestions are welcome!

## Features

### Core Functionality
-   **PDF Text Extraction**: Upload any PDF document for automatic text extraction and analysis
-   **AI-Powered Analysis**: Leverages Google's Gemini 2.5 Flash model for intelligent content processing
-   **Concept Extraction**: Automatically identifies and summarizes 4-8 key concepts from your document
-   **Interactive Chat**: Ask questions and discuss each concept with an AI Socratic tutor
-   **Multi-Language Support**: Automatically detects and responds in the language of your document

### User Experience
-   **Modern UI**: Clean, gradient-based design with Inter font family and smooth animations
-   **Native Theming**: Utilizes Streamlit's built-in theme system for consistent appearance
-   **Feedback System**: Share your experience via integrated Google Sheets feedback collection
-   **Real-Time Processing**: Instant AI responses with loading indicators

## Tech Stack

-   **Python 3.8+**
-   **[Streamlit](https://streamlit.io/)**: Interactive web interface framework
-   **[Google Gemini API](https://ai.google.dev/)**: AI model for content generation and chat (gemini-2.5-flash)
-   **[PyPDF2](https://pypi.org/project/PyPDF2/)**: PDF text extraction
-   **[gspread](https://gspread.readthedocs.io/)**: Google Sheets integration for feedback collection
-   **[python-dotenv](https://pypi.org/project/python-dotenv/)**: Environment variable management

## Installation & Setup

### 1. Clone the repository
```bash
git clone <repository-url>
cd AI_SAG
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Set up Environment Variables
Create a `.env` file in the root directory:

```env
# Required: Google Gemini API Key
GOOGLE_API_KEY=your_api_key_here

# Optional: Google Sheets name for feedback (default: LearnFromPDF_Feedback)
SHEET_NAME=your_sheet_name
```

**Alternative**: You can enter the API key directly in the app interface if not provided via `.env`

### 4. (Optional) Set up Feedback Integration
For feedback collection to work, you need Google Sheets API credentials:

**Local Development:**
- Place your Google Service Account JSON file in the root directory
- Name it `lfpdf-479215-51af785aa8fa.json` (or update `LOCAL_GSPREAD_KEY_FILE` constant in `app.py`)

**Cloud Deployment (Streamlit Cloud):**
- Add your service account credentials to Streamlit secrets as `gspread`

> **Note:** The feedback feature will gracefully degrade if credentials are not configured.

## Usage

### 1. Run the application
```bash
streamlit run app.py
```

### 2. Upload & Process
- Upload a PDF document using the file uploader
- Click the **magic wand icon** button to generate content

### 3. Learn Interactively
- Browse extracted **Study Concepts** with AI-generated summaries
- Expand any concept to view its summary
- Use the **chat interface** within each concept to ask questions and deepen understanding
- Chat maintains conversation history for contextual responses

### 4. Share Feedback (Optional)
- After generation, provide feedback via the feedback form
- Rate your experience and leave comments

## Project Structure

```
AI_SAG/
├── app.py                              # Main application with UI and logic
├── requirements.txt                    # Python dependencies
├── .env                               # Environment variables (API keys)
├── .gitignore                         # Git ignore rules
├── lfpdf-479215-51af785aa8fa.json    # Google Service Account credentials (gitignored)
└── README.md                          # This file
```

## Key Components

### `app.py`
- **Page Configuration**: Sets up Streamlit with wide layout and custom page title
- **CSS Styling**: Custom Inter font, gradient hero titles, and icon-based buttons
- **Helper Functions**:
  - `get_gspread_client()`: Initializes Google Sheets client with fallback authentication
  - `submit_feedback()`: Handles feedback submission to Google Sheets
  - `extract_text_from_pdf()`: Extracts text content from uploaded PDFs
  - `generate_study_material()`: Calls Gemini API to extract key concepts
  - `generate_chat_response()`: Manages conversational AI for each concept
  - `process_generation()`: Orchestrates the full generation workflow

### Session State Management
- `study_material`: Stores extracted PDF text
- `generated_data`: Stores AI-generated concepts
- `chat_histories`: Maintains conversation history per concept
- `pdf_text`: Full PDF text for context in chat
- `show_feedback` / `feedback_submitted`: Controls feedback UI state

## Contributing

Feedback and contributions are welcome! Feel free to:
- Report bugs or suggest features via issues
- Submit pull requests with improvements
- Share your experience using the feedback form in the app
