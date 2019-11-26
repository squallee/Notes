# tuple
1. 不可变, iterable
```
name_tuple = ('bob', 'sam')
for name in name_list:
	print(name)
name_tuple[0] = 'Tim' # error
```
2. 拆包
```
user_tuple = ("bobby", 29, 175)
name, age, height = user_tuple
else:
name = user_tuple[0]
age = user_tuple[1]
height = user_tuple[2]
user_tuple = ("bobby", 29, 165, "beijing")
name, *others = user_tuple
print(name, others)
ohters is a list
```
3. tuple的不可变不是绝对的
```
name_tuple = ("bobby", [29, 175])
name_tuple[1].append(22)
print(name_tuple)
```
tuple内的不可hash对象是可变的
4. tuple比list多的功能
   1. immutable的重要性
      # 性能优化
      	指出元素全部为immutabble的tuple会作为常量在编译时确定，因此产生了显著的速度差异
      # 线程安全
      # 可以作为dict的key
      ···
      name_tuple = ('bobby',29）
      user_info_dict = {}
      user_info_dict[user_tuple] = "bobby"
      ···
      # 拆包特性
   2. 如果拿C语言类比，tuple是struct, list是array
# namedtuple
1. usage
```
from collections import namedtuple
User = namedtuple("User", ["name", "age", "height"])
user = User(name="bobby", age=29, height=175)
print(user.age, user.name, user.height)

class User:
	def __init__(self, name, age, height):
		pass
# why not define a class
# namedtuple是tuple的一个子类，使用起来比较简单
# 省空间, 不必创建不需要的类属性
···
2. 可由tuple初始化namedtuple
···
from collections import namedtuple
User = namedtuple("User", ["name", "age", "height"])
user_tuple = ("bobby", 29, 175)
user = User(*user_tuple)
User2 = namedtuple("User", ["name", "age", "height", "edu"])
user2 = User2(*user_tuple, "master")
···
3. _make()的用法
```
# def _make(cls, iterable, ...)
User = namedtuple("User", ['name', 'age', 'height', 'edu'])
user_list = ['bobby', 28, 175, 'master']
user_tuple = ('bobby', 28, 175, 'master')
user_dict = { "name": "bobby", "age": 29, "height": 175, "edu": "master"}
user = User._make(user_list)
user2 = User._make(user_tuple)
user3 = User._make(user_dict)
```
4. asdict()的用法 tuple -> dict
```
# def _asdict(self)
User = namedtuple("User", ["name", "age", "height"])
user_tuple = ("bobby", 29, 175)
user = User(*user_tuple)
user_info_dict = user._asdict()

# defaultdict
1. dict usage: setup a dict
```
users = ['bobby1', 'bobby2', 'bobby3', 'bobby1', 'bobby2', 'bobby1']
duer_dict = {}
for user in users:
	if user not in user_dict:
		user_dict[user] = 1
	else:
		user_dict[user] += 1
print(user_dict)
```
2. setdefault usage
```
users = ['bobby1', 'bobby2', 'bobby3', 'bobby1', 'bobby2', 'bobby1']
duer_dict = {}
for user in users:
	user_dict.setdefault(user, 0)
	user_dict[user] += 1
print(user_dict)
```
3. defaultdict usage
```
from collections import defaultdict
default_dict = defaultdict(list) # callable object
default_dict['bobby']
users = ['bobby1', 'bobby2', 'bobby3', 'bobby1', 'bobby2', 'bobby1']
default_dict2 = defaultdict(int)
for user in users:
	default_dict2[user] = 1
```
4. defaultdict and dict
```
def gen_default():
	return {
		"name": "test",
		"nums": 0
	}

default_dict = defaultdict(gen_default)
default_dict['group1']

# deque
1. usage
```
from collections import deque
example = deque()
user_deque = deque(['bobby1', 'bobby2'])
user_deque.append('bobby3')
user_deque.appendleft('bobby0')
user_deque2 = user_deque.copy() # shallow copy
print(id(user_deque), di(user_deque2))
import copy
user_deque3 = copy.deepcopy(user_deque)
```
2. deque thread safe/ list is not thread safe
	deque GIL
3. reverse

# Counter
```
from collections import Counter
users = ['bob1', 'bob2', 'bob3', 'bob1', 'bob2', 'bob2']
user_counter = Counter(users)
print(user_counter)

letters = Counter('adfhjaphtapwehadhgadh')
print(letters)
letters.update('vjfdklga')
print(letters)
letters2 = Counter('jfda')
letters.update(letters2)
print(letters)
max_heap = letters.most_common(2)
print(max_heap)
```

# OrderedDict
```
from collections import OrderedDict
user_dict = Dict()
user_dict['b'] = 'bob2'
user_dict['a'] = 'bob1'
user_dict['c'] = 'bob3'
print(user_dict)

user_dict = OrderedDict()
user_dict['b'] = 'bob2'
user_dict['a'] = 'bob1'
user_dict['c'] = 'bob3'
print(user_dict)

#in python3, Dict() is ordered. in python2, Dict() is random
print(user_dict.move_to_end('b'))
print(user_dict)

print(user_dict.popitem())
print(user_dict)
```

# ChainMap
```
from collections import ChainMap
user_dict1 = {'a': 'bob1', 'b': 'bob2'}
user_dict2 = {'c': 'bob2', 'd': 'bob3'}
for key, value in user_dict1.items():
    print(key, value)
for key, value in user_dict2.items():
    print(key, value)

new_dict = ChainMap(user_dict1, user_dict2)
for key, value in new_dict.items():
    print(key, value)

user_dict1 = {'a': 'bob1', 'b': 'bob2'}
user_dict2 = {'b': 'bob3', 'c': 'bob4'}
new_dict = ChainMap(user_dict1, user_dict2)
for key, value in new_dict.items():
    print(key, value)

new_dict.new_child({"aa": "aa", "bb": "bb"})
for key, value in new_dict.items():
    print(key, value)

print(new_dict.maps)
new_dict.maps[0]["a"] = 'bobby'
print(user_dict1)
```
