# React-Hooks
### 1. useState()
### 2. useEfect()
### 3. useRef()
### 4. useMemo()
### 5. useCallback()
### 6. useContext()
### 7. useReducer()
### 8. useLayoutEfect()
### 9. custom Hooks


## 1. useState()

UseState is a react hook, which creates an **"State Variable**". Which helpsus to track state in components & upates the user Interface when state changes.

useState hook gives output array.
in first index we use to store a initital vlue in a variable and second index is function that updates the initial value according to state change.

    const [name, setName]=useState(" ")

Here useState holds an empty string initially in the variable called name. setName is a function whenever changes.

We can use Object to store multiple states.

     const [car, setCar] = useState({
        brand: "Honda",
        color: "White",
        name: "Honda City",
        year: "2024",
      });
    
      const updateIt = () => {
        setCar((prev) => {
          return { ...prev, color: "black" };
        });
      };
    
    <h1>My car is {car.name}!</h1>
          <h2>
            It is {car.brand} brand, and {car.color} and it is {car.year} Model.
          </h2>
    <button onClick={updateIt}>Modify</button>

**Change the state based on previous state**

    const [count, setCount] = useState(0);
      const increaseCount = () => {
        setCount(count + 1); //1
        setCount(count + 1); //1
        setCount(count + 1); //1
        setCount(count + 1); //1
    
        // Here we are increasing counter by 4 times by using seCount function, 
        // but when we to tried to click on button, it will increase counter by nly one value.
      };
    
     <h1>Count is {count}</h1>
          <button onClick={increaseCount}>Increase</button>

**If we want to increse value by 4 times, then use arrow function inside setCount function,  inside increaseCount function.**


      const [count, setCount] = useState(0);
      const increaseCount = () => {
        setCount((count) => count + 1); //1
        setCount((count) => count + 1); //2
        setCount((count) => count + 1); //3
        setCount((count) => count + 1); //4
      };
    
      return (
        <div className="App">
          <h1>Count is: {count}</h1>
          <button onClick={increaseCount}>Increase</button>
        </div>
    )


## 2. useEffect()

The useEffect() hook allows you to perform side effects in your components. 

Some of the examples of side effects are:
- Fetching data from API
- Directly updating the DOM
- Timers like SetTimeOut and SetInterval()

      useEffect (callback)
      useEffect (()=>{}, [])
      useEffect(()=>{},[dependency1, dependency2, dependency3...])
  
- If there is no dependency in useEffect, every chages happens in the state, the useEffect callback function will execute.
- If there is an empty array in dependency array, then callback function will executes only once when component gets loaded.
- If we add any varibale in dependency array, then, callback function will executes when component gets loaded, and whenever the varibale's value changes.

      const [count, setCount] = useState(0)
      useEffect(()=>{
        setTimeout(()=>{
          setCount(count=>count+1)
        }, 2000);
      })
      return (
        <div >
          <h1>I have rendered {count} times!</h1>
        </div>
      )
In this code, there are no dependenices, so on every state (any state) change, it will re-render the code. Every 2 seconds state is changing. so it will calling again setTimeOut function, so it will goes till infinite.

- If we add an empty [] array in dependency, the function executes only once when the component gets loaded. (It increase the counter by once and stops the execution).
- If we add 'count' variable in dependency array [count] , function will executes whenever the value of count is changes. 


## 3. useRef()

useRef() is a react Hook that allow us to create mutable variables, which will not re-render the component.

Means, when we create a varibale using useRef, whenever the value changes, then component will not re-render.

useRef is also used for accessing/modifying DOM elements.

     const [value,setValue] = useState(0)
     const count = useRef(0)
      
      useEffect(()=>{
        count.current = count.current+1
      })
    
      return (
        <div >
          <button onClick ={()=>{setValue(prev=>prev-1)}}>-1</button>
          <h1>{value}</h1>
          <button onClick ={()=>{setValue(prev=>prev+1)}}>+1</button>
          <h1>Render is:{count.current}</h1>
        </div>
      )

We use useRef if we don't want to re-render the component, whenever the state is gets changed.

##### Accessing DOM Elements using useRef()

    function App() {
      const inputElemnet = useRef()
      
    const btnClick=()=>{
      // console.log(inputElemnet)
      // console.log(inputElemnet.current)
      inputElemnet.current.style.background= 'blue'
    }
    
      return (
        <div >
         <input type="text" ref={inputElemnet}></input>
         <button onClick = {btnClick}> Click</button>
        </div>
      )
    }

## 4. useMemo()

The react useMemo() hook returns a memoized value. (It's like caching a value so that it does't need to be re-calculated.)

The useMemo hook only runs when one of its dependencies gets updated. This can imporove the performance of the application. 

There is one more hook in react to improve performance, that is useCallback() hook.

