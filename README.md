import sqlite3
def createpatient():
connection = sqlite3.connect("patient.db")
cursor = connection.cursor()
sql_cmd ="""CREATE TABLE records(p_ID INTEGER
PRIMARY KEY,Name TEXT,Mobile_Number TEXT,Gender
TEXT,ailment TEXT,consultant TEXT);"""
cursor.execute(sql_cmd)
cursor.close()
def droptpatient():
connection = sqlite3.connect("patient.db")
cursor = connection.cursor()
cursor.execute("""DROP TABLE records;""")
cursor.close()
def addpatient():
connection = sqlite3.connect("patient.db")
connection2=sqlite3.connect("hospital.db")
cursor2=connection2.cursor()
cursor = connection.cursor()
name=input("\n\t\t\tENTER NAME : ")
idn=int(input("\n\t\t\tENTER ID : "))
mb=input("\n\t\t\tENTER MOBILE NUMBER : ")
gender=input("\n\t\t\tENTER GENDER : ")
sql = """SELECT DISTINCT Designation FROM records"""
cursor2.execute(sql)
result1=cursor2.fetchall()
print("----------------SPECILIZATION -----------------")
for r in result1:
print("|\t\tDESIGNATIONS : ",r[0])
print(" ----------------------------------------------")
ail=input("\n\t\t\tENTER THE SPECILIZATION : ")
sql="""SELECT Name FROM records WHERE Designation =?"""
cursor2.execute(sql,(ail,))
result=cursor2.fetchall()
print("----------------DOCTOR LIST -----------------")
for r in result:
print("|\t\tNAME : ",r[0])

