## 1  spaCy的安装基于anaconda3虚拟环境

### 1.1  安装

1. 进入虚拟环境

   ```shell
    conda activate <虚拟环境>
   ```

2. spaCy 安装

	```shell
    pip install spacy
    ```

3. 模型下载

   ```shell
    python -m spacy download <模型名>
    # 这里使用的是 en_core_web_sm
    python -m spacy download en_core_web_sm
   ```

### 1.2  使用

```python
import spacy

# 1 加载模型
nlp = spacy.load('en_core_web_sm')

text = "he was running late"

# 2 分词
doc = nlp(text)

cleaned = [str(token) for token in doc]
print(cleaned)

for token in doc:
    
    # 3 词形还原 token.lemma_
    print('{} --> {}'.format(token, token.lemma_))

    # 4 词性标注 token.pos_
    print('{} --> {}'.format(token, token.pos_))
```
