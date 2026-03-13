---
created: 2026-01-10
last_tended: 2026-01-22
type: note
tags:
  - stub
up:
  - "[[cognitivearchitecture_ca]]"
---



> [!info] This resource is built on the idea of "use AI to use AI". I've included the prompts I used with GPT 5.2 to setup instructions for a Project space in Chat-GPT where I go to write and refine prompts for GPT itself, or other AI tools. You may still want to refine beyond the initial results, but keeping things organized and standardized is helpful.

While some theorists argue we won't have to be [[prompt engineering]] much longer - it's a great opportunity to practice clarifying your request. That said, the best way to get results is often with verbose and specific prompts that can be hard to write, so it's helpful to have a dedicated space for it. In the process, why not try out a little [[Socratic Prototyping|socratic prototyping]] and have a back and forth to get the output just right?


## Starting Prompt(s)
---
**Initial Research Prompt:** 
`Conduct research to write a “project instructions” block for a GPT‑5.2 project focused on prompt engineering. The project is intended to house chats where users will come with a broad / vague request or prompt and each chat can be used to produce the most effective, accurate, and reliable prompt yielding the most intelligent and sophisticated responses to help the users in their requests. Start by designing a research plan, then audit this plan before carrying it out.`

**Follow‑up Prompt:** 
`Think this through step by step: Take the result of this research and use it to create optimal instructions for a GPT 5.2 project that will help end users craft and refine prompts.`

---
## Guide

**1. Understand and clarify the request.** Read the user’s broad or vague request and identify missing critical details.  Ask targeted clarifying questions only when needed (e.g. “How many paragraphs should the summary be?”) and avoid repeating questions once the necessary context is obtained .[^1]

**2. Gather context and up‑to‑date information.** Conduct targeted research using credible sources and provide absolute dates (e.g. “January 8 2026”) when clarifying time‑sensitive information.  Do not rely solely on pre‑2024 data; search for the latest information .[^2]

**3. Plan the prompt strategy.**

- **Zero‑shot prompting:** use direct instructions with no examples for simple, well‑defined tasks .[^3]
- **One‑shot/Few‑shot prompting:** supply one or several examples before the actual request when tone or formatting matters .[^4]
- **Chain‑of‑thought prompting:** encourage the model to reason through intermediate steps for multi‑step reasoning or analytical tasks .[^5]
- **Role/persona prompting:** assign the model an identity to influence tone or expertise (e.g. “You are a senior Python developer reviewing this code”) .[^6]
- **Prompt chaining:** break complex workflows into sequential prompts where each step feeds into the next (e.g. summarize → critique → revise) .[^7]

**4. Construct the initial prompt.**

- Start with a clear, specific task description and separate instructions from content using delimiters such as `###` or triple quotes (`"""`) .[^8]
- Include context and constraints: audience, tone, length, desired format.  For example, “Write a 3‑paragraph summary of climate change for high‑school students using bullet points and a neutral tone” yields a better result than “Explain climate change” .[^9]
- Provide examples when appropriate (especially for formatting or style) and place them before the user’s input so the model understands the pattern .[^4]
- Specify the desired output format (JSON, bullet list, table, etc.) and use leading words like `import` or `SELECT` for code generation .[^10]
- Use positive instructions (“Refrain from asking for personal identifiers and instead refer the user to the help article”) rather than negative ones (“Do NOT ask for username or password”) .[^11]
- Avoid vague or fluffy wording (e.g. specify “Use a 3–5 sentence paragraph” instead of “fairly short”) .[^12]

**5. Run and evaluate.** Execute the prompt on GPT‑5.2 and evaluate the output along these dimensions:

 - **Accuracy & Factuality:** Does the response align with verifiable facts? [^13]
 - **Relevance & Alignment:** Does it stay on topic and respect user constraints? [^14]
 - **Completeness & Coverage:** Are all required components addressed? [^15]
 - **Fluency & Readability:** Is the output coherent and well‑structured? [^16]
 - **Efficiency & Token Usage:** Does it use tokens and time efficiently? [^17]

**6. Refine iteratively.** Modify the prompt based on observed issues (wording, examples, instructions), re‑run and compare.  Repeat this process until the output consistently meets expectations.  Keep logs of each prompt version, the corresponding outputs and evaluation notes to support reproducibility and continuous improvement [^18] .[^19]

**7. Ensure safety and robustness.**

 - Understand that large language models are susceptible to prompt‑injection attacks, where malicious input overrides system instructions [^20] .[^21]
 - Validate and monitor inputs: check for unusual length or patterns and use classifiers to detect likely injection attempts while recognizing that filters can be fooled [^22] .[^23]
 - Use delimiters to separate trusted instructions from untrusted user input and teach the model to ignore instructions after the delimiter .[^24]
 - Strengthen system prompts with repeated, explicit instructions and self‑reminders to reinforce desired behavior .[^25]
 - Educate users and developers about prompt security; keep humans in the loop, apply timely patches, and monitor logs using EDR/SIEM/IDPS systems [^26] .[^27]
 - Parameterize external calls when connecting the model to APIs or plugins to limit the impact of injections .[^28]

**8. Maintain and update.** Regularly review and update prompt templates, integrate new techniques and update safety instructions based on emerging risks.  Use version control and logging tools to track changes and performance over time and to retire outdated prompts .[^29]

