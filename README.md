# Rpoblema-2---Automatizar-la-gesti-n-y-el-seguimiento-del-desempe-o-de-sus-ventas
Automatizar la gestión y el seguimiento del desempeño de sus ventas
ventas_por_vendedor = {}
limite_bono_mensual = 5000

def ingresar_ventas_vendedor():
    # Solicita un nombre y una cantidad al usuario. #
    vendedor = input("Ingrese su nombre: ")
    mes = input("Ingrese el mes de las ventas: ")
    try:
        ventas_mes = int(input(f"Ingrese las ventas de {mes}: "))
    except ValueError as e:
        print(f"Error: {e}. El valor ingresado no es numérico. Se usará 0 por defecto.")
        ventas_mes = 0
    
    return vendedor, mes, ventas_mes

def registrar_venta_mensual(ventas_por_vendedor, vendedor, mes, ventas_mes):
    # Agrega un nuevo mes de ventas al registro del vendedor #
    if vendedor not in ventas_por_vendedor:
        ventas_por_vendedor[vendedor] = {}
    ventas_por_vendedor[vendedor][mes] = ventas_mes
    return ventas_por_vendedor

def calcular_bono_vendedor(ventas_mes, limite_bono_mensual):
    # Verifica si el vendedor califica para un bono en el mes. #
    if ventas_mes > limite_bono_mensual:
        monto_bono = (ventas_mes - limite_bono_mensual) * 0.10
        print(f"¡Felicidades! Gana un bono de: {monto_bono}")
    else:
        print("Siga esforzándose para el bono.")

while True:
    print("\n--- Registro de ventas ---")

    vendedor, mes, ventas_mes = ingresar_ventas_vendedor()
    ventas_actualizadas = registrar_venta_mensual(ventas_por_vendedor, vendedor, mes, ventas_mes)

    #total_anual = sum(ventas_actualizadas.values())
    
    try:
        calcular_bono_vendedor(ventas_mes, limite_bono_mensual)
        print(f"Ventas de vendedor {vendedor} en {mes}: {ventas_mes}")
    except ValueError as e:
        print("Error en el cálculo: ", e)

    continuar = input("¿Desea registrar otra venta? (S/N): ")
    if continuar.upper() != "S":
        break
