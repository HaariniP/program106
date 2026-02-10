# program106
import sqlite3
conn = sqlite3.connect("school.db")
cursor = conn.cursor()
cursor.execute("""
CREATE TABLE IF NOT EXISTS Students (
    StudentID INTEGER PRIMARY KEY AUTOINCREMENT,
    Name TEXT NOT NULL,
    Age INTEGER,
    Grade TEXT)
""")
conn.commit()
students = [("Alice", 20, "A"), ("Bob", 21, "B"), ("Charlie", 19, "A")]
cursor.executemany("INSERT INTO Students (Name, Age, Grade) VALUES (?, ?, ?)", students)
conn.commit()
print("All Students:")
cursor.execute("SELECT * FROM Students")
for row in cursor.fetchall():
    print(row)
cursor.execute("DELETE FROM Students WHERE StudentID = ?", (2,))
conn.commit()
print("\nStudents After Deletion:")
cursor.execute("SELECT * FROM Students")
for row in cursor.fetchall():
    print(row)
conn.close()
