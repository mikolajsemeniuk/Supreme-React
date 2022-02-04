# Components
* Function components

## Function components
in `src/components/child.tsx`
```tsx
const ChildComponent = () => {
    return (
        <div className="">
            child component here
        </div>
    )
}

export default ChildComponent
```
in `src/App.tsx`
```tsx
import './App.css';
import ChildComponent from './components/child'

function App() {
  return (
    <div className="App">
      <h1>Title</h1>
      <ChildComponent />
    </div>
  );
}

export default App;
```
