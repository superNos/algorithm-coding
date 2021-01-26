#### JSON.stringify实现
注意点：
* `NaN`、`Infinity`直接返回`null`
* `function`、`symbol`、`undefined`变为`undefined`
* 如果复杂类型，并且有`toJSON`方法，转换`toJSON的返回值`


```javascript
function jsonStringify (data) {
    const type = typeof data
    if (type !== 'object') {
        if (Number.isNaN(data) || data === Infinity || data === -Infinity) {
            return 'null'
        }
        if (type === 'function' || type === 'symbol' || type === 'undefined') {
            return undefined
        }
        if (type === 'string') {
            return '"' + data + '"'
        }
        return String(data)
    } else {
        if (data === null) {
            return 'null'
        }
        if (data.toJSON && typeof data.toJSON === 'function') {
            return jsonStringify(data.toJSON())
        }
        if (data instanceof Array) {
            let result = []
            data.forEach((i, index) => {
                if (Number.isNaN(i) || typeof i === 'function' || typeof i === 'symbol') {
                    result[index] = 'null'
                } else {
                    result[index] = jsonStringify(i)
                }
            })
            result = '[' + result + ']'
            return result.replace(/'/g, '"')
        }
        let result = []
        Object.keys(data).forEach(key => {
            if (typeof key !== 'symbol') {
                if (typeof data[key] !== 'undefined' && typeof data[key] !== 'function' && typeof data[key] !== 'symbol') {
                    result.push('"'+key+'":'+jsonStringify(data[key]))
                }
            }
        })
        result = '{' + result + '}'
        return result.replace(/'/g, '"') 
    }
}
```