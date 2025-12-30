# Leksa: AI-Powered Socratic Learning Platform for Schools

Final project for the Building AI course

**Project Team:** Michael Bergman & Shamil Rosén

## Summary

Leksa is an AI-driven educational platform that guides students through Socratic questioning rather than providing direct answers. With full teacher oversight, multi-AI provider intelligence, and GDPR-compliant infrastructure, it transforms AI from a cheating tool into a legitimate learning companion for schools.

![Leksa platform role selection interface](/image(9).png)
*Role selection interface - Admin, Teacher, Student, System Administrator*

## Background

### The Problem

Swedish schools face a critical challenge with AI adoption. Recent studies paint a concerning picture:

* **75% of Swedish students aged 15-24** have used generative AI (like ChatGPT) for schoolwork<sup>[1]</sup>
* **Over 50% of students** believe they've used AI in ways that may not be permitted<sup>[1]</sup>
* **90% of gymnasium students** on natural science and technology programs have used AI tools in the past month<sup>[2]</sup>
* **40% of students** are unsure what rules actually apply to AI use in school<sup>[1]</sup>

The current response from many schools has been **prohibition** – blocking ChatGPT on school computers and limiting digital tools<sup>[1]</sup>. But this approach is fundamentally flawed:

1. **Students use AI anyway** on their personal devices
2. **Complete prohibition prevents learning** how to use AI responsibly
3. **Teachers cannot provide guidance** if the tools are banned
4. **Sweden falls behind** other countries integrating AI in education

### Our Motivation

This project originated from real needs expressed by Katrineholm Municipality's education administration. Working with municipal digitalization and AI implementation, we've witnessed firsthand how teachers struggle with:

* Detecting when students copy answers from ChatGPT
* Assessing whether students actually learned anything
* Balancing AI benefits with academic integrity
* Lacking tools designed for educational scaffolding

The traditional binary choice – "allow AI and accept cheating" or "ban AI and ignore reality" – is untenable. As a team combining technical expertise with deep understanding of educational needs, we saw an opportunity to create something better.

### Why This Matters Now

**AI is not going away.** In fact, it's becoming essential:

* The Swedish government is developing national AI guidelines for schools<sup>[3]</sup>
* **From autumn 2024**, Swedish gymnasium schools can offer courses in "Artificial Intelligence"<sup>[3]</sup>
* Teachers report AI use is **already widespread** but without pedagogical frameworks<sup>[4]</sup>
* Research shows AI can **particularly benefit students** with concentration difficulties and executive function challenges<sup>[5]</sup>

We need solutions that embrace AI's benefits while maintaining educational integrity. That's what Leksa provides.

---

## How is it used?

### The Learning Experience: A Real Scenario

**Meet Emma, a Grade 9 student working on a history essay about WWII:**

```
Emma opens Leksa and types:
"Why did World War II start?"

Leksa responds:
"That's an important and complex question! Let's explore it together. 
Have you thought about what major events or tensions existed in Europe 
before the war began?"

Emma: "Hitler came to power I think?"

Leksa:
"Exactly right – Hitler did come to power in Germany. That's a key piece 
of the puzzle. Now, can you think about WHEN that happened compared to 
when the war actually started? What might have happened in between?"

Emma: "Was it like... he became leader and then started the war?"

Leksa:
"Good thinking! Let's dig deeper: Hitler became Chancellor in 1933, 
but WWII started in 1939. That's 6 years. What do you think might have 
happened during those 6 years that eventually led to war?"

Emma: "Maybe he was preparing? Building an army?"

Leksa:
"Excellent observation! Yes, Germany did rebuild its military during 
this time, despite the Treaty of Versailles restrictions. This is 
called rearmament. But there's more to the story... Have you heard 
about any specific events or actions Germany took during the 1930s 
that alarmed other countries?"
```

![Chat Interface](/image(11).png)
Chat Interface

**What happens next:**
* Emma continues this dialogue, gradually building understanding
* She writes her essay using the concepts she's discovered
* She submits both the essay AND the AI conversation in Leksa
* Her teacher sees the entire learning process

### Teacher Perspective: Full Transparency

**Ms. Andersson, Emma's history teacher, opens Leksa's dashboard:**

**Student Interactions Panel:**
* List of all students in class
* Filter by subject: "History"
* Emma Svensson: **24 messages** in conversation about WWII

**Clicking on Emma's conversation, Ms. Andersson sees:**
1. **The complete dialogue** – every question Emma asked
2. **Emma's thinking process** – how she reasoned from simple to complex
3. **Quality assessment** – Emma genuinely engaged, didn't ask for direct answers
4. **Concept coverage** – Emma explored Treaty of Versailles, rearmament, appeasement

**Ms. Andersson's assessment:**
> "I can clearly see Emma worked through this herself. She started with basic knowledge and built deeper understanding through guided questioning. The AI never gave her the answer – it helped her think. This is exactly the kind of process I want to evaluate."

