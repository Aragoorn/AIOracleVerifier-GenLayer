🛡️ AIOracleVerifier — GenLayer Intelligent Contract
An advanced, production-grade on-chain fact-checking oracle built on GenLayer, leveraging GenVM, real-world web scraping, and custom validator consensus logic.

📖 Overview
AIOracleVerifier is a decentralized intelligent contract designed to solve the oracle problem for subjective and real-world data. Unlike traditional blockchains that rely on deterministic data feeds, this contract uses GenLayer's non-deterministic AI execution to fetch live web sources, analyze statements objectively, and reach secure consensus among decentralized AI validators.

✨ Key Features
Live Web Scraping: Automatically fetches and renders live HTML content from external sources (gl.nondet.web.render) to gather factual evidence.

Non-Deterministic AI Reasoning: Utilizes prompt-based evaluation (gl.nondet.exec_prompt) to judge statements with structured JSON outputs (verdict, confidence, justification).

Custom Validator Consensus (leader_fn & validator_fn): Implements rigorous validation rules where validator nodes independently verify the leader's outcome, ensuring confidence score tolerances and consensus integrity.

Immutable On-Chain State: Persists historical queries, confidence metrics, verdicts, and total verification counters securely on-chain.

🛠️ Contract Architecture
from genlayer import *

@gl.contract
class AIOracleVerifier:
    last_query: str
    last_source: str
    last_result: str
    last_verdict: str
    last_confidence: u256
    verification_count: u256
    
    # ... (core verification, leader_fn, and validator_fn logic)

    🚀 How It Works
Submit Statement & Source: A user calls verify_statement(statement, source_url).

Leader Node Execution: The leader node scrapes the target URL (if provided), builds a strict evaluation prompt, and queries the GenLayer AI runtime for a structured JSON response.

Validator Consensus: Validator nodes run validator_fn to cross-check the verdict and ensure the confidence delta is within safe margins (
≤25
).

State Update: Once consensus is achieved, the verified result is permanently stored on-chain, incrementing the verification counter.

📦 Public Methods
verify_statement(statement: str, source_url: str) -> str: Executes the AI fact-checking flow and returns the formatted verdict.

get_last_result() -> str: Returns the detailed result string of the last verification.

get_last_verdict() -> str: Returns the raw verdict (TRUE, FALSE, or UNCLEAR).

get_last_confidence() -> u256: Returns the confidence score (0-100).

get_verification_count() -> u256: Returns the total number of verified queries processed.

📄 License
This project is open-source and developed for the GenLayer ecosystem.