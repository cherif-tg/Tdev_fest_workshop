# IA et langues locales : traduire, auditer, déployer

[![Ouvrir dans Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/cherif-tg/workshop-langues-locales/blob/main/workshop_langues_locales_tdev.ipynb)

Matériel du workshop pratique présenté au **TDev Festival 2026** (60 minutes, niveau technique). On y explore ce que les modèles d'IA savent faire, et ne savent pas faire, avec une langue à faibles ressources : **l'éwé**.

## Ce que vous allez faire

| Partie | Durée | Contenu |
|---|---|---|
| 1. Traduction | 15 min | Traduire du français vers l'éwé avec NLLB-200, mesurer la qualité par domaine (chrF aller-retour et note humaine) |
| 2. Audit de LLM | 20 min | Poser 7 questions en français puis en éwé à un LLM, noter exactitude, langue et hallucination |
| 3. Démo RAG | 15 min | Chatbot sur la FAQ d'une entreprise (fictive) qui comprend et répond en français ou en éwé |

## Contenu du dépôt

```
.
├── workshop_langues_locales_tdev.ipynb   # notebook du workshop (Colab)
├── feuille_notation.csv                  # grille de notation de l'audit (à importer dans un Google Sheet)
├── requirements.txt                      # dépendances pour une exécution locale
└── README.md
```

Les fichiers `evaluation_traduction.csv` et `audit_llm.csv` sont générés par le notebook pendant le workshop.

## Démarrage rapide (Google Colab)

1. Cliquez sur le badge **Ouvrir dans Colab** en haut de cette page.
2. `Exécution` > `Modifier le type d'exécution` > **GPU T4** (recommandé ; le notebook fonctionne aussi sur CPU, plus lentement).
3. Exécutez les cellules dans l'ordre. Le premier chargement du modèle télécharge environ 2,5 Go.

## Exécution locale

Prérequis : Python 3.10 ou plus récent.

```bash
git clone https://github.com/cherif-tg/workshop-langues-locales.git
cd workshop-langues-locales
python -m venv .venv && source .venv/bin/activate   # sous Windows : .venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook workshop_langues_locales_tdev.ipynb
```

## Configuration du LLM audité (partie 2)

La variable `BACKEND` du notebook choisit comment le LLM est interrogé :

| Valeur | Usage | Prérequis |
|---|---|---|
| `hf` | API d'inférence Hugging Face | Un jeton en lecture dans la variable `HF_TOKEN` (sur Colab : *Secrets*) ; vérifier que le modèle de `HF_MODEL` est disponible |
| `ollama` | Modèle local | Ollama lancé sur la machine (ne fonctionne pas sur Colab) |
| `manuel` | Sans API | Vous collez la réponse d'un chatbot ouvert dans un autre onglet |

Pour un groupe nombreux, évitez que tout le monde appelle l'API en même temps : lancez l'audit une fois, sauvegardez `audit_llm.csv` et partagez-le.

## Adapter la démo RAG à votre propre FAQ

1. Remplacez la liste `FAQ` (questions et réponses en français) dans la partie 3.
2. Testez quelques questions réelles et ajustez la constante `SEUIL` : en dessous, le bot répond qu'il ne sait pas au lieu d'inventer.
3. Gardez la version française affichée à côté de la réponse en éwé, pour permettre le contrôle.

## Limites et bonnes pratiques

- Les traductions en éwé sont **automatiques** : elles doivent être validées par un locuteur avant tout usage réel.
- Les nombres, noms propres et termes techniques sont les points faibles à tester en priorité.
- Les questions éwé de l'audit sont générées par NLLB et peuvent contenir des erreurs.
- Le score chrF aller-retour peut être trompeur : un mot conservé tel quel donne un bon score sans traduction correcte.
- Le kabiyè ne figure pas dans NLLB-200, à ma connaissance : vérifiez la liste des langues avant de l'utiliser.

## Ressources pour aller plus loin

- [Masakhane](https://www.masakhane.io) : communauté de recherche en NLP pour les langues africaines
- [Common Voice](https://commonvoice.mozilla.org) : contribuer des enregistrements dans votre langue
- [Hugging Face](https://huggingface.co) : modèles et jeux de données ouverts

## Modèles et licences

| Composant | Utilisation |
|---|---|
| `facebook/nllb-200-distilled-600M` | Traduction (partie 1 et 3) |
| `sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2` | Embeddings pour la recherche dans la FAQ |
| Gradio | Interface de la démo |

Vérifiez les licences de chaque modèle avant un usage commercial : NLLB-200 est, à ma connaissance, publié sous une licence non commerciale (CC-BY-NC 4.0).

Licence du code de ce dépôt : [à choisir, par exemple MIT].

## Auteur

**Cherif Tenga** · Data Scientist et AI Engineer
[LinkedIn / contact à compléter]

Les contributions sont les bienvenues : propositions de questions d'audit, corrections de traductions par des locuteurs éwé, ajout d'autres langues locales.