### Multiple User Contexts

**Students use Leksa for:**
* Homework assistance without getting direct answers
* Exam preparation with Socratic questioning
* Understanding difficult concepts step-by-step
* Research guidance that teaches critical thinking
* Writing process support (not writing for them)

**Teachers use Leksa to:**
* Monitor how students engage with AI
* Assess learning processes, not just final products
* Upload course materials for AI to reference (RAG system)
* Create and grade assignments directly in platform
* Communicate with classes through announcements

**School administrators benefit from:**
* GDPR-compliant infrastructure (data stays in EU)
* Vendor independence through multi-AI provider system
* Cost-effective solution compared to commercial alternatives
* Full control over data retention and user management

---

## Data sources and AI methods

### Data Architecture

**Training Data:**
* **Swedish educational standards** – Skolverket curriculum guidelines
* **Subject-specific materials** – Teachers upload course documents, textbooks, lecture notes
* **Student interaction logs** – Anonymous conversation patterns (GDPR-compliant)

**Data Storage:**
* **Primary database:** Supabase PostgreSQL hosted in **Stockholm, Sweden**
* **Vector database:** pgvector extension for RAG (Retrieval-Augmented Generation)
* **File storage:** Supabase Storage with EU-based CDN
* **Embedding generation:** OpenAI text-embedding-3 (anonymized prompts only)

**Future enhancement:** Local AI models (Llama) will be added for complete data sovereignty.

### AI Techniques & Methods

#### 1. **Multi-Provider AI Router** (Classification + Intelligent Routing)

Leksa doesn't rely on a single AI provider. Instead, it uses **subject-aware routing**:

```
Student question: "Can you help me solve 3x + 5 = 20?"

Step 1: Subject Detection
→ NLP classification identifies "mathematics" (equation, solve)

Step 2: Provider Selection
→ Mathematics → Claude 3.5 Haiku (excellent logical reasoning)

Step 3: Fallback Strategy
→ If Claude unavailable → O4-Mini → Gemini 2.5 Flash
```

**Available AI Providers:**
| Provider | Strength | Use Case |
|----------|----------|----------|
| Claude 3.5 Haiku | Logical reasoning | Mathematics, Physics |
| O4-Mini | Code understanding | Computer Science, Programming |
| Gemini 2.5 Flash | Factual accuracy | History, Science |
| Perplexity Sonar Pro | Current events | Social Studies |
| Grok-2 | Creative thinking | Literature, Essay writing |

**Why multi-provider?**
* **Vendor independence** – Not locked to one company's pricing/API changes
* **Subject optimization** – Each AI has strengths
* **Cost efficiency** – Route simple queries to cheaper models
* **Reliability** – Automatic fallback if one provider is down

Students can also **manually select** pedagogical styles through the "AI-Väljaren" dropdown, choosing specialists like "Matematikgeniet" or "Språkmästaren".

#### 2. **RAG System** (Vector Similarity Search)

**Problem:** Generic AI doesn't know your school's specific curriculum or materials.

**Solution:** Retrieval-Augmented Generation

**How it works:**

```
Teacher uploads: "Katrineholm History 1900s - Course Materials.pdf"

Processing:
1. Text extraction from PDF
2. Chunking (500 tokens per chunk)
3. Embedding generation (OpenAI text-embedding-3)
4. Storage in pgvector database

Student query: "What did our teacher say about the railroad in Katrineholm?"

RAG Search:
1. Convert query to embedding
2. Vector similarity search (threshold > 0.7)
3. Retrieve relevant chunks from course PDF
4. Include in AI prompt context

AI Response:
"According to your course materials, the railroad to Katrineholm 
was built in [year]... [cites specific course content]"
```

**Benefits:**
* AI can reference school-specific materials
* Reduces hallucinations (AI making up facts)
* Aligns responses with curriculum
* Teacher sees when AI used course materials

#### 3. **Socratic Prompting System** (System Prompt Engineering)

**Core Innovation:** Custom system prompts that enforce Socratic method

**Example System Prompt (Mathematics):**
```
You are a Socratic mathematics tutor for Swedish schools.

RULES:
1. NEVER give direct answers or complete solutions
2. ALWAYS respond with guiding questions
3. Break complex problems into smaller steps
4. Encourage student's own reasoning
5. Praise effort and thinking process, not just correctness
6. Use Swedish language appropriate for student's grade level
7. If student asks "give me the answer", explain why that 
 doesn't help learning and suggest a starting question instead

APPROACH:
- Start by checking what student already understands
- Guide through one concept at a time
- Encourage reflection: "Why do you think...?" "What if...?"
- Celebrate when student discovers answer themselves
```

