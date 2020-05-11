---
type: slides

---

### Let's start with some data on virtual instruction at Haverford.
We'll make a column with responses to  

`worked_best = Which online instructional methods have worked best for you?`

and 

`didnt_work = Of the online instructional methods that you have experienced, which ones have not worked well for you?`

[src](https://sites.google.com/haverford.edu/covidcontingency/home)

---

<a href="https://colab.research.google.com/drive/1TMcCtGURz6wI1i9iS3mI-HBiAiROsdnj?usp=sharing"><img src="https://colab.research.google.com/assets/colab-badge.svg"/></a>

```python
import pandas as pd
import requests 
worked_best = {'type':'best', 'text': requests.get('https://raw.githubusercontent.com/apjanco/files/master/q12.txt').text }
didnt_work = {'type':'worst', 'text': requests.get('https://raw.githubusercontent.com/apjanco/files/master/q14.txt').text }
data = [worked_best, didnt_work]
df = pd.DataFrame(data)
```
---

```python
import spacy
nlp = spacy.load('en')
import scattertext as st
corpus = st.CorpusFromPandas(df, 
                             category_col='type', 
                             text_col='text',
                             nlp=nlp).build()

html = st.produce_scattertext_explorer(corpus,
                                       category='best',
                                       category_name='Best',
                                       not_category_name='Worst',
                                       width_in_pixels=1000,
                                       )
```


if we save the html variable to a file 
```python
from pathlib import Path
p = Path.cwd() / 'scatter.html'
p.write_text(html)
```

we get [this](https://raw.githubusercontent.com/apjanco/files/master/scatter.html)

---


<a href="https://peaceful-knuth-705f49.netlify.app/" target="_blank"><img src="scatter.png"></a>

---

