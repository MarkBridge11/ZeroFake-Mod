## Why forking the repo?
This forked repo contains a notebook called `ddim_inversion.ipynb` that includes `uni-ddim-inversion.py` and `sim.py`. This notebook was built to address a resource constraints problem, since, as the author mentions in its paper, this zero-shot method is computationally expensive. Having a notebook allowed me to run this into Google Colab exploiting the limited usage of T4 GPU.
I changed some paths in the used files to make everything work in the Colab environment. Also some small changes were made to the code, to make it work with newer versions of the dependencies needed.

## How to use it?
Load your images (or use the imported dataset) and change the variables `output_folder` and `images_path` accordingly (as long as other related paths) and run the notebook, then your images will be reconstructed. 

## Improvements
- The function `replace_first_noun(…)` was sometimes missing the first noun to take resulting into a poor adversarial prompt. For example I noticed that it was considering *“pope”* as proper noun, so I decided to insert the detection also of proper noun(s) and plural nouns. A successive problem was the detection of compound nouns, so reading the documentation of spaCy I find out the `noun_chunks`, that divide phrases into noun chunks (not in textual order).
- In the paper they cite that they have used a hand-crafted list of nouns that ensure that the adversial prompt is helping deceiving the reconstruction and inversion. Nevertheless this list is missing and was only present a single word *“the big tree”* in the code given. For this reason I curated a list of most common english nouns filtering out articles, verbs, abstract nouns, words with punctuation and words with less than 3 characters.
- In the original code a way to take an adversarial prompt that was minimizing the cosine similarity between the original prompt and the adversarial one was not present. For this reason I imported a small `sentence-transformer` model to ensure a context-aware replacement. Then len(noun_list) prompts are generated replacing, as mentioned in the paper, the first noun that appears with each of the most common nouns. Cosine similarity of the original prompt with respect to the perturbed one is calculated, taking the one with the minimum value (most divergent).