**Technical Implementation:**
* Subject-specific prompt templates
* Dynamic prompt adjustment based on student responses
* Guardrails to prevent AI from giving complete answers
* Swedish language optimization

#### 4. **Neural Network Architecture** (From Building AI Course)

The classification system for subject detection uses principles learned in the course:

* **Logistic Regression** for binary classification (is this math? yes/no)
* **Multi-class Classification** for subject routing (math, science, history, language)
* **Nearest Neighbor** methods for finding similar past queries
* **Natural Language Processing** for understanding Swedish educational text

---

## Challenges

### What Leksa Does NOT Solve

#### 1. **AI Hallucinations**
Even with RAG and careful prompting, AI can still generate incorrect information. 
* **Mitigation:** Teacher review, multiple source verification, clear disclaimers
* **Reality:** This is a limitation of current AI technology

#### 2. **Complete Cheating Prevention**
A determined student could still:
* Use external ChatGPT and paste answers
* Have someone else do the work
* Copy from classmates

**However:** Teachers can see if work quality doesn't match AI conversation history.

#### 3. **Dependency Risk**
Students might become **too reliant** on AI scaffolding and struggle without it.
* **Consideration:** Balance AI-assisted work with AI-free assessments
* **Teacher role:** Gradually reduce AI support as skills develop

#### 4. **Different Learning Styles**
Socratic questioning doesn't work equally well for all students.
* Some students need direct instruction first
* Some have language processing challenges
* Some prefer hands-on learning

**Leksa complements but doesn't replace** diverse teaching methods.

### Ethical Considerations

#### Privacy & Data Protection
* **Concern:** Student conversations are logged and analyzed
* **Safeguards:** 
 - GDPR compliance with EU data hosting
 - Admin-controlled retention policies
 - Students cannot delete history (prevents evidence destruction)
 - Parent notification for users under 15

#### Bias in AI Responses
* **Risk:** AI models trained on internet data may contain biases
* **Mitigation:**
 - Swedish-focused training to reduce American/English bias
 - RAG prioritizes school materials over general internet knowledge
 - Teacher flagging system for inappropriate responses
 - Continuous monitoring and prompt refinement

#### Digital Divide
* **Issue:** Students with better technology access may benefit more
* **Response:** 
 - Web-based platform (no expensive hardware needed)
 - Works on tablets and phones
 - School computer lab access
 - Offline assignment completion options

#### Assessment Validity
* **Question:** Does AI assistance make grades less meaningful?
* **Perspective:** Assessments must evolve to value **process over product**
 - Traditional "write an essay at home" → vulnerable to AI
 - Leksa model: "show your thinking process" → reveals learning

---

## What next?

### Short-term Growth (6-12 months)

**Pilot Testing Phase:**
* Partner with 3-5 Swedish schools for controlled rollout
* Collect teacher and student feedback
* Measure learning outcomes vs. traditional methods
* Iterate based on real classroom use

**Technical Enhancements:**
* Complete OneDrive/Google Drive integration for document sync
* Automated assignment reminders and deadline management
* Enhanced mobile experience (dedicated iOS/Android apps)
* Local AI model integration (Llama) for full data sovereignty

**Teacher Tool Expansion:**
* Assignment template library for common subjects
* AI-assisted grading suggestions (teacher maintains final control)
* Analytics dashboard showing class-wide AI usage patterns
* Calendar integration for assignment scheduling

### Medium-term Vision (1-2 years)

**Personalized Learning Paths:**
* AI-generated adaptive curricula based on student performance
* Automated difficulty adjustment (like adaptive testing)
* Skill gap identification and targeted practice
* Achievement system gamification

**Expanded Integration:**
* **Skolverket alignment** – Direct integration with national standards
* **Municipal SSO** – Single sign-on with existing school systems
* **Parent portal** – Progress visibility for younger students
* **LMS integration** – Connect with Schoolsoft, Google Classroom, etc.

**Advanced AI Features:**
* Voice-first learning for accessibility
* Multimodal support (image analysis, diagram interpretation)
* Real-time translation for multilingual students
* Predictive intervention (flag struggling students early)

### Long-term Ambition (3-5 years)

**National Scale:**
* Adoption by **Swedish municipalities** as standard platform
* Government partnership for nationwide implementation
* Integration with Swedish national assessment systems

**International Adaptation:**
* Translate and customize for Nordic countries (Norway, Denmark, Finland)
* European expansion (Germany, Netherlands, etc.)
* Adaptation to different educational systems

**Research Collaboration:**
* Partner with Swedish universities (Lund, Uppsala, KTH) for educational research
* Publish peer-reviewed studies on AI-assisted learning outcomes
* Contribute to AI ethics and education policy discussions

### What We Need to Grow

**Skills:**
* **Educational researchers** – Validate learning outcomes scientifically
* **UX designers** – Optimize student/teacher experience
* **AI engineers** – Advanced NLP and model fine-tuning
* **Sales/partnerships** – Build relationships with Swedish schools

