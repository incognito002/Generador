import os
import time
import random

# Lista de BINs válidos
BIN_LIST = {
    "Visa": ["400000", "411111", "455660", "471610"],
    "MasterCard": ["510510", "520520", "530530", "540540"],
    "American Express": ["370000", "340000"],
    "Discover": ["601100", "622126"],
}

# Función para limpiar la pantalla
def clear_screen():
    # Comando para limpiar la pantalla dependiendo del sistema operativo
    if os.name == 'nt':  # Si el sistema es Windows
        os.system('cls')
    else:  # Si el sistema es Unix-based (Linux/macOS)
        os.system('clear')

# Función para animar el banner
def animated_banner(text, delay=0.05):
    for char in text:
        print(char, end='', flush=True)
        time.sleep(delay)
    print("\n")

# Función para animar las frases tipo hacker
def hacker_typing_animation(text):
    for char in text:
        print(char, end='', flush=True)
        time.sleep(random.uniform(0.03, 0.07))  # Velocidad variable para el efecto "hacker"
    print("\n")

# Algoritmo de Luhn para generar número de tarjeta válido
def generate_card_number(bin_number):
    # Aseguramos que la longitud de la tarjeta sea de 16 dígitos
    card_number = list(bin_number) + [str(random.randint(0, 9)) for _ in range(10)]  # Ahora genera 16 dígitos
    sum_digits = 0

    # Algoritmo de Luhn (sumar dígitos de derecha a izquierda)
    for i in range(15, -1, -1):
        digit = int(card_number[i])
        if i % 2 == 0:
            digit *= 2
            if digit > 9:
                digit -= 9
        sum_digits += digit

    check_digit = (10 - (sum_digits % 10)) % 10
    card_number.append(str(check_digit))  # Se añade el dígito de verificación
    
    return "".join(card_number)

# Función para generar tarjetas
def generate_cards():
    try:
        count = int(input("\n🔹 ¿Cuántas tarjetas deseas generar? (máximo 100): "))
        if count <= 0 or count > 100:
            print("⚠️ Número inválido, intenta de nuevo. (Entre 1 y 100)")
            return

        print("\n💳 Generando tarjetas...\n")
        time.sleep(1)

        for _ in range(count):
            brand = random.choice(list(BIN_LIST.keys()))  # Selecciona una marca aleatoria
            bin_list = BIN_LIST.get(brand, [])  # Obtiene la lista de BINs de la marca

            if not bin_list:  # Verifica si la lista no está vacía
                print(f"⚠️ No hay BINs disponibles para {brand}.")
                continue

            bin_number = random.choice(bin_list)  # Selecciona un BIN válido
            card_number = generate_card_number(bin_number)  # Genera el número de tarjeta
            
            # Generación de fecha de vencimiento (a partir del año actual hasta 2026 o posterior)
            current_year = 2025
            expiry_year = random.randint(current_year, current_year + 5)  # Año de expiración entre 2025 y 2030
            expiry_month = random.randint(1, 12)  # Mes aleatorio entre 1 y 12
            exp_date = f"{expiry_month:02d}/{expiry_year}"

            cvv = f"{random.randint(100, 999)}"  # CVV de 3 dígitos

            print(f"🔹 {brand}")
            print(f"   💳 Número: {card_number}")
            print(f"   📅 Expira: {exp_date}")
            print(f"   🔐 CVV: {cvv}\n")

    except ValueError:
        print("⚠️ Ingresa un número válido.")

# Función para validar credenciales
def login():
    user = input("🔹 Usuario: ")
    password = input("🔹 Contraseña: ")

    if user == "family401" and password == "fm 40100":
        print("\n✅ Inicio de sesión exitoso\n")
        return True
    else:
        print("\n❌ Usuario o contraseña incorrectos. Inténtalo de nuevo.\n")
        return False

# Función del menú principal
def main_menu():
    while True:
        clear_screen()  # Limpiar la pantalla antes de mostrar el menú
        print("📌 Menú Principal:")
        print("1️⃣ Generar Tarjetas")
        print("2️⃣ Generar BIN de prueba")
        print("3️⃣ Salir")
        
        opcion = input("\nSelecciona una opción: ")

        if opcion == "1":
            generate_cards()
        elif opcion == "2":
            print("\n🏦 Generando BIN de prueba...")
            time.sleep(1)
            print("✅ BIN generado: 400012\n")
        elif opcion == "3":
            print("\n👋 Saliendo... ¡Hasta pronto!")
            break
        else:
            print("\n⚠️ Opción no válida, intenta de nuevo.")

# Programa principal
if __name__ == "__main__":
    # Animación tipo hacker
    clear_screen()  # Limpiar pantalla al inicio
    animated_banner("🔷 Iniciando sistema de generación de tarjetas... 🔷")
    time.sleep(1)

    hacker_typing_animation("Conectando con la red...")
    hacker_typing_animation("Accediendo al servidor principal...")
    hacker_typing_animation("Cargando módulos...")
    hacker_typing_animation("Validando credenciales de usuario...")

    while not login():
        pass  # Repite hasta que el usuario ingrese correctamente

    hacker_typing_animation("Acceso confirmado, bienvenido al sistema...")

    # Menú
    main_menu()