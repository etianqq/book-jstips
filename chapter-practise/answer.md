1. react hooks

```
// 第一种:
function statusHandleChange(val) {
        setModelStatus(val);
        // 直接把参数的值 传进去 拿到的就是最新的了
        search(val);
    }

function search(value) {
    
	console.log(value);  
	props.callApi(value);
}
// 第二种:
const [modelStatus, setModelStatus] =useState("");
const modelStatusRef = useRef(null);

useEffect(()=>{
	// 每次 更新 把值 复制给 modelStatusRef
	modelStatusRef.current = modelStatus;
}, [modelStatus]); // 依赖的值 等modelStatus 改变了 才出发里面的值

function statusHandleChange(val) {
        setModelStatus(val);
        
        // **设置一个延迟 0毫秒,这个 很重要**
        setTimeout(search, 0);
    }

function search(value) {
	// 这里的值 就是 拿到最新的值了
    let _modelStatus = modelStatusRef .current;
	console.log(_modelStatus );  
	props.callApi(_modelStatus );
}
// 第三种方法: (其实第三种方法跟第二种方法差别不大)
useEffect(()=>{
           setModelStatus(modelStatus);
},[modelStatus]);
```