# Forms
* Inputs, forms
## Inputs, forms
```jsx
import { useState } from "react"

enum RelationshipStatus {
    Single,
    Married,
    Other
}

interface Input {
    name: string
    birthday: Date
    age: number
    sex: boolean
    status: RelationshipStatus
}

const Parent = (): JSX.Element => {
    
    const [input, setInput] = useState<Input>({
        name: '',
        birthday: new Date(),
        age: 0,
        sex: false,
        status: RelationshipStatus.Single
    })
    
    const setName = (event: React.ChangeEvent<HTMLInputElement>): void => {
        setInput({
            ...input,
            name: event.target.value,
        })
    }

    const setDate = (event: React.ChangeEvent<HTMLInputElement>): void => {
        setInput({
            ...input,
            birthday: new Date(event.target.value)
        })
    }

    const setAge = (event: React.ChangeEvent<HTMLInputElement>): void => {
        setInput({
            ...input,
            age: Number(event.target.value)
        })
    }

    const setSex = (event: React.ChangeEvent<HTMLInputElement>): void => {
        setInput({
            ...input,
            sex: event.target.checked
        })
    }

    const setStatus = (event: React.ChangeEvent<HTMLSelectElement>): void => {
        setInput({
            ...input,
            status: RelationshipStatus[event.target.value as keyof typeof RelationshipStatus]
        })
    }

    const handleSubmit = (event: React.FormEvent<HTMLFormElement>): void => {
        alert(`name: ${input.name}, 
               birthday: ${input.birthday}, 
               age: ${input.age},
               sex: ${input.sex},
               status: ${input.status}`);
        event.preventDefault()
    }
    

    return (
        <>
            <form onSubmit={handleSubmit}>
                <h1>fill me</h1>

                <p>{input.name}</p>
                <input type="text" value={input.name} onChange={setName} />

                <p>{input.birthday.toLocaleDateString('en-CA')}</p>
                <input type="date" value={input.birthday.toLocaleDateString('en-CA')} onChange={setDate} />

                <p>{input.age}</p>
                <input type="number" value={input.age} onChange={setAge} />

                {input.sex && <p>true</p>}
                {!input.sex && <p>false</p>}
                <input type="checkbox" checked={input.sex} onChange={setSex} />

                <p>{input.status}</p>
                <select onChange={setStatus}>
                    {Object.keys(RelationshipStatus).map((status, index) => (
                        isNaN(Number(status)) && <option key={index} value={status}>{status}</option>
                    ))}
                </select>

                <br />
                <button type="submit">
                    Submit me
                </button>
            </form>
        </>
    )
}

export default Parent
```
