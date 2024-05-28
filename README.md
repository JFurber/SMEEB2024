<script type="text/javascript" id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"> </script> <script type="text/x-mathjax-config"> MathJax.Hub.Config({ "HTML-CSS": { linebreaks: { automatic: true } }, SVG: { linebreaks: { automatic: true } } }); </script>


&nbsp;

<h1 style="text-align: center;"> Stochastic Models and Experiments in Ecology and Biology (SMEEB) 2024, L' Aquila, Italy  </h1>

Thank you to the Institute of Applied Mathematics (IMA) for a small grant to help to in attending this conference.

<h2 style="text-align: center;"> Abstract </h2>

We investigate a modelling framework to understand the fine-scale movement of the European badger (_Meles meles_) within their environment. It is widely understood that badgers play a crucial role in the transmission of bovine tuberculosis (bTB), where bTB is a serious disease of cattle and has a significant economic impact on farmers. However, despite all the GPS data, ecologists still do not understand what they can learn from the data about fine-scale badger movement. A key research question we would like to answer is can we generate a dynamical model to explore and understand better badger movement?

We model the movements of individual badgers using stochastic particle models on an energy surface. Such an approach has been successful in describing the movements of free-ranging elk and their avoidance of vehicles and humans, but has yet to be applied to the study of badgers. An exploratory modelling framework has been built that describes how badgers move around their landscape foraging, defaecating, and interacting with other badgers (including male and female differences). The model uses data driven methods to parametrize the energy surface using GPS data and the noisy random walks of badgers.

The modelling framework that we have created allow us to answer key ecological questions such as, how does badger movement affect the spread of bTB? With the role badgers play in the spread of bTB, the answer to these questions could be crucial in strategic planning of disease control.

In this presentation, we explore the results of the parameterized model and use it to investigate transition rates between badger social groups, where badgers cross various territories. We also discuss the pros and cons of the generation of an energy surface and the estimation of a noise term. 


---

<h2 style="text-align: center;"> Generated Trajectory </h2>

Below is the animation linked to Figure 3, where the 'badger' can be seen to be moving along its trajectory. The initial position links to an individual badger that is being monitored at the park, and the diffusion term of the badger has been calculated. 

The animation is plotted every two iterations to show a smoother movement of the badger following its trajectory. This is a great tool to have a better visual of the badger movements in the park.

<p align="center">
<img src="Video_Traj_10000.gif"
      width = "500">
</p>

---
<h2 style="text-align: center;"> Extended Dynamic Mode Decomposition </h2>

<p> This section compliments the box on transition probabilities. We use an algorithm called Extended Dynamic Mode Decomposition (EDMD) to estimate the metastable states of the dynamical system. For information on EDMD and algorithm, see references [5] and [7]. In essence,the eigenvalues and eigenfunctions of the Koopman operator capture the long-term dynamics of the observables of the dynamical system. EDMD is used to compute an approximation for the Koopman operator directly. We analyze the Koopman operator via its spectrum. </p>

<p> One requirement for using EDMD is uniformly spaced time intervals. Due to the nature of the GPS collection, unfortunately, we do not have uniform time intervals. We overcome this by interpolating the data. Here, we assume that the badgers are moving in a linear fashion between coordinates, and they are moving the same speed. We need to find a lag time so the space is not too small that we lose the dynamics, and not too large that we are unable to see the dynamics. For example, if we interpolate so we have 2-minute intervals, then we are literally assuming the badgers are moving in a straight line between points A and B. Yet, by reference [6] it is proved by <i> dead reckoning </i> that badgers do not take a linear route. If we use 35-minute intervals, then we are unable to see anything in the results. Hence, we interpolate the data for every 17.5 minutes. Whilst this is assuming we know the position halfway, it gives more ‘freedom’ for the badger between each point. </p>

<figure>
<p align="center">
<img src = "WoodchesterInterp.png" 
      width="350"  />
<img src = "DeadReckoning.png" 
      width="350"  />
      <figcaption> <em>Figure</em>. <b>Left</b>: Investigation into interpolating the data for different choices. <b>Right</b>: Figure 3 from [6]. Dead reckoned data of a single badger's movement. </figcaption>
</p>
</figure>

