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

[github, fork artbocha](https://github.com/softAdd/react-redux-reactRouter)

**Предохранители, ErrorBoundary**

Классовый компонент является предохранителем если включает одно из:
1. static getDerivedStateFromError() - для рендера запасного UI в случае ошибки.
2. componentDidCatch() - для сохранения информации об отловленной ошибке.

Использование предохранителей:
1. Отлавливают ошибки иключительно в дочерних компонентах.
2. Не отлавливают ошибки внутри себя.
3. Целесообразно написать один предохранитель и использовать его по всему приложению.

Из документации React:
```jsx
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    // Обновить состояние с тем, чтобы следующий рендер показал запасной UI.
    return { hasError: true };
  }

  componentDidCatch(error, errorInfo) {
    // Можно также сохранить информацию об ошибке в соответствующую службу журнала ошибок
    logErrorToMyService(error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      // Можно отрендерить запасной UI произвольного вида
      return <h1>Что-то пошло не так.</h1>;
    }

    return this.props.children; 
  }
}
```