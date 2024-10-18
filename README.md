# PhD Project: Explore the effect of the latency period on estimates of the basic reproductive number obtained from exponential growth data

The raison d'être for this project was to explain a graph I saw in a paper[1] by Lorenzo Sadun. Sadun took the $R_0-r$ relations, that is the expressions estimate the basic reproductive number $R_0$ from the exponential growth rate in disease incidence $r$, of three different model and plotted them as a function of the latent period. He held the total amount of time that an individual was expected to spend infected constant but changed the proportion $p_L$ of it that was spent latent. The three models he looked at were a standard SEIR model (ExpExp) where both the latent period and infectious period were exponentially distributed, an SEIR model (FixExp) where the time spent in the latent period was fixed while the time spent in the infectious period was exponentially distributed and finally an SEIR model (FixFix) where the time spent in both the latent and infectious period were fixed. This resulted in what I considered an odd graph:

![Sadun's graph](images/Sadun_three_graphs.png)

Why does the estimated $R_0$ for the ExpExp model rise until it hits a max and then wane while the other two models continue to rise? Is there a general principle here that can be ascertained? Thankfully there is and it is quite simple. The key lies in the relationship between $R_0$, $r$, and the generation-interval distribution. A generation interval is the time The generation-interval distribution $g(\tau)$ is the proportion of a persons infectiousness that occurs at age-of-infection $\tau$, that is $\tau$ time units after they were infected. The $R_0-r$ relation is thus given by 
```math
R_0 = \frac{1}{\bar{g}(r)}
```
where $\bar{g}(r) = \int_0^{\infty} e^{-r \tau}g(\tau) d \tau$. $e^{-r \tau}g(\tau)$ weights the generation intervals by their size with the longer generation intervals being the most affected. So imagine we, by varying some parameter but leaving $r$ constant, shifted the generation-interval distribution such that it was more squashed around $\tau = 0$, implying that infected indviduals were infectious earlier. $\bar{g}(r)$ would increase in this case which would lower the estimate value of $R_0$ according the the $R_0-r$ relation above. Thus for a given $r$, shorter generation intervals mean a lower $R_0$. Why?

The key is that $r$ has been held constant, which means that a certain rate of exponential growth in infections has be produced. 

## References
[1] Effects of Latency on Estimates of the COVID-19 Replication Number - Lorenzo Sadun - DOI: 10.1007/s11538-020-00791-2
