from flask import Flask, jsonify, request

app = Flask(__name__)

# Lista inicial de productos
productos = [
    {"id": 1, "nombre": "Laptop", "precio": 5500},
    {"id": 2, "nombre": "Mouse", "precio": 150},
    {"id": 3, "nombre": "Teclado", "precio": 250}
]

@app.route('/')
def home():
    return "Bienvenido al sistema de productos."

@app.route('/acerca')
def acerca():
    return jsonify({
        "aplicacion": "Gestión de Productos",
        "version": 1.0,
        "autor": "jhonny victor juchazara orco"
    })

# Obtener todos los productos
@app.route('/productos', methods=['GET'])
def get_productos():
    return jsonify(productos)

# Obtener producto por ID
@app.route('/productos/<int:id>', methods=['GET'])
def get_producto(id):
    producto = next((p for p in productos if p["id"] == id), None)
    if producto:
        return jsonify(producto)
    return jsonify({"error": "Producto no encontrado"}), 404

# Insertar producto nuevo
@app.route('/productos', methods=['POST'])
def add_producto():
    nuevo = request.get_json()
    if "nombre" not in nuevo or "precio" not in nuevo:
        return jsonify({"error": "Datos inválidos"}), 400
    nuevo_id = max([p["id"] for p in productos]) + 1
    nuevo_producto = {
        "id": nuevo_id,
        "nombre": nuevo["nombre"],
        "precio": nuevo["precio"]
    }
    productos.append(nuevo_producto)
    return jsonify({"mensaje": "Producto agregado correctamente"})

# Eliminar producto por ID
@app.route('/productos/<int:id>', methods=['DELETE'])
def delete_producto(id):
    global productos
    producto = next((p for p in productos if p["id"] == id), None)
    if producto:
        productos = [p for p in productos if p["id"] != id]
        return jsonify({"mensaje": "Producto eliminado correctamente"})
    return jsonify({"error": "Producto no encontrado"}), 404

if __name__ == '_main_':
    app.run(debug=True)

app = Flask(__name__)

# Lista inicial de productos
productos = [
    {"id": 1, "nombre": "Laptop", "precio": 5500},
    {"id": 2, "nombre": "Mouse", "precio": 150},
    {"id": 3, "nombre": "Teclado", "precio": 250}
]

@app.route('/')
def home():
    return "Bienvenido al sistema de productos."

@app.route('/acerca')
def acerca():
    return jsonify({
        "aplicacion": "Gestión de Productos",
        "version": 1.0,
        "autor": "jhonny victor juchazara orco"
    })

# Obtener todos los productos
@app.route('/productos', methods=['GET'])
def get_productos():
    return jsonify(productos)

# Obtener producto por ID
@app.route('/productos/<int:id>', methods=['GET'])
def get_producto(id):
    producto = next((p for p in productos if p["id"] == id), None)
    if producto:
        return jsonify(producto)
    return jsonify({"error": "Producto no encontrado"}), 404

# Insertar producto nuevo
@app.route('/productos', methods=['POST'])
def add_producto():
    nuevo = request.get_json()
    if "nombre" not in nuevo or "precio" not in nuevo:
        return jsonify({"error": "Datos inválidos"}), 400
    nuevo_id = max([p["id"] for p in productos]) + 1
    nuevo_producto = {
        "id": nuevo_id,
        "nombre": nuevo["nombre"],
        "precio": nuevo["precio"]
    }
    productos.append(nuevo_producto)
    return jsonify({"mensaje": "Producto agregado correctamente"})

# Eliminar producto por ID
@app.route('/productos/<int:id>', methods=['DELETE'])
def delete_producto(id):
    global productos
    producto = next((p for p in productos if p["id"] == id), None)
    if producto:
        productos = [p for p in productos if p["id"] != id]
        return jsonify({"mensaje": "Producto eliminado correctamente"})
    return jsonify({"error": "Producto no encontrado"}), 404

if __name__ == '_main_':
    app.run(debug=True)
