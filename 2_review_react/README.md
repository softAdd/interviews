## (Не)контроллируемые компоненты

```jsx
// На каждое изменение, вызывается setInputState.
const component = () => {
    const [inputState, setInputState] = useState('');

    const handleChange = (evt) => {
        setInputState(evt.target.value);
    }

    return (
        <input type="text" value={inputState} onChange={handleChange} />
    )
}
// Изменения состояния компонента не происходит.
const uncotrolledComponent = () => {
    const input = useRef(null);

    const handleSubmit = (evt) => {
        evt.preventDefault();
        console.log(this.input.current.value);
    }

    return (
        <>
            <input
                type="text"
                ref={this.input}
            />
            <input type="submit" value="submit" />
        </>
    )
}
```