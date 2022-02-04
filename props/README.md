# Props
* Props
* Props reversed
* Triangle
## Props
in `src/components/Parent.tsx`
```ts
import Child1 from "./Child1"

const Parent = () => {
    const parentProps = {
        one : 1,
        two : "2",
    }

    return (
        <>
            <h2>
                Parent here: one {parentProps.one}, two: {parentProps.two}
            </h2>
            <Child1 parentProps={parentProps}></Child1>
        </>
    )
}

export default Parent
```
in `src/components/Child1.tsx`
```ts
import Child2 from "./Child2"

interface Props {
    parentProps: {
        one : number
        two : string
    }
}

const Child1 = (props: Props): JSX.Element => {
    return (
        <>
            <h3>
                Child1 here: one {props.parentProps.one}, two: {props.parentProps.two}
            </h3>
            <Child2 parentProps={props.parentProps}></Child2>
        </>
    )
}

export default Child1
```
in `src/components/Child2.tsx`
```ts
interface Props {
    parentProps: {
        one : number
        two : string
    }
}

const Child2 = (props: Props): JSX.Element => {
    return (
        <h4>
            Child2 here: one {props.parentProps.one}, two: {props.parentProps.two}
        </h4>
    )
}

export default Child2
```
## Props reversed
in `src/components/Parent.tsx`
```tsx
import { useState } from "react"
import Child1 from "./Child1"

const Parent = () => {
    const [parentProps, setParentProps] = useState({
        one : 1,
        two : "2",
    })

    const set = () => {
        setParentProps({
            ...parentProps,
            one: parentProps.one + 1
        })
    }

    return (
        <>
            <h2>
                Parent here: one {parentProps.one}, two: {parentProps.two}
            </h2>
            <button onClick={set}>hi</button>
            <Child1 set={set} parentProps={parentProps}></Child1>
        </>
    )
}

export default Parent
```
in `src/components/Child1.tsx`
```ts
import Child2 from "./Child2"

interface Props {
    parentProps: {
        one : number
        two : string
    },
    set: () => void
}

const Child1 = (props: Props): JSX.Element => {
    return (
        <>
            <h3>
                Child1 here: one {props.parentProps.one}, two: {props.parentProps.two}
            </h3>
            <button onClick={props.set}>hi</button>
            <Child2 set={props.set} parentProps={props.parentProps}></Child2>
        </>
    )
}

export default Child1
```
in `src/components/Child2.tsx`
```tsx
interface Props {
    parentProps: {
        one : number
        two : string
    }
    set: () => void
}

const Child2 = (props: Props): JSX.Element => {
    return (
        <>
            <h4>
                Child2 here: one {props.parentProps.one}, two: {props.parentProps.two}
            </h4>
            <button onClick={props.set}>hi</button>
        </>
    )
}

export default Child2
```
