##### Object.keys() 
    作用, 返回一个数组, 里面包含对象最外层的 key 或者 字符串和数组的索引
    
    1. 传入对象
        返回对象第一层的所有key的数组
        var obj = {
            'a': 1,
            'b': [1, 2, 3],
            'c': {
                'c1': 1,
                'c2': 2
            },
            'd': 1
        };
        Object.keys(obj);   // ['a', 'b', 'c', 'd']
        
    2. 传入数组
        var arr = [
            'a', 
            ['b1', 'b2', 'b3'], 
            {
                'a': 1,
                'b': 2,
                'c': 3
            }, 
            'd'
        ];
        Object.keys(obj);   // ['0', '1', '2', '3'] 
    
    
    3. 传入字符串
        var str = 'abcdef';
        Object.keys(str);   // ['0', '1', '2', '3', '4', '5']