The useMemo() and useCallback() hooks are similar. The main difference is:
  - useMemo() returns a memoized value value.
  - useCallack() returns a memoized function.

        function App() {
          const [number, setNumber] = useState(0)
          const [counter, setCounter] = useState(0)
          
          function cubeNum(num){
            console.log('calculation done!')
            return Math.pow(num,3)
          }
          
          const result = cubeNum(number)
        
          return (
            <div >
             <input type="number" value={number} onChange={(e)=>setNumber(e.target.value)} />
             <h1>Cube of Number is: {result}</h1>
             <button onClick ={()=>{setCounter(counter+1)}}>Counter++</button>
             <h1>Counter:{counter}</h1>
            </div>
          )
        }
In the above code, the function cubeNum() is executing on every re-render the component. To overcome with this, we use useMemo. 


        function App() {
          const [number, setNumber] = useState(0)
          const [counter, setCounter] = useState(0)
          
          function cubeNum(num){
            console.log('calculation done!')
            return Math.pow(num,3)
          }
          
          const result = useMemo(()=>cubeNum(number), [number])
        
          return (
            <div >
             <input type="number" value={number} onChange={(e)=>setNumber(e.target.value)} />
             <h1>Cube of Number is: {result}</h1>
             <button onClick ={()=>{setCounter(counter+1)}}>Counter++</button>
             <h1>Counter:{counter}</h1>
            </div>
          )
        }
cubeNum() function will executes only when the number gets changed. It will not executes on every re-render. The counter is re-rendering the component but not executing the function. by this type we can prevent function re-rendering and we can enhance the performance of application

## 5. useCallback()

useCallback() is a react hook that lets you cache a function defination between re-renders.

It means, when we use the useCallback hook, it doesn't create multiple instance of same function when re-render happens.

Instead of creating new instance of the function, it provides the cached function on re-render of the function.


**Create new Header compnent **

    const Header = ()=>{
      console.log("Header is rendered!")
      return (
        <>
          <h1>Header Component</h1>
        </>
        )
    }
    export default Header;

    //App.jsx file
    
    function App() {
      const [count, setCount] = useState(0)
    
      return (
        <div >
          <Header/>
          <h1 >Rendered {count} times!</h1>
          <button onClick ={()=>setCount(prev=>prev+1)}>
            Click Here</button>
        </div>
      )
    }
Whenever we click on  button, the Header component is also re-rendering. To overcome this,we use memo method in Header Component. (In export default Header line, we have to change it to --> **export default React.memo(Header)**).

Now, If we pass a function from App compooent as a child to Header componet, then again it will starts re-rendering on every click.

    function App() {
      const [count, setCount] = useState(0)
      const newFn = ()=>{}
      
      return (
        <div >
          <Header newFn = {newFn}/>
          <h1 >Rendered {count} times!</h1>
          <button onClick ={()=>setCount(prev=>prev+1)}>
            Click Here</button>
        </div>
      )
    }
This is bacause of **"Referential Equality".** When we re-render, a new instance will be created for newFn() (It will be created in new memory location.) and Hence We are passing new function to Header component (Props is changing) and It is re-rendering the component. 

**This issue is solved by using useCallback() Hook.**

pass the function with help of useCallback()

    const newFn = useCallback(()=>{},[])

If we pass dependency, and parameter as count, the function gets executed on every count change, and new function is passed to header. then header will re-render on every count change.

    function App() {
      const [count, setCount] = useState(0)
      const newFn = useCallback((count)=>{},[count])
      
      return (
        <div >
          <Header newFn = {newFn}/>
          <h1 >Rendered {count} times!</h1>
          <button onClick ={()=>setCount(prev=>prev+1)}>
            Click Here</button>
        </div>
      )
    }

    //Header Component
    const Header = ()=>{
      console.log("Header is rendered!")
      return (
        <>
          <h1>Header Component</h1>
        </>
        )
    }
    export default React.memo(Header);

If we remove dependency, It will not reacte new function, and uses cached fucntion and prevents re-rendering.

## 6.useContext()

useConext() is a react hook that allows you access data from any component without explicitly passing it down through props at every level.

useContext() is used to manage Global data in the React App.

- Creating Context
- Providing the Context
- Consuming the Conext

**Creating the context** 

    import {useContext} from 'react'
    
      export const AppContext = useContext();
      
      const contextProvider = (props)=>{
        
        const contact_num = +91 8974562310
        
        return(
          <AppContext.Provider value = {contact_num}>
            {props.children}
          </AppContext.Provider>
          )
      }
      export default contextProvider

Now wrap the App component with context provider in **main.jsx** file

    import ContextProvider from './context/AppContext.jsx'
    <ContextProvider>
        <App/>
    </ContextProvider>

Now, all the data which is present in AppContext will be accessed by any of the Component easily.  

Consuming the Context:
