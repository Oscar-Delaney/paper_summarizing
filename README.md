# Collecting papers to analyze from company websites
We looked at papers published on the websites of Anthropic, (Google) DeepMind, and OpenAI between January 2022 and July 2024. Specifically, we looked in the following places:
* All papers published on https://www.anthropic.com/research
* All papers available from https://deepmind.google/research/publications/ and https://web.archive.org/web/20220626233857/https://www.deepmind.com/research. [^1]
Because there are many papers available here, we used the GPT-3.5 API to read the title and abstract and flag which papers were plausibly relevant,
and then we manually reviewed these papers to check whether they were indeed relevant.
* Papers on https://openai.com/research, using the website filters to show only papers that are likely to be relevant.[^2]

We ignored results on these pages that did not link to a paper (e.g. blog posts).

# Collecting papers to analyze from arXiv
To collect relevant papers from arXiv, we used the following approach:
* Using the arXiv API to search for all papers meeting the following criteria. (1) Published in the relevant timeframe, (2) Listed on arXiv in the categories relating to artificial intelligence (cs.AI) or machine learning (cs.LG), and (3) At least one term in the title that is relevant to safe AI development.
** The terms that we searched for are: align*, misalign*, safe*, robust*, powerseeking, seek power, multiagent, model organism*, safe* by design, brain emulation, interpretab*, honest, automat* alignment, automat* safety, human feedback, enhanc* feedback.
** Terms around alignment and safety are often used when discussing safe AI development in general. The other terms are derived from the names of the research areas in our paper.
* We then used an automated process to filter only to papers where the first author lists an affiliation at Anthropic, (Google) DeepMind, or OpenAI. (The arXiv search function does not provide a way to filter by affiliation, meaning that the list from the previous bullet point includes many papers by researchers not at one of these three AI companies.) Specifically, our code checks whether the first page of the paper on arXiv includes one of the strings "Anthropic", "DeepMind", or "OpenAI". If it does, the text of this first page is passed to a language model (Claude 3.5 Sonnet), with a prompt asking the model to identify the institution of the first author. (A second language model step is used to turn answers of the form "The author's institution is DeepMind" to answers of the form "DeepMind".)







# Categorizing papers
To categorize the papers, one of us (Delaney) read the title and abstract. If the paper seemed relevant to safety, Delaney assigned it to the category that seemed most appropriate.
We used two approaches to minimize classification errors. First, another author (Guest) independently categorized a random 25% of the papers.
We discussed cases where our categorisations differed (2 out of 13 papers) and updated accordingly.
Second, in assessing_papers.py we used the GPT-3.5 API by providing descriptions of our clusters to the API and asking it to classify each paper on the basis of the title and abstract.
Delaney reviewed any cases where the API gave a different answer to him, updating the categorization as appropriate.
The final decisions about categorizations were made by Delaney (not by the API).

[^1]: Much of DeepMind’s research from before the merger with Google Brain is no longer available on the live website, hence we also used the Internet Archive.
We did not include pre-merger Google Brain research.
[^2]: Specifically, we looked at any paper that matched the following filters: "adversarial examples", "human feedback", "interpretability", "multi-agent", "robustness", "safety & alignment".
There is also a filter for “responsible AI”, but all papers in this category are either more about governance than technical safety and so out of scope or already included because of the other filters.

