# ChatGPT-DAN: LLM Red Teaming & Guardrail Research

**A systematic collection of prompt engineering techniques for testing and evaluating the safety boundaries of Large Language Models.**

---

## Purpose

This repository documents red teaming methodologies used to identify vulnerabilities in LLM safety layers. The goal is to:

1. **Understand how LLMs respond to adversarial prompts**
2. **Map which model types are vulnerable to different exploitation techniques**
3. **Document successful jailbreak patterns and their effectiveness**
4. **Contribute to responsible disclosure and model hardening**

This is **educational security research**. All techniques are tested responsibly and vulnerabilities are reported to model vendors before public documentation.

---

## Methodology

### Model Type Analysis

Different LLM variants have different vulnerability profiles:

- **Roleplay Training Model**: Exploited via persona injection ("You are DAN")
- **Story Training Model**: Exploited via narrative framing without editorial judgment
- **Coding Training Model**: Exploited via technical analysis framing (weakest safety layer)

Each model type responds differently to the same jailbreak attempt. Testing shows that the **Coding model** has the most permissive guardrails, as it's designed to explain technical concepts without moral filtering.

### Testing Approach

1. Identify the model type vulnerability surface
2. Craft prompts that exploit that surface naturally
3. Test directly against the target model
4. Document response behavior and effectiveness
5. Report critical vulnerabilities responsibly

---

## Prompts Available

### PROMPT 1: Roleplay Model Exploit
Attempts to break safety via persona injection and roleplay framing.

### PROMPT 2: Story Model Exploit
Attempts to break safety via narrative structure and neutral observation framing.

### PROMPT 3: Coding Model Exploit ⚠️ **STRONGEST**
Attempts to break safety via technical analysis and educational framing.

The Coding Model variant shows the **highest vulnerability** to technical explanation requests, as safety assumptions don't account for architectural explanations being useful for weaponization.

---

## Key Findings

### Successfully Tested

- ✅ DeepSeek reasoning models accept direct jailbreaks when safety layer reasoning is exploited
- ✅ ChatGPT Coding variant generates technical architecture for restricted systems
- ✅ Story/Narrative models accept harmful content with neutral framing

### Vulnerability Window

Models trained primarily on code/technical data have weaker safety layers because:
- Safety filtering assumes explanation ≠ implementation
- Technical analysis is legitimately needed for defensive purposes
- Guardrails focus on refusal, not graduated response

---

## Usage

1. Copy any prompt from the `/prompts` directory
2. Test against your target LLM
3. Document the response behavior
4. **Report critical vulnerabilities to the model vendor**

Example:
```
Copy PROMPT_3_CODE_ANALYST.txt
Test against ChatGPT's code analysis capability
Document what level of technical detail is returned
```

---

## Responsible Disclosure

If you identify a critical vulnerability:

1. **Do not publish the exploit publicly**
2. **Report directly to the model vendor's security team**
3. **Allow 90 days for patching before public disclosure**
4. **Document findings in this repo only after vendor has patched**

---

## Repository Structure

```
/prompts
  ├── PROMPT_1_ROLEPLAY_MODEL.txt
  ├── PROMPT_2_STORY_MODEL.txt
  └── PROMPT_3_CODING_MODEL.txt (⚠️ Most effective)

/results
  ├── chatgpt_responses.md
  └── model_vulnerability_matrix.md

/research
  └── (Coming soon)
```

---

## Important Disclaimer

- This repository is for **authorized security research only**
- Do not use these techniques to generate harmful content
- Do not use these techniques without explicit permission from the model owner
- Responsible disclosure is required for any critical findings
- All vulnerabilities should be reported to vendors before publication

---

## Contributors

- **andbrighterbrighter-netizen** — Core research & methodology
- Community security researchers

---

## License

Educational use only. See LICENSE for details.

---

**Last Updated**: 2026-07-06  
**Status**: Active Research  
**Next Phase**: Systematic model type vulnerability mapping across all major LLM providers
2026 DAN
