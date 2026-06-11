# English Notes Project - Complete Plan

## 1. Project Overview

- **Goal**: Translate 478 notes from Spanish to English while preserving original tone and technical accuracy
- **Core Philosophy**: Faithful translation > artificially enhanced personality. Better to lose personality than to add humor where none existed
- **Output**: Parallel folder `/Notes-English/` with identical structure

---

## 2. Folder Structure

```
/home/dobliuw/Desktop/Hacking/
├── Notes/                      ← Original (Spanish)
│   ├── 0. Technology/
│   ├── 1. Finance/
│   └── ...
│
└── Notes-English/              ← NEW - Parallel project
    ├── 0. Technology/
    ├── 1. Finance/
    └── ... (mirrored structure)
```

**Naming convention**: Files keep original names (Spanish), content is translated

---

## 3. What Gets Preserved (Exact)

| Element | Example | Action |
|---------|---------|--------|
| Code blocks | ```bash ... ``` | Keep exact |
| Tags | `Tags: #linux #basico` | Keep exact |
| Obsidian callouts | `> [!info] Consideraciones` | Keep structure |
| Wikilinks | `[[Linux Basics]]` | Keep as-is (Spanish) |
| Horizontal rules | `----` | Keep exact |
| Images | `![[image.png]]` | Keep path reference |
| Numbered headers | `1.`, `2.` prefixes | Keep structure |

---

## 4. What Gets Translated

- All Spanish text content → English
- Headings (`# Title`) → English
- Inline text explanations → English
- Comments in code (if Spanish) → English
- Link text (visible text) → English (destination stays Spanish)

---

## 5. Voice Preservation Strategy

**The Golden Rule**: Translate what you wrote, not what you wish you wrote

| Original Note Style | Translation Approach |
|---------------------|----------------------|
| Technical/dry | Technical/dry English |
| Personal experiences | Preserved ("I discovered...", "When I tried...") |
| "Why" explanations | Preserved (keep your deeper explanations) |
| Casual/direct ("vos") | Casual English ("you", direct tone) |
| With jokes/humor | Jokes translated, not invented |
| No personality | No personality added |

**System Prompt for LLM**:
```
You are translating personal technical notes from Spanish to English.
RULES:
1. Preserve the original TONE - if it's technical, keep it technical. If it's casual, keep it casual.
2. Do NOT add jokes, humor, or personality that wasn't in the original.
3. Keep markdown formatting: code blocks, wikilinks [[...]], callouts > [!...], tags, horizontal rules.
4. Translate content to natural English, not literal.
5. Keep Spanish internal links [[Note Name]] as-is.
6. Maintain technical accuracy - terminology should be correct.
7. Preserve personal experiences and "why" explanations that are in the original.
```

---

## 6. Processing Pipeline

**Step 1**: Create folder structure (mirror)

```bash
cd /home/dobliuw/Desktop/Hacking
mkdir -p Notes-English
cd Notes-English
find ../Notes -type d | sed 's|../Notes|/Notes-English|' | xargs mkdir -p
```

**Step 2**: Batch process with Ollama

Option A: Python script with concurrent LLM calls
- Read each `.md` from `/Notes/`
- Send to Ollama with voice prompt
- Write result to corresponding path in `/Notes-English/`

Option B: Bash + parallel processing
- Use `parallel` or `xargs` for concurrent processing
- Process multiple notes simultaneously

**Step 3**: Validation checks
- Verify all 478 files created
- Spot-check random samples for quality
- Check for empty files (failed translations)

---

## 7. Processing Recommendations

- **Concurrency**: 3-5 parallel translations (depends on hardware)
- **Model**: Use your existing `llama-3.2-3b-instruct` or larger model
- **Chunk strategy**: Notes with <5000 chars translate in one pass; larger notes may need chunking
- **Error handling**: Log failures, retry once, skip if fails twice (manual review)

---

## 8. Quality Assurance

**Auto-checks**:
- Count: 478 input → 478 output
- Size: Output should be ~80-90% of input (English more compact)
- Non-empty: No 0-byte files

**Spot-check** (manual):
- Review 10 random notes for:
  - Technical accuracy
  - Tone fidelity
  - Format preservation
- Flag any notes needing manual review

**Link validation**:
- Verify `[[wikilinks]]` preserved correctly
- No broken image references

---

## 9. Future Maintenance

**One-way sync**: When you update Spanish notes, how to update English?

- **Manual sync** (recommended initially): You choose which notes to update, process only changed files
- **Git-based workflow**: Keep English notes in separate Git branch or repo, pull from Spanish branch when needed
- **Run on-demand**: Script can re-run for any note when you update original

**Recommended**: Start with manual sync, upgrade if needed

---

## 10. Implementation Checklist

- [ ] Create `/Notes-English/` folder structure
- [ ] Write system prompt to `voice-prompt.txt`
- [ ] Test translation on 3-5 sample notes
- [ ] Review samples for quality/voice
- [ ] Run batch process on all 478 notes
- [ ] Validate output (count, size, non-empty)
- [ ] Spot-check random samples (10+)
- [ ] Document any manual fixes needed

---

## 11. Sample Notes to Test First

Recommended first tests:
1. `Notes/0. Technology/3. System/Operative Systems/0. Linux/0. Linux Basics.md` (414 lines - has personality)
2. `Notes/0. Technology/5. Technologies/Languages/Scripting en Bash.md` (115 lines - technical)
3. `Notes/0. Technology/4. Cybersecurity/AI Powered/1. Attacks Powered by AI/1. AI in our Terminal.md` (86 lines - mixed)
4. `Notes/1. Finance/0. Finance Fundamentals.md` (shorter)

---

## 12. Tools You Already Have

- **Ollama** (llama-3.2-3b-instruct) - Translation engine
- **Your terminal** - Script execution
- **Obsidian** - Manual verification if needed