**Resources:**
* **Funding** – Seed capital for pilot expansion (~€100k-300k)
* **School partnerships** – Access to real classrooms for testing
* **Teacher training** – Professional development materials
* **Legal/compliance** – Educational data protection expertise

**Institutional Support:**
* **Skolverket endorsement** – National education agency backing
* **Teacher union collaboration** – Lärarförbundet support
* **Municipality partnerships** – SALAR (Sveriges Kommuner och Regioner) engagement

---

## Acknowledgments

### Inspiration & Research
* **Building AI Course** – University of Helsinki & Reaktor Innovations
 - Multi-provider AI routing concept inspired by course ML techniques
 - Classification and NLP methods from course modules
* **Lunds universitet research** – Studies on student AI usage in Swedish schools<sup>[5]</sup>
 - Johan Klarin et al.: "ChatGPT usage among Swedish secondary students"
* **Högskolan i Halmstad research** – Student AI strategies and cognitive approaches<sup>[2]</sup>
* **Skolverket guidelines** – Swedish National Agency for Education AI recommendations<sup>[3]</sup>

### Technology & Open Source
* **Supabase** – Open-source Backend-as-a-Service (PostgreSQL, Auth, Storage)
 - [Supabase License: Apache 2.0](https://github.com/supabase/supabase/blob/master/LICENSE)
* **pgvector** – PostgreSQL extension for vector similarity search
 - [pgvector License: PostgreSQL License](https://github.com/pgvector/pgvector)
* **Next.js** – React framework by Vercel
 - [Next.js License: MIT](https://github.com/vercel/next.js/blob/canary/license.md)
* **shadcn/ui** – React component library
 - [shadcn/ui License: MIT](https://github.com/shadcn-ui/ui/blob/main/LICENSE.md)

### AI Provider APIs
* **Anthropic Claude** – Socratic reasoning and mathematics
* **OpenAI GPT-4o & O4-Mini** – Language understanding and embeddings
* **Google Gemini** – Factual knowledge and science
* **xAI Grok** – Creative writing and critical thinking
* **Perplexity** – Current events and research

### Data Sources
* **Ungdomsbarometern 2024** – Swedish youth AI usage statistics<sup>[1]</sup>
 - [Report: "Back to School 2024"](https://www.ungdomsbarometern.se/)
* **SVT Nyheter** – Swedish public broadcasting AI in education coverage
* **Forskning.se** – Swedish research news on AI and learning
* **Skolverket** – National curriculum and digital competence frameworks

### Municipal Partnership
* **Katrineholm Municipality** – Educational administration collaboration

---

## Project Team

**Michael Bergman** – AI Implementation & Business Development
* Role: Verksamhetsutveckling och AI implementation

**Shamil Rosén** – Technical Architecture & Development
* Role: Full-stack development and AI integration

### Our Story
This collaboration emerged from our work in Katrineholm Municipality's digitalization efforts. Our understanding of educational administration combined with technical knowlege created the foundation for Leksa. When the educational organization expressed concerns about uncontrolled AI use in schools, we realized the use for something that transforms AI from a threat into a pedagogical tool.

The result: a platform that represents the intersection of educational need and technological possibility. Leksa is our answer to the question every Swedish school faces – not a banning of AI, but a transformation of it into a legitimate learning companion.

---

## References

[1] SVT Nyheter (2024). "Ny rapport: Många elever använder AI för att fuska i skolan." Retrieved from: https://www.svt.se/nyheter/inrikes/ny-rapport-manga-elever-anvander-ai-for-att-fuska-i-skolan

[2] Högskolan i Halmstad (2025). "Genomtänkta val när gymnasieelever använder AI i skolarbetet." Retrieved from: https://www.hh.se/information/nyheter/nyheter/2025-02-27-genomtankta-val-nar-gymnasieelever-anvander-ai-i-skolarbetet.html

[3] Skolverket (2024). "Råd om AI, Chattbottar och liknande verktyg." Retrieved from: https://www.skolverket.se/kompetensutveckling/stod-i-arbetet/rad-om-ai-chattbottar-och-liknande-verktyg

[4] Skolverket (2024). "Oro för att AI lockar till genvägar istället för lärande." Retrieved from: https://www.skolverket.se/om-oss/aktuellt/nyheter/nyheter/2024-08-21-oro-for-att-ai-lockar-till-genvagar-istallet-for-larande

[5] Lunds universitet (2024). "ChatGPT mer populärt hos vissa skolelever." Retrieved from: https://www.lu.se/artikel/chatgpt-mer-populart-hos-vissa-skolelever

---

**Building AI course project** | Created January 2025 | [GitHub Repository: leksa-ai](https://github.com/yourusername/leksa-ai)
