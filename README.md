# InsightPulse AI

### Turning audience comments into real-time actionable insights using AI

---

## Overview

**InsightPulse AI** is a production-grade end-to-end AI system that analyzes large-scale YouTube and Instagram comments in real-time using NLP and MLOps pipelines. It is delivered as a **Chrome Extension** that integrates directly with YouTube and Instagram in the browser.

It helps influencers transform unstructured audience feedback into **actionable insights**, enabling data-driven content and engagement strategies.

---

## Origin & Business Context

This project was conceived while working at an **Influencer Management Company (IMC)**.

### What is an IMC?

An IMC acts as an intermediary between brands and influencers:

- A brand like Samsung wants a popular influencer to market their product
- Samsung does not contact the influencer directly — they go through the IMC
- The IMC then reaches out to the influencer on the brand's behalf

### The Problem the IMC Faced

- Limited marketing budget to attract new clients (brands) and onboard new influencers
- Needed a way to demonstrate value and build trust with influencers before formally onboarding them

### The Strategy

Build a free tool that genuinely helps influencers solve a real pain point. Once influencers see value, they trust the IMC and are willing to onboard. The tool acts as the growth lever — solving a problem influencers actually have, while building the IMC's influencer network.

### Why Comment Analysis?

Influencers receive **millions of comments** across their content but have no solid mechanism (on YouTube or Instagram) to make sense of them at scale. Understanding what their audience feels, wants, and needs is critical for content strategy — but manually reading thousands of comments is not feasible.

**InsightPulse AI solves this.**

---

## Problem Statement

Influencers struggle to:

- Understand audience sentiment across thousands or millions of comments
- Identify key feedback, suggestions, and concerns from their community
- Track how sentiment evolves over time
- Detect spam or bot-generated comments polluting their data
- Make informed, data-backed content decisions

Neither YouTube nor Instagram provides a solid native mechanism for this kind of analysis.

---

## Solution

InsightPulse AI provides a **Chrome Extension** that sits directly on top of YouTube and Instagram in the browser, requiring zero workflow change from the influencer.

- Real-time comment analysis right on the video/post page
- NLP-powered sentiment classification
- Automated comment summarization and theme extraction
- Trend tracking over time
- Spam and bot detection
- Interactive charts and visualizations

**Why a Chrome Extension?**
It integrates seamlessly with YouTube and Instagram already open in the browser, eliminating any friction of switching to a separate tool. This was a deliberate product decision to maximize adoption.

---

## Features

### Feature 1: Sentiment Analysis

**Real-time Sentiment Classification**
- Analyzes all comments on a YouTube video or Instagram post in real time
- Classifies each comment as Positive, Negative, or Neutral

**Sentiment Distribution Visualization**
- Pie charts showing percentage breakdown of Positive / Negative / Neutral comments

**Detailed Sentiment Insights**
- Drill down into comments by sentiment category

**Trend Tracking**
- X-axis: time / date of comments
- Y-axis: volume of Positive, Negative, and Neutral comments
- Reveals how audience sentiment shifts over time

---

### Feature 2: Comment Summarization

**Automated Comment Summarization**
- Condenses thousands of comments into a concise summary

**Key Theme Highlighting**
- Identifies and surfaces dominant themes: suggestions, feedback, concerns raised by the audience

**Topic Modelling** *(paid feature)*
- Dropdown-based topic exploration for deeper audience segmentation

---

### Feature 3: Additional Comment Analytics

**Word Cloud Visualization**
- Visual representation of the most frequently used words in comments

**Average Comment Length**
- Metric indicating depth of audience engagement

**Spam and Troll Detection**
- Dedicated model to filter out spam and bot-generated comments
- Keeps analysis clean and based on genuine audience feedback

**Export Data Functionality**
- Export raw data, insights, and reports (CSV / structured formats)

---

## System Architecture

```
YouTube / Instagram Page (Chrome Browser)
                ↓
        Chrome Extension (JS)
                ↓
          Flask API (Backend)
                ↓
     ML Models (Sentiment + NLP + Spam)
                ↓
        Aggregation & Processing Layer
                ↓
    Frontend Visualizations (Charts, Insights)
```

