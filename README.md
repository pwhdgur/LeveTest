# LevelTest
Level 1 1번~10번

1. 2016년 a월 b일은 무슨 요일일까요?라는 문제
	
	1.1
	function solution(a, b) {
	  return ['SUN', 'MON', 'TUE', 'WED', 'THU', 'FRI', 'SAT'][new Date(2016, a - 1, b).getDay()];
	}

	1.2
	var week = ['일', '월', '화', '수', '목', '금', '토'];
	var dayOfWeek = week[new Date('2016-07-28').getDay()];
	console.log(week);
	console.log(dayOfWeek);
	return dayOfWeek;

2. 가운데 글자 가져오기 : abcde에서는 c를 가져오고 qwer에서는 we 두 글자를 가져오는 문제
	
	2.1
	function solution(s) {
	  return s.substr(Math.ceil(s.length / 2) - 1, s.length % 2 === 0 ? 2 : 1);
	}

	2.2
	function solution(s) {
	    var answer = '';
	    if(s.length % 2 ===0){
		answer = answer.concat(s[s.length/2 -1]);
		answer = answer.concat(s[s.length/2]);
	    }else{
		answer = answer.concat(s[Math.floor(s.length/2)]);
	    }
	    return answer;
	}

3. 같은 숫자는 싫어 : [1,1,3,3,0,1,1]이면 [1,3,0,1]로 연속되는 중복을 제거하는 문제

	3.1
	function solution(arr) {
	  return arr.filter((v, i) => v !== arr[i + 1]);
	}

4. 나누어 떨어지는 숫자 배열 : [5,9,7,10]과 5가 주어지면 [5, 10]을 리턴해야 합니다. 아무것도 없으면 [-1]을 리턴

	4.1
	function solution(arr, divisor) {
	  const answer = arr.filter(el => el % divisor === 0);
	  return answer.length ? answer.sort((p, c) => p - c) : [-1];
	}

	4.2
	const solution = (arr, divisor) => {
	    var answer = [];
	    answer = arr.filter((arrList) => arrList%divisor === 0);
	    if(answer.length == 0) {
		return [-1];
	    } else {
		return answer.sort((a, b) => a - b);	//작은 숫자순서, b-a 경우 큰숫자순서
	    }
	}

5. 두 정수 사이의 합 : 3과 5가 주어지면 3+4+5를 해서 리턴

	5.1
	function solution(a, b) {
	  a > b && ([a, b] = [b, a]);
	  return Array(b - a + 1).fill().map((v, i) => a + i).reduce((a, c) => a + c);
	}

	5.2
	function solution(a, b) {
	    var answer = 0;
	    var small, big;
	    if(a > b){
		big = a;
		small = b;
	    }else if(b > a){
		big = b;
		small = a;
	    }else{
		answer = a;
	    } 
	    for(var i =small ; i <= big ; i++){
		answer +=i;
	    }
	    return answer;
	}

6. 문자열 내 마음대로 정렬하기 : ['abce', 'abcd', 'cdx']와 2가 주어지면 2번째 인덱스 글자(c, c, x)를 기준으로 정렬합니다. 만약 2번째 인덱스 글자가 서로 같다면(c, c처럼) 사전순으로 정렬합니다. abce와 abcd를 사전순으로 정렬하는 것이죠.

	6.1
	function solution(strings, n) {
	  return strings.sort((p, c) => p[n] === c[n] ? p.localeCompare(c) : p[n].localeCompare(c[n]))
	}

	6.2 문자열로 구성된 리스트 strings와, 정수 n이 주어졌을 때, 각 문자열의 인덱스 n번째 글자를 기준으로 오름차순 정렬하려 합니다. 
	예를 들어 strings가 [sun, bed, car]이고 n이 1이면 각 단어의 인덱스 1의 문자 u, e, a로 strings를 정렬합니다.
	
	function solution(strings, n) {
	    strings.sort(function(a,b){
		var first = a[n];
		var second = b[n];
		if(first === second){
		    return (a > b) - (a < b);
		}else{
		    return (first > second) - (first < second);
		}
	    })
	    return strings;
	}

