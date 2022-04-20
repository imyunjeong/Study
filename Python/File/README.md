```python
>>> import pickle

>>> path = './test.txt'
>>> data = ['123', '456', 'abc', 'def']

>>> with open(path, 'wb') as f:
>>>    pickle.dump(testList, f)
    
>>> with open(path, 'rb') as f:
>>>    readList = pickle.load(f)
>>>    print(readList)        # ['123', '456', 'abc', 'def']
````

```python
>>> import json

>>> path = './test.txt'
>>> data = '{"id":"01", "language":"korean","edition":"third", "author":"wonwoo joo"}'
>>> json.loads(data)   # 문자열을 읽을 때 loads 씀


# data를 json 파일로 저장
>>> data = {'id': '1000', 'language': {'first': 'korean', 'seconds': 'english'}, 'grade': 'A', 'name': 'honaldo'}
>>> with open(path, "w", encoding="utf-8-sig") as f:
>>>     json.dump(data, f)
>>> with open(path, "r", encoding="utf-8-sig") sa f:
>>>     readJson = json.load(f)
>>>     print(readJson)   #  {'id': '1000', 'language': {'first': 'korean', 'seconds': 'english'}, 'grade': 'A', 'name': 'honaldo'}
```
