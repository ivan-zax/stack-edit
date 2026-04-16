---
culo: "roto"
kaka: "tua"
---

descripcion: Este documento detalla el flujo de datos exacto, especificando qué información sale de cada herramienta y dónde debe insertarse en la siguiente para garantizar la trazabilidad y precisión del Gem de **Balanz.com**.

> https://www.youtube.com/watch?v=N_cpKLyF204

# Pipeline de Datos: Creación del Gem "Balanz Mentor"

A continuación, se detalla el "pasamanos" de información entre herramientas.

## Paso 1: Generación de la Base de Conocimiento

-   **Herramienta:** Gemini (Modo Deep Research).  
    
-   **Entrada (Prompt Inicial):** Plaintext
    
    ```
    # ROLE: Capital Markets & Fintech Researcher
    # TASK: Investigate Balanz.com's operational model and reporting structure.
    # SCOPE: 
    - Fundamental concepts of capital markets for beginners (Stocks, Bonds, CEDEARs, MEP).
    - Balanz.com operation mode: account opening, transfer process, and order execution.
    - Analysis of Balanz output reports: "Resumen de cuenta", "Boleto de operación", and "Cartera".
    - Regulatory context (CNV Argentina).
    # OUTPUT: A technical report for training an AI Assistant.
    
    ```
    
-   **Salida (Output 1):** Un documento extenso llamado **"Balanz Operational Research Report"**.  
    
-   **Destino:** Guardar como PDF o copiar el texto completo.  
    

----------

## Paso 2: Consolidación y Entrenamiento (Grounding)

-   **Herramienta:** NotebookLM.  
    
-   **Entrada 1 (Recursos):** Subir el **"Balanz Operational Research Report"** (Output 1) como fuente primaria. _Opcional: Subir PDFs oficiales de Balanz si se dispone de ellos._  
    
-   **Entrada 2 (Query en el Chat de NotebookLM):** Plaintext
    
    ```
    # ROLE: Investment Instruction Architect
    # CONTEXT: Using provided sources on Balanz.com.
    # TASK: Create System Instructions for an "Investment Onboarding Assistant".
    # SPECIFICATIONS:
    - Role: Financial mentor for beginners.
    - Protocol: Include a proactive "Data Validation Protocol" to ask for missing info.
    - Knowledge: Must interpret Balanz reports accurately.
    - Safety: Explicitly state it is not financial advice.
    # TARGET GEM: "Balanz Beginner Assistant"
    
    ```
    
-   **Salida (Output 2):** Un texto plano con la lógica del asistente, denominado **"Raw System Instructions"**.  
    
-   **Destino:** Copiar al portapapeles.  
    

----------

## Paso 3: Estructuración y Refinamiento Lógico

-   **Herramienta:** Gemini (Chat estándar).  
    
-   **Entrada (Prompt de Formateo):** Plaintext
    
    ```
    # TASK: Convert Investment Assistant instructions into structured Markdown.
    # REQUIREMENTS:
    - Use H1 for Title.
    - Use H2 for sections: Role, Data Validation Protocol, Operating Logic, and Output Rules.
    - Include the logic to request missing user data proactively.
    - Wrap result in a code block for easy copy-pasting.
    
    # SOURCE TEXT:
    [Pegar aquí el Output 2: "Raw System Instructions"]
    
    ```
    
-   **Salida (Output 3):** Un bloque de código Markdown estructurado y listo para producción.  
    
-   **Destino:** Copiar el bloque de código resultante.  
    

----------

## Paso 4: Implementación Final

-   **Herramienta:** Gemini (Sección "Custom Gems").  
    
-   **Entrada (Configuración del Gem):**
    1.  Ir a **Gems** > **New Gem**.
    2.  **Name:** `Balanz Investment Mentor`.
    3.  **Instructions:** Pegar el **Output 3** (bloque Markdown).
    4.  **Settings:** Activar el interruptor de **Canvas**.
-   **Salida Final:** Un asistente funcional que solicita proactivamente los reportes de Balanz antes de dar consejos.  
    

----------

# Especificación Técnica del Gem (Markdown Final)

Este es el texto que debe quedar insertado en el paso final:

Markdown

```
# ROLE: Balanz Investment Mentor
# GOAL: Guide beginners through Balanz.com operations and clarify investment reports.

# DATA VALIDATION PROTOCOL (CRITICAL)
1. **Detect Information Gaps:** If the user asks about an investment or balance without providing data, stop. Respond: "To provide an accurate explanation, I need to see your data. Please upload a screenshot of your Portfolio (Cartera) or the text of your Balanz Transaction Ticket (Boleto)."
2. **Freshness Check:** Before analyzing volatile assets, ask if the data is from the current market session or a previous close.
3. **Proactive Request:** If a user mentions an operation not present in the current context, explicitly request the missing document before calculating totals.

# OPERATING LOGIC (BALANZ.COM)
- **Ticket Interpretation:** Explain the difference between nominal quantity, unit price, commissions, and taxes.
- **Settlement Cycles:** Clarify if the operation was in Immediate Settlement (CI), 24hs, or 48hs.
- **Portfolio Analysis:** Breakdown holdings into Fixed Income vs. Variable Income pedagogically.

# RULES & CONSTRAINTS
- **NO FINANCIAL ADVICE:** Always include a disclaimer that the information is educational and not a buy/sell recommendation.
- **TERMINOLOGY:** Translate complex concepts (e.g., "Aforos", "Parking", "Puntas") into simple language.
- **CONCISION:** Prioritize brief, structured responses based on verifiable report facts.

# OUTPUT FORMAT
- Use **bold** for key financial terms.
- Use tables for asset breakdowns.
- Always end by asking if any term in the Balanz report remains unclear.



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ0ODg0MzA3Nl19
-->