7. 문자열 내 p와 y의 개수 
대문자와 소문자가 섞여있는 문자열 s가 주어집니다. s에 ‘p’의 개수와 ‘y’의 개수를 비교해 같으면 True, 다르면 False를 return 하는 solution를 완성하세요. 
‘p’, ‘y’ 모두 하나도 없는 경우는 항상 True를 리턴합니다. 단, 개수를 비교할 때 대문자와 소문자는 구별하지 않습니다.

	7.1
	function solution(s){
	    let strArr = s.toUpperCase().split('');
	    if(!strArr.includes('P') && !strArr.includes('Y')){
		return true;
	    }
	    let count1 =0;
	    let count2 =0;
	    for(let i=0; i<strArr.length; i++){
		if(strArr[i] === 'P'){
		    count1++;
		}else if(strArr[i]==='Y'){
		    count2++;
		}
	    }
	    if(count1 === count2){
		return true;
	    }else{
		return false;
	    }
	}

	7.2
	function numPY(s){
	  return s.toUpperCase().split("P").length ===  s.toUpperCase().split("Y").length;
	}

8. 문자열 내림차순으로 배치하기 
문자열을 역순으로 정렬합니다. 대문자는 소문자보다 뒤에 위치해야 합니다. 예를 들어 Zbcdefg는 gfedcbZ가 됩니다.

	8.1
	function solution(s) {
	// 1. 문자열을 배열로 쪼갠다.
	// 2. sort메소드로 순차적으로 나열해준다. 
	// 3. reverse메소드로 반전시켜준다. (역순 나열)
	// 4. join메소드로 문자열로 바꿔줘서 반환한다.
	    return s.split('').sort().reverse().join('');
	}

9. 문자열 다루기 기본
문자열의 길이가 4 또는 6이고 숫자로만 구성되어 있는지 확인합니다.
예를들어 s 가 a234 이면 False 를 리턴하고 1234 라면 True 를 리턴하면 됩니다.

	9.1
	function alpha_string46(s) {
	  return s.length == 4 || s.length == 6 ? !isNaN(s) : false;
	}

10. 서울에서 김서방 찾기 
['Jane', 'Kim']이란 배열이 있으면 Kim의 위치를 찾으면 됩니다.

	10.1
	function findKim(seoul){
	  var idx = seoul.indexOf('Kim');

	  // indexOf 메소드는 배열 내의 요소의 최초의 인덱스를 반환

	  return "김서방은 " + idx + "에 있다";
	}

11. 소수 찾기 
1~n 사이의 소수의 개수를 반환

	11.1
	function solution(n) {

		let results = [];

		// 1과 n 사이의 숫자 중에 소수를 구하기 우ㅟ한 반복문
		for (let i=1; i <= n ; i++) {
			let isPrimeNumber = true;

			for (let j=2; j < i; j++) {
				if(i % j === 0) {
				 isPrimeNumber = false;
				}
			}
			if(isPrimeNumber) {
				results.push(i);
			}
		}

		return results;
	}

12. 수박수박수박수박수 
3이면 수박수, 4면 수박수박, 5면 수박수박수를 리턴하면 됩니다.

	12.1
	function solution(n) {
	  return '수박'.repeat(n).substr(0, n);
	}

13. 문자열을 정수로 바꾸기
	function solution(s) {
	  return parseInt(s);
	}

14. 시저 암호 
문자열 "s"와 거리 n을 입력받아 "s"를 n만큼 민 암호문을 만드는 함수, solution을 완성해 보세요.
(AB는 1만큼 밀면 BC가 되고, AB를 3만큼 밀면 DE가 됩니다. z는 1만큼 밀면 a가 됩니다. 공백은 그대로 공백이고요.)

	14.1
	function solution(s, n) {
	    let result = ""; 
	    for (let i=0; i<s.length;i++) { 
		if ( s[i] == ' ' ) 
		    result += ' ' 
		else 
		    result += String.fromCharCode( (s.charCodeAt(i)>90)
			    ? (s.charCodeAt(i)+n-97)%26+97 
			    : (s.charCodeAt(i)+n-65)%26+65 ) 
	    } 
	    return result;
	}