<p> The results using the 17.5 minute interpolated data are presented. The eigenfunctions depict where there are energy barriers within the park (i.e. where there are few transitions between areas). When we compare the clustered eigenfunctions against the initial investigation of k-means clustering of the data we find that the clustering are very similar. One benefit of using EDMD over pure k-means clustering of the data, is that EDMD is looking at the dynamics of the system. Whereas k-means clustering is looking at the Euclidean distance of points to a centroid mean. From this perspective, EDMD is a better representation of the clusters. Yet, the disadvantage is that the data does need to be interpolated to use the method. Nonetheless, despite these limitations and the need to manipulate the data, the output from EDMD of the metastable clusters could be insightful into the long-term badger movements. </p>

___
<h2 style="text-align: center;"> Transition Probabilities </h2>

<p> Using the clusters generated with EDMD, we allocate each coordinate (from the 17.5 minute interpolated data) a cluster. Then, we are able to calculate the transition at each time point between the eight clusters. </p>
      
<p> The transition matrix corresponding to Figure 5 is seen below. As is can be seen, there are very strong probabilities of staying in the original cluster at the next time point, with few transitions to the adjacent cluster. There are no jumps across the park in a single time step. This was to be expected as the clusters are made up of multiple territories, where Figure 1 highlights the territories that were seen within the park in 2018. In 2018, there were 31 territories within the park (although 3 without data in them due to logistics of catching the badgers), however, these can change over time. For instance, boundaries can move and teritories can merge due to the death of a senior/leader badger. The clusters that have been calculated incorporate multiple territories into a single cluster, showing that the badgers stay generally amongst multiple territories, rather than wandering to others. This could have implications if wanting to control the spread of bovine Tuberculosis. </p>

$$\begin{pmatrix}
0.9920 &	0.0008 &	0.0026 &	0 &	0 &	0 &	0 &	0 \\
0.0023 &	0.9960 &	0.0054 &	0.0012 &	0 &	0 &	0 &	0 \\
0.0057 & 	0.0026 &	0.9886 &	0.0005 &	0 &	0.0024 &	0 &	0 \\ 
0 &	0.0006 &	0.0005 &	0.9893 &	0.0031 &	0.0002 &	0 &	0 \\ 
0 &	0 &	0 &	0.0087 &	0.9900 &	0.0002 &	0 &	0.0103 \\
0 &	0 &	0.0028 &	0.0004 &	0.0001 &	0.9936 &	0.0013 &	0 \\
0 &	0 &	0 &	0 &	0.0001 &	0.0036 &	0.9983 &	0.0008 \\
0 &	0 &	0 &	0 &	0.0069 &	0.0000 &	0.0004 &	0.9890 \\
\end{pmatrix}$$


<h2 style="text-align: center;"> Bibliography </h2>

[1] Brillinger, D., Preisler, H., Ager, A., Kie, J., and Service, U. *The use of potential functions in modelling animal movement*. Data Analysis from Statistical Foundations: A Festschrift in Honour of the 75th Birthday of DAS Fraser (05 2001).

[2] Burt, W. H. *Territoriality and home range concepts as applied to mammals*. Journal of Mammalogy 24, 3 (1943),
346–352.

[3] Do Linh San, E., Ferrari, N., and Weber, J.M. *Spatio-temporal ecology and density of badgers meles meles in the swiss jura mountains*. European Journal of Wildlife Research 53 (2007), no. 4, 265–275.

[4] Downs, J., Horner, M., Lamb, D., Loraamm, R. W., Anderson, J., and Wood, B. *Testing time-geographic density estimation for home range analysis using an agent-based model of animal movement*. International Journal of Geographical Information Science 32, 7 (2018), 1505–1522.

[5] Klus, S., Koltai, P., and Schutte, C. *On the numerical approximation of the Perron-Frobenius and Koopman operator*. Journal of Computational Dynamics (2015).

[6] Magowan, E.A., Maguire, I.E., Smith, S., Redpath, S., Marks, N.J., Wilson, R.P., Menzies, F., O’Hagan, M., and Scantlebury, D.M., *Dead-reckoning elucidates fine-scale habitat use by European badgers Meles meles*. Animal Biotelemetry 10 (2022), no. 1, 10.

[7] Niemann, J.H., Klus, S., and Schutte, C., *Data-driven model reduction of agent-based systems using the Koopman generator*. PLOS ONE 16 (2021), no. 5, 1–23.

[8] Preisler, H., Ager, A., Johnson, B., and Kie, J. *Modeling animal movements using stochastic differential equations*. Environmetrics 15636 (11 2004), 643–657.

[9] Preisler, H. K., Ager, A. A., and Wisdom, M. J. *Analyzing animal movement patterns using potential functions*.
Ecosphere 4, 3 (2013), 1–13.