---

## Tech Stack

### Machine Learning & NLP

- Scikit-learn (TF-IDF, Logistic Regression)
- NLTK / spaCy (text preprocessing)
- Optuna (hyperparameter tuning)

### MLOps

- DVC (Data Version Control and pipeline management)
- MLflow (experiment tracking and model registry)

### Backend

- Flask (REST APIs)

### Frontend

- Chrome Extension (JavaScript, HTML, CSS)
- D3.js (visualizations)

### Cloud & DevOps

- AWS EC2 (hosting)
- AWS S3 (data storage)
- Docker (containerization)
- GitHub Actions (CI/CD)

### Testing

- Pytest (backend and ML)
- Jest (frontend / extension)

---

## Project Workflow

The end-to-end build follows this sequence:

1. **Data Collection** — Fetch comments using YouTube Data API v3 (video ID + developer API key)
2. **Data Preprocessing** — Cleaning, normalization, tokenization
3. **EDA** — Exploratory Data Analysis to understand data distributions and quality
4. **Model Building** — Training, hyperparameter tuning, evaluation, and experiment tracking (MLflow)
5. **DVC Pipeline** — Reproducible ML pipeline with data and model versioning
6. **Model Registry** — Register and version production-ready models via MLflow
7. **API Development** — Build Flask REST API to serve model predictions
8. **Chrome Extension Development** — Build the browser plugin integrating with YouTube and Instagram
9. **CI/CD Setup** — GitHub Actions pipelines for automated testing and deployment
10. **Testing** — Unit, integration, and API testing
11. **Docker** — Containerize the backend service and push image to Docker Hub
12. **Deployment** — Deploy on AWS EC2 with monitoring

---

## Challenges

### Data Challenges

| Challenge | Detail |
|---|---|
| Data availability | Comments can be fetched via YouTube API with video ID and API key, but labeled datasets for training are scarce |
| Dataset generalization | Lack of diverse domain coverage (political, entertainment, educational, etc.) |
| Multi-language comments | Global influencer audiences comment in many languages |
| Slang, emojis, informal text | Non-standard language patterns are hard for traditional NLP |
| Sarcasm detection | A comment that is positive in phrasing may carry negative intent |
| Evolving language | Words change meaning over time (e.g., "sick" = ill or great) — leads to model drift |
| Privacy and data compliance | Handling user-generated content requires compliance with data regulations |
| Spam and bot comments | Bot-generated noise degrades model quality and analysis accuracy |

### Latency Challenges

- Real-time analysis on an active page demands low-latency inference
- Model serving must be optimized to avoid noticeable delay in the extension UX

### Model Challenges

- Data noise and variability across domains
- Class imbalance (negative comments often underrepresented)
- Model drift as language evolves over time

### User Experience Challenges

- Surfacing insights in a clean, intuitive way within the extension UI
- Ensuring the extension does not slow down the browser page

---

## Deployment

- Dockerized backend service pushed to Docker Hub
- CI/CD pipeline via GitHub Actions
- Deployed on AWS EC2
- Monitoring via AWS CloudWatch

---

## Testing

- Unit and integration testing for ML pipeline and backend using Pytest
- API testing via Postman
- Frontend and extension testing using Jest

---

## Project Structure

```
InsightPulse_AI/
├── data/
├── notebooks/
├── src/
├── api/
├── chrome_extension/
├── mlops/
├── tests/
└── docker/
```

---

## How to Run Locally

```bash
# Clone repo
git clone https://github.com/your-username/InsightPulse_AI.git

# Install dependencies
pip install -r requirements.txt

# Run API
python api/app.py
```

---

## Future Improvements

- Transformer-based models (BERT / DistilBERT) for higher accuracy
- Multi-language support
- Real-time streaming pipeline (Kafka)
- GenAI-based auto-reply suggestions for influencers
- Personalization dashboard per influencer

---

## License

This project is licensed under the MIT License.

---

## Author

**Avinash Yerolkar**
Machine Learning Engineer | AI Enthusiast
