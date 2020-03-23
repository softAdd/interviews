## (Не)контроллируемые компоненты

```jsx
// На каждое изменение, вызывается setInputState.
const controlledComponent = () => {
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

**Хороший пример односоставных условий**

```jsx
const appComponent = ({ isRight }) => {
    return (
        <>
            {isRight && <RightComponent>}
            {!isRight && <WrongComponent>}
        </>
    )
}
```


**Замена bind при вызове методов компонентов**

```jsx
// экспериментальный синтаксис общедоступных полей классов
class LoginButton extends React.Component {
    handleClick = () => {
        console.log('button is pressed');
    }

    render() {
        return (
            <button onClick={this.handleClick}>
                Press me
            </button>
        )
    }
}
// с использование стрелочных функций
class LoginButton extends React.Component {
    handleClick() {
        console.log('button is pressed');
    }

    render() {
        return (
            <button onClick={(evt) => this.handleClick(evt)}>
                Press me
            </button>
        )
    }
}
```

**Хороший пример роутинга**

[github, artbocha](https://github.com/artbocha/react-redux-reactRouter/tree/master/src)