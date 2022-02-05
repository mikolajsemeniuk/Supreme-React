# Hooks
* UseEffect
## UseEffect
```tsx
import { useState, useEffect } from "react"

interface Input {
    email: string
    password: string
}

const Parent = (): JSX.Element => {
    // function `setInput` re-render whole component
    const [input, setInput] = useState<Input>({
        email: '',
        password: ''
    })

    const [isValid, setIsValid] = useState<boolean>(false)

    const [isLoggedIn, setIsLoggedIn] = useState<boolean>(false)

    const [title, setTitle] = useState<string>('')

    const setEmail = (event: React.ChangeEvent<HTMLInputElement>): void => {
        setInput({
            ...input,
            email: event.target.value
        })
    }

    const setPassword = (event: React.ChangeEvent<HTMLInputElement>): void => {
        setInput({
            ...input,
            password: event.target.value
        })
    }

    const onSetTitle = (event: React.ChangeEvent<HTMLInputElement>): void => {
        setTitle(event.target.value)
    }

    const submit = (event: React.FormEvent<HTMLFormElement>): void => {
        event.preventDefault()
        alert(`email: ${input.email}, password: ${input.password}`)
        localStorage.setItem('isLoggedIn', '1')
        setIsLoggedIn(true)
    }

    const logout = (event: React.MouseEvent<HTMLButtonElement, MouseEvent>): void => {
        localStorage.removeItem('isLoggedIn')
        setIsLoggedIn(false)
    }

    // this function run only once
    // Equivalent for `componentDidMount`
    useEffect(() => {
        if (localStorage.getItem('isLoggedIn') === '1') {
            setIsLoggedIn(true)
        } else {
            setIsLoggedIn(false)
        }
    }, []) 

    // this function run when input changes
    // Equivalent for `componentDidUpdate`
    useEffect(() => {
        if (input.email.includes('@') && input.password.length > 5) {
            setIsValid(true)
        } else {
            setIsValid(false)
        }
    }, [input]) 

    // this function run when title changes
    // Equivalent for `componentWillUnmount`
    useEffect(() => {
        const pointer = setTimeout(() => {
            console.log('changes saved!')
        }, 1000)
        return () => {
            clearTimeout(pointer)
        }
    }, [title])

    return (
        <>
            {!isLoggedIn && (
                <>
                    <h3 className="">
                        UseEffect
                    </h3>
                    <form onSubmit={submit}>
                        <p>email</p>
                        <input type="text" value={input.email} onChange={setEmail} />
                        <p>password</p>
                        <input type="password" value={input.password} onChange={setPassword} />
                        <br />
                        <button disabled={!isValid} type="submit">
                            login
                        </button>    
                    </form>
                </>
            )}
            {isLoggedIn && (
                <>
                    <h3 className="">
                        Welcome user
                    </h3>
                    <input type="text" value={title} onChange={onSetTitle} />
                    <br />
                    <button onClick={logout} className="">
                        logout
                    </button>
                </>
            )}    
        </>
    )
}

export default Parent
```
