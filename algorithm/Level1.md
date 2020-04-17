###Level 1 알고리즘 함수 정리

####1. split 메소드
> String 객체를 지정한 구분자를 이용하여 여러개의 문자열로 나눈다

```js
const str = 'The quick brown fox jumps over the lazy dog';
const chars = str.split('');

console.log(chars[8]); // 8번째 문자열인 'k' 출력
```

####2. filter() 메소드
> 주어진 함수의 테스트를 통과하는 모든 요소를 모아 새로운 배열로 반환

```js
const words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];
const result = words.filter(word => word.length > 6);

console.log(result); // 문자열이 6보다 큰 'exuberant', 'destruction', 'present' 출력
```

####3. includes() 메소드
> 배열이 특정 요소를 포함하고 있는지 판별

```js
const array1 = [1, 2, 3];

console.log(array1.includes(2)); // array1 배열안에 2를 포함하고 있으니 true 출력
```
```js
const pets = ['cat', 'dog', 'bat'];

console.log(pets.includes('cat')); // pets 배열안에 'cat'을 포함하고 있으니 true 출력
console.log(pets.includes('at')); // 'at'은 없으니 false 출력 
```

####4. sort() 메소드
> 배열의 요소를 적절한 위치에 정렬한 후 그 배열을 반환
>
> 기본 정렬 순서는 문자열의 유니코드 코드포인트를 따른다
```js
const months = ['Mar', 'Jan', 'Feb', 'Dec'];
months.sort();

console.log(months); // ['Dec', 'Feb', 'Jan', 'Mar'] 가 출력
```
```js
const array1 = [1, 30, 4, 21, 100000];
array1.sort();

console.log(array1); // [1, 100000, 21, 30, 4] 가 출력
```

####5. reverse() 메소드
> 배열의 순서를 반전하여 반환
```js
const array1 = ['one', 'two', 'three'];
const reversed = array1.reverse();

console.log('reversed: ', reversed); // reversed: ['three', 'two', 'one'] 가 출력
```

####6. join() 메소드
> 배열의 모든 요소를 연결해 하나의 문자열로 만든다
```js
const elements = ['Fire', 'Air', 'Water'];

console.log(elements.join()); // 'Fire,Air,Water' 가 출력
```