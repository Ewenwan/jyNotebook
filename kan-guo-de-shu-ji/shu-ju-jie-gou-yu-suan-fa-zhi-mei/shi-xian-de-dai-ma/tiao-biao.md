```
// * 经常复习重点
import random
from typing import Optional

class Node(object):

    def __init__(self,key:Optional[int]=None):
        self._key = key
        self._points = []


class SkipList:

    _MAX_LEVEL = 100

    def __init__(self):
        self._level_count = 1
        self._head = Node()
        self._head._points = [None] * type(self)._MAX_LEVEL

    def find(self,value:int) -> Optional[Node]:
        p = self._head
        for i in range(self._level_count-1,-1,-1):
            while p._points[i] and p._points[i]._key < value:
                p = p._points[i]

        return p._points[0] if p._points[0] and p._points[0]._key == value else None

    def insert(self,value:int):
        level = self._random_level()
        if self._level_count < level: self._level_count = level
        new_node = Node(value)
        new_node._points = [None] * level
        update = [self._head] * level

        p = self._head
        for i in range(level-1,-1,-1):
            while p._points[i] and p._points[i]._key < value:
                p = p._points[i]

            update[i] = p

        for i in range(level):
            new_node._points[i] = update[i]._points[i]
            update[i]._points[i] = new_node

    def _random_level(self,p:float=0.5) -> int:
        level = 1
        while random.random() < p and level < type(self)._MAX_LEVEL:
            level += 1
        return level

    def delete(self,value):
        update = [None] * self._level_count
        p = self._head
        for i in range(self._level_count-1,-1,-1):
            while p._points[i] and p._points[i]._key < value:
                p = p._points[i]

            update[i] = p

        if p._points[0] and p._points[0]._key == value:
            for i in range(self._level_count-1,-1,-1):
                if update[i]._points[i] and update[i]._points[i]._key == value:
                    update[i]._points[i] = update[i]._points[i]._points[i]

    def __repr__(self) -> str:
        values = []
        p = self._head
        while p._points[0]:
            values.append(str(p._points[0]._key))
            p = p._points[0]
        return '->'.join(values)


if __name__ == "__main__":
    l = SkipList()
    for i in range(10):
        l.insert(i)
    print(l)
    p = l.find(7)
    print(p._key)
    l.delete(3)
    print(l)
```



