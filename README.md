import sys
from PySide6.QtWidgets import (
    QApplication, QWidget, QLabel, QVBoxLayout,
    QGridLayout, QFrame, QDialog
)
from PySide6.QtCore import Qt
from PySide6.QtCore import QTimer

# ─────────────────────────────────────────
# Cuadro de dos colores
# ─────────────────────────────────────────
def create_color_tile(color1, color2, size=30):
    frame = QFrame()
    frame.setFixedSize(size, size)
    frame.setCursor(Qt.PointingHandCursor)

    frame.setStyleSheet(f"""
        QFrame {{
            background: qlineargradient(
                x1:0, y1:0, x2:1, y2:0,
                stop:0 {color1},
                stop:0.5 {color1},
                stop:0.5 {color2},
                stop:1 {color2}
            );
            border-radius: 6px;
            border: 1px solid #555;
        }}
        QFrame:hover {{
            border: 2px solid #0078d7;
        }}
    """)
    return frame


# ─────────────────────────────────────────
# Ventana emergente de detalle
# ─────────────────────────────────────────
def show_detail_window(color1, color2, text1, text2):
    dialog = QDialog()
    dialog.setWindowTitle("Detalle")
    dialog.setFixedSize(320, 260)

    layout = QVBoxLayout(dialog)
    layout.setAlignment(Qt.AlignTop)

    color_view = create_color_tile(color1, color2, size=200)
    layout.addWidget(color_view, alignment=Qt.AlignCenter)

    label1 = QLabel(text1)
    label1.setAlignment(Qt.AlignCenter)
    label1.setStyleSheet("font-weight: bold;")

    label2 = QLabel(text2)
    label2.setAlignment(Qt.AlignCenter)
    label2.setStyleSheet("font-weight: bold;")

    layout.addWidget(label1)
    layout.addWidget(label2)

    dialog.exec()


# ─────────────────────────────────────────
# Bloque completo (título + cuadro)
# ─────────────────────────────────────────
def create_tile_block(title, color1, color2, text1, text2):
    container = QWidget()
    layout = QVBoxLayout(container)
    layout.setAlignment(Qt.AlignCenter)
    layout.setSpacing(4)

    title_label = QLabel(title)
    title_label.setAlignment(Qt.AlignCenter)
    title_label.setStyleSheet("font-weight: bold;")

    tile = create_color_tile(color1, color2)

    # Hacer el cuadro clickeable
    tile.mousePressEvent = lambda event: show_detail_window(
        color1, color2, text1, text2
    )

    layout.addWidget(title_label)
    layout.addWidget(tile)

    return container

def center_window(window):
    screen = window.screen()
    screen_geometry = screen.availableGeometry()
    window_geometry = window.frameGeometry()

    window_geometry.moveCenter(screen_geometry.center())
    window.move(window_geometry.topLeft())
# ─────────────────────────────────────────
# MAIN
# ─────────────────────────────────────────
app = QApplication(sys.argv)

window = QWidget()
window.setWindowTitle("Recuadros interactivos")
window.resize(500, 400)
#self.left, self.top, self.width, self.height
grid = QGridLayout(window)
grid.setSpacing(0.5)

# Datos de ejemplo
data = [
    ("125/126", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("52/53", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("125/126", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("52/53", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("125/126", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("52/53", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("125/126", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("52/53", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("125/126", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("52/53", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("125/126", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("52/53", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("125/126", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("52/53", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("125/126", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("52/53", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("125/126", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("52/53", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("125/126", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("52/53", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("125/126", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("52/53", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("125/126", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("52/53", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("125/126", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("52/53", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("125/126", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("52/53", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("125/126", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("52/53", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("125/126", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("52/53", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("125/126", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("52/53", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("125/126", "red", "blue", "Rojo: energía", "Azul: calma"),
    ("52/53", "red", "blue", "Rojo: energía", "Azul: calma")
    
]

cols = 32  # número de columnas

for i, (title, c1, c2, t1, t2) in enumerate(data):
    block = create_tile_block(title, c1, c2, t1, t2)
    grid.addWidget(block, i // cols, i % cols)

window.show()
QTimer.singleShot(0, lambda: center_window(window))

sys.exit(app.exec())
