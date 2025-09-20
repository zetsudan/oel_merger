# oel_merger

Веб-инструмент для визуализации доступных оптических интервалов (сетка 12.5 GHz).  
Позволяет вручную добавлять OEL и их passband-диапазоны, строить итоговую таблицу занятости и график Summary.  
Работает в Docker на порту **9002**.

---

## Возможности
- Ручной ввод OEL: имя + passband (список диапазонов через `:`).  
- Итоговая таблица:
  - колонки: **Edge Freq | Central Freq | Edge Freq** + каждый OEL + сводный `Summary (ALL)`;
  - FREE — зелёным, IN USED — красным;
  - доступна в веб-интерфейсе `/summary` и в Excel.  
- Экспорт Excel:
  - имя файла `oel_YYYYMMDD_HHMMSS.xlsx`;
  - включены Wrap Text в заголовках;
  - FREE/IN USED с цветной заливкой.  
- График `/chart`:
  - ось X — интервалы (нижняя граница);
  - цветовая индикация занятости;
  - hover показывает интервал и статус.  

---

## Запуск через Docker

1. Клонировать проект:
   ```bash
   git clone https://github.com/zetsudan/oel_merger.git
   cd oel_merger
   ```

2. Собрать контейнер:
   ```bash
   docker build -t oel_merger:latest .
   ```

3. Запустить:
   ```bash
   docker run -d --name oel_merger \
     -p 9002:9002 \
     --restart unless-stopped \
     oel_merger:latest
   ```

---

## Использование

После запуска веб доступен по адресу:  
👉 [http://localhost:9002](http://localhost:9002)

- **Главная страница** — форма для добавления OEL и passband.  
- **`/summary`** — итоговая таблица в отдельном окне.  
- **`/chart`** — график свободных/занятых интервалов.  
- **Скачать Excel** — кнопка на главной странице.  

---

## Пример passband

```
(191.325 - 191.3625):(192.7375 - 192.7500):(196.0625 - 196.1250)
```

---

## Стек
- Python 3.11
- FastAPI + Jinja2
- openpyxl
- Plotly.js (frontend)
- Docker