15. 약수의 합
자연수 n을 입력받아 n의 약수를 모두 더한 값을 리턴하는 함수
(12의 약수는 1, 2, 3, 4, 6, 12입니다. 이를 모두 더하면 28입니다.)

	15.1
	function solution(n) {
	    let answer = 0;
	    for (let i = 0; i <= n; i++) {
		if( n % i === 0) { answer += i}
	    }
	    return answer
	}

16. 이상한 문자 만들기 
단어의 짝수번째 문자는 대문자로, 홀수번째 문자는 소문자로 바꿉니다. try hello world는 TrY HeLlO WoRlD가 되네요.

	16.1
	function solution(s) {
	  return s.split(' ').map(w => (
	    w.split('').map((v, i) => (i % 2 ? v.toLowerCase() : v.toUpperCase())).join('')
	  )).join(' ');
	}

17. 자릿수 더하기 
자연수 N이 주어지면, N의 각 자릿수의 합을 구해서 return 하는 solution 함수를 만들기
(예를들어 N = 123이면 1 + 2 + 3 = 6을 return 하면 됩니다.)

	17.1
	function solution(n)
	{
	    var answer = 0;
	    var m=String(n);
	​
	    for(var i=0; i<m.length; i++){
		answer+=parseInt(m[i]);
	    }
	    return answer;
	}

18. 자연수 뒤집어 배열로 만들기
12345를 뒤집어 [5,4,3,2,1]로 만들면 됩니다. 

	18.1
	function solution(n) {
	    return n.toString().split('').reverse().map(o => o = parseInt(o));
	}

19. 정수 내림차순으로 배치하기
118372면 내림차순으로 873211을 리턴하면 됩니다.

	19.1
	function solution(n) {
	  // p - c : 오름차순
	  return +String(n).split('').sort((p, c) => c - p).join('');
	}

20. 정수 제곱근 판별
n이 정수 x의 제곱이라면 x+1의 제곱을 리턴하고, 아니라면 -1을 리턴합니다.
설명 : 임의의 정수 n에 대해, n이 어떤 정수 x의 제곱인지 아닌지 판단하려 합니다. n이 정수 x의 제곱이라면 x+1의 제곱을 리턴하고, n이 정수 x의 제곱이 아니라면 -1을 리턴하는 함수
(121은 정수 11의 제곱이므로, (11+1)를 제곱한 144를 리턴, 3은 정수의 제곱이 아니므로, -1을 리턴)

	20.1
	function solution(n) {
	    return (Number.isInteger(Math.sqrt(n))) ? Math.pow((Math.sqrt(n)+1), 2) : -1;
	}

21. 제일 작은 수 제거하기 
arr 에서 가장 작은 수를 제거한 배열을 리턴하는 함수
예를들어 arr이 [4,3,2,1]인 경우는 [4,3,2]를 리턴 하고, [10]면 [-1]을 리턴

	21.1
	function solution(arr) {
	    var answer = [];
	    if(arr.length <= 1){
	       answer[0] = -1;
	    }
	    else{
		arr.splice(arr.indexOf(Math.min.apply(null, arr)),1);

			//arr.splice(arr.indexOf(Math.min(...arr)),1);

		answer = arr;
	    }
	    return answer;
	}

22. 짝수와 홀수

	22.1
	function solution(num) {
	  return num % 2 == 0 ? 'Even' : 'Odd';
	}


