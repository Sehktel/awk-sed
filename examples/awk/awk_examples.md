# Примеры awk от начального до профессионального уровня

## Уровень 1: Простой вывод
```bash
# Вывод всех строк файла
awk '{print $0}' data.txt
```

## Уровень 2: Выборка полей
```bash
# Вывод второго столбца
awk '{print $2}' data.txt
```

## Уровень 3: Условная фильтрация
```bash
# Вывод строк, где второе поле > 50
awk '$2 > 50 {print $0}' data.txt
```

## Уровень 4: Математические операции
```bash
# Сумма значений второго столбца
awk '{sum += $2} END {print "Сумма:", sum}' data.txt
```

## Уровень 5: Регулярные выражения
```bash
# Вывод строк, содержащих слово "error"
awk '/error/ {print $0}' log.txt
```

## Уровень 6: Форматированный вывод
```bash
# Красивый вывод с форматированием
awk '{printf "Имя: %-10s Возраст: %3d\n", $1, $2}' people.txt
```

## Уровень 7: Пользовательские функции
```bash
# Функция для вычисления максимума
awk '
function max(a, b) {
    return a > b ? a : b
}
{print "Максимум:", max($1, $2)}
' numbers.txt
```

## Уровень 8: Работа с несколькими файлами
```bash
# Агрегация данных из нескольких файлов
awk '{total[$1] += $2} END {
    for (name in total) {
        print name ":", total[name]
    }
}' file1.txt file2.txt
```

## Уровень 9: Сложная обработка CSV
```bash
# Анализ CSV с разделителем и группировкой
awk -F',' '
BEGIN {print "Отчет по категориям"}
$3 == "Sales" {sales[$1] += $2}
END {
    for (category in sales) {
        print category ": $" sales[category]
    }
}' sales_data.csv
```

## Уровень 10: Продвинутый парсинг и статистика
```bash
# Полный анализ данных с расширенной статистикой
awk '
BEGIN {
    print "Расширенный статистический анализ"
    count = 0
    sum = 0
    min = 999999
    max = -999999
}
{
    count++
    sum += $1
    min = $1 < min ? $1 : min
    max = $1 > max ? $1 : max
    values[count] = $1
}
END {
    avg = sum / count
    
    # Вычисление дисперсии
    variance = 0
    for (i = 1; i <= count; i++) {
        variance += (values[i] - avg)^2
    }
    variance /= count
    
    print "Количество записей: " count
    print "Сумма: " sum
    print "Среднее: " avg
    print "Минимум: " min
    print "Максимум: " max
    print "Дисперсия: " variance
}' data.txt
``` 