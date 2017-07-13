# Regular expression

## Common

## Python Regular Expression
*Match accross '\n' in a big string*

Use ```re.S``` ,  python versions should be >= 2.7
```python
stri = 
'''
li yong qing
ni hao
ni hao
'''
print re.search(r'li.*hao',  ' can you see me ', str, flags=re.S);
```

*Non-greedy match*
Using ?
```python
re.match(r'li.*?', str)
```


## grep 
### Match a word rather than substring

grep  *-wR*  connect  *  # match all connect keyword, but not including disconnect 