23. 최대공약수와 최소공배수
두 수를 입력받아 두 수의 최대공약수와 최소공배수를 반환하는 함수
	23.1
	function solution(n, m) { 
		let gcd = getGCD(n, m) 
		let lcm = m * n / gcd return [gcd, lcm] 
	} 
	function getGCD(a, b){ 
		return a%b ? getGCD(b, a%b) : b 
	}

	23.2
	function solution(n, m) {
	  function u(n, m) { return m % n ? u(m % n, n) : n; }
	  const gcd = u(n, m);
	  return [gcd, n * m / gcd];
	}


24. 콜라츠 추측 
주어진 수가 1이 될때까지 다음 작업을 반복하면, 모든 수를 1로 만들 수 있다는 추측입니다. 작업은 다음과 같습니다.
1-1. 입력된 수가 짝수라면 2로 나눕니다. 
1-2. 입력된 수가 홀수라면 3을 곱하고 1을 더합니다.
2. 결과로 나온 수에 같은 작업을 1이 될 때까지 반복합니다.
예) 입력된 수가 6이라면 6→3→10→5→16→8→4→2→1 이 되어 총 8번 만에 1이 됩니다. 위 작업을 몇 번이나 반복해야하는지 반환하는 함수

	24.1
	function solution(num, count = 0) {
	    return count === 500 
		? -1 
		: num === 1
		    ? count
		    : solution(num % 2 ? num * 3 + 1 : num / 2, count + 1);
	}

25. 평균 구하기
정수를 담고 있는 배열 arr의 평균값을 return하는 함수

	25.1
	function solution(arr) {
	    var answer = 0;
	    for(var i=0; i<arr.length; i++){
		answer += arr[i];
	    }
	    return answer/arr.length;
	}

	25.2
	function solution(arr) {
	    return arr.reduce((a, b) => a + b) / arr.length;
	}

26. 하샤드 수
x의 자릿수의 합으로 x가 나눠 떨어지면 x는 하샤드 수입니다. 
예) 18의 자리수의 합은 1 + 8 = 9이고, 18은 9로 나눠 떨어지므로 18은 하샤드 수인거죠.
일단 자릿수를 쪼개서 더하는 것부터 합시다. split과 reduce면 되죠.

	26.1
	function solution(x) {
	    var answer = true;    
	    var n = String(x).split('').reduce((a, b) => Number(a) + Number(b));

	    answer = x % n == 0 ? true : false;

	    return answer;
	}

27. 핸드폰 번호 가리기
전화번호 뒷 4자리를 빼고 나머지를 전부 *로 바꾸는 문제입니다.
뒷 네자리를 떼내고 앞은 다 *로 바꾼 뒤 다시 붙이면됨

	27.1
	function solution(phone_number) {
	    return '*'.repeat(phone_number.length - 4) + phone_number.slice(-4);
	}

28. 행렬의 덧셈
[[1,2],[2,3]]과 [[3,4],[5,6]]이 있으면 [[4,6],[7,9]]가 됩니다. 끼리끼리 더하면 됩니다.

	28.1
	cosnt solution = (arr1, arr2) => {
	  return arr1.map((arr, i) => arr.map((v, j) => v + arr2[i][j]))
	}

29. x만큼 간격이 있는 n개의 숫자 
x의 배수를 n개 나열하면 됩니다. 2와 5면 [2,4,6,8,10]이고 -4와 2면 [-4,-8]입니다.

	29.1
	function solution(x, n) {
	    return Array(n).fill(x).map((v, i) => (i + 1) * v)
	}

30. 직사각형 별찍기
5와 3이 주어지면 5열3행의 별을 찍으면 됩니다.

	30.1
	function solution(a, b) {
	  return Array(b).fill().map(() => '*'.repeat(a)).join('\n');
	}

< Level 2 >

