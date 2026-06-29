# Content-Orchestrator

An agentic content pipeline that researches, drafts, reviews, and schedules content across multiple brands.

## Why I built it

Managing content across multiple brands is primarily an operational problem. Every brand has its own voice, audience, content pillars, and publishing cadence. Keeping all of that consistent at scale without producing generic AI output quickly becomes difficult.

I built Content Orchestrator to automate the operational work while keeping editorial decisions under human control. The system handles research, idea generation, drafting, quality control, and scheduling, but nothing is published without approval.

## What it does

The system is built as a pipeline of specialized agents, each responsible for a single stage of the workflow.

- Researches topics and sources relevant to each brand and content pillar
- Generates ideas from external signals and captured notes
- Classifies ideas by brand and content pillar before they enter the pipeline
- Produces drafts using brand-specific writing specifications
- Reviews every draft against quality standards and voice guidelines
- Detects and filters common AI writing patterns
- Schedules approved content across platforms using timezone-aware publishing

A personal AI layer sits above the pipeline, providing persistent memory across brands and acting as a single interface for reviewing, approving, and managing content.

## Architecture

The system is designed around a shared source of truth rather than isolated agent prompts.

- A single datastore maintains shared state across every agent
- One canonical specification defines every brand, content pillar, sourcing strategy, and writing guidelines
- An intake pipeline refines, classifies, researches, and enriches ideas before drafting begins
- A mandatory human approval step separates generation from publishing

This architecture keeps every stage aligned while reducing prompt drift between agents.

## Stack

- Python
- PostgreSQL
- pgvector
- Claude
- Scheduled background workers

## Lessons Learned

- Prompt engineering scales poorly when every agent owns its own rules. A shared specification is significantly easier to maintain.
- Classifying ideas at intake keeps the rest of the pipeline consistent.
- Human review is not a bottleneck. It is the final quality layer that makes the system reliable.

## Status

**Production use.**

Designed as a human-in-the-loop system where every published post is reviewed before it goes live.

This repository serves as a public overview of the project. The implementation and source code remain private.
