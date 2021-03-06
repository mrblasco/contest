# Contest package in R

Description of the `contest` package in R, 

## What the contest package does?

* This package solves an extension of the [Moldovanu and Sela (2001)](https://www.aeaweb.org/articles?id=10.1257/aer.91.3.542)'s contest model that encompasses race contests (the first wins) and tournament contests (the best wins).

* It provides an easy way to compute numerical integration when the model does not allow for explicit solutions (which happens many times)

* Helps running Montecarlo simulations to find optimal contest design (number of competitors, prize structure, deadlines, entry requirements, etc.)


## Installation

The latest version of the package is on GitHub. 

First, you need to install and invoke the `devtools` package.

```r
install.packages('devtools')
library(devtools)
```

Second, you need to install the package from the repo `"mrblasco/contest"` with the following command 

```r
install_github("mrblasco/contest")
```


## The MS contest model

* It is an "all-pay" contest model: everyone incurs a cost from effort that is paid before uncertainty about rivals' actions is fully realized

* Players compete for $k=1,..., q$ prizes of decreasing value $v_1\geq v_2\geq ...\geq v_q$ with $\sum v_k = 1$.

* Decide simultaneously completion time $t$ and performance $y$ (or equivalently: speed $s$ and performance $y$)

* Players have ability $a\sim F$ on a bounded interval.

* Costs are multiplicative: $c(a, y, t)$ with elasticities $\alpha<0$, $\beta>0$, and $\gamma<0$.  


## The `contest()` function

Arguments:

* `x`: a vector of realized abilities
* `n`: the number of competitors in the contest
* `type`: either a race or a tournament
* `prize`: a vector with prizes for 1st and 2nd place (prizes higher than 2nd place are ignored)
* `elasticity`: a vector with cost elasticities
* `p, d`: distribution and density functions for abilities
* `xlim`: interval for ability distribution
* `deadline, target`: parameters of the contest


## Outcomes

Computes the symmetric equilibrium via `R` builtin numerical integration  tool `integrate()`.

Values:

* `ability`: a vector of input abilities
* `score`: a vector of equilibrium performances
* `timing`: a vector of equilibrium completion times
* `utility`: a vector of expected payoffs
* `marginal.type`: ability level below which it is not optimal to enter the contest
* `params:` list of contest parameters

## Usage
 
```r
library(contest)
ability <- runif(10) # uniformly distributed (default)
contest(
	sort(ability)
	, n=10 # 10 players	
	, prize=c(1,0) # Winner-takes-all
	, deadline=10 # Time upper-limit
	, target=0.5 # Performance lower-limit
)	
```

