# ChatOps

## flow

triggers -> rules -> workflows -> actions -> results -> triggers

triggers: when an event happens

rules: check what needs to be done

workflows: run a set of instructions

actions: execute relevant commands

results: process results for analysis or additional triggers

## 拼写检查

```
git: 'ls' is not a git command. See 'git --help'.

The most similar command is
	log
```


```python
def edits1(word):
    n = len(word)
    return set([word[0:i]+word[i+1:] for i in range(n)] +                     # deletion
               [word[0:i]+word[i+1]+word[i]+word[i+2:] for i in range(n-1)] + # transposition
               [word[0:i]+c+word[i+1:] for i in range(n) for c in alphabet] + # alteration
               [word[0:i]+c+word[i:] for i in range(n+1) for c in alphabet])  # insertion
```

## others

install dependencies

```
pip3 install rasa
pip3 install spacy
python3 -m spacy download en_core_web_md
```

train 

```
rasa train
```

output

```
Core model training completed.
Your Rasa model is trained and saved at '/Users/zhouxinzheng/code/rasa/examples/reminderbot/models/20210720-004948.tar.gz'.
```

in project path

```
rasa run actions
```

output

```
2021-07-20 00:50:50 INFO     rasa_sdk.endpoint  - Action endpoint is up and running on http://0.0.0.0:5055
```

/Users/zhouxinzheng/Library/Python/3.8/lib/python/site-packages/rasa/utils/train_utils.py

CONSTRAIN_SIMILARITIES

constrain_similarities


警告：/var/tmp/rpm-tmp.vvKSbh: 头V4 RSA/SHA1 Signature, 密钥 ID e257814a: NOKEY

软件包 k3s-selinux-0.1.1-rc1.el7.noarch 已经安装

