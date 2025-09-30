# Agents Instructions – How to Use

This repository includes a **modular system** for defining rules and instructions for coding agents (Copilot, Claude, Gemini, etc.).

## Structure
- **AGENTS-TEMPLATE.md** → Main template. Summarizes all rules and links to modules.  
- **AGENTS-GUIDED-PROMPT.md** → Paste into your coding agent to be guided step by step in completing the template.  
- **MODULES-INDEX.md** → Index of all available modules with their scope.  
- **/modules/** → Individual modular instruction files (`*.instructions.md`).  
- **README-START.md** → Quick start guide.  

## How to Use
1. **Choose Modules**  
   - Open `MODULES-INDEX.md`.  
   - Decide which modules apply (core are mandatory, optional can be added).  

2. **Fill Each Module**  
   - Open files in `/modules/`.  
   - Complete the sections: **Inputs Required**, **Rules**, **Examples**, **Validation**, **Source of Truth**.  
   - Use the “Fill-in tips” included in each file.  

3. **Use Guided Prompt**  
   - Open `AGENTS-GUIDED-PROMPT.md`.  
   - Paste it into your coding agent and type **start**.  
   - Answer questions; the agent will help you complete all modules and assemble the master `AGENTS.md`.  

4. **Maintain Master File**  
   - Keep `AGENTS.md` short and high-level.  
   - Put details in `/modules/`.  
   - Update whenever project rules change.  
