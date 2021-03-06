![Test](https://github.com/comprehensivetech/frozenjsondict/workflows/Test/badge.svg?branch=master)

# frozenjsondict

Inspired in [https://github.com/slezica/python-frozendict](https://github.com/slezica/python-frozendict), this variation
takes it one step further and lets you build immutable JSON dictionaries that can be used as dictionary keys and set
elements.

Its hash function uses JSON serialization, so you can use it as long as your data is JSON-serializable.

Example of usage:

```python
from frozenjsondict import FrozenJsonDict

fjd_1 = FrozenJsonDict({"a": [1, 2, 3]})
fjd_2 = FrozenJsonDict({"b": [3, 4], "c": [6]})
fjd_3 = FrozenJsonDict({"c": [6], "b": [3, 4]})

# Support for common interfaces
"a" in fjd_1  # True
fjd_1["a"]  # [1, 2, 3]
fjd_1.a  # [1, 2, 3]
len(fjd_2)  # 2
fjd_2 == fjd_3  # True
for key, value in fjd_2.items():
    print(f"{key}: {value}")
    # b: [3, 4]
    # c: [6]

# Usage as dictionary key
fjd_dict = dict()
fjd_dict[fjd_1] = 1
fjd_dict[fjd_2] = 2
fjd_dict[fjd_3] = 3
print(fjd_dict)
# {<FrozenJsonDict {"a":[1,2,3]}>: 1, <FrozenJsonDict {"b":[3,4],"c":[6]}>: 3}

# Usage as set element
fjd_set = set()
fjd_set.add(fjd_1)
fjd_set.add(fjd_2)
fjd_set.add(fjd_3)
print(fjd_set)
# {<FrozenJsonDict {"a":[1,2,3]}>, <FrozenJsonDict {"b":[3,4],"c":[6]}>}
```