
def is_valid_hex(token):
    # Только шестнадцатеричные цифры
    for c in token:
        if c not in '0123456789abcdefABCDEF':
            return False
    if len(token) <= 3:
        return False
    n = int(token, 16)
    return n % 2 == 1 and n <= 409510

def num_to_words(n):
    d = {'0':'ноль','1':'один','2':'два','3':'три','4':'четыре','5':'пять','6':'шесть','7':'семь','8':'восемь','9':'девять'}
    return '-'.join([d[x] for x in str(n)])

def process_file(file_path):
    f = open('D:/input.txt')
    buffer = ''
    numbers = []
    while True:
        chunk = f.read(1024)
        if not chunk:
            break
        buffer += chunk
        parts = buffer.split(' ')
        buffer = parts[-1]
        for token in parts[:-1]:
            t = token.strip()
            if t and is_valid_hex(t):
                numbers.append(int(t,16))
    # остался хвост
    t = buffer.strip()
    if t and is_valid_hex(t):
        numbers.append(int(t,16))
    if numbers:
        numbers.sort()
        print('Подходящие числа:', numbers)
        print('Количество чисел:', len(numbers))
        print('Минимальное число прописью:', num_to_words(numbers[0]))
    else:
        print('Подходящих чисел не найдено.')

process_file('input.txt')
