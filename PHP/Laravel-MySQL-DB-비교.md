# MySQL 두개의 DB에서 존재하지 않는 컬럼 획득

```
/**
 * @test 
 * @testdox 두개의 디비에서 존재하지 않는 컬럼을 확인한다.
 * @return void
 */
public function testCompareDBColumns(): void
{
    $checkFreeTables = []; 
    $tables = DB::select('SHOW TABLES');
    
    foreach ($tables as $table) {
        $name = $table->#key_name#;
        if (in_array($name,
            $checkFreeTables
        )) {
            continue;
        }
        $liveColumns = Schema::setConnection(DB::connection('mysql_live'))->getColumnListing($name);
        $preColumns = Schema::setConnection(DB::connection('mysql'))->getColumnListing($name);

        $diffs = array_diff($preColumns, $liveColumns);
        $diffs2 = array_diff($liveColumns, $preColumns);
        
        if (count($diffs) > 0) {
            print_r($name);
            print_r($diffs);
        } else if(count($diffs2) > 0) {
            print_r($name);
            print_r($diffs);
        }
    }
}
```

## `getColumnListing(테이블명)`
- 테이블의 컬럼 리스트를 배열로 반환한다. 
