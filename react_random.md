# React Random
## Default constructors
- Note that using a constructor is optional, and you can initialize your state like so if your Babel setup has support for class fields:
- You may still need a constructor, though, if you need to use a ref. 

## Hooks  
- Helps you be able to use functional components for nearly everything.
- Avoiding the ‘this’ confusion. 
- Uses the same react concepts (state and props).
- Tends to make React easier to understand and less likely to make mistakes. 
- Helps you share logic between components.  
- 3 most commonly used hooks: * useState (local state) * useEffect (side effects) This can be thought of as the. componentDidMount + componentDidUpdate + componentWillUnmount It accepts a function as a call. * useContext (access data in context)

Example of array destructuring: 
```
const [email, setEmail] = useState(“”)
//useState returns an array, the first element is the piece of state. The second element is the setter.
```
### Rules of Hooks. 
- You can **only** call in hooks from react function components or your own custom hook.
- Hooks must be declared at the top level (put the condition inside the hook). Because React tracks the order of your hooks.
- Render() is implied in a functional component.
- Remember to declare the dependency array [] as the second argument for useEffect() (where we tell useEffect when it should re-run!), otherwise it will rerun continuously. 
