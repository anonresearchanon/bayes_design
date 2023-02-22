# BayesDesign
<img src="https://github.com/anonresearchanon/bayes_design/blob/master/data/figs/bayes_design.png?raw=true" alt="drawing" width="700"/>

BayesDesign is an algorithm for designing proteins with high stability and conformational specificity..

Try out the BayesDesign model here:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/anonresearchanon/bayes_design/blob/master/examples/BayesDesign.ipynb)

Dependencies: `./dependencies/requirements.txt`.

## One-line sequence design
To design a protein sequence to fit a protein backbone:
```
python3 design.py --model_name bayes_design --protein_id 6MRR --decode_order n_to_c --decode_algorithm beam --n_beams 128 --fixed_positions 67 68
```

## Detailed steps to run with Docker
- Clone repository
```
git clone https://github.com/anonresearchanon/bayes_design.git
```
- Build docker image (should take ~5 minutes)
```
docker build -t bayes_design -f ./bayes_design/dependencies/Dockerfile ./bayes_design/dependencies
```
- Run container
```
docker run -dit --gpus all --name bayes_dev --rm -v $(pwd)/bayes_design:/code -v $(pwd)/bayes_design/data:/data bayes_design
docker exec -it bayes_dev /bin/bash
```
- Redesign a protein backbone
```
cd ./code && python3 design.py --model_name bayes_design --protein_id 6MRR --decode_order n_to_c --decode_algorithm beam --n_beams 128 --fixed_positions 67 68
```
On a V100 GPU, the greedy algorithm predicts ~10 residues/s and beam search with 128 beams predicts 1 residue every 2s.
