# The $0 Modern Tech Stack: How I Built My Website Using Only AI and Free Tiers

In today's landscape, the barrier between an idea and a live, hosted product has never been lower. I recently launched [jb-agiledev.com](http://jb-agiledev.com), and the entire process—from brainstorming to deployment—cost me exactly zero dollars in platform fees. 

Here is the "AI-First" workflow I used to go from zero to live in a single afternoon.

### 1. Strategic Brainstorming (Claude.ai)
I started by using Claude.ai to define the site's architecture. We brainstormed the content for every page, ensuring the messaging was aligned with my goals. 
*   **The Output:** A series of Markdown (.md) files saved locally, serving as the "source of truth" for the site’s copy.

### 2. Visual Identity & Logo Design (Claude + ChatGPT)
For the logo, I experimented with two approaches:
*   **Claude:** Excellent for generating clean, functional SVG code for simple, minimalist logos.
*   **ChatGPT:** When I wanted something more "stylish" or intricate, ChatGPT’s DALL-E integration (or SVG generation) provided that extra creative edge.
*   **Pro-Tip:** SVGs are ideal for web performance since they are resolution-independent and lightweight.

### 3. Prompt Engineering for Lovable
Instead of coding manually, I asked Claude to write a comprehensive "Master Prompt" for [Lovable](https://lovable.dev/). 
*   **The Prompt included:** Color schemes, reference sites for layout inspiration, and the structural requirements derived from my initial brainstorming.
*   **Reference Sites:** Using a reference site as a template gave the AI a clear visual target, reducing the need for iterative "guesses."

### 4. Rapid Prototyping (Lovable)
Lovable is a powerful tool for turning prompts into functional web apps. 
*   **The Credit Hack:** Lovable offers 5 free credits per day. I was able to generate a high-quality initial version of the site in just about 3 credits.
*   **Fine-Tuning:** I spent a few minutes tweaking the layout directly in Lovable until it felt just right.

### 5. Version Control & Automated Hosting (Git + Vercel)
Once the design was ready, Lovable allowed me to link the project to a GitHub repository.
*   **Hosting:** I used [Vercel](https://vercel.com/) for deployment. Vercel’s free tier is generous and automatically deploys any changes I push to Git. It’s the gold standard for hobbyists and developers looking for high-performance hosting at no cost.

### 6. The "LLM Consultant" Strategy
Throughout the process, whenever I hit a technical snag or needed a step-by-step guide on how to link a domain, I used Claude and Gemini as on-call consultants. 

### Final Thoughts
You don't need a massive budget or a month-long development cycle to establish a professional presence online. By orchestrating specialized AI tools—Claude for content, ChatGPT for visuals, Lovable for build, and Vercel for hosting—you can launch a modern website for free in hours, not weeks.
