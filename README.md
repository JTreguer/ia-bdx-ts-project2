# ia-bdx-ts-project2
Suite de l'introduction aux séries temporelles

La semaine précédente, nous avons vu :
- la notion de séries temporelles
- différents types de séries temporelles
- la décomposition de séries temporelles en niveau (constante), tendance, cycles (saisons) et erreur (bruit) 

Les 2 prochains jours nous allons approfondir l'analyse des séries temporelles avec BigML et Jupyter.

## A Faire :

### Revoir rapidement la décomposition de séries temporelles [ici](https://www.youtube.com/watch?v=0ar9extHObg)

### BigML Time Series
 * Regarder la vidéo sur les séries temporelles dans BigML ([vidéo](https://www.youtube.com/watch?v=wsyiOHUBE8c&list=PL1bKyu9GtNYHAk0PUojkLYZzASoYVcsTQ&index=10))
 * Appliquer le workflow BigML au dataset cité dans la vidéo (dataset disponible [ici](https://github.com/plotly/datasets/blob/master/monthly-milk-production-pounds.csv), suivre les étapes de la vidéo
 * Appliquer le même workflow BigML au dataset sunspot.csv (disponible sur Kaggle, github, etc.) avec l'outil Time Series : à quoi vous attendez-vous ? Que constatez-vous ?
 * Choisir une série temporelle dans une des bases ci-après et appliquer le même workflow dans BigML avec l'outil Time Series 
 
 * Mise en commun
 
### Recherches

 * Rechercher les 2 manières habituelles de splitter un dataset de série temporelle en vue d'entraîner et d'évaluer un modèle de prédiction. Dans le cas du walk-forward, quelles sont les 2 possibilités de split ?
 Voir [ici](https://machinelearningmastery.com/backtest-machine-learning-models-time-series-forecasting/)
 * Rechercher la différence entre une série univariée et multivariée
 * Choisir un dataset parmi ceux proposés dans les bases ci-après (faire valider par l'animateur). Ce dataset servira pour toute la suite 

## Modèles auto-régressif

 * Vous avez déjà étudié de près un modèle de régression linéaire où une variable dépendante est prédite à l'aide d'une combinaison linéaire d'autres variables 
 * De même, dans une série temporelle, un modèle auto-régressif est une régression linéaire d'une variable sur ses valeurs passées
 * Quels points communs et quelles différences voyez-vous entre la régression linéaire et un modèle auto-régressif ?
 * Une vidéo sur ces modèles [ici](https://www.youtube.com/watch?v=Mc6sBAUdDP4)
 * Pour illustrer le modèle AR, implémenter le notebook :
https://machinelearningmastery.com/autoregression-models-time-series-forecasting-python/

### Auto-corrélation

 * Un modèle auto-régressif fait appel à la notion d'auto-corrélation, c'est-à-dire à la corrélation entre des valeurs d'une série temporelle séparées par un intervalle de temps constant. Par exemple, la température moyenne aujourd'hui à un endroit donné est fortement corrélée avec la température au même endroit la veille et moins corrélée avec la température 3 mois avant.
 * Implémenter le notebook :
https://machinelearningmastery.com/gentle-introduction-autocorrelation-partial-autocorrelation/

## Livrable du projet Time Series
 * Un notebook Python avec le contenu suivant :
    * Chargement d'une série temporelle
    * Visualisation de la série
    * Commentaire sur les caractéristiques de la série
    * Nettoyage éventuel des données
    * Prédiction par une méthode classique (ARMA/ARIMA) :
     * Décomposition de la série en tendance, saisons, résidus
     * Test de stationnarité
     * Plot d'auto-corrélation (ACF/PACF)
     * Choix d'un modèle (hyper-paramètres)
     * Split des données
     * Prédiction sur l'ensemble de tests avec :
      * visualisation
      * calcul d'une métrique de performance
    * Prédiction par une méthode moderne de ML, au choix RNN (LSTM/GRU) ou ensembliste (Random Forest / xgboost)
     * Evaluation par walk-forward

*Note :* La première partie de ce canevas reprend les grandes étapes classiques d'une analyse de séries temporelles :
1. Observer la série
2. Nettoyer les données si nécessaire
3. Transformer la série en série stationnaire en enlevant sa moyenne, sa tendance, ses éléments saisonniers
4. Vérififer que le résultat de 3 est stationnaire par une méthode empirique ou un test statistique (ex. : Augmented Dickey-Fuller)
5. Etudier l'auto-corrélation en traçant l'ACF et la PACF enfin de fixer les ordres p et q d'un modèle ARMA ou ARIMA
6. Splitter les données
7. Fitter le modèle, tester des variantes du modèle autour des valeurs p et q trouvées en 5, les classer suivant une métrique
8. Evaluer le(s) modèle(s) avec des fenêtres glissantes training/test
9. Evaluer aussi la performance du modèle après avoir inversé les opérations de l'étape 3
10. Pour la production, suivre à intervalles réguliers la performance du modèle, ré-entraîner en cas de divergence avérée

*Note :* Pour le choix des ordres p et q pour les parties AR et MA du modèle,
O on prend p tel que :
  * La PACF passe sous les intervalles de confiance à partir de p+1
* On prend q pour la partie MA tel que :
  * l'ACF passe sous les intervalles de confiance à partir de q+1
* Si l'ACF décroit régulièrement de façon exponentielle sans pic, le modèle sera un AR pur, q = 0
* Si le le PACF décroit régulièrement de façon exponentielle sans pic, le modèle sera un MA pur, p = 0

Voir une discussion plus détaillée (et nuancée), en français, [ici](https://didierdelignieresblog.files.wordpress.com/2019/09/arimacomplet.pdf=

## Grille d'évaluation mutuelle du livrable

A COMPLETER


# Ressources

## BigML
Les séries temporelles dans BigML ([vidéo](https://www.youtube.com/watch?v=wsyiOHUBE8c&list=PL1bKyu9GtNYHAk0PUojkLYZzASoYVcsTQ&index=10))
(et [ici](https://bigml.com/whatsnew/timeseries) pour les fonctionnalités principales)

## Datasets
 * 7 datasets collectés dans un article de Jason Brownlee : [ici](https://machinelearningmastery.com/time-series-datasets-for-machine-learning/)
 * 41 séries temporelles : [ici](https://data.world/datasets/time-series)
 * 102 datasets de l'UCI :[ici](https://archive.ics.uci.edu/ml/datasets.php?format=&task=&att=&area=&numAtt=&numIns=&type=ts&sort=taskUp&view=table)
 
## Séries multivariées
https://www.analyticsvidhya.com/blog/2018/09/multivariate-time-series-guide-forecasting-modeling-python-codes/
 
 ## Ressources précédentes
  
* Décomposition d'une série temporelle :
[ici](https://machinelearningmastery.com/decompose-time-series-data-trend-seasonality/)
et [là](https://anomaly.io/seasonal-trend-decomposition-in-r/index.html) et [ici](https://machinelearningmastery.com/time-series-trends-in-python/)

* Stationnarité et test de Dickey-Fuller augmenté :
[ici](https://fr.wikipedia.org/wiki/Stationnarit%C3%A9_d%27une_s%C3%A9rie_temporelle)
[ici](https://towardsdatascience.com/stationarity-in-time-series-analysis-90c94f27322)
et [là](https://machinelearningmastery.com/time-series-data-stationary-python/)
et [ici](https://nwfsc-timeseries.github.io/atsa-labs/sec-boxjenkins-aug-dickey-fuller.html)

* Désaisonnalisation : [ici](https://machinelearningmastery.com/time-series-seasonality-with-python/)

* FFT : [ici](https://www.ritchievink.com/blog/2017/04/23/understanding-the-fourier-transform-by-example/)

* Un bon notebook Kaggle utilisant la librairie statsmodel : [ici](https://www.kaggle.com/harryren/boston-arima-forecast-and-analysis)

* Un cours complet sur les séries temporelles avec des exemples en python : [ici](https://www.tutorialspoint.com/time_series/index.htm)

* Un exemple très complet sur la sélection des ordres d'un modèle ARMA, en français ! [ici](https://www.ceremade.dauphine.fr/~roche/Enseignement/Series_temps_exMaster/TP2_SeriesTemp.html)

* Librairie statsmodels [ici](https://www.statsmodels.org/stable/index.html)

* Méthodes de prédictions classiques : [ici](https://machinelearningmastery.com/simple-time-series-forecasting-models/) et [là](https://machinelearningmastery.com/time-series-forecasting-methods-in-python-cheat-sheet/) et [là](https://www.kaggle.com/thebrownviking20/everything-you-can-do-with-a-time-series) et [là](https://towardsdatascience.com/time-series-in-python-exponential-smoothing-and-arima-processes-2c67f2a52788)

* ACF/PACF : [ici](https://machinelearningmastery.com/gentle-introduction-autocorrelation-partial-autocorrelation/) et [là](https://towardsdatascience.com/significance-of-acf-and-pacf-plots-in-time-series-analysis-2fa11a5d10a8)

* ARIMA : [ici](https://machinelearningmastery.com/arima-for-time-series-forecasting-with-python/), [là](http://people.duke.edu/%7Ernau/Notes_on_nonseasonal_ARIMA_models--Robert_Nau.pdf) et [là](https://people.duke.edu/~rnau/411arim2.htm)

* Validation de modèles de prédiction : [ici](https://machinelearningmastery.com/backtest-machine-learning-models-time-series-forecasting/) et [là](https://blog.insightdatascience.com/whats-wrong-with-my-time-series-model-validation-without-a-hold-out-set-94151d38cf5b)

* Des modèles plus exotiques : ARCH, GARCH [voir](https://en.wikipedia.org/wiki/Autoregressive_conditional_heteroskedasticity)

* Un exemple d'analyse de série temporelle : [ici](https://towardsdatascience.com/almost-everything-you-need-to-know-about-time-series-860241bdc578)

* Vidéo d'ouverture sur d'autres méthodes, l'exemple d'Uber : [ici](https://youtu.be/VYpAodcdFfA)

* Un livre entier sur les méthodes de prédiction : [ici](https://otexts.com/fpp2/)

* Grid search sur les time series https://machinelearningmastery.com/how-to-grid-search-deep-learning-models-for-time-series-forecasting/

* Un exemple de notebook avec un modèle ARIMA https://github.com/JTreguer/arima_example