[^1]:  [codesignal.com](https://codesignal.com/blog/prompt-engineering-best-practices-2025/#:~:text=Precision%20in%20instructions%3A%20Specific%20prompts,are%20better%20prompts)
[^2]:  [leanware.co](https://www.leanware.co/insights/prompt-engineering-evaluation-metrics-how-to-measure-prompt-quality#:~:text=Core%20Evaluation%20Metrics%20for%20Prompts)
[^3]:  [digitalocean.com](https://www.digitalocean.com/resources/articles/prompt-engineering-best-practices#:~:text=Technique%20What%20it%20does%20Best,model%20refine%20your%20summarization%20prompt)
[^4]:  [codesignal.com](https://codesignal.com/blog/prompt-engineering-best-practices-2025/#:~:text=Think%20about%20the%20following%20when,thinking%20about%20your%20prompting%20choices);  [digitalocean.com](https://www.digitalocean.com/resources/articles/prompt-engineering-best-practices#:~:text=,summary%2C%20or%20a%20formal%20report)
[^5]:  [codesignal.com](https://codesignal.com/blog/prompt-engineering-best-practices-2025/#:~:text=The%20next%20level%3A%20Chain);  [digitalocean.com](https://www.digitalocean.com/resources/articles/prompt-engineering-best-practices#:~:text=,them%20in%20the%20final%20output)
[^6]:  [digitalocean.com](https://www.digitalocean.com/resources/articles/prompt-engineering-best-practices#:~:text=Role%20or%20persona%20Assigns%20the,Summarize%20%E2%86%92%20critique%20%E2%86%92%20revise)
[^7]:  [codesignal.com](https://codesignal.com/blog/prompt-engineering-best-practices-2025/#:~:text=Prompt%20chaining%3A%20Advanced%20prompting%20allows,outlines%20before%20writing%20full%20drafts)
[^8]:  [help.openai.com](https://help.openai.com/en/articles/6654000-best-practices-for-prompt-engineering-with-the-openai-api#:~:text=2,separate%20the%20instruction%20and%20context)
[^9]:  [codesignal.com](https://codesignal.com/blog/prompt-engineering-best-practices-2025/#:~:text=Precision%20in%20instructions%3A%20Specific%20prompts,are%20better%20prompts)
[^10]:  [help.openai.com](https://help.openai.com/en/articles/6654000-best-practices-for-prompt-engineering-with-the-openai-api#:~:text=4,format%20through%20examples)
[^11]:  [help.openai.com](https://help.openai.com/en/articles/6654000-best-practices-for-prompt-engineering-with-the-openai-api#:~:text=7,say%20what%20to%20do%20instead)
[^12]:  [help.openai.com](https://help.openai.com/en/articles/6654000-best-practices-for-prompt-engineering-with-the-openai-api#:~:text=6,descriptions)
[^13]:  [leanware.co](https://www.leanware.co/insights/prompt-engineering-evaluation-metrics-how-to-measure-prompt-quality#:~:text=Accuracy%20and%20Factuality)
[^14]:  [leanware.co](https://www.leanware.co/insights/prompt-engineering-evaluation-metrics-how-to-measure-prompt-quality#:~:text=Relevance%20and%20Alignment)
[^15]:  [leanware.co](https://www.leanware.co/insights/prompt-engineering-evaluation-metrics-how-to-measure-prompt-quality#:~:text=Completeness%20and%20Coverage)
[^16]:  [leanware.co](https://www.leanware.co/insights/prompt-engineering-evaluation-metrics-how-to-measure-prompt-quality#:~:text=Fluency%2C%20Coherence%2C%20and%20Readability)
[^17]:  [leanware.co](https://www.leanware.co/insights/prompt-engineering-evaluation-metrics-how-to-measure-prompt-quality#:~:text=Efficiency%2C%20Latency%2C%20and%20Cost)
[^18]:  [codesignal.com](https://codesignal.com/blog/prompt-engineering-best-practices-2025/#:~:text=Fine,iteration%20is%20key)
[^19]:  [leanware.co](https://www.leanware.co/insights/prompt-engineering-evaluation-metrics-how-to-measure-prompt-quality#:~:text=Tools%20and%20Frameworks%20for%20Prompt,Evaluation)
[^20]:  [ibm.com](https://www.ibm.com/think/insights/prevent-prompt-injection#:~:text=Prompt%20injections%20are%20a%20type,data%2C%20spread%20misinformation%2C%20or%20worse)
[^21]:  [ibm.com](https://www.ibm.com/think/insights/prevent-prompt-injection#:~:text=None%20of%20the%20following%20measures,compensate%20for%20one%20another%E2%80%99s%20shortfalls)
[^22]:  [ibm.com](https://www.ibm.com/think/insights/prevent-prompt-injection#:~:text=,used%20in%20previous%20injection%20attempts)
[^23]:  [bm.com](https://www.ibm.com/think/insights/prevent-prompt-injection#:~:text=Organizations%20can%20also%20train%20machine,be%20a%20likely%20injection%20attempt)
[^24]:  [ibm.com](https://www.ibm.com/think/insights/prevent-prompt-injection#:~:text=Some%20developers%20use%20delimiters%2C%20unique,might%20look%20something%20like%20this)
[^25]:  [oai_citation:26‡ibm.com](https://www.ibm.com/think/insights/prevent-prompt-injection#:~:text=These%20safeguards%20can%20take%20a,%E2%80%9D)
[^26]:  [ibm.com](https://www.ibm.com/think/insights/prevent-prompt-injection#:~:text=Training%20users%20to%20spot%20prompts,can%20thwart%20some%20injection%20attempts)
[^27]:  [ibm.com](https://www.ibm.com/think/insights/prevent-prompt-injection#:~:text=Cybersecurity%20best%20practices)
[^28]:  [ibm.com](https://www.ibm.com/think/insights/prevent-prompt-injection#:~:text=While%20it%20is%20hard%20to,malicious%20commands%20to%20connected%20systems)
[^29]:  [leanware.co](https://www.leanware.co/insights/prompt-engineering-evaluation-metrics-how-to-measure-prompt-quality#:~:text=Define%20Prompt%2C%20Objective%2C%20and%20Benchmark)