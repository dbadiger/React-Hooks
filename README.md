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

## 3. useRef()

useRef() is a react Hook that allow us to create mutable variables, which will not re-render the component.

## 4. useMemo()

The react useMemo() hook returns a memoized value. (It's like caching a value so that it does't need to be re-calculated.)

The useMemo hook only runs when one of its dependencies gets updated. This can imporove the performance of the application. 

There is one more hook in react to improve performance, that is useCallback() hook.

The useMemo() and useCallback() hooks are similar. The main difference is:
  - useMemo() returns a memoized value value.
  - useCallack() returns a memoized function. 
