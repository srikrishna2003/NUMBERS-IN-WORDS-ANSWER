maps = {}
maps[0] = 0
maps[1] = 3
maps[2] = 3
maps[3] = 5
maps[4] = 4
maps[5] = 4
maps[6] = 3
maps[7] = 5
maps[8] = 5
maps[9] = 4
maps[10] = 3
maps[11] = 6
maps['and'] = 3
maps['teen'] = 4
maps[20] = 6
maps[30] = 6
maps[40] = 5
maps[50] = 5
maps[60] = 6
maps[70] = 7
maps[80] = 6
maps[90] = 6
maps[100] = 7
maps[1000] = 8

# create a list of numbers 1-1000
def int_to_list(number):
    s = str(number)
    c = []
    for digit in s:
        a = int(digit)
        c.append(a)
    return c  # turn a number into a list of its digits
def list_to_int(numList):
    s = map(str, numList)
    s = ''.join(s)
    s = int(s)
    return s


L = []
for i in range(1,1001,1):
    L.append(i)

def one_digit(n):
    q = maps[n]
    return q
def eleven(n):
    q = maps[11]
    return q
def teen(n):
    digits = int_to_list(n) 
    q = maps[digits[1]] + maps['teen']
    return q
def two_digit(n):
    digits = int_to_list(n)
    first = digits[0]
    first = first*10
    second = digits[1]
    q = maps[first] + one_digit(second)
    return q
def three_digit(n):
    digits = int_to_list(n)
    first = digits[0]
    second = digits[1]
    third = digits[2]

    # first digit length
    f = maps[first]+maps[100]

    if second == 1 and third == 1:
        s = maps['and'] + maps[11]
    elif second == 1 and third != 1:
        s = digits[1:]
        s = list_to_int(s)
        s = maps['and'] + teen(s)
    elif second == 0 and third == 0:
        s = maps[0]
    elif second == 0 and third != 0:
        s = maps['and'] + maps[third]
    else:
        s = digits[1:]
        s = list_to_int(s)
        s = maps['and'] + two_digit(s)

    q = f + s
    return q
def thousand(n):
    q = maps[1000]
    return q

# generate a list of all the lengths of numbers

lengths = []


for i in L:
    if i < 11:
        n = one_digit(i)
        lengths.append(n)
    elif i == 11:
        n = eleven(i)
        lengths.append(n)
    elif i > 11 and i < 20:
        n = teen(i)
        lengths.append(n)
    elif i > 20 and i < 100:
        n = two_digit(i)
        lengths.append(n)
    elif i >= 100 and i < 1000:
        n = three_digit(i)
        lengths.append(n)
    elif i == 1000:
        n = thousand(i)
        lengths.append(n)
    else:
        pass

# since "eighteen" has eight letters (not 9), subtract 10
sum = sum(lengths) - 10
print "Your number is: ", sum
