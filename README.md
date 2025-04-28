def is_valid_hex_number(token):
    """ Проверяет, является ли строка валидным шестнадцатеричным числом. """
    try:
        # Преобразуем строку в шестнадцатеричное число
        value = int(token, 16)
        # Проверяем условия
        return (
            value % 2 == 1 and                   # Нечетное
            value <= 409510 and                  # Не превышает 409510
            len(token) > 3                       # Содержит более 3 цифр
        )
    except ValueError:
        return False

def number_to_words(number):
    """ Преобразует число в строку, где каждая цифра представлена прописью. """
    digit_to_word = {
        '0': 'ноль', '1': 'один', '2': 'два', '3': 'три', '4': 'четыре',
        '5': 'пять', '6': 'шесть', '7': 'семь', '8': 'восемь', '9': 'девять'
    }
    return '-'.join(digit_to_word[digit] for digit in str(number))

def process_file(file_path, block_size=1024):
    """ Читает файл блоками и обрабатывает данные. """
    buffer = ''
    valid_numbers = []
    
    with open(file_path, 'r') as f:
        while chunk := f.read(block_size):
            buffer += chunk
            tokens = buffer.split()
            buffer = tokens.pop() if not chunk.endswith(' ') else ''
            
            for token in tokens:
                if is_valid_hex_number(token):
                    valid_numbers.append(int(token, 16))
    
    if valid_numbers:
        valid_numbers.sort()
        print(f"Подходящие числа: {valid_numbers}")
        print(f"Количество чисел: {len(valid_numbers)}")
        print(f"Минимальное число прописью: {number_to_words(valid_numbers[0])}")
    else:
        print("Подходящих чисел не найдено.")

# Укажите путь к вашему файлу
file_path = 'D:/input.txt'
process_file(file_path)
