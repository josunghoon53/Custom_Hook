# Custom Hook 


본 자료는 노마드 코더 [실전형 리액트 Hooks 10개](https://nomadcoders.co/react-hooks-introduction) 강의를 참고하여 내가 자주쓰는 기능들을 

좀 더 효율적으로 사용하고자 해서 만들게 되었습니다.

> 리액트가 클래스형 컴포넌트에서 함수형으로 바뀌게 되면서 여러 변수의 상태관리와 생명주기 메서드 사용이 불가해지자 이를 해결하기 위해 hooks가 등장하게 되었다.
>
> 즉, hooks는 함수형 컴포넌트가 클래스형 컴포넌트의 기능을 사용할 수 있또록 해주는 기능이다.


&nbsp; 

### 1. useResize

```javascript

export const useResize = () =>{

    //초기값은 현재화면의 넓이와 높이로 지정해놓았다.
	const [state,setState] = useState({
		w : window.innerWidth,
		h : window.innerHeight
	});

	const resizeFuc = () =>{
		setState({
			w : window.innerWidth,
			h : window.innerHeight
		});
	}

	useEffect(()=>{
		window.addEventListener('resize',resizeFuc);
		return () => window.removeEventListener('resize',resizeFuc);
	},[])


	return state

}
```

&nbsp; 

### 2. useHover

```javascript
import { useEffect, useRef, useState } from "react"

export const useHover = (hoverFuc) =>{

  const [value, setValue] = useState(false);

  const element = useRef(null);

	//ref를 통해 dom 접근시 범위안쪽일때 true 바깥쪽은 false
  const handleMouseEnter = () => setValue(true);
  const handleMouseLeave = () => setValue(false);

	useEffect(()=>{

		const node = element.current;
		if (node) {
			node.addEventListener('mouseenter', handleMouseEnter);
			node.addEventListener('mouseleave', handleMouseLeave);

			return () => {
				node.removeEventListener('mouseenter', handleMouseEnter);
				node.removeEventListener('mouseleave', handleMouseLeave);
			};
		}

	},[element.current])

  
	return [element, value];

}

```


&nbsp; 
### 3. useScroll

```javascript
import { useEffect, useState } from "react"


export const useScroll = () =>{
	const [state,setState] = useState({
		x : 0,
		y : 0,
	})

	const scrollFuc = () =>{
		setState({
			x : window.scrollX,
			y : window.scrollY
		})
	}

	useEffect(()=>{
		window.addEventListener('scroll',scrollFuc);
		return ()=> window.removeEventListener('scroll',scrollFuc);
	},[])


	return state;
	
}
```

