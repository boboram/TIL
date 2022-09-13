```
import os
import unittest

import pymysql

from dotenv import load_dotenv

class TestMysqlConnetion(unittest.TestCase):

    load_dotenv()

    def setUp(self):
        self.con = pymysql.connect(host=os.environ.get('DB_READ'),
                              user=os.environ.get('DB_USERNAME'),
                              password=os.environ.get('DB_PASSWORD'),
                              db=os.environ.get('DB_DATABASE'),
                              charset='utf8mb4')
        self.cur = self.con.cursor(pymysql.cursors.DictCursor)
      
    def test_select(self):
    sql = "SELECT * FROM TABLE_NAME"
    self.cur.execute(sql)

    list = self.cur.fetchall()

    for item in list:
        print(f"{item['id']} ::::: {item['name']}")
```

## pymysql
- 터미널 : `pip install pymysql`  && `impoert pymysql`

## connection
- os, dotenv를 통해 .env 파일에 존재하는 환경파일을 가져와서 DB 연결한다. 

## cursor
- cursor는 실제 DB 의 sql 구문을 실행(excute) 시키고 조회된 결과를 가져온다(fetchall).
- `pymysql.cursors.DictCursor` 옵션을 추가해야만 select 시에 컬럼 이름으로 조회가능
  - 옵션 X : `item[0]`으로 조회 
  - 옵션 있으면 : `item['id']`로 조회 가능 