23
print("-------------------------------------------- ")
design = input("\n\t\t\tENTER AILMENT : ")
shift=input("\n\t\t\tENTER CONSULTANT : ")
cl=(idn,name,mb,gender,design,shift)
cursor.execute("INSERT INTO records VALUES (?,?,?,?,?,?)",cl)
connection.commit()
connection2.commit()
cursor2.close()
cursor.close()
def displaypatient():
connection = sqlite3.connect("patient.db")
cursor = connection.cursor()
cursor.execute("SELECT * FROM records")
result=cursor.fetchall()
for r in result:
print(" -------------------------------------")
print("|\t\tID : ",r[0])
print("|\t\tNAME : ",r[1])
print("|\t\tMOBILE NUMBER : ",r[2])
print("|\t\tGENDER : ",r[3])
print("|\t\tAILMENT : ",r[4])
print("|\t\tCONSULTANT : ",r[5])
print(" -------------------------------------")
def droppatient():
connection = sqlite3.connect("patient.db")
cursor = connection.cursor()
temp=int(input("\n\t\tENTER THE ID TO BE REMOVED : "))
sql="""DELETE FROM records WHERE p_ID=?"""
connection.execute(sql,(temp,))
print("\n\t\t-----------DATA REMOVED SUCCESSFULLY------------
")
connection.commit()
cursor.close()
def searchpatient():
connection = sqlite3.connect("patient.db")
cursor = connection.cursor()
temp = int(input("\n\t\tENTER THE ID TO BE SEARCHED : "))

24

sql="""SELECT * FROM records WHERE p_ID=?"""
cursor.execute(sql,(temp,))
result=cursor.fetchone()
print(result)
connection.commit()
cursor.close()
def updatepatient():
connection = sqlite3.connect("patient.db")
cursor = connection.cursor()
temp=int(input("\n\t\tENTER THE ID TO BE UPDATED : "))
inloop=1
while(inloop==1):
print("\n\t\tWHAT DO YOU WANT TO UPDATE ")
print("\t\t1.NAME ")
print("\t\t2.MOBILE NUMBER")
print("\t\t3.GENDER")
print("\t\t4.AILMENT")
print("\t\t5.CONSULTANT")
print("\t\t6.EXIT")
opt=int(input("\n\t\tENTER YOUR CHOSE : "))
if(opt==1):
chan=input("\n\tENTER THE NAME : ")
sql="""UPDATE records SET Name = ? WHERE p_ID = ?"""
connection.execute(sql,(chan,temp,))
connection.commit()
print("\n\t-----------UPDATED SUCCESSFULLY ------ ")
elif(opt==2):
chan = input("\n\tENTER THE MOBILE NUMBER : ")
sql = """UPDATE records SET Mobile_Number = ? WHERE
p_ID = ?"""
connection.execute(sql, (chan, temp,))
connection.commit()
print("\n\t-----------UPDATED SUCCESSFULLY ------ ")
elif(opt==3):
chan = input("\n\tENTER THE GENDER : ")
sql = """UPDATE records SET Gender = ? WHERE p_ID =
?"""
connection.execute(sql, (chan, temp,))

25

connection.commit()
print("\n\t-----------UPDATED SUCCESSFULLY ------ ")
elif(opt==4):
chan = input("\n\tENTER THE DESIGNATION : ")
sql = """UPDATE records SET ailment = ? WHERE p_ID =
?"""
connection.execute(sql, (chan, temp,))
connection.commit()
print("\n\t-----------UPDATED SUCCESSFULLY ------ ")
elif(opt==5):
chan = input("\n\tENTER THE SHIFT : ")
sql = """UPDATE records SET consultant = ? WHERE p_ID =
?"""
connection.execute(sql, (chan, temp,))
connection.commit()
print("\n\t-----------UPDATED SUCCESSFULLY ------ ")

--"))
elif(opt==6):
inloop=0
else:
print(("\n\t--------------------INVALID CHOSE-----------------------
cursor.close()
def create():
connection = sqlite3.connect("hospital.db")
cursor = connection.cursor()
sql_cmd ="""CREATE TABLE records(p_ID INTEGER
PRIMARY KEY,Name TEXT,Mobile_Number TEXT,Gender
TEXT,Designation TEXT,Shift TEXT);"""
cursor.execute(sql_cmd)
cursor.close()
def dropt():
connection = sqlite3.connect("hospital.db")
cursor = connection.cursor()
cursor.execute("""DROP TABLE records;""")
cursor.close()
def add():
connection = sqlite3.connect("hospital.db")
cursor = connection.cursor()
name=input("\n\t\t\tENTER NAME : ")

26
idn=int(input("\n\t\t\tENTER ID : "))
mb=input("\n\t\t\tENTER MOBILE NUMBER : ")
gender=input("\n\t\t\tENTER GENDER : ")
design=input("\n\t\t\tENTER DESIGNATION : ")
shift=input("\n\t\t\tENTER SHIFT : ")
cl=(idn,name,mb,gender,design,shift)
cursor.execute("INSERT INTO records VALUES (?,?,?,?,?,?)",cl)
connection.commit()
cursor.close()
def display():
connection = sqlite3.connect("hospital.db")
cursor = connection.cursor()
cursor.execute("SELECT * FROM records")
result=cursor.fetchall()
for r in result:
print(" -------------------------------------")
print("|\t\tID : ",r[0])
print("|\t\tNAME : ",r[1])
print("|\t\tMOBILE NUMBER : ",r[2])
print("|\t\tGENDER : ",r[3])
print("|\t\tDESIGNATION : ",r[4])
print("|\t\tSHIFT : ",r[5])
print(" -------------------------------------")
def drop():
connection = sqlite3.connect("hospital.db")
cursor = connection.cursor()
temp=int(input("\n\t\tENTER THE ID TO BE REMOVED : "))
sql="""DELETE FROM records WHERE p_ID=?"""
connection.execute(sql,(temp,))
print("\n\t\t-----------DATA REMOVED SUCCESSFULLY------------
")
connection.commit()
cursor.close()
def search():
connection = sqlite3.connect("hospital.db")
cursor = connection.cursor()
temp = int(input("\n\t\tENTER THE ID TO BE SEARCHED : "))
sql="""SELECT * FROM records WHERE p_ID=?"""

27

cursor.execute(sql,(temp,))
result=cursor.fetchone()
print(result)
connection.commit()
cursor.close()
def update():
connection = sqlite3.connect("hospital.db")
cursor = connection.cursor()
temp=int(input("\n\t\tENTER THE ID TO BE UPDATED : "))
inloop=1
while(inloop==1):
print("\n\t\tWHAT DO YOU WANT TO UPDATE ")
print("\t\t1.NAME ")
print("\t\t2.MOBILE NUMBER")
print("\t\t3.GENDER")
print("\t\t4.DESIGNATION")
print("\t\t5.SHIFT")
print("\t\t6.EXIT")
opt=int(input("\n\t\tENTER YOUR CHOSE : "))
if(opt==1):
chan=input("\n\tENTER THE NAME : ")
sql="""UPDATE records SET Name = ? WHERE p_ID = ?"""
connection.execute(sql,(chan,temp,))
connection.commit()
print("\n\t-----------UPDATED SUCCESSFULLY ------ ")
elif(opt==2):
chan = input("\n\tENTER THE MOBILE NUMBER : ")
sql = """UPDATE records SET Mobile_Number = ? WHERE
p_ID = ?"""
connection.execute(sql, (chan, temp,))
connection.commit()
print("\n\t-----------UPDATED SUCCESSFULLY ------ ")
elif(opt==3):
chan = input("\n\tENTER THE GENDER : ")
sql = """UPDATE records SET Gender = ? WHERE p_ID =
?"""
connection.execute(sql, (chan, temp,))
connection.commit()

28

print("\n\t-----------UPDATED SUCCESSFULLY-------")
elif(opt==4):
chan = input("\n\tENTER THE DESIGNATION : ")
sql = """UPDATE records SET Designation = ? WHERE p_ID
= ?"""
connection.execute(sql, (chan, temp,))
connection.commit()
print("\n\t-----------UPDATED SUCCESSFULLY ------ ")
elif(opt==5):
chan = input("\n\tENTER THE SHIFT : ")
sql = """UPDATE records SET Shift = ? WHERE p_ID = ?"""
connection.execute(sql, (chan, temp,))
connection.commit()
print( "\n\t-----------UPDATED SUCCESSFULLY ------")
elif(opt==6):
inloop=0
else:
print(("\n\t--------------------INVALID CHOSE-----------------------
--"))
cursor.close()
#------------------------------------------------------------------------------------------
--------------------------------------------------------------------------#

loopout=1;
while(loopout==1):
print("\n\t\t\t------------------------------ HOSPITAL MANAGEMENT
SYSTEM----------------------------------- ")
ch=int(input("\n\t\t\t1.PATIENT PORTAL \n\t\t\t2.DOCTORS
PORTAL \n\t\t\t3.ADMINISTRATION PORTAL \n\t\t\t4.EXIT
\n\t\t\tENTER YOUR CHOSE : "))
print("\n\t\t\t------------------------------------------------------------------------
---------------------")
if(ch==1):
fist=1
while(fist==1):
print("\n\t\t\t ---------------------PATIENT PORTAL--------------------
------")

29

print("\n\t\t\t\t\t\t\t\t\t\tMENU")
print("\t\t\t\t1.ADD INFO")
print("\t\t\t\t2.DISPLAY INFO")
print("\t\t\t\t3.SEARCH INFO")
print("\t\t\t\t4.UPDATE INFO")
print("\t\t\t\t5.DELETE INFO")
print("\t\t\t\t6.EXIT")
print("\n\t\t\t----------------------------------------------------------------- ")
ch = int(input("\n\t\t\tENTER YOUR CHOISE "))
if ch == 1:
addpatient()
elif ch == 2:
displaypatient()
elif ch == 3:
searchpatient()
elif ch == 4:
updatepatient()
elif ch == 5:
droppatient()
elif ch == 6:
fist = 0
else:
print("\n----------------------INVALID CHOISE --------------- ")
elif(ch==2):
fist=1
while (fist == 1):
print("\n\t\t\t ---------------------DOCTORS PORTAL----------------
----------")
print("\n\t\t\t\t\t\t\t\t\t\tMENU")
print("\t\t\t\t1.ADD INFO")
print("\t\t\t\t2.DISPLAY INFO")
print("\t\t\t\t3.SEARCH INFO")
print("\t\t\t\t4.UPDATE INFO")
print("\t\t\t\t5.DELETE INFO")
print("\t\t\t\t6.EXIT")
print("\n\t\t\t-------------------------------------------------------------- ")
ch = int(input("\n\t\t\tENTER YOUR CHOISE "))
if ch == 1:

30

add()
elif ch == 2:
display()
elif ch == 3:
search()
elif ch == 4:
update()
elif ch == 5:
drop()
elif ch == 6:
fist = 0
else:
print("\n----------------------INVALID CHOISE--------------- ")
elif(ch==3):
ap=1
while(ap==1):
print("\n\t\t\t-------------------------------- ADMINISTRATION
PORTAL-------------------------------------- ")
fist=int(input(" \n\t\t\t1.DEVELOPER \n\t\t\t2.EXIT
\n\t\t\tENTER YOUR CHOSE : "))
print("\n\t\t\t---------------------------------------------------------------------
------------------------")
while(fist==1):
i=5
code=int(input("\n\t\tENTER THE ACCESS CODE : "))
if(code==1818):
while(fist==1):
print("\n\t\t\t--------------------------------- DEVELOPER
ENVIRONMENT ----------------------------------------------")

loop=int(input("\n\t\t\t1.CREATE DOCTOR RECORDS
\n\t\t\t2.DELETE DOCTOR RECORDS \n\t\t\t3.CREATE PATIENT
RECORD \n\t\t\t4.DELETE PATIENT
RECORD\n\t\t\t5.EXIT\n\n\t\tENTER YOUR CHOSE : "))

print("\n\t\t\t---------------------------------------------------------------

------------------------------")
if loop==1:
create()
elif loop==2:
dropt()

31

elif loop==3:

createpatient()
elif loop==4:
droptpatient()
elif loop==5:
fist=0
else:
print("\n\t------INVALID CHOSE------ ")
else:
print("\n\t\t\tPLEASE ENTER THE CORRECT

PASSWORD YOU HAVE ",i-1,"TRIES LEFT")

--i
if(i==0):
break
else:
pass
if(fist==2):
ap=0
elif(ch==4):
loopout=0
else:
print("\n\t\t\t--------------------INVALID CHOSE--------------------------
--------")
