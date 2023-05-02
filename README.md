# Manuel d'utilisation de l'annotation au format CoNLL-U

## Description:
Cet API est principalement utilisé pour convertir un fichier XML en format CoNLL-U et effectuer la tokénisation de mots à l'aide de la fonction ***'Tokenisation.py'***, et puis les écrit dans un ficher CoNLL-U. Et puis cet API réalise une séries de fonctions, ***'Lemmatisation.py'***, ***'Posparse.py'***, ***'Featsparse.py'***, ***'Depparse.py'***, ***'Headparse.py'*** pour le traitement de la langue, tels que la segmentation des mots, la lemmatisation et l'étiquetage morphosyntaxique etc, et les écrit dans un même ficher CoNLL-U. ***'main.py'*** est responsable d'appeler les modules qu'on a mentionné au-dessus afin de réaliser le traitement de la langue.


## Utilisation
Dans le ficher ***'main.py'***, l'utilisateur doit d'abord exécuter la classe **‘Tokenisation’**. Poue l'exécuter, il faut saisir le chemin d'accès du fichier XML et les processors. Une exception sera levée, si on ne trouve pas le ficher, le ficher n'est pas au format XML, ou les processors ne sont pas dans le même format que les descriptions, à savoir:

processors={

        "language":"fr",
        
        "tokenize" : {
        
                "tool":"nltk",
                
                "model":"tokenizers/punkt/french.pickle"
        },
        
        "pos": {
        
                "tool":"stanza",
                
                "model":"partut"
                
        },
        
        "feats": {
        
            "tool": "stanza",
            
            "model": "partut"
            
        },
        
        "lemma": {
        
                "tool":"spacy",
                
                "model":"fr_core_news_sm",
                
        },
        
        "headparse": {
        
            "tool": "stanza",
            
            "model": "standard"
            
        },
        
        "depparse": {
        
                "tool":"spacy",
                
                "model":"fr_core_news_sm"
                
        }
        
    }
   
Puis on appèle les autres classes, ***'Lemmatisation'***, ***'Posparse'***, ***'Featsparse'***, ***'Depparse'***, ***'Headparse'***. 

Il faut noter que les fichier CoNLL-U d'entrée pour ces classes est le fichier de sortie de la tokenisation alors que le  format de processors est le même que celui mentionné ci-dessus.


## API

* **Tokenisation.py**
  * Desciption: Ce code permet de transformer des fichiers XML en fichiers au format CoNLL-U et d'utiliser différents outils tels que stanza、spacy、udpipe et nltk pour réaliser la tokénisation de mots.
  * Entrée :
    * input_file: le chemin d'accès du fichier XML 
    * xpath_expression:  l'expression XPath utilisée pour sélectionner la zone de texte à traiter
    * processors:  un dictionnaire contenant des informations sur la langue
    * output_file: le chemin d'accès du fichier CoNLL-U
  * Return :
    * output_file: le fichier CoNLL-U

* **Lemmatisation.py**
  * Desciption: Ce code définit une classe ‘Lemmatisation’ avec une méthode ‘lemma_wrapper’ qui lemmatise un fichier CoNLL-U en utilisant différentes outils (Stanza, spaCy et UDPipe) 
  * Entrée :
    * conllu_filename: le chemin d'accès du fichier CoNLL-U
    * processors : un dictionnaire contenant des informations sur la langue
  * Return :
    * output_file: le fichier CoNLL-U
* **Posparse.py**
  * Desciption: Ce code définit une classe ‘Featsparse’ avec une méthode ‘pos_wrapper’ qui réalise un étiquetage de parties du discours (POS) en utilisant différentes outils (Stanza, spaCy et UDPipe) 
  * Entrée :
    * conllu_filename: le chemin d'accès du fichier CoNLL-U
    * processors : un dictionnaire contenant des informations sur la langue, l'outil et le modèle à utiliser pour réaliser l'étiquetage de parties du discours (POS)
  * Return :
    * output_file: le fichier CoNLL-U

* **Featsparse.py**
  * Desciption: Ce code définit une classe ‘Featsparse’ avec une méthode ‘feats_wrapper’ qui permet de calculer les caractéristiques pour chaque jeton en utilisant différentes outils (Stanza, spaCy et UDPipe) 
  * Entrée :
    * conllu_filename: le chemin d'accès du fichier CoNLL-U
    * processors : un dictionnaire contenant des informations sur la langue, l'outil et le modèle à utiliser pour calculer les caractéristiques pour chaque jeton
  * Return :
    * output_file: le fichier CoNLL-U

* **Depparse.py**
  * Desciption: Ce code définit une classe ‘Depparse’ avec une méthode ‘deprel_wrapper’ qui réalise l'analyse des dépendances en utilisant différentes outils (Stanza, spaCy et UDPipe).
  * Entrée :
    * conllu_filename: le chemin d'accès du fichier CoNLL-U
    * processors : un dictionnaire contenant des informations sur la langue,l'outil et le modèle à utiliser pour l'analyse des dépendances
  * Return :
    * output_file: le fichier CoNLL-U

* **Headparse.py**
  * Desciption: Ce code définit une classe ‘Headparse’ avec une méthode ‘head_wrapper’ qui permet de réaliser l'analyse de la tête de chaque jeton en utilisant différentes outils (Stanza, spaCy et UDPipe).
  * Entrée :
    * conllu_filename: le chemin d'accès du fichier CoNLL-U
    * processors : un dictionnaire contenant des informations sur la langue,l'outil et le modèle à utiliser pour l'analyse de la tête de chaque jeton 
  * Return :
    * output_file: le fichier CoNLL-U

* **main.py**
  * Ce code permet de faire appel aux différentes classes pour le traitement de la langue, tels que la segmentation des mots, la lemmatisation et l'étiquetage morphosyntaxique etc.
