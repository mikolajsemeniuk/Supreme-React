# Rendering
* If else
* Loops

## If Else
in `src/components/Parent.tsx`
```tsx
const Parent = (): JSX.Element => {
    const data = {
        name: "my name",
        date: new Date(),
        sex: null
    }

    const one = <h3>{data.sex}</h3>
    const two = <h3>no sex :(</h3>
    let three

    if (data.sex) {
        three = <h3>{data.sex}</h3>
    } else {
        three = <h3>no sex :(</h3>
    }

    return (
        <>
            <h2>
                data.name: {data.name}, data.date: {data.date.toISOString()},
            </h2>

            {/* if */}
            {data.name && <h3>name exists</h3>}

            {/* if else */}
            {data.sex ? <h3>{data.sex}</h3> : <h3>no sex :(</h3>}

            {/* if else another */}
            {data.sex ? one : two}

            {/* if else another */}
            {three}

            {/* if else if else */}
            {data.sex ? <h3>{data.sex}</h3>
            : data.name ? <h3>name exists</h3>
            : <h3>nothing exists</h3>}
        </>
    )
}

export default Parent
```
## Loops
in `src/components/Parent.tsx`
```ts
const Parent = (): JSX.Element => {
    
    let data = [
        {
            id: 0,
            name: "one"
        },
        {
            id: 1,
            name: "two"
        }
    ]

    return (
        <>
            {data.map(element => (
                <div key={element.id} className="">
                    <h1>{element.id}</h1>
                    <h2>{element.name}</h2>
                </div>
            ))}
            <p>second list</p>
            {data.map((element, index) => (
                <div key={index} className="">
                    <h1>{element.id}</h1>
                    <h2>{element.name}</h2>
                </div>
            ))}
        </>
    )
}

export default Parent
```
