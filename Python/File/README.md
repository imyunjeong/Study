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


## Read and Write JSON data by Python
json.org의 JSON 소개 내용에 따르면, JSON (JavaScript Object Notation) 은 XML, YAML 과 함께 효율적으로 데이터를 저장하고 교환(exchange data)하는데 사용하는 텍스트 데이터 포맷 중의 하나입니다. JSON은 사람이 읽고 쓰기에 쉬우며, 또한 기계가 파싱하고 생성하기도에 쉽습니다. JSON은 그 이름에서 유추할 수 있듯이 JavaScript의 프로그래밍 언어의 부분에 기반하고 있으며, C-family 프로그램밍 언어 (C, C++, C#, Java, JavaScript, Perl, Python 등)의 규약을 따르고 있어서 C-family 프로그래밍 언어 간 데이터를 교환하는데 적합합니다. 

JSON은 아래의 두개의 구조로 이루어져 있습니다. 
- 이름/값 쌍의 집합 (A collection of name/value pairs): object, record, struct, dictionary, hash table, keyed list, associative array
- 정렬된 값의 리스트 (An ordered list of values): array, vector, list, sequence

```python
>>> import json
>>> json_string = json.dumps(py_data)

>>> py_data = json.loads(json_file)
```

출처: https://rfriend.tistory.com/474 [R, Python 분석과 프로그래밍의 친구 (by R Friend)]


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


- loads, dumps : s가 붙으면 json 문자열 관련
- load, dump : 대상을 파싱해서 파이썬 객체(dict 등)로 변환
