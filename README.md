def is_valid_hex(A):
    for c in A:
        if c not in '0123456789abcdefABCDEF':
            return False
    if len(A) <= 3:
        return False
    n = int(A, 16)
    return n % 2 == 1 and n <= 409510

def num_to_words(n):
    d = {'0':'ноль','1':'один','2':'два','3':'три','4':'четыре','5':'пять','6':'шесть','7':'семь','8':'восемь','9':'девять'}
    return '-'.join([d[x] for x in str(n)])
f=open('input.txt', 'r')
while line := f.readline():
    print(line)
    values = line.split()
    
"""    
    print('Подходящие числа:')
    print('Количество чисел:')
    print('Минимальное число прописью:')
    print('Подходящих чисел не найдено.')

process_file('input.txt')
"""
