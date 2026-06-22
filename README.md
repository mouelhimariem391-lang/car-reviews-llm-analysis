
# 🚗 Car Reviews LLM Analysis

Prototype de chatbot NLP multi-tâches pour une entreprise fictive de vente et location de voitures ("Car-ing is Sharing"), combinant plusieurs **LLM spécialisés** de Hugging Face pour analyser des avis clients : classification de sentiment, traduction, question-réponse extractive et résumé automatique.

---

## 📋 Description du projet

Plutôt que d'utiliser un seul LLM généraliste, ce projet illustre une approche courante en NLP appliqué : **orchestrer plusieurs modèles pré-entraînés, chacun spécialisé dans une tâche précise**, pour traiter différents types de demandes sur des avis clients automobiles.

Le projet répond à quatre besoins métier :

1. **Analyse de sentiment** — classifier automatiquement les avis clients comme positifs ou négatifs
2. **Traduction automatique** — traduire un extrait d'avis de l'anglais vers l'espagnol pour les nouveaux marchés
3. **Question-réponse** — extraire une réponse précise à une question posée sur un avis
4. **Résumé automatique** — condenser un avis long en quelques phrases

---

## 🛠️ Technologies utilisées

- **Python 3**
- **Hugging Face Transformers** (`pipeline`)
- **PyTorch**
- **pandas**
- **scikit-learn** (métriques accuracy / F1)
- **evaluate** (métrique BLEU)

### Modèles pré-entraînés

| Tâche | Modèle | Famille |
|---|---|---|
| Sentiment | `distilbert-base-uncased-finetuned-sst-2-english` | Encodeur (BERT) |
| Traduction EN→ES | `Helsinki-NLP/opus-mt-en-es` (MarianMT) | Encodeur-décodeur |
| Question-réponse | `deepset/minilm-uncased-squad2` (MiniLM) | Encodeur (BERT) |
| Résumé | `facebook/bart-large-cnn` (BART) | Encodeur-décodeur |

---

## 📂 Structure du projet

```
car-reviews-llm-analysis/
│
├── data/
│   ├── car_reviews.csv              # Dataset des avis clients
│   └── reference_translations.txt   # Traductions de référence pour le score BLEU
│
├── car_reviews_llm_analysis.ipynb   # Notebook principal
└── README.md
```

---

## ⚙️ Installation

```bash
git clone https://github.com/ton-username/car-reviews-llm-analysis.git
cd car-reviews-llm-analysis
pip install pandas torch transformers scikit-learn evaluate
```

---

## ▶️ Utilisation

Ouvre le notebook et exécute les cellules dans l'ordre :

```bash
jupyter notebook car_reviews_llm_analysis.ipynb
```

Le notebook charge le dataset, applique chaque modèle à la tâche correspondante, puis affiche les résultats et métriques d'évaluation.

---

## 📊 Résultats obtenus

| Tâche | Métrique | Résultat |
|---|---|---|
| Sentiment | Accuracy | 0.80 |
| Sentiment | F1-score | 0.857 |
| Traduction | BLEU score | ~0.75 |
| Question-réponse | Réponse extraite | *"ride quality, reliability"* |
| Résumé | Longueur | 50–55 tokens |

---

## 💡 Points clés

- **Approche extractive vs générative** : le modèle de QA extrait une réponse directement du texte source (pas d'hallucination possible), tandis que le modèle de résumé reformule le contenu de façon abstractive.
- **Évaluation rigoureuse** : chaque sortie de modèle est validée par une métrique adaptée (accuracy/F1 pour la classification, BLEU pour la traduction).
- **Architecture multi-modèles** : chaque modèle, plus léger et spécialisé qu'un LLM généraliste, offre un meilleur compromis performance/coût/rapidité sur sa tâche dédiée.

---

## 📄 Licence

Projet réalisé à des fins d'apprentissage personnel.
