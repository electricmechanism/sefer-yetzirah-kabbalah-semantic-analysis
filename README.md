# Sefer Yetzirah Semantic Analysis

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.17373232.svg)](https://doi.org/10.5281/zenodo.17373232)

Computational methodology for semantic text analysis based on the symbolic structure of the ancient Hebrew Kabbalistic treatise *Sefer Yetzirah*. This approach formalizes the sefirot-letter system as a weighted directed graph and applies spectral analysis to identify semantic patterns in Hebrew texts.

## 📄 Publication

**Paper:** *Semantic Analysis in the Context of Jewish Theology and the Symbolism of the Kabbalistic Treatise Sefer Yetzirah*  
**DOI:** [10.5281/zenodo.17373232](https://doi.org/10.5281/zenodo.17373232)  
**Keywords:** Judaism, Kabbalah, Sefer Yetzirah, Digital Humanities, Computational Linguistics, Graph Theory

## 🎯 Overview

This repository contains the implementation of a novel semantic analysis method that:

1. **Formalizes** the Sefer Yetzirah symbolic system as a graph:
   - 10 **sefirot** (vertices) representing archetypal concepts
   - 22 **Hebrew letters** (edges) connecting sefirot
   
2. **Analyzes** Hebrew texts by:
   - Building text-specific graphs based on letter frequencies
   - Applying **spectral clustering** to identify semantic phases
   - Using **TF-IDF normalization** to suppress structural artifacts

3. **Interprets** results through the lens of Kabbalistic tradition, providing a bridge between computational methods and hermeneutic analysis.

### Key Features

- ✅ **Graph-based semantic model** rooted in Sefer Yetzirah
- ✅ **Spectral analysis** for text segmentation
- ✅ **TF-IDF weighting** to identify text-specific patterns
- ✅ **Reproducible** analysis pipeline
- ✅ **Visualization** tools for graph structures and semantic phases

## 🚀 Quick Start
```python
from src.build_graph import build_sephirot_graph
from src.tfidf_analysis import get_top_sfirot_tfidf
from data.sfirot import sfirot
from data.letter_to_sfirot import letter_to_sfirot

# Load your Hebrew text
text = """
בראשית ברא אלהים את השמים ואת הארץ
"""

# Build graph
G = build_sephirot_graph(letter_to_sfirot, sfirot, text=text, method="log")

# Analyze with TF-IDF
baseline_activity = compute_baseline_activity(letter_to_sfirot, sfirot, [text])
top_sfirot = get_top_sfirot_tfidf(G, sfirot, baseline_activity, top_n=3)

# Results: most semantically significant sefirot for this text
for name, meaning, activity, specificity in top_sfirot:
    print(f"{name} ({meaning}): specificity = {specificity:.3f}")
```

## 📦 Installation

### Requirements

- Python 3.8+
- Dependencies listed in `requirements.txt`

### Setup
```bash
# Clone the repository
git clone https://github.com/yourusername/sefer-yetzirah-semantic-analysis.git
cd sefer-yetzirah-semantic-analysis

# Install dependencies
pip install -r requirements.txt

# Run example analysis
python examples/analyze_psalm119.py
```

## 📂 Repository Structure
```
sefer-yetzirah-semantic-analysis/
├── README.md                   # This file
├── LICENSE                     # CC BY 4.0 license
├── requirements.txt            # Python dependencies
├── src/
│   ├── build_graph.py         # Graph construction
│   ├── spectral_clustering.py # Clustering methods
│   ├── tfidf_analysis.py      # TF-IDF normalization
│   └── visualize.py           # Visualization utilities
├── data/
│   ├── sfirot.py              # Sefirot definitions
│   ├── letter_to_sfirot.py    # Letter-sefirot mappings
│   └── sample_texts/          # Example Hebrew texts
├── examples/
│   ├── analyze_psalm119.py    # Complete example
│   └── basic_usage.ipynb      # Jupyter notebook tutorial
└── tests/
    └── test_graph.py          # Unit tests
```

## 🔬 Methodology

### 1. Graph Model

The Sefer Yetzirah framework is formalized as a weighted directed graph **G = (V, E)**:

- **Vertices (V):** 10 sefirot representing archetypal concepts:
  - כתר (Keter, Crown)
  - חכמה (Chokhmah, Wisdom)
  - בינה (Binah, Understanding)
  - חסד (Chesed, Mercy)
  - גבורה (Gevurah, Strength)
  - תפארת (Tiferet, Beauty)
  - נצח (Netzach, Eternity)
  - הוד (Hod, Glory)
  - יסוד (Yesod, Foundation)
  - מלכות (Malkhut, Kingdom)

- **Edges (E):** 22 Hebrew letters connecting sefirot based on Sefer Yetzirah tradition

### 2. Text Analysis Pipeline
```
Input Text (Hebrew)
    ↓
Letter Frequency Analysis
    ↓
Weighted Graph Construction
    ↓
Spectral Clustering
    ↓
TF-IDF Normalization
    ↓
Semantic Phase Identification
    ↓
Interpretation via Kabbalistic Framework
```

### 3. TF-IDF for Semantic Specificity

To suppress structural artifacts (e.g., centrally positioned sefirot dominating all texts), we apply:

**TF-IDF(s, p) = TF(s, p) × IDF(s)**

Where:
- **TF(s, p)** = activity of sefira *s* in phase *p* (normalized by total activity)
- **IDF(s)** = inverse of baseline frequency of *s* across corpus

This highlights sefirot that are **anomalously active** for specific text segments.

## 📊 Example: Psalm 119 Analysis

The method was validated on Psalm 119 (176 verses), revealing six semantic phases:

| Phase | Top Sefirot | Interpretation |
|-------|-------------|----------------|
| 1 | Gevurah, Chokhmah, Chesed | Strictness of law, wisdom, divine mercy |
| 2 | Malkhut, Yesod, Keter | Kingdom, foundation, divine source |
| 3 | Netzach, Binah, Keter | **Eternity** ("forever, O Lord, Your word") |
| 4 | Hod, Malkhut, Yesod | Glory, praise of the law |
| 5 | Gevurah (max), Keter, Binah | Judgment, fear, understanding |
| 6 | Malkhut, Chokhmah, Binah | Kingdom, wisdom-understanding pair |

**Statistical validation:** p < 0.001 (non-random correspondence with text themes)

See full analysis in `examples/analyze_psalm119.py`

## 📖 Usage Examples

### Basic Analysis
```python
from src.build_graph import build_sephirot_graph
from data import sfirot, letter_to_sfirot

# Your Hebrew text
text = "..."

# Build graph with log-normalization
G = build_sephirot_graph(letter_to_sfirot, sfirot, text=text, method="log")

# Get degree centrality (simple analysis)
import networkx as nx
centrality = nx.degree_centrality(G)
print(centrality)
```

### Advanced: Multi-Phase Analysis
```python
from src.spectral_clustering import cluster_text_segments
from src.tfidf_analysis import get_top_sfirot_tfidf

# Split text into segments
segments = split_text_into_segments(text, n=200)

# Cluster segments
clusters = cluster_text_segments(segments, letter_to_sfirot, sfirot)

# Analyze each phase
for phase_id, segment_ids in enumerate(clusters):
    phase_text = " ".join([segments[i] for i in segment_ids])
    G_phase = build_sephirot_graph(letter_to_sfirot, sfirot, text=phase_text)
    
    top_sfirot = get_top_sfirot_tfidf(G_phase, sfirot, baseline, top_n=3)
    print(f"Phase {phase_id+1}: {top_sfirot}")
```

### Visualization
```python
from src.visualize import draw_sephirot_graph

# Visualize the graph with Hebrew labels
draw_sephirot_graph(G)
```

## 🧪 Running Tests
```bash
# Run all tests
pytest tests/

# Run specific test
pytest tests/test_graph.py -v
```

## 📚 Data Sources

### Sefer Yetzirah Model

This implementation uses the **Saadia Gaon version** (10th century) of Sefer Yetzirah, which systematizes the 22 Hebrew letters into:
- 3 mother letters (אמש)
- 7 double letters (בגדכפרת)
- 12 simple letters

Letter-sefirot mappings are based on the **231 Gates** (שערים) concept and classical commentaries (Raavad, Ramban).

### Hebrew Texts

Example texts are from:
- **Sefaria.org** (open API, CC BY-NC license)
- **Mechon Mamre** (public domain)

For copyright reasons, full Tanakh corpus is not included. Users should obtain texts from these sources.

## 🤝 Contributing

Contributions are welcome! Areas for improvement:

- [ ] Additional Sefer Yetzirah versions (Gra, Ari)
- [ ] Comparison with baseline NLP methods (LDA, Word2Vec)
- [ ] Expansion to other languages (Arabic, Greek)
- [ ] Quantitative evaluation metrics
- [ ] Web interface for interactive analysis

Please open an issue or submit a pull request.

## 📝 Citation

If you use this code in your research, please cite:
```bibtex
@misc{author2025sefer,
  title={Semantic Analysis in the Context of Jewish Theology and the Symbolism of the Kabbalistic Treatise Sefer Yetzirah},
  author={[Your Name]},
  year={2025},
  publisher={Zenodo},
  doi={10.5281/zenodo.17373232},
  url={https://doi.org/10.5281/zenodo.17373232}
}
```

**APA format:**
```
[Your Name]. (2025). Semantic Analysis in the Context of Jewish Theology 
and the Symbolism of the Kabbalistic Treatise Sefer Yetzirah. Zenodo. 
https://doi.org/10.5281/zenodo.17373232
```

## 📄 License

This work is licensed under a [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/).

**You are free to:**
- Share — copy and redistribute the material
- Adapt — remix, transform, and build upon the material

**Under the following terms:**
- Attribution — You must give appropriate credit, provide a link to the license, and indicate if changes were made.

## 🙏 Acknowledgments

This research draws upon:
- Classical Kabbalistic commentaries (Saadia Gaon, Raavad, Ramban)
- Modern computational linguistics methodologies
- Open-source tools: NetworkX, NumPy, SciPy, scikit-learn

Special thanks to the Digital Humanities community for inspiration and feedback.

## 📧 Contact

For questions, collaborations, or feedback:
- **Email:** [av.el3@yandex.com]
- **ResearchGate:** [https://www.researchgate.net/profile/Elena-Avraham]
- **Issues:** [GitHub Issues](https://github.com/yourusername/sefer-yetzirah-semantic-analysis/issues)

---

**⭐ If you find this work useful, please star the repository!**

**🔗 Related Resources:**
- [Sefer Yetzirah (English translation)](https://www.sacred-texts.com/jud/yetzirah.htm)
- [Sefaria - Open Jewish Texts](https://www.sefaria.org)
- [Digital Humanities Quarterly](http://digitalhumanities.org/dhq/)
