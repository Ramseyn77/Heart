Description : Ensemble de données sur les maladies cardiaques, permettant de prédire la présence d'une maladie cardiaque chez un patient.
Source : UCI Machine Learning Repository.

age: age in years
sex: sex (1 = male; 0 = female)
cp: chest pain type -- Value 0: typical angina -- Value 1: atypical angina -- Value 2: non-anginal pain -- Value 3: asymptomatic
trestbps: resting blood pressure (in mm Hg on admission to the hospital)
chol: serum cholestoral in mg/dl
fbs: (fasting blood sugar > 120 mg/dl) (1 = true; 0 = false)
restecg: resting electrocardiographic results -- Value 0: normal -- Value 1: having ST-T wave abnormality (T wave inversions and/or ST elevation or depression of > 0.05 mV) -- Value 2: showing probable or definite left ventricular hypertrophy by Estes' criteria
thalach: maximum heart rate achieved
exang: exercise induced angina (1 = yes; 0 = no)
oldpeak = ST depression induced by exercise relative to rest
slope: the slope of the peak exercise ST segment -- Value 0: upsloping -- Value 1: flat -- Value 2: downsloping
ca: number of major vessels (0-3) colored by flourosopy
thal: 0 = normal; 1 = fixed defect; 2 = reversable defect and the label
condition: 0 = no disease, 1 = disease



âge : ége en années
Sexe : sexe (1 = masculin ; 0 = féminin)
CP : type de douleur thoracique -- Valeur 0 : angine typique -- Valeur 1 : angine atypique -- Valeur 2 : douleur non angineuse -- Valeur 3 : asymptomatique
Trestbps : pression artérielle au repos (en mm Hg � l'admission à l'hôpital)
Chol : cholestérol sérique en mg/dl
Fbs : glycémie à jeun > 120 mg/dl (1 = vrai ; 0 = faux)
Restecg : résultats électrocardiographiques au repos -- Valeur 0 : normal -- Valeur 1 : pr�sence d'anomalie de l'onde ST-T (inversions de l'onde T et/ou élévation ou dépression de > 0,05 mV) -- Valeur 2 : montrant une hypertrophie ventriculaire gauche probable ou définitive selon les critères d'Estes
Thalach : fréquence cardiaque maximale atteinte
Exang : angine induite par l'exercice (1 = oui ; 0 = non)
Oldpeak : dépression de l'onde ST induite par l'exercice par rapport au repos
Slope : la pente du segment ST à l'effort maximal -- Valeur 0 : ascendante -- Valeur 1 : plate -- Valeur 2 : descendante
Ca : nombre de gros vaisseaux (0-3) colorés par fluoroscopie
Thal : 0 = normal ; 1 = défaut fixe ; 2 = défaut réversible et l'étiquette
Condition : 0 = pas de maladie, 1 = maladie

ANALYSE ET EXPLORATION DES DONNEES :

Analyse de la forme :
La target : condition
Taille  : (297, 14)
les types de donnés : 
    int64      13
    float64     1
les variables manquantes : Aucune valeur manquantes

Analyse du fond :
Analyse de la target : 
    0  =  160
    1  =  137
    Le nombre de cas positif représente 50% de la dataset (équilibrer). 
Analyse des variables (oldpeak) : 
    La variable ne suit pas la loi normal alors elles n'est pas standarisée
Analyse de la relation variable-target :
    Variation des variables en fonctions de la target (posiotive, negative) :
        'age','cp','restecg','thalach','oldpeak','slope' et 'ca' sont les varibles qui présentes le plus de variations pour les cas positifs et négatifs du dataset
        Hypothèse : Ces varibales joue un rôle très importants dans la détermination des cas positifs et négatifs
    Relation target-age :
        La target présente une forte variation en fonction de l'âge du patient. De cet dataset les plus grands nombres des cas positifs à la maladie sont au delà de 54 ans 
    Relation Variables-Variables
        -Corrélation entre les variables : trés faibles corrélation entre les variables
    Relation oldpeak/thalach-target :
        On remarque plus de cas positif avec thalac > 140 et oldpeak  > 1


PREPROCESSING :
    -Importation de sklearn et les différents module pour le preprocessing
    -Création des datasets (trainset et testset ) pour l'entraînement du model et le test 
    -La creation des fonctions preprocessing et evaluation pour la preprocessing et l'evaluation des performances du model 
    -Lors de l'evaluation on remarque que le model de RandomForestClassifier du module ensemble de sklearn présente plus un bonne adaptation par rapport aux autres...
    -Elimination des variables moins importantes : 'sex','fbs','restecg','exang','slope' (Création de la fonction imputation pour gerer)
    -Utiisation d'une pipeline : Pas de grand changement au niveau du val score (une légère amélioration sur la courbe d'apprentissage)
    -Maintenant on essaye une autre methode en utilisant le selectKeyBest avec f_classif (nous nous limiteraons touours à 10 variables) : amelioration evidentes (moins d'erreur du modele)