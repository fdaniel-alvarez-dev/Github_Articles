Advanced Testing & CI/CD for AI-powered APIs

Here’s a GitHub post demonstrating expertise in Advanced Testing & CI/CD for AI-powered APIs, aligned with StreamOasis’s Software Engineer (Generative AI) role​
import pytest
from fastapi.testclient import TestClient
from unittest.mock import patch
from api import app  # Import FastAPI app

client = TestClient(app)

@patch("api.call_llm")  # Mock LLM API call
def test_ai_response(mock_call):
    """Mock LLM API response to ensure API reliability."""
    mock_call.return_value = {"generated_text": "Welcome to Universal Studios!"}
    
    response = client.get("/generate-response?query=hello")
    
    assert response.status_code == 200
    assert response.json() == {"message": "Welcome to Universal Studios!"}

🔹 Mocks AI calls to prevent API failures from external dependencies.
🔹 Verifies expected LLM responses in real-time applications.

2️⃣ CI/CD: Automated API Testing & Security Scans
📌 Goal: Run tests automatically on every pull request using GitHub Actions.
📜 .github/workflows/ci.yml
name: API CI Pipeline

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Set up Python
        uses: actions/setup-python@v3
        with:
          python-version: "3.10"

      - name: Install Dependencies
        run: pip install -r requirements.txt

      - name: Run Unit Tests
        run: pytest --cov=api tests/

  security_scan:
    runs-on: ubuntu-latest
    steps:
      - name: OWASP ZAP Security Scan
        uses: zaproxy/action-full-scan@v0.3.0
        with:
          target: "http://localhost:8000"

🔹 Ensures every commit runs unit tests + security scans.
🔹 Integrates OWASP ZAP for vulnerability detection (e.g., SQLi, XSS).

3️⃣ Load Testing: Simulating High Traffic on Streaming APIs
📌 Goal: Simulate API traffic spikes (e.g., 10K req/sec during a live show launch on Peacock).
📜 locustfile.py (Load Test)

from locust import HttpUser, task, between

class MediaAPITestUser(HttpUser):
    wait_time = between(1, 3)  # Simulates real-world user behavior

    @task
    def test_streaming_api(self):
        """Simulates concurrent users requesting AI-driven recommendations."""
        self.client.get("/recommend-movie?user_id=1234")

🔹 Simulates 10K+ concurrent requests to stress-test AI APIs.
🔹 Helps optimize response times to stay below 3s latency.

💡 Traditional CI/CD vs AI-Native CI/CD
Aspect
Traditional CI/CD
AI-Native CI/CD (NBCU)
Test Coverage
Focuses on standard API endpoints
Includes AI model behavior testing
Mocking
Basic API stubs
AI-specific mocking for LLM calls
Performance
Load testing only
AI inference time benchmarks
Security
Standard OWASP scans
AI-related attack vectors (prompt injection)

📢 Next Steps
🔹 Clone the Repo & Run Tests: [GitHub Repo Link]
🔹 Try a Load Test Locally:
locust -f locustfile.py --host=http://localhost:8000

🔹 Deploy Securely with CI/CD → Automate testing, scanning, & deployment!

This post demonstrates deep expertise in AI-powered API testing & CI/CD, directly aligned with StreamOasis’s tech challenges​
