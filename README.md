# oel_merger (fix3)
- Исправлен 500 на `/summary` (убран `enumerate` в Jinja; используется `loop.index0`).
- График теперь показывает интервалы (ось X — нижняя граница; в подсказке — `lower–upper THz`).
- Компактные строки в таблице; экспорт `oel_YYYYMMDD_HHMMSS.xlsx`.
