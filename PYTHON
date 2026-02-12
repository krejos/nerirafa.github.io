from flask import Flask, render_template, request, jsonify
import sqlite3

app = Flask(__name__)

# ---------------------------
# BANCO
# ---------------------------
def connect():
    return sqlite3.connect("database.db")

with connect() as con:
    con.execute("""
    CREATE TABLE IF NOT EXISTS contatos(
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        nome TEXT,
        email TEXT,
        mensagem TEXT
    )
    """)

# ---------------------------
# FRONT
# ---------------------------
@app.route("/")
def home():
    return render_template("index.html")

# ---------------------------
# API CONTATO
# ---------------------------
@app.route("/api/contato", methods=["POST"])
def contato():

    data = request.json

    with connect() as con:
        con.execute("""
        INSERT INTO contatos (nome,email,mensagem)
        VALUES (?,?,?)
        """,(
            data["nome"],
            data["email"],
            data["mensagem"]
        ))

    return jsonify({"status":"ok"})

# ---------------------------
# START
# ---------------------------
if __name__ == "__main__":
    app.run(debug=True)
