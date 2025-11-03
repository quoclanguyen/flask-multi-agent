# Flask Multi-Agent Insurance Pricing System

A sophisticated multi-agent orchestration system built with Flask, CrewAI, and Gemini AI for intelligent insurance price recommendations and market analysis.

## 🎯 Overview

This system provides an end-to-end solution for analyzing insurance customer needs, researching market data, and generating pricing recommendations with comprehensive reports. It uses a multi-agent architecture where specialized AI agents collaborate to deliver accurate insights.

## Demo
For the demo, we use another github repository to implement the UI: https://github.com/quoclanguyen/insurechat/  
<video src="https://github.com/user-attachments/assets/414f1e93-a866-4f76-a13e-f9e6d06ec773" controls width="100%"></video>

## 🏗️ Architecture

The system consists of **7 specialized agents** working in sequence:

1. **NLU Agent** - Natural Language Understanding to parse Vietnamese customer requests
2. **Scraper Hybrid Agent** - Market research using LLM + fuzzy matching + heuristics
3. **RAG Lookup Agent** - Internal company product database lookup
4. **Market Intelligence Researcher** - Web search for competitive market insights
5. **Evaluator Agent** - Price recommendation based on all collected data
6. **Visualizer Agent** - Generate charts and visualizations
7. **Report Generator Agent** - Compile comprehensive HTML/PDF reports

## 🚀 Features

- **Multi-Agent Orchestration**: Sequential and parallel task execution
- **Vietnamese Language Support**: NLU for natural language processing
- **Hybrid Market Research**: Combines LLM semantic matching with fuzzy/heuristic scoring
- **Comprehensive Analysis**: Evaluates company products vs. market competition
- **Rich Visualizations**: Auto-generated charts and dashboards
- **Detailed Reports**: HTML and PDF reports with full analysis

## 📋 Prerequisites

- Python 3.8+
- Google Gemini API key
- Serper API key (for web search)
- Access to insurance product data API

## 🛠️ Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/flask-multi-agent.git
cd flask-multi-agent
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Set up environment variables:
Create a `.env` file in the project root:
```env
GEMINI_API_KEY=your_gemini_api_key_here
SERPER_API_KEY=your_serper_api_key_here
SERPER_API_KEY=your_serper_api_key_here
```

## 🎮 Usage

### Running the Flask Server

```bash
python api/index.py
```

The server will start on `http://0.0.0.0:3000`

### API Endpoints

#### POST `/run`
Execute the full multi-agent pipeline.

**Request:**
```json
{
  "data_query": "Tôi cần bảo hiểm sức khỏe với quyền lợi ung thư và ngoại trú, giá khoảng 3.5 triệu/năm"
}
```

**Response:**
```json
{
  "ok": true,
  "data_query": "...",
  "report": {
    "agent_outputs": {
      "NLU": {...},
      "Scraper": {...},
      "RAG": {...},
      "MarketIntelligence": {...},
      "Evaluator": {...},
      "Visualizer": {...},
      "ReportGenerator": {...}
    }
  }
}
```

#### POST `/agent1`
Run NLU agent only:
```json
{
  "data_query": "Tôi cần bảo hiểm sức khỏe...",
  "feedback": "optional feedback text"
}
```

#### POST `/agent2`
Run Scraper agent:
```json
{
  "data_query": "...",
  "analysis_result": {...}
}
```

#### POST `/agent3`
Run RAG Lookup agent:
```json
{
  "data_query": "...",
  "analysis_result": {...},
  "optimization_result": {...}
}
```

#### POST `/agent4`
Run Market Intelligence agent:
```json
{
  "data_query": "...",
  "analysis_result": {...},
  "additional_insights": {...}
}
```

#### POST `/agent5`
Run Report Generator:
```json
{
  "data_query": "...",
  "analysis_result": {...},
  "optimization_result": {...},
  "additional_insights": {...},
  "qa_result": {...},
  "feedback": "..."
}
```

#### GET `/`
Health check endpoint.

## 📁 Project Structure

```
flask-multi-agent/
├── api/
│   └── index.py              # Main Flask application & multi-agent orchestration
├── crew_setup.py             # CrewAI setup and configurations
├── requirements.txt          # Python dependencies
├── vercel.json              # Vercel deployment configuration
└── README.md                # This file
```

## 🔑 Key Technologies

- **Flask**: Web framework and API server
- **CrewAI**: Multi-agent orchestration framework
- **Google Gemini AI**: Large Language Model for NLU and analysis
- **Pydantic**: Data validation and schema
- **Matplotlib**: Chart generation
- **RapidFuzz**: Fuzzy string matching
- **WeasyPrint**: PDF report generation (optional)
- **CrewAI Tools**: SerperDev and ScrapeWebsite tools

## 🧪 Example Workflow

1. Customer submits request in Vietnamese
2. NLU Agent parses request into structured JSON
3. Scraper & RAG agents run in parallel to gather market and company data
4. Market Intelligence agent supplements with web research
5. Evaluator agent computes price recommendation
6. Visualizer generates comparison charts
7. Report Generator compiles final HTML/PDF report

## 📊 Output Structure

Reports include:
- Customer profile analysis
- Market price comparisons
- Company product matching
- Recommended price changes
- Alternative scenarios
- Benefit adjustments
- Visual charts
- Detailed rationale

## 🚢 Deployment

### Vercel Deployment

The project is configured for Vercel deployment with `vercel.json`:

```bash
vercel deploy
```

Ensure environment variables are set in Vercel dashboard.

## 🔒 Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `GEMINI_API_KEY` | Google Gemini API key | Yes |
| `SERPER_API_KEY` | Serper.dev search API key | Yes |
| `USE_NATIVE_CREW` | Use native CrewAI (0 or 1) | No |

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📝 License

This project is licensed under the MIT License.

## 🙋 Support

For issues and questions, please open an issue in the GitHub repository.

## 📖 Additional Notes

- The system supports both sequential and parallel agent execution
- Fallback stubs are provided if CrewAI native package is unavailable
- PDF generation requires WeasyPrint (optional on Windows)
- All agents use Pydantic for data validation
- The system gracefully handles API failures with error messages

