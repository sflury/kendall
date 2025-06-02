# kendall
Calculate non-parametric correlation coefficient Kendall's tau, accounting for censoring (upper/lower limits),
based on the two-variable correlation formalism of Akrita & Siebert. 1996. MNRAS 278, 919-924.
Additional function is included to determine the sensitivity of the correlation coefficient 
to individual datum (done by bootstrapping) and/or uncertainties in the data (done by Monte Carlo sampling).

While this code is provided publicly, I request that any use thereof be cited in any publications in which this 
code is used. For this purpose, the zenodo DOI is listed below as well as a BibTeX reference.
This script was initially developed, implemented, and tested for work presented in Flury et al. 2022 ApJ 930, 126.

## Example Usage
``` python
from kendall import *
# gen random data
np.random.seed(123)
x = np.random.rand(89)
y = x+0.1*np.random.randn(len(x))
# gen random "upper limits"
censors = np.ones((2,len(x)))
uplims = np.unique(np.random.randint(0,high=len(x)-1,size=60))
censors[1,uplims]=0
uncens = [i for i in range(len(x)) if i not in uplims]
# faux uncertainties, accounting for upper limits
x_err = 0.1*np.random.rand(len(x))*censors[0]
y_err = 0.1*np.random.rand(len(y))*censors[1]
# Kendall tau
tau,p = kendall(x,y,censors=censors)
tau_lo,tau_up = tau_conf(x,y,censors,method='bootstrap')
print(f'censored Kendall tau: {tau:.3f}-{tau_lo:.3f}+{tau_up:.3f}, p: {p:.3e}')
```
which prints the following to the command line
```
censored Kendall tau: 0.465-0.018+0.018, p: 1.094e-10
```

## BibTeX Reference

``` bibtex
@SOFTWARE{Flury_kendall,
       author = {{Flury}, Sophia R.},
        title = "{kendall}",
         year = 2023,
        month = aug,
      version = {1.0.0},
          url = {https://github.com/sflury/kendall},
          doi = {10.5281/zenodo.14732912} }
```

Zenodo DOI badge:

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.14732913.svg)](https://doi.org/10.5281/zenodo.14732913)

### Flury et al. 2022 ApJ 930, 126.
``` bibtex
@ARTICLE{2022ApJ...930..126F,
       author = {{Flury}, Sophia R. and {Jaskot}, Anne E. and {Ferguson}, Harry C. and {Worseck}, G{\'a}bor and {Makan}, Kirill and {Chisholm}, John and {Saldana-Lopez}, Alberto and {Schaerer}, Daniel and {McCandliss}, Stephan R. and {Xu}, Xinfeng and {Wang}, Bingjie and {Oey}, M.~S. and {Ford}, N.~M. and {Heckman}, Timothy and {Ji}, Zhiyuan and {Giavalisco}, Mauro and {Amor{\'\i}n}, Ricardo and {Atek}, Hakim and {Blaizot}, Jeremy and {Borthakur}, Sanchayeeta and {Carr}, Cody and {Castellano}, Marco and {De Barros}, Stephane and {Dickinson}, Mark and {Finkelstein}, Steven L. and {Fleming}, Brian and {Fontanot}, Fabio and {Garel}, Thibault and {Grazian}, Andrea and {Hayes}, Matthew and {Henry}, Alaina and {Mauerhofer}, Valentin and {Micheva}, Genoveva and {Ostlin}, Goran and {Papovich}, Casey and {Pentericci}, Laura and {Ravindranath}, Swara and {Rosdahl}, Joakim and {Rutkowski}, Michael and {Santini}, Paola and {Scarlata}, Claudia and {Teplitz}, Harry and {Thuan}, Trinh and {Trebitsch}, Maxime and {Vanzella}, Eros and {Verhamme}, Anne},
        title = "{The Low-redshift Lyman Continuum Survey. II. New Insights into LyC Diagnostics}",
      journal = {\apj},
     keywords = {Reionization, Galactic and extragalactic astronomy, Hubble Space Telescope, Ultraviolet astronomy, Emission line galaxies, 1383, 563, 761, 1736, 459, Astrophysics - Astrophysics of Galaxies, Astrophysics - Cosmology and Nongalactic Astrophysics},
         year = 2022,
        month = may,
       volume = {930},
       number = {2},
          eid = {126},
        pages = {126},
          doi = {10.3847/1538-4357/ac61e4},
archivePrefix = {arXiv},
       eprint = {2203.15649},
 primaryClass = {astro-ph.GA},
       adsurl = {https://ui.adsabs.harvard.edu/abs/2022ApJ...930..126F},
      adsnote = {Provided by the SAO/NASA Astrophysics Data System}
}
```

### Akritas & Seibert 1996
``` bibtex
@ARTICLE{1996MNRAS.278..919A,
       author = {{Akritas}, M.~G. and {Siebert}, J.},
        title = "{A test for partial correlation with censored astronomical data}",
      journal = {\mnras},
     keywords = {METHODS: STATISTICAL, GALAXIES: ACTIVE, X-RAYS: GALAXIES, Astrophysics},
         year = 1996,
        month = feb,
       volume = {278},
       number = {4},
        pages = {919-924},
          doi = {10.1093/mnras/278.4.919},
archivePrefix = {arXiv},
       eprint = {astro-ph/9508018},
 primaryClass = {astro-ph},
       adsurl = {https://ui.adsabs.harvard.edu/abs/1996MNRAS.278..919A},
      adsnote = {Provided by the SAO/NASA Astrophysics Data System}
}
```

## Licensing
<a href="https://github.com/sflury/kendall">kendall</a> © 2022 by <a href="https://sflury.github.io">Sophia Flury</a> is licensed under <a href="https://creativecommons.org/licenses/by-nc-nd/4.0/">Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International</a>

<img src="https://mirrors.creativecommons.org/presskit/icons/cc.svg" style="max-width: 1em;max-height:1em;margin-left: .2em;"><img src="https://mirrors.creativecommons.org/presskit/icons/by.svg" style="max-width: 1em;max-height:1em;margin-left: .2em;"><img src="https://mirrors.creativecommons.org/presskit/icons/nc.svg" style="max-width: 1em;max-height:1em;margin-left: .2em;"><img src="https://mirrors.creativecommons.org/presskit/icons/nd.svg" style="max-width: 1em;max-height:1em;margin-left: .2em;">

This license enables reusers to copy and distribute kendall in any medium or format in unadapted form only, for noncommercial purposes only, and only so long as attribution is given to the creator. CC BY-NC-ND 4.0 includes the following elements:

BY: credit must be given to the creator.
NC: Only noncommercial uses of the work are permitted.
ND: No derivatives or adaptations of the work are permitted.

You should have received a copy of the CC BY-NC-ND 4.0 along with this program. If not, see <https://creativecommons.org/licenses/by-nc-nd/4.0/>.
