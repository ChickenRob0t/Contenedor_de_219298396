from openpyxl import load_workbook
from openpyxl.styles import PatternFill

# --- Abrir archivo ---
wb = load_workbook("datos.xlsx")
ws = wb["Sheet1"]

# --- Listas de números ---
lista_verde = [10, 20, 30, 40]
lista_amarilla = [15, 25, 35]

# --- Estilos ---
fill_verde = PatternFill(start_color="C6EFCE", end_color="C6EFCE", fill_type="solid")
fill_amarillo = PatternFill(start_color="FFF2CC", end_color="FFF2CC", fill_type="solid")

# --- Rango a revisar ---
for row in ws.iter_rows(min_row=1, max_row=10, min_col=1, max_col=4):
    for cell in row:
        if isinstance(cell.value, (int, float)):
            if cell.value in lista_verde:
                cell.fill = fill_verde
            elif cell.value in lista_amarilla:
                cell.fill = fill_amarillo

# --- Guardar ---
wb.save("datos_coloreados.xlsx")
