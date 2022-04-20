```python
>>> import pickle

>>> filePath = './test.txt'
>>> testList = ['123', '456', 'abc', 'def']
>>> with open(filePath, 'wb') as f:
>>>    pickle.dump(testList, f)
    
>>> with open(filePath, 'rb') as f:
>>>    readList = pickle.load(f)
>>>    print(readList)        # ['123', '456', 'abc', 'def']
````
