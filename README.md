# Student-log-b
import tkinter
import tkinter  as tk
from tkinter import *
import mysql.connector
import mysql.connector
from mysql.connector import Error



# creates a Tk() object
master = Tk()

# sets the geometry of main
 # root window
master.geometry("800x400")


# function to open a new window
# on a button click

L0 = tkinter.Label( text="   WELCOME TO STUDENT LOG BOOK \nPlease enter your correct information\n",font=('arial', 10), fg='black')
L0.grid(row=0, column=1)
L1 = tkinter.Label(master, text="Name ", font=('arial', 20), fg='blue')
L1.grid(row=2, column=0)
E1 = tkinter.Entry(master, bd=5, width=50)
E1.grid(row=2, column=1)

L2 = tkinter.Label(master, text="age ", font=('arial', 20), fg='blue')
L2.grid(row=3, column=0)
E2 = tkinter.Entry(master, bd=5, width=50)
E2.grid(row=3, column=1)
L3 = tkinter.Label(master, text="Roll no ", font=('arial', 20), fg='blue')
L3.grid(row=4, column=0)
E3 = tkinter.Entry(master, bd=5, width=50)
E3.grid(row=4, column=1)
L4 = tkinter.Label(master, text="Student college ", font=('arial', 20), fg='blue')
L4.grid(row=5, column=0)
E4 = tkinter.Entry(master, bd=5, width=50)
E4.grid(row=5, column=1)
L5 =Label(master, text=" **THANK YOU**  ", font=('arial', 20), fg='brown')
L5.grid(row=12, column=1)

def mainprogram():
    print("Name is: ", E1.get())
    print("age is: ", E2.get())
    print("roll number is: ", E3.get())
    print("student college name is: ", E4.get())


mydb = mysql.connector.connect(host='localhost',
                                   database='my',
                                   port='3306',
                                   user='root',  # default user name is root
                                   password='Akshada13@')

cursor = mydb.cursor()
try:



    Insert_query = lambda :"INSERT INTO  student VALUES(name,age,roll no,studentcol)"
    cursor.execute(Insert_query)
    mydb.commit()
    print("Table inserted successfully")
except Error as e:
     print("Error while inserting data to db", e)
     mydb.rollback()
finally :
    mydb.close ( )
    print("db ended successfully")



def new_win():
     my_w = tk.Tk()
     my_w.geometry("800x150")

     my_connect = mysql.connector.connect(
         host="localhost",
         user="root",
         passwd="Akshada13@",
         database="my"
     )

     my_conn = my_connect.cursor()
     ####### end of connection ####
     my_conn.execute("SELECT * FROM student limit 0,10 ")
     i = 0
     for student in my_conn:
         for j in range(len(student)):
             e = Entry(my_w, width=30, fg='blue')
             e.grid(row=i, column=j)
             e.insert(END, student[j])
         i = i + 1



BInsert = Button(master,text='INSERT',fg='White' , bg='brown',font=('arial' , 13 , 'bold'),command=lambda :mainprogram())
BInsert.grid(row=8, column=0)

BUpdate = Button(master,text='SHOW',fg='White' , bg='brown',font=('arial' , 13 , 'bold'),command=lambda :new_win())
BUpdate.grid(row=8, column=1)

mainloop()




