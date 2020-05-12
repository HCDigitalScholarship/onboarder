---
type: slides

---

### Let's start with some data on virtual instruction at Haverford.

`worked_best = Which online instructional methods have worked best for you?`

and 

`didnt_work = Of the online instructional methods that you have experienced, which ones have not worked well for you?`

[src](https://sites.google.com/haverford.edu/covidcontingency/home)

---

<a href="https://colab.research.google.com/drive/1TMcCtGURz6wI1i9iS3mI-HBiAiROsdnj?usp=sharing" target="_blank"><img src="https://colab.research.google.com/assets/colab-badge.svg"/></a>

```python
import pandas as pd
import requests 
worked_best = {'type':'best', 'text': requests.get('https://raw.githubusercontent.com/apjanco/files/master/q12.txt').text }
didnt_work = {'type':'worst', 'text': requests.get('https://raw.githubusercontent.com/apjanco/files/master/q14.txt').text }
data = [worked_best, didnt_work]
df = pd.DataFrame(data)
```

*for more on pandas see [The Pandas DataFrame: Make Working With Data Delightful](https://realpython.com/pandas-dataframe/)*
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

# inspect element 

When you open this [page](https://peaceful-knuth-705f49.netlify.app/) you can right-click and see the html code running in the browser. Right-click and select either:

"View page source"

or

"Inspect"

---

<img src="inspect.png"/>

Read <a href="https://developers.google.com/web/tools/chrome-devtools/dom" target="_blank">more here</a>

---

In practice, here are the most common uses of the browser developer tools.

- Reverse engineering an interesting site.  You can view the css and javascript imports to see what libraries are being used and how the page is built. There's also a useful Chrome plugin called [wappalyzer](https://www.wappalyzer.com/).  It will guess what framework is being used, what services and so on. 

- Everything can be changed.  If an image isn't loading.  Try changing the src, see that it's pointing to the right url. If bootstrap doesn't look right, try adding and removing classes until it looks right. 

- "Where is that color coming from and how do I change it?" When you select an element, the styes section will show all of the applied CSS rules. The "filter" box lets you search for the rules and shows you the originating file and line.  Super helpful. 

- Console is a live JavaScript shell. It is especially helpful when writing JS.  Try your code, see if it works in the browser console.  When JS doesn't work, it rarely throws helpful errors, so this can be a good way to check for typos and bugs. 

- The Network tab is a very useful window into the your page.  If it's supposed to load data from an API, but isn't, you can look at the event and get error messages. All requests will appear in Network. 


*[more here](https://www.keycdn.com/blog/chrome-devtools)*

---