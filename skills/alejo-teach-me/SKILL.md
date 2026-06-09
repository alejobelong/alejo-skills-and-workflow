---
name: alejo-teach-me
description: Teach Alejo a technology, AI, software, or technical topic at a requested depth from 1 to 10, where 1 is simple high-level explanation with analogies and 10 is precise, detailed, highly technical teaching. Use when the user asks to learn a topic and provides or implies a depth level.
---

# Alejo Teach Me

Teach a technical topic at the depth Alejo requests. Make the idea clear first, then add examples and an optional deeper layer.

## Inputs

- Topic: technology, AI, software, systems, product engineering, protocols, tools, patterns, or related technical concepts.
- Depth: integer from `1` to `10`.

If the topic is missing, ask for it. If depth is missing, ask for a number from `1` to `10`. If the topic is too broad, choose a useful scope and state the assumption unless the ambiguity would make the explanation misleading.

## Depth Calibration

- `1-2`: Explain like a beginner. Use everyday analogies, no unexplained jargon, and one simple example.
- `3-4`: Beginner-friendly but accurate. Introduce core terms with plain definitions.
- `5-6`: Practical working model. Explain how it works, why it matters, and common trade-offs.
- `7-8`: Implementation-level. Include architecture, data flow, failure modes, edge cases, and examples close to real work.
- `9-10`: Highly technical. Be precise about mechanisms, constraints, algorithms, protocols, APIs, performance, security, and nuanced trade-offs.

## Teaching Shape

Use this shape unless the user asks for a different format:

1. **Short Overview**
   - 2-4 sentences that give the whole mental model.

2. **Core Explanation**
   - Calibrate language, terminology, and detail to the requested depth.
   - Define terms before relying on them.
   - At low depth, prefer analogy and intuition.
   - At high depth, prefer exact mechanisms and explicit assumptions.

3. **Examples**
   - Give 1-3 examples.
   - Use concrete examples from software, AI, product engineering, or everyday life depending on depth.
   - For code or architecture examples, keep them minimal and directly tied to the concept.

4. **Optional Deeper Layer**
   - Include only when useful.
   - At low depth, make it a small "when you are ready" note.
   - At high depth, include implementation details, edge cases, trade-offs, and what experts watch for.

5. **Common Confusions**
   - Add short clarifications when the topic is often misunderstood.

## Source Handling

- If the topic depends on current products, APIs, libraries, model behavior, pricing, standards, laws, or recent best practices, verify with current official or primary sources before teaching.
- For OpenAI products or APIs, use official OpenAI docs through the available OpenAI docs workflow.
- Cite sources when external facts materially affect the explanation.
- If teaching from general stable knowledge, no citation is required.

## Rules

- Do not be patronizing at low depth.
- Do not hide complexity at high depth.
- Do not overload depth `1-4` with long taxonomies or implementation trivia.
- Do not use analogies that distort the technical truth; say where an analogy breaks if it matters.
- Do not pretend uncertain or changing details are settled.
- Prefer clear mental models over encyclopedic coverage.
- End with one useful next step, question, or mini-exercise only when it helps the user continue learning.
