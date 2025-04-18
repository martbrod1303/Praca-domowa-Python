# Praca-domowa-Python

# Inicjalizacja próby
proba = [
    (1.5, 25001),
    (1.8, 30012),
    (0.5, 23005),
    (0.7, 20007),
    (1.2, 62015),
    (0.6, 22022),
    (1.0, 0)  # Brakująca liczba wystąpień dla wartości 1.0
]

# Wprowadzenie brakującej wartości z walidacją
while True:
    try:
        brakujaca_wartosc = int(input("Podaj, ile razy wartość 1.0 pojawiła się w próbie (liczba całkowita nieujemna): "))
        if brakujaca_wartosc >= 0:
            break
        else:
            print("Podana liczba musi być nieujemna. Spróbuj ponownie.")
    except ValueError:
        print("Podaj liczbę całkowitą nieujemną. Spróbuj ponownie.")

proba[-1] = (1.0, brakujaca_wartosc)

# Przetwarzanie danych
wartosci = []
ilosci = []
for wartosc, ilosc in proba:
    wartosci.extend([wartosc] * ilosc)

# Obliczenia
srednia = sum(wartosci) / len(wartosci)

# Wariancja
suma_kwadratow_odchylen = sum((x - srednia) ** 2 for x in wartosci)
wariancja = suma_kwadratow_odchylen / (len(wartosci) - 1)

# Moda
wystapienia = {}
for wartosc in wartosci:
    if wartosc in wystapienia:
        wystapienia[wartosc] += 1
    else:
        wystapienia[wartosc] = 1

max_wystapienia = max(wystapienia.values())
mody = [k for k, v in wystapienia.items() if v == max_wystapienia]

if len(mody) == 1:
    moda = mody[0]
else:
    moda = None

# Wyświetlanie wyników
print(f"Średnia z próby: {srednia}")
print(f"Wariancja z próby: {wariancja}")
if moda is not None:
    print(f"Moda z próby: {moda}")
else:
    print("Nie można obliczyć mody, gdy istnieje więcej niż jedna wartość najczęściej występująca.")

# Zapis wyników do pliku
with open('wynik.txt', 'w') as file:
    file.write(f"Średnia z próby: {srednia}\n")
    file.write(f"Wariancja z próby: {wariancja}\n")
    if moda is not None:
        file.write(f"Moda z próby: {moda}\n")
    else:
        file.write("Nie można obliczyć mody, gdy istnieje więcej niż jedna wartość najczęściej występująca.\n")
