# Отчет по практическому занятию №7

## 1. Анализ потоков данных (DFA)
### 1.1. Def-Use цепочки
| Переменная | Def | Use |
|---|---|---|
| log_entry | стр.3, стр.9 | стр.11 |
| status | стр.5 | стр.9, стр.12 |
| balance | стр.6 | стр.7 |
| new_balance | стр.7 | стр.8 |
| file | стр.10 | стр.11 (close отсутствует) |

### 1.2. Дефекты
- **Дефект 1 (UnboundLocalError):** `status` определена только при `amount > 0`.
- **Дефект 2 (Dead Store):** `log_entry = "Start processing"` перезаписывается до чтения.
- **Дефект 3 (Resource Leak):** файл открыт, но не закрыт.

## 2. Дизассемблирование
### 2.1. Восстановленный код
```python
acc = 0
i = 1
while i <= 10:
    acc += i
    i += 1
```
### 2.2. Пояснение
Цикл суммирует числа от 1 до 10 (результат 55).

## 3. Деобфускация
### 3.1. Расшифрованная строка
`import os; os.system('rm -rf /')`
### 3.2. Анализ угрозы
Выполнение `rm -rf /` — удаление всей файловой системы.
### 3.3. Методы защиты
Запрет exec/eval, SAST, принцип наименьших привилегий, sandbox.

## 4. Линтер
### 4.1. Правила .flake8
max-line-length=80, extend-ignore=E203,W503, exclude=.git,__pycache__,docs.
### 4.2. Ссылка на Pull Request
https://github.com/kedr00/practice-7/pull/1
### 4.3. Скриншот Checks
<img width="1920" height="1080" alt="Снимок экрана (7)" src="https://github.com/user-attachments/assets/489a4d39-f302-4f6d-9dd2-9bd762be6e33" /> 
