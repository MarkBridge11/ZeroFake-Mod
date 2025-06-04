### Why forking the repo?
This forked repo contains a notebook called `ddim_inversion.ipynb` that contains `uni-ddim-inversion.py` and `sim.py`. This notebook was built to address some resource constraints, since, as the author mentions in its paper, this zero-shot method is computationally expensive. Having a notebook allowed me to run this into Google Colab exploiting the limited usage of T4 GPU.
I changed some paths in the used files to make everything work in the Colab environment. Also some small changes were made to the code, to make it work with newer versions of the dependencies needed.

### How to use it?
Run the notebook and insert your images within `/imgs` folder, then your images will be reconstructed, with name corresponding to the index number of the current image in analysis. Then (for now) you have to manually change paths in the last code chunk before "Other code" section, to calculate the SSIM score between the original and the reconstructed image.

### Improvements
In the original code a way to take an adversarial prompt that was minimizing the cosine similarity between the original prompt and the adversarial one was not present. For this reason I implemented a simple and lightweight mechanism, that takes 1k (without duplicates) nouns from Brown corpus of nltk. Then 1k prompts are generated replacing, as mentioned in the paper, the first noun that appears with each of the 1k nouns. Cosine similarity of the original prompt with respect to the perturbed one is calculated, taking the one with the minimum value. To use cosine similarity and maintain efficiency, I decided (for now), to use embeddings that are not context-aware like Fasttext one.

# Future improvements
- [ ] Adjust the cycle that perform the comparison between reconstructed and original images from `/imgs` folder. Right now you have to manually change paths.



