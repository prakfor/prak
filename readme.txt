Задание 1: Настройка CI-пайплайна для Python с GitHub Actions
Цель: Создать автоматический пайплайн, который запускает тесты и проверяет код при каждом коммите или Pull Request.
Инструкция:
1. Подготовка репозитория
1.	Создайте репозиторий на GitHub:
o	Откройте github.com в браузере.
o	Нажмите New repository, назовите его (например, python-ci-example).
o	Выберите Public и создайте репозиторий.
2.	Клонируйте репозиторий в VS Code:
o	Откройте VS Code → Terminal → New Terminal.
o	Выполните:
bash
Copy
Download
git clone https://github.com/ваш-логин/python-ci-example.git
cd python-ci-example
________________________________________
2. Создаем тестовый проект на Python
1.	Файл main.py (основной код):
python
Copy
Download
def add(a, b):
    return a + b

def subtract(a, b):
    return a - b
2.	Файл test_main.py (тесты с использованием pytest):
python
Copy
Download
import main

def test_add():
    assert main.add(2, 3) == 5

def test_subtract():
    assert main.subtract(5, 2) == 3
3.	Файл requirements.txt (зависимости):
Copy
Download
pytest
________________________________________
3. Настройка GitHub Actions
1.	Создайте папку .github/workflows:
bash
Copy
Download
mkdir -p .github/workflows
2.	Создайте файл ci.yml (внутри .github/workflows):
yaml
Copy
Download
name: Python CI Pipeline
on: [push, pull_request]  # Запуск при коммитах и PR

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4  # Клонирует репозиторий
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.11'  # Версия Python
      - name: Install dependencies
        run: pip install -r requirements.txt
      - name: Run tests
        run: pytest test_main.py -v  # Запуск тестов
________________________________________
4. Запушим изменения в GitHub
1.	Добавим файлы в Git:
bash
Copy
Download
git add .
git commit -m "Add Python project with CI pipeline"
git push origin main
2.	Проверяем работу CI:
o	Откройте репозиторий в браузере → вкладка Actions.
o	Должен появиться запущенный workflow (зелёная галочка = успех).
________________________________________
Что проверить, если тесты не проходят?
•	Убедитесь, что в test_main.py нет ошибок.
•	Если pytest не установлен локально, добавьте его в requirements.txt.
•	В логах GitHub Actions будут подробные ошибки (открыть вкладку Actions → выбрать запуск).
33333333
import { useState } from 'react';
function App() {
  const [tasks, setTasks] = useState([]);
  const [input, setInput] = useState('');
  const addTask = () => {
    if (input.trim()) {
      setTasks([...tasks, { text: input, done: false }]);
      setInput('');
    }
  };
  const toggleTask = (index) => {
    const newTasks = [...tasks];
    newTasks[index].done = !newTasks[index].done;
    setTasks(newTasks);
  };
  const deleteTask = (index) => {
    setTasks(tasks.filter((_, i) => i !== index));
  };
  return (
    <div>
      <input value={input} onChange={(e) => setInput(e.target.value)} />
      <button onClick={addTask}>Add</button>
      <ul>
        {tasks.map((task, index) => (
          <li key={index}>
            <span style={{ textDecoration: task.done ? 'line-through' : 'none' }}>
              {task.text}
            </span>
            <button onClick={() => toggleTask(index)}>Toggle</button>
            <button onClick={() => deleteTask(index)}>Delete</button>
          </li>
        ))}
      </ul>
    </div>
  );
}
export default App;

4444444444444

import { useState, useEffect } from 'react';
import axios from 'axios';
function App() {
  const [rates, setRates] = useState({});
  const [amount, setAmount] = useState(1);
  const [from, setFrom] = useState('USD');
  const [to, setTo] = useState('EUR');
  const [result, setResult] = useState(0);
  useEffect(() => {
    axios.get('https://api.exchangerate-api.com/v4/latest/USD')
      .then(res => setRates(res.data.rates))
      .catch(err => console.error(err));
  }, []);
  const convert = () => {
    if (rates[to] && rates[from]) {
      setResult((amount * rates[to]) / rates[from]);
    }
  };
  return (
    <div>
      <input type="number" value={amount} onChange={(e) => setAmount(e.target.value)} />
      <select value={from} onChange={(e) => setFrom(e.target.value)}>
        <option value="USD">USD</option>
        <option value="EUR">EUR</option>
        <option value="RUB">RUB</option>
      </select>
      <span> to </span>
      <select value={to} onChange={(e) => setTo(e.target.value)}>
        <option value="USD">USD</option>
        <option value="EUR">EUR</option>
        <option value="RUB">RUB</option>
      </select>
      <button onClick={convert}>Convert</button>
      <p>Result: {result.toFixed(2)}</p>
    </div>
  );
}
export default App;

