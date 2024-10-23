
# PhD Project: Explore the effect of the latency period on estimates of the basic reproductive number obtained from exponential growth data

The raison d'être for this project was to explain a curious graph I saw in a paper [1] by Lorenzo Sadun. For three different models, Sadun plotted expressions called $R_0-r$ relations which relate the basic reproductive number $R_0$ to the exponential growth rate $r$ in disease incidence against the proportion $p_L$ of the total infected time that an individual was expected to spend in the latent stage, that is the stage where they are infected but not yet infectious. The three models were a standard SEIR model (ExpExp) where both the latent period and infectious period were exponentially distributed, an SEIR model (FixExp) where the time spent in the latent period was fixed while the time spent in the infectious period was exponentially distributed and finally an SEIR model (FixFix) where the time spent in both the latent and infectious period were fixed. This resulted in what I considered an odd graph:

![Sadun's graph](images/Sadun_three_graphs.png)

Why does the estimated $R_0$ for the ExpExp model rise and then wane while it monotonically rises for the other two models? Is there a general principle here that can be ascertained? The key insight is that while $p_L$ is being varied, $r$ is held constant which means we implicitly assume a fixed amount of exponential growth is being produced.

We can think of exponential growth as being shaped by two factors: the total infectiousness and the rate at which that infectiousness is 'released'. $R_0$ is an averaged abstract measure of the total infectiousness per person, which is released at a rate decided by the generation-interval distribution $g$ where $g(\tau)$ can be thought as the proportion of $R_0$ that is released at age-of-infection $\tau$; where the age-of-infection $\tau$ is how long a person has been infected for.  Thus an epidemic with lower total infectiousness but a quick rate of release can produce the same level of exponential growth as one with higher total infectiousness but slow rate of release. The graph below shows how two different epidemics can show the same initial exponential growth in disease incidence but result in two very different epidemiological outcomes.  Notice that when we plot on the right the generation-interval distributions that correspond to each epidemic, the epidemic (blue) whose generation-interval distribution is more squashed around $\tau = 0$, and thus has a quicker rate of release, ends up with far smaller total number of people infected.

![Two epidemics with the same exponential growth rate](images/two_seir_epidemics_same_r.png)

If we take a closer look at the $R_0-r$ relation, we see that the portion of a person's infectiousness that is released sooner is exponentially more influential that the portion that is released later:
```math
R_0 = \frac{1}{\bar{g}(r)}
```
where $\bar{g}(r) = \int_0^{\infty} e^{-r \tau}g(\tau) d \tau$. If we shift $g$ to the right and consequently delay the release of infectiousness then $\bar{g}(r)$ quickly approaches zero. This implies that infectiousness that is shortly released after infection is key for exponential growth. This is quite intuitive; infections that occur earlier drive the initial explosion in disease incidence. The diagram below plots a generation-interval distribution with each segment coloured by $e^{-r \tau}$ to show the relative influence on $\bar{g}(r)$:

![g(tau) coloured by exponential weighting](images/seir_exponentially_weighted_g.png)

As $r$ is produced by that balance between $R_0$  and $g$, we can derive two heuristics to predict how a parameter will affect the estimated value of $R_0$. Let $T_g$ and $V_g$ be the mean and variance of the generation-interval distribution $g$. The first is that increasing $T_g$ will tend to increase $R_0$ while the second is that increasing $V_g$ will tend to reduce it. Increasing $T_g$ shifts a person's infectiousness to later and thus the total infectiousness $R_0$ must increase if the same amount of exponential growth is to be produced. Increasing $V_g$ is more complicated: as the variance increases, we would expect some proportion of a person's infectiousness to be released sooner while another portion to be released later as the $g$ relaxes around its mean $T_g$. The former occurrence results in downwards pressure on $R_0$ while the latter would have the opposite effect. Which will take precedence? As the portion of $g$ that occurs for low values of $\tau$ has a disproportionately larger influence on $\bar{g}(r)$ due to the exponential damping term $e^{-r \tau}$, the releasing of some infectiousness sooner will cause the overpowering effect and thus lead to a smaller $R_0$ as the total infectiousness must decrease to balance the faster transmission. 

Armed with this, we can now explain the estimates of $R_0$ produced in the introductory graph. For the ExpExp model, the analysis is easy. $T_g$ isn't affected by $p_L$ and thus $R_0$ is completely controlled by $V_g$:

![ExpExp model](images/T_g_V_g_R0_m_1_n_1.png)

The same is true for the FixExp model:

![FixExp model](images/T_g_V_g_R0_m_inf_n_1.png)

In the FixFix model, $T_g$ increases with $p_L$ while $V_g$ decreases, both of which slow transmission which must be balanced by a larger estimate of $R_0$:

![FixFix model](images/T_g_V_g_R0_m_inf_n_inf.png)

I then extended this project to an $S E^m I^nR$ model where the times spent in the latent and infectious compartments were Erlang distributed. An interesting result was that increasing $n$, which decreased the variance in the time spent in the infectious compartment $I$, wasn't very influential as it lead to a smaller $T_g$ but also a smaller $V_g$, which had counteracting effects on $R_0$. 

## References
[1] Effects of Latency on Estimates of the COVID-19 Replication Number - Lorenzo Sadun - DOI: 10.1007/s11538-020-00791-2
