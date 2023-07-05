# CFMAR Lab - Physics-Informed Neural Networks for American Option/GMIB Variable Annuity Pricing
This repository contains two folders dedicated towards demonstrating the potential of Physics-Informed Neural Networks in the finance and insurance industries. The code in each folder is used to solve for the premium of American Options and the optimal withdrawals strategy of Guaranteed Minimum Income Benefit Variable Annuities respectively.

## The Physics-Informed Neural Network

Physics-Informed Neural Networks (PINNs) are function approximators capable of utilizing known partial differential equations (PDEs) to generate a solution. Training data in the form of collocation points are generated along some $n$-dimensional domain (where $n \in N$) using a random sampling method, and the PINN attempts to produce a function whose PDE residuals are at or near zero for each collocation point. Initial/terminal and boundary conditions (I.C., T.C., and B.C.) are also set and enforced within the loss function, since an infinite number of solutions would exist for a given PDE without these conditions. Although PINNs can also incorporate tabular data to better fit the approximated function, our methodology focuses purely on minimizing residuals and properly fitting I.C.s, T.C.s, and B.C.s. As a result, our PINNs requires training for each unique option and variable annuity in order to reveal the option's premium and variable annuities optimal withdrawals strategy on a predefined time and underlying asset price domain.

## The American Option

We began this project by first utilizing a Crank-Nicolson finite difference method (FDM) and enforcing a maximum constraint within this scheme to act as a benchmark against our novel Physics-Informed Neural Network in pricing American Options. The functions used to visualize the FDM solution and the associated Free Boundary (used to determine whether exercising or holding the option is optimal) can be found in the American-Options folder under the Finite-Difference-Method.py file. The implementation of the Physics-Informed Neural Network was repurposed from a program used to solve the Burgers and Eikonal equations. The original PINN can be found in [1], while our adapted version and solution visualizations can be found in the mentioned American-Options folder under the Physics-Informed-Neural-Network.py file. We also included a file under the name PINN-Error.py to determine the difference between a given American Option PINN approximation and an exact solution.

## The Guaranteed Minimum Income Benenfit Variable Annuity

After successfully implementing a PINN for pricing American Options, we began the process of further repurposing the PINN framework to price the Guaranteed Minimum Income Benefit (GMIB) Variable Annuity. The GMIB Variable Annuity's PDE form is similar to the Black-Scholes equation, but has different terminal and boundary conditions. Additionally, the existence of a continuous spectrum of possible decisions open to a given policyholder makes the process of solving for the optimal decision strategy significantly more difficult. Determining the optimal withdrawals strategy is handled through the addition of a jump condition under the assumption that a policyholder can withdraw any amount from their account value at any time between the contract inception and annuitization.

### Citations

[1] @misc{blechschmidt2021ways, <br />
  &emsp; title={Three Ways to Solve Partial Differential Equations with Neural Networks --- A Review}, <br />
  &emsp; author={Jan Blechschmidt and Oliver G. Ernst}, <br />
  &emsp; year={2021}, <br />
  &emsp; eprint={2102.11802}, <br />
  &emsp; archivePrefix={arXiv}, <br />
  &emsp; primaryClass={math.NA} <br />
}