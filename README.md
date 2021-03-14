# reduce() trong JavaScript

## 1.  Tìm phần tử khác nhau giữa 2 array
```
    const diffItem = (arr = [], otherArr = []) =>
    arr.reduce((t, v) => (!otherArr.includes(v) && t.push(v), t), []);

    const a = [1, 2, 3, 4, 5];
    const b = [2, 3, 6];

    console.log(diffItem(a, b)); // > Array [1, 4, 5]
```
## 2. Chia nhỏ array
```
    const chunkArr = (arr = [], size = 1) => {
    return arr.length
        ? arr.reduce((t, v) => (
            t[t.length - 1].length === size
            ? t.push([v])
            : t[t.length - 1].push(v), t)
        , [[]])
        : [];
    }

    const a = [1, 2, 3, 4, 5];

    console.log(chunkArr(a, 2)); // > Array [[1, 2], [3, 4], [5]]
```
## 3. Ngược lại với thằng thứ 2
```
    const flatArr = (arr = []) => 
        arr.reduce((t, v) => t.concat(Array.isArray(v) ? flatArr(v) : v), [])

    const a = [0, 1, [2, 3], [4, 5, [6, 7]], [8, [9, 10, [11, 12]]]];

    console.log(flatArr(a));
    // > Array [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
```
## 4. Đếm số lượng phần tử giống nhau trong Array
```
    const Count = (arr = []) => arr.reduce((t, v) => (t[v] = (t[v] || 0) + 1, t), {});

    const arr = [0, 1, 1, 2, 2, 2, 7, 4, 4, 3, 1];
    console.log(Count(arr)); // > Object { 0: 1, 1: 3, 2: 3, 3: 1, 4: 2, 7: 1 }
```
## 5. Convert object sang params url
```
    const StringifyUrlSearch = (search = {}) =>
        Object.entries(search).reduce(
            (t, v) => `${t}${v[0]}=${encodeURIComponent(v[1])}&`,
            Object.keys(search).length ? "?" : ""
        ).replace(/&$/, "");

    const obj = { age: 30, name: "John" };
    console.log(StringifyUrlSearch(obj)) // > "?age=30&name=John"
```
## 6. Ngược lại với 5
```
    const ParseUrlSearch = (url = location.search) =>
        url.replace(/(^\?)|(&$)/g, "").split("&").reduce((t, v) => {
            const [key, val] = v.split("=");
            t[key] = decodeURIComponent(val);
            return t;
        }, {});

    console.log(ParseUrlSearch('?rlz=1C1GCEA&sclient=psy-ab'));
    // > Object { rlz: "1C1GCEA", sclient: "psy-ab" }
```
## 7. Tìm kiếm từ khóa trong array
```
    const Keyword = (arr = [], keys = []) =>
        keys.reduce((t, v) => (arr.some(w => w.includes(v)) && t.push(v), t), []);

    const arr = [
    "google facebook is big company",
    "google.com",
    "Search the world's information, including webpages, images, videos and more",
    ];
    const keyword = ["javascript", "google", 'words', "lazada", "facebook"];

    console.log(Keyword(arr, keyword)); // > Array ["google", "facebook"]
```
## 8. Tách phần tử trong Array theo đúng type of
```
    const Unzip = (arr = []) =>
        arr.reduce(
            (t, v) => (v.forEach((w, i) => t[i].push(w)), t),
            Array.from({
            length: Math.max(...arr.map(v => v.length))
            }).map(v => [])
        );

    const arr = [["a", 1, true], ["b", 2, false]];
    console.log(Unzip(arr)); // > Array [Array ["a", "b"], Array [1, 2], Array [true, false]]
```