1. 124 나라의 숫자
1,2,4만으로 숫자를 표현합니다. 변형된 3진법입니다. 1, 2, 4, 11, 12, 14, 21, 22, 24, 41, 42, 44, 111 이런 순으로 숫자가 커집니다.
규칙만 찾으면 쉽습니다(반대로 규칙을 못 찾으면 어렵습니다). 3 대신 4가 있는 게 좀 까다롭습니다. 규칙은 3으로 나눴을 때 나머지를 보시면 됩니다.

	1.1
	function solution(n) {
		return n ? solution((n - (n % 3 || 3)) / 3) + (n % 3 || 4): '';
	}

2. 가장 큰 정사각형 찾기


3. 올바른 괄호
괄호 (와 )가 올바르게 짝지어져 있으면 true를 리턴합니다. ()()와 (())()는 올바른 괄호고, )()(나 (()(는 올바르지 않습니다.
스택을 흉내내서 (면 넣고 )면 빼면 될 것 같습니다. 최종 개수가 0이면 모두 짝지어진 것이라 올바른 괄호입니다. 단 스택을 직접 구현할 필요는 없습니다.

	3.1
	function solution(s){
		let count = 0;
		for (let i = 0; i < s.length; i++) {
			s[i] === '(' ? count++ : count--;
			if (count < 0) return false;
		}
		if (count !== 0) return false;
		return true;
	}


4. 다음 큰 숫자
n보다 크면서 이진수로 변환했을 때 n의 이진수와 1의 개수가 같은 숫자를 찾습니다. 78(1001110)의 다음 숫자는 83(1010011)입니다.
이진법 1의 개수를 세고, n에서부터 1씩 올리면서 이진법 1의 개수가 같은지 비교하면 됩니다.

	4.1
	function solution(n) {
		const bin = n.toString(2).match(/1/g).length;
		while (n++) {
			if (n.toString(2).match(/1/g).length === bin) return n;
		}
	}

5. 땅따먹기
1 2 3 5
5 6 7 8
4 3 2 1
위와 같은 땅이 있다면 위에서부터 5, 7, 4를 밟으면 점수가 최대가 됩니다(5를 골랐으면 바로 아래 8은 고르지 못합니다)
알고리즘 문제는 크게 두 가지로 나눌 수 있는데요. 하나는 공식이나 규칙을 찾아서 쉽게 푸는 문제, 다른 하나는 모든 경우의 수를 구해서 푸는 문제. 
이건 후자입니다. 아까 가장 큰 정사각형 찾기도 후자였습니다. 
윗줄에서부터 한줄씩 내려와 누적 최대 점수를 구하면 쉽습니다(바로 아랫줄로 못 가는 규칙은 적용하셔야 합니다).

1 2 3 5
9 10 11 12
12 14 15 16
이런 식이 됩니다. 예를 들어 첫줄 5를 골랐다면 다음 줄까지의 누적 최대합은 12입니다(8을 못 고르므로 5 + 7) 
그리고 12까지 왔다면 그 다음줄의 누적 최대합은 16(12 + 4)가 되고요. 이렇게 최대인 15를 골라내면 됩니다.

	5.1
	function solution(land) {
		return Math.max(...land.reduce((a, c, i) => {
			return [
				c[0] + Math.max(a[1], a[2], a[3]),  
				c[1] + Math.max(a[0], a[2], a[3]),
				c[2] + Math.max(a[0], a[1], a[3]),
				c[3] + Math.max(a[0], a[1], a[2]),
			];
		}, [0, 0, 0, 0]));
	}


6. 숫자의 표현
자연수 n을 연속한 자연수의 합으로 표현하는 가짓수를 묻습니다. 예로 15는 1 + 2 + 3 + 4 + 5, 4 + 5 + 6, 7 + 8, 15까지 네 가지입니다.
연속된 숫자의 개수에 주목해주세요. 5, 3, 2, 1개입니다. 2는 15랑 매핑하면 됩니다. 6의 경우는 1 + 2 + 3, 6 이렇게 두 가지로 나타낼 수 있는데, 
개수를 세보면 3과 1입니다. 홀수인 약수의 개수랑 일치하죠? 다른 숫자들도 해보세요.

	6.1
	function solution(n) {
		return Array(n).fill().map((v, i) => i + 1).filter(v => (!(n % v) && v % 2) ).length;
	}

7. 최댓값과 최솟값
문자열에서 최댓값과 최솟값을 찾으면 됩니다. "1 2 3 4"면 1과 4죠.
문자열을 배열로 만들어서 최댓값, 최솟값 찾는 메서드를 쓰면 되겠습니다.

	7.1
	function solution(s) {
		const o = s.split(' ').map(v => +v);
		return [Math.min(...o), Math.max(...o)].join(' ');
	}

8. 최솟값 만들기
[1, 4, 2], [5, 4, 4]가 주어진다면 각 배열에서 두 수 씩 뽑아 곱한 후, 그것들은 더한 값이 최소가 되도록 하는 문제입니다. 
1 * 5 + 4 * 4, + 2 * 4면 29가 최소가 됩니다.
첫 번째 배열은 오름차순으로, 두 번째 배열은 내림차순으로 정렬한 후 곱하고 더해나가면 됩니다.
[1, 2, 4] * [5, 4, 4] 이렇게 하면 되는 것이죠.

	8.1
	function solution(A,B){
		const b = B.sort((p, c) => c - p);
		return A.sort((p, c) => p - c).map((v, i) => v * b[i]).reduce((a, c) => a + c, 0)
	}

9. 피보나치 수
n번째 피보나치 수를 구합니다. 재귀적(탑다운)으로 할 수도 있고, 그냥 저처럼 바텀업 방식으로 할 수도 있습니다. 
1234567은 이걸로 나눈 결괏값을 리턴하라고 해서 넣어준 것입니다.

	9.1
	function solution(n) {
		const arr = [0, 1];
		for (let i = 1; i <= n; i++) {
			arr.push((arr[i - 1] + arr[i]) % 1234567);
		}   
		return arr[n];
	}

10. 행렬의 곱셈 
[1, 4], [3, 2], [4,1]]과 [[3,3],[3,3]]이 주어지면 [[15,15],[15,15],[15,15]]가 반환되면 됩니다. 
행렬의 곱셈은 수학적인 지식이므로 여기서는 더 자세하게 설명하지 않습니다.
첫 행렬의 열의 개수와, 두 번째 행렬의 행의 개수가 일치해야 하는 성질이 있죠. 
그러면 결과물 행렬은 첫 행렬의 행의 개수 X 두 번째 행렬의 열의 개수가 됩니다. 
결과물 행렬의 모양을 생각해서 내용물을 만들면 됩니다.

	10.1
	function solution(arr1, arr2) {
		return Array(arr1.length).fill().map((r, i) => Array(arr2[0].length).fill().map((v, j) => arr1[i].reduce((a, c, k) => a + c * arr2[k][j], 0)))
	}

11. JadenCase 문자열 만들기 
단어의 첫 문자가 대문자이고, 나머지는 소문자인 문자열로 바꿉니다. 3people unFollowed me는 3people Unfollowed Me가 됩니다.
단어별로 쪼개서 첫 글자만 대문자로, 나머지는 소문자로, 설명 그대로 바꿔주면 됩니다. 참 쉽죠?

	11.1
	function solution(s) {
		return s.split(' ').map(v => { 
			return v.split('').map((a, i) => i ? a.toLowerCase() : a.toUpperCase()).join('');
		}).join(' ');
	}

12. N개의 최소공배수 
여러 숫자 배열의 최소공배수를 구합니다. [2, 6, 8, 14]면 168입니다.
두 수의 곱은 최소공배수와 최대공약수의 곱과 같다는 성질과, 최대공약수는 유클리드 호제법으로 구할 수 있다는 성질을 이용해서, 
두 수씩 최소공배수를 구해나가면 됩니다.

	12.1
	function solution(arr) {
		return arr.reduce((a, c) => {
			function u(n, m) { return m % n ? u(m % n, n) : n; }
			return a * c / u(a, c);
		}, 1);
	}



