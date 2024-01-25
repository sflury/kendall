# kendall
Calculate non-parametric correlation coefficient Kendall's tau, accounting for censoring (upper/lower limits),
based on the two-variable correlation formalism of Akrita & Siebert. 1996. MNRAS 278, 919-924.
Additional function is included to determine the sensitivity of the correlation coefficient 
to individual datum (done by bootstrapping) and/or uncertainties in the data (done by Monte Carlo sampling).

While this code is provided publicly, I request that any use thereof be cited in any publications in which this code is used.
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
Flury et al. 2022 ApJ 930, 126.
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

## Licensing

This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with this program. If not, see <https://www.gnu.org/licenses/>.
