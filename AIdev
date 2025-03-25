# ✅ FastAPI Backend for Agentic AI - Claims Triage
from fastapi import FastAPI, Request
from pydantic import BaseModel
from fastapi.middleware.cors import CORSMiddleware
import os
from typing import Optional

# Optional: Load environment variables from a .env file
from dotenv import load_dotenv
load_dotenv()

# Agentic AI (LangChain/AutoGen integration example - simplified placeholder)
def agentic_claims_triage(claim_id: str) -> dict:
    # Simulated policy lookup and decision logic
    mock_data = {
        "CLM123": {"holder": "John Doe", "valid": True, "amount": 12000},
        "CLM999": {"holder": "Jane Smith", "valid": False, "amount": 8500},
    }
    data = mock_data.get(claim_id)
    if not data:
        return {"status": "error", "message": "Claim not found."}

    if not data["valid"]:
        decision = "Denied - Policy Invalid"
    elif data["amount"] > 10000:
        decision = "Escalated - Amount exceeds threshold"
    else:
        decision = "Approved"

    return {
        "claim_id": claim_id,
        "holder": data["holder"],
        "amount": data["amount"],
        "decision": decision
    }

# FastAPI Setup
app = FastAPI()

# Enable CORS for frontend communication
app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)

# Request schema
class ClaimRequest(BaseModel):
    claim_id: str

# Route to handle claims triage
@app.post("/triage")
async def triage_claim(request: ClaimRequest):
    result = agentic_claims_triage(request.claim_id)
    return result

# Health check route
@app.get("/")
def root():
    return {"message": "Agentic AI Claims Triage API is running."}
