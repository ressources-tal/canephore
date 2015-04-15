# Canéphore
Corpus français de tweets annotés pour l'évaluation de la fouille d'opinion ciblée 

## Présentation

La fouille d'opinion ciblée (_aspect-based sentiment analysis_) connaît ces dernières années un intérêt particulier, visible dans les sujets des récentes campagnes d'évaluation [_SemEval_ 2014](http://alt.qcri.org/semeval2014/task4/) et [2015](http://alt.qcri.org/semeval2015/task12/) ainsi que [DEFT 2015](https://deft.limsi.fr/2015/index.php). Cependant les corpus annotés et publiquement disponibles permettant l'évaluation de cette tâche sont rares. Canéphore est un corpus français librement accessible de 10 000 tweets manuellement annotés.

### Objectifs

Cette ressource permet d'évaluer un système réalisant une fouille d'opinion au niveau des sujets discutés. L'objectif est de pouvoir mesurer la détection d'opinion dans un cadre le plus formel possible, magré la subjectivité de ce type d'évaluation. Ce cadre est celui défini par B. Liu ([Liu, 2010](http://gnode1.mib.man.ac.uk/tutorials/NLP-handbook-sentiment-analysis.pdf)), modélisant une opinion par un tuple _(énonciateur, temps d'énonciation, cible jugée, aspect de la cible jugé, sentiment exprimé)_. Les annotations ici ne concernent que la cible, ses aspects et le sentiment exprimé. L'annotation a été réalisée grâce à l'outil [Brat](http://brat.nlplab.org/).

### Contenu

Le corpus provient d'un ensemble de tweets échangés pendant l'événement "Miss France" en 2012. Les doublons, les retweets, les citations ainsi que les tweets considérés trop courts (moins de 3 mots) ont été retirés afin d'éviter le biais que peuvent apporter les répétitions. Ces suppressions réduisent le corpus à 10 000 documents, soit environ 127 000 mots.

L'ensemble du corpus est séparé en 10 parties de 1000 documents, d'une part pour alléger la navigation dans les fichiers et d'autre part pour faciliter l'évaluation en parties d'entrainement, de développement et de test.

La liste `tweets-ids` répertorie les identifiants de tous les tweets. Les annotations sont disponibles au format Brat Standoff, et stockés dans les fichiers dont le nom respecte la nomenclature [tweet_id].ann, pour chaque tweet.

Les annotations effectuées décrivent des opinions **directes**, qu'elles soient **explicites** ou **implicites**.  L'information annotée doit être non ambigüe pour un humain lisant le tweet.

####Exemples:
_Ces exemples sont des tweets du corpus, modifiés pour le respect de l'anonymat_

###### Opinions directes ou indirectes, explicites ou implicites 

Opinion directe et explicite :
> J'aime pas Miss A

* La cible et le sentiment exprimé sont évidents
* Le marqueur d'opinion _aime_ et la cible _Miss A_ sont annotés. Le marqueur de négation _pas_ est annoté et inverse le sentiment de _aime_

Opinion directe et implicite:
> Miss B on dirait qu'elle a prit un coup de pelle

* La cible est évidente, et le sentiment - bien qu'il soit est exprimé de façon implicite - est clair pour un lecteur francophone 
* La cible _Miss B_ et le marqueur d'opinion implicite _a prit un coup de pelle_ sont annotés

Opinion indirecte et explicite:
> Elle est très belle

* Le sentiment exprimé est évident, mais la cible ne peut pas être identifiée
* Aucune annotation n'est effectuée

Opinion indirecte et implicite:
> Celle là, c'est pas possible

* La cible ne peut pas être identifiée, et le sentiment exprimé n'est pas évident
* Aucune annotation n'est effectuée

###### Cas des opinions contextuelles

Opinion directe contextuelle :
> Miss C on dirait ma tante

* La cible est évidente, mais le sentiment demande une connaissance du contexte
* Aucune annotation n'est effectuée

###### Cas des aspects implicites
Opinion directe et explicite, mais aspect implicite :
> Miss D est mal coiffée

* Le sentiment exprimé est évident, mais la cible (ici la coiffure) demande d'être inférée 
* Le marqueur d'opinion _mal_ , la cible _Miss D_ et l'aspect implicite _coiffée_ sont annotés

###### Cas des comparaisons

Comparaison :
> Miss A est mieux que Miss B

* Les cibles et le sentiment exprimés sont évidents
* Le marqueur d'opinion _mieux_ et les cibles _Miss A_, _Miss B_ sont annotés. Le mot _que_ est annoté, il est considéré comme une marque de négation inversant le sentiment de _mieux_ pour la cible _Miss B_

## Téléchargement des tweets

Le script `retrieve-tweets.py` permet de télécharger le texte des tweets associés aux identifiants fournis. Il est nécessaire de posséder un compte Twitter et un accès à l'API, qui peut être obtenu gratuitement en remplissant [le formulaire de création d'application Twitter](https://apps.twitter.com/app/new). Cet accès doit être renseigné dans le fichier `retrieve-tweets.config`.

Il suffit alors de lancer:
```
python retrieve-tweets.py chemin_vers_config chemin_vers_la_liste_d'ids chemin_vers_le_dossier_sortie
```

Attention ! Le téléchargement par id est limité dans le cadre d'une utilisation gratuite de l'API Twitter: il faut compter 1 h pour le téléchargement de 500 tweets environ.

## Licence
Ce corpus est disponible sous la licence GNU GPL V2