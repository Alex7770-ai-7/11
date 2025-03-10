import sqlite3

conn = sqlite3.connect("FruitBasket.db")
cur = conn.cursor()
cur.execute("CREATE TABLE IF NOT EXISTS Fruits (ID INTEGER PRIMARY KEY, Name TEXT, Color TEXT)")
cur.executemany("INSERT INTO Fruits (Name, Color) VALUES (?, ?)", 
                [("Яблуко", "Червоне"), ("Банан", "Жовтий"), ("Апельсин", "Помаранчевий")])
conn.commit()

cur.execute("UPDATE Fruits SET Color = 'Зелене' WHERE Name = 'Яблуко'")
cur.execute("SELECT * FROM Fruits WHERE Color = 'Жовтий'")
print("Жовті фрукти:", cur.fetchall())

cur.execute("SELECT * FROM Fruits")
print("Усі фрукти:", cur.fetchall())

conn.close()
