# 단위 테스트 
```
import unittest

class TestStringMethods(unittest.TestCase):

    def setUp(self):
    

    def test_upper(self):
        self.assertEqual('foo'.upper(), 'FOO')

    def test_isupper(self):
        self.assertTrue('FOO'.isupper())
        self.assertFalse('Foo'.isupper())

    def test_split(self):
        s = 'hello world'
        self.assertEqual(s.split(), ['hello', 'world'])
        # check that s.split fails when the separator is not a string
        with self.assertRaises(TypeError):
            s.split(2)
```

## setup 
- `def setUp(selft):` 로 시작해서 초기 설정 처리 

## assert 
- `self.assertTrue(condition)`
- `self.assertFalse(condition)`
- `self.assertEqual(expect, actual)`
