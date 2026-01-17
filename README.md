from openpyxl import load_workbook
from openpyxl.styles import PatternFill


#           ------------------------------------ Info del documento ------------------------------------
# --- Abrir archivo ---
wb = load_workbook("Prueba_estaciones.xlsx")
ws = wb["Hoja 1"]

# --- Listas de números ---
lista_verde = [15, 20, 8, 12]
lista_amarilla = [15, 25, 35]

# --- Estilos ---
fill_verde = PatternFill(start_color="C6EFCE", end_color="C6EFCE", fill_type="solid")
fill_amarillo = PatternFill(start_color="FFF2CC", end_color="FFF2CC", fill_type="solid")

# --- rows ---
rows_verde = [1,6]
rows_amarillo = [6,10]
# -- cols ---
cols_verde = [1,15]
cols_amarillo = [1,15]


#Hoja,color,lista_n,rows,cols
#Compilado xd
compilado=[[ws,fill_verde,lista_verde,rows_verde,cols_verde],[ws,fill_amarillo,lista_amarilla,rows_amarillo,cols_amarillo] ]

def coloreado(hoja,color,lista_n,rows,cols):
    for row in hoja.iter_rows(min_row=rows[0], max_row=rows[1], min_col=cols[0], max_col=cols[1]):
        for cell in row:
            if isinstance(cell.value, (int, float)):
                if cell.value in lista_n:
                    cell.fill = color

for valores in compilado:
    a,b,c,d,e = valores
    coloreado(a,b,c,d,e)
wb.save("datos_coloreados.xlsx")

