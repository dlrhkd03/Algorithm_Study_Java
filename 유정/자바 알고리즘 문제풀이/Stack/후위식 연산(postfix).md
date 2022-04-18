# 후위식 연산(postfix)



**설명**

후위연산식이 주어지면 연산한 결과를 출력하는 프로그램을 작성하세요.

만약 3*(5+2)-9 을 후위연산식으로 표현하면 352+*9- 로 표현되며 그 결과는 12입니다.

 

**입력**

첫 줄에 후위연산식이 주어집니다. 연산식의 길이는 50을 넘지 않습니다.

식은 1~9의 숫자와 +, -, *, / 연산자로만 이루어진다.

 

**출력**

연산한 결과를 출력합니다.

 

예시 입력 1

```
352+*9-
```

예시 출력 1

```
12
```



### 성공 코드

```
import java.util.*;

public class Main {
	public int solution(String str) {
		int answer = 0;
		Stack<Integer> stack = new Stack<>();
		int lt = 0;
		int rt = 0;
		for(char c : str.toCharArray()) {
			// 현재 c는 char형 -> c-48해야 (아스키코드가 아닌) 숫자가 들어감
			if(Character.isDigit(c)) stack.push(c-48);
			else {
				// 연산자 만나면 2개 rt,lt 순서로 pop
				rt = stack.pop();
				lt = stack.pop();
				// lt 연산 rt한 것 stack에 push
				if(c == '+') stack.push(lt+rt);
				else if(c == '-') stack.push(lt-rt);
				else if(c == '*') stack.push(lt*rt);
				else if(c == '/') stack.push(lt/rt);
			}
		}
		// 다 끝났으면 stack.get(0)을 return
		answer = stack.get(0);
		return answer;
	}

	public static void main(String[] args) {
		Main T = new Main();
		Scanner kb = new Scanner(System.in);
		String str = kb.next();
		System.out.println(T.solution(str));
	}

}
```



**문제 해설**

[Notion]: https://lealea.tistory.com/5?category=1008807

