import sqlite3

# Connect to the database
conn = sqlite3.connect('students.db')
c = conn.cursor()
# Create the table
c.execute('''CREATE TABLE students (student_id INTEGER PRIMARY KEY, 
                                    first_name 
                                    TEXT, 
                                    last_name TEXT, 
                                    major TEXT, 
                                    grad_year INTEGER, 
                                    email TEXT, 
                                    gpa FLOAT)''')
# Insert sample records
students = [
    (1, 'Christina', 'Vu', 'Computer Science', 2027, 'cvu@students.unwsp.edu', '3.6'),
    (2, 'Anna', 'Schellin', 'Computer Science', 2027, 'akschellin@students.unwsp.edu', '3.5'),
    (3, 'Katherine', 'Westrich', 'Computer Science', 2027, 'kmwestrich@students.unwsp.edu', '3.4'),
    (4, 'Alice', 'Brown', 'Biology', 2024, 'abrown@university.edu', '3.3'),
    (5, 'Tom', 'Wilson', 'Mathematics', 2022, 'twilson@university.edu', '3.9'),
    (6, 'Samantha', 'Lee', 'Physics', 2023, 'slee@university.edu', '4.0'),
    (7, 'David', 'Garcia', 'Political Science', 2022, 'dgarcia@university.edu', '3.9'),
    (8, 'Emily', 'Davis', 'Sociology', 2023, 'edavis@university.edu', '3.5'),
    (9, 'Michael', 'Taylor', 'Economics', 2024, 'mtaylor@university.edu', '3.2'),
    (10, 'Karen', 'Clark', 'Psychology', 2022, 'kclark@university.edu', '3.1')
]
c.executemany('INSERT INTO students VALUES (?, ?, ?, ?, ?, ?, ?)', students)
# Save (commit) the changes
conn.commit()
# Close the connection
conn.close()


def main():
    import sqlite3
    # Connect to the database
    conn = sqlite3.connect('students.db')
    c = conn.cursor()
    cursor = conn.execute('SELECT * FROM students')
    for row in cursor:
        print(row)
    # print data
    for row in cursor:
        print(f'{row[0]:<7} {row[1]:<12} {row[2]:<10} {row[3]:<14} {row[4]:<16} {row[5]:<18} {row[6]:<19}')
    # ask user what they want to change
    # use info from user to find wanted change
    record_id = int(input('Enter the ID of the record you want to edit: '))
    field_name = input('Enter the name of the field you want to edit: ')
    new_value = input('Enter the new value of the field: ')
    # update change in database
    conn.execute(f"UPDATE students SET {field_name} = ? WHERE student_id = ?", (new_value, record_id))
    # commit the changes to the database
    conn.commit()
    # select new updated data from students database
    cursor = conn.execute('SELECT * FROM students')
    # print updated data
    for row in cursor:
        print(f'{row[0]:<7} {row[1]:<12} {row[2]:<10} {row[3]:<14} {row[4]:<16} {row[5]:<18} {row[6]:<19}')
    # close the connection
    conn.close()


# call main Function
if __name__ == "__main__":
    main()
SAMPLE RUN:
(1, 'Christina', 'Vu', 'Computer Science', 2027, 'cvu@students.unwsp.edu', 3.6)
(2, 'Anna', 'Schellin', 'Computer Science', 2027, 'akschellin@students.unwsp.edu', 3.5)
(3, 'Katherine', 'Westrich', 'Computer Science', 2027, 'kmwestrich@students.unwsp.edu', 3.4)
(4, 'Alice', 'Brown', 'Biology', 2024, 'abrown@university.edu', 3.3)
(5, 'Tom', 'Wilson', 'Mathematics', 2022, 'twilson@university.edu', 3.9)
(6, 'Samantha', 'Lee', 'Physics', 2023, 'slee@university.edu', 4.0)
(7, 'David', 'Garcia', 'Political Science', 2022, 'dgarcia@university.edu', 3.9)
(8, 'Emily', 'Davis', 'Sociology', 2023, 'edavis@university.edu', 3.5)
(9, 'Michael', 'Taylor', 'Economics', 2024, 'mtaylor@university.edu', 3.2)
(10, 'Karen', 'Clark', 'Psychology', 2022, 'kclark@university.edu', 3.1)
Enter the ID of the record you want to edit: 3
Enter the name of the field you want to edit: first_name
Enter the new value of the field: Katie
1       Christina    Vu         Computer Science 2027             cvu@students.unwsp.edu 3.6                
2       Anna         Schellin   Computer Science 2027             akschellin@students.unwsp.edu 3.5                
3       Katie        Westrich   Computer Science 2027             kmwestrich@students.unwsp.edu 3.4                
4       Alice        Brown      Biology        2024             abrown@university.edu 3.3                
5       Tom          Wilson     Mathematics    2022             twilson@university.edu 3.9                
6       Samantha     Lee        Physics        2023             slee@university.edu 4.0                
7       David        Garcia     Political Science 2022             dgarcia@university.edu 3.9                
8       Emily        Davis      Sociology      2023             edavis@university.edu 3.5                
9       Michael      Taylor     Economics      2024             mtaylor@university.edu 3.2                
10      Karen        Clark      Psychology     2022             kclark@university.edu 3.1   
