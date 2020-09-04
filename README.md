# Image-based haplotype-guided evolutionary inference <img align="right" width="150" height="150" src="https://github.com/tomouellette/IHapE/blob/master/icon.svg">

This repository contains code for *image-based haplotype-guided evolutionary inferences* for populations with phased genomes. **IHapE** treats evolutionary inference as an image recognition problem, harnessing the power of convolutional neural networks. Images are formed by aligning haplotypes, or entire genomes together, to make evolutionary inferences.

### Overview
---

IHapE is written and python and uses numpy to generate haplotype arrays. Any simulation software can be used to generate haplotypes for analysis, but we provide a simple evolutionary simulation framework that models  exponentially growing population under a a random birth-death process. It was developed for modeling SARS-CoV-2 evolution (allows for back mutations under a neutral model), but can be adapted to any non-recombining genome.

### Getting started
---

Inferences require four basic steps: (1) simulations; (2) training the CNN; and (3) converting empirical haplotypes into numpy arrays; (4) predicting evolutionary model. 

##### (1) Simulations

- Simulations require two scripts, virus.py (defines Virus and Population classes) and simulation.py (generates simulated data)

```python
from virus import Virus, Population
from simulation import simulateViralEvolution

neutral = simulateViralEvolution(r = 2.02, x = 1, w = 1, probBen = 0, mutRate = 1e-4, initSize = 250, genomeSize = 5000)

```

- The parameters are replication rate (r), death rate (x), fitness (w), probability of a beneficial mutation (probBen; multiplied by mutation rate), mutation rate (mutRate), initial population size (initSize), haplotype or genome size (genomeSize). Check `simulation.py` to see other default parameters.

**Note**: If you would like to perform many simulations simultaneously and automatically save output in the numpy format, you can run `exec.py` from the command line.

<pre><code>python3 exec.py -r 2.02 -w 1 -x 1 -p 0 -u 1e-2 -i 110 -gs 1000 -g 250 -ms 1e5 -n 250 -out ./output_folder/
</code></pre>

`exec.py` will return simulation formatted [fitness]\_[id]\_[time].npy for further scripts e.g. 1.05_7092001_18.npy