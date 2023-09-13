# Python-Conmector

print()
print()

#mysql credentials declaration
def connection():
     global a
     global b
     global c
     global d
     a=str(input("host:"))
     b=str(input("passwd:"))
     c=str(input("user:"))
     d=str(input("auth_plugin:"))
#mysql connection and datbase creation
connection()
import mysql.connector as him
con=him.connect(host=a,
                passwd=b,
                user=c,
                auth_plugin=d)   
if con.is_connected():
    print ("your connection to sql is established.")
    e=con.cursor()
    e.execute("CREATE DATABASE IF NOT EXISTS HOTEL")
    e.execute("COMMIT")
else:
    print("you've entered the wrong credentials. try again !!!")

#mysql database connection 
def mysql_connection():
    global con    
    con=him.connect(host=a,
                    passwd=b,
                    user=c,
                    database='HOTEL',
                    auth_plugin=d)
    if con.is_connected():
        print ("congratulations!!! your connection to sql database is established.")
mysql_connection()

print("WELCOME TO HOTEL MANAGEMENT SYSTEM... ")

#choices

def choices(): 
      print ("1.Guest information") #customer table  
      print ("2.Booking record")   #booking table
      print ("3.Employees info.")  #Employee table 
      print ("4.Room info")   #room table
      print ("5.Room availibility/fares")   #roomtype table
      print ("6.Internet bills") #speed,usage,amount
      print ("7.Cars bill") #luxury car options , no. of days , amount
      print ("8.Restraunt bill") #breakfat , lunch , dinner , extra snacks 
      print ("9.Casino bill")  #games played , amount bet , amount lost , gain , profit
      print ("1o.Guest Reviews") #feedback table
      global p
      p=int(input("Enter your Choice: "))


def secondary_choices():
    print ("1.To add a new record")
    print ("2.Show a record.")
    print ("3.Delete a record.")
    print ("4.Show the complete table.")


def leisure_choices():
    print("...Enter the IDs....")
    global q
    if (p==5):
       q=str(input("your choice: "))
    else:
       q=int(input("your choice: "))  

def cursor():
    global e
    e=con.cursor()

cursor()


def guest():
    e.execute("CREATE TABLE GUEST(GUEST_ID INTEGER PRIMARY KEY,GUEST_NAME VARCHAR(25), ADDRESS VARCHAR(100), CONTACT_NO BIGINT, AGE INTEGER, EMAIL VARCHAR(100), ID_PROOF BLOB)")
    e.execute("ALTER TABLE GUEST DROP COLUMN ID_PROOF")
    sql=("INSERT INTO GUEST(GUEST_ID, GUEST_NAME, ADDRESS, CONTACT_NO, AGE, EMAIL) VALUES(%s,%s,%s,%s,%s,%s)")
    val=[("100","HIMANSH","10 DOWNING STREET","9415076287","19","HIMANSH12@GMAIL.COM"),
         ("101","SHRIYA","THE WINTER PALACE","9839228389","17","SHRIYA12@GMAIL.COM"),
         ("102","SIKHAR","THE HYDERABAD HOUSE","9083437422","28","SIKHAR12@GMAIL.COM")]
    e.executemany(sql,val)
    e.execute("COMMIT") 


def booking():
    e.execute("CREATE TABLE BOOKING (BOOKING_ID VARCHAR(25) PRIMARY KEY,ROOM_ID VARCHAR(50),GUEST_ID INTEGER , BOOKING_DATE DATE , CHECK_IN DATETIME , CHECK_OUT DATETIME)")
    sql5=("INSERT INTO BOOKING (BOOKING_ID, ROOM_ID, GUEST_ID , BOOKING_DATE , CHECK_IN , CHECK_OUT) VALUES (%s,%s,%s,%s,%s,%s)")
    val5=[("AB10","A100","100","2022-02-01","2022-02-07 16:00:00","2022-02-10 20:00:00"),
          ("AB20","B200","101","2022-02-05","2022-02-10 15:00:00","2022-02-13 15:30:00"),
          ("AB30","B300","102","2022-03-05","2022-03-06 20:00:00","2022-03-08 22:00:00")]
    e.executemany(sql5,val5)
    e.execute("COMMIT") 

def employee():
    e.execute("CREATE TABLE EMPLOYEE (EMPLOYEE_ID VARCHAR(25) PRIMARY KEY , EMPLOYEE_NAME VARCHAR(50) ,EMPLOYEE_TYPE VARCHAR(50))")
    sql5=("INSERT INTO EMPLOYEE (EMPLOYEE_ID, EMPLOYEE_NAME, EMPLOYEE_TYPE) VALUES (%s,%s,%s)")
    val5=[("EMP100","JOE","HOTEL MANAGER"),
          ("EMP101","VLADIMIR","ROOM ATTENDANT"),
          ("EMP102","KIM","HOTEL RECEPTIONISTS")]
    e.executemany(sql5,val5)
    e.execute("COMMIT")


def room():
    e.execute("CREATE TABLE ROOM (ROOM_NUMBER VARCHAR(25) PRIMARY KEY ,STATUS VARCHAR(50))")
    sql5=("INSERT INTO ROOM (ROOM_NUMBER , STATUS) VALUES (%s,%s)")
    val5=[("ROOM100", "FILLED"),
          ("ROOM101","UNFILLED"),
          ("ROOM102","FILLED")]
    e.executemany(sql5,val5)
    e.execute("COMMIT")


def roomtype():
    e.execute("CREATE TABLE ROOMTYPE (ROOM_NUMBER VARCHAR(25) PRIMARY KEY , ROOM_TYPE VARCHAR(150), DESCRIPTION VARCHAR(200) , COST INTEGER ,STATUS VARCHAR(30))")
    sql5=("INSERT INTO ROOMTYPE (ROOM_NUMBER , ROOM_TYPE , DESCRIPTION , COST , STATUS) VALUES (%s,%s,%s,%s,%s)")
    val5=[("ROOM100", "TWIN BED","2 single beds","5000","FILLED"),
          ("ROOM101","QUEEN","1 double bed","10000","UNFILLED"),
          ("ROOM102","EXECUTIVE","1 double bed, more facilities than Queen","15000","FILLED"),
          ("ROOM103","SUITE","2 double beds, most luxurious","20000","UNFILLED")]
    e.executemany(sql5,val5)
    e.execute("COMMIT") 


def internet_bills():
    e.execute("CREATE TABLE INTERNET (INTERNET_ID INTEGER PRIMARY KEY , DATA_SPEED VARCHAR(150), COST INTEGER)")
    sql5=("INSERT INTO INTERNET (INTERNET_ID , DATA_SPEED ,COST) VALUES (%s,%s,%s)")
    val5=[("1", "100 MBPS","600"),
          ("2","200 MBPS","800"),
          ("3","300 MBPS","1000"),
          ("4","400 MBPS","1200")]
    e.executemany(sql5,val5)
    e.execute("COMMIT") 


def car_bills():
    e.execute("CREATE TABLE CARS (CAR_ID INTEGER PRIMARY KEY , CAR_NAME VARCHAR(150), COST_DAY INTEGER)")
    sql5=("INSERT INTO CARS (CAR_ID , CAR_NAME, COST_DAY) VALUES (%s,%s,%s)")
    val5=[("1", "LAMBORGHINI URUS","20000"),
          ("2","E-RICKSHAW","1000"),
          ("3","TATA SUMO","100"),
          ("4","BOLERO","500")]
    e.executemany(sql5,val5)
    e.execute("COMMIT") 


def food_bills():
    e.execute("CREATE TABLE FOOD (FOOD_ID INTEGER PRIMARY KEY , FOOD_NAME VARCHAR(150), COST INTEGER)")
    sql5=("INSERT INTO FOOD (FOOD_ID , FOOD_NAME, COST) VALUES (%s,%s,%s)")
    val5=[("1", "MEXICAN FOOD","800"),
          ("2","CHINESE FOOD","300"),
          ("3","ITALIAN FOOD","500"),
          ("4","INDIAN FOOD","200")]
    e.executemany(sql5,val5)
    e.execute("COMMIT") 

def casino_bills():
    e.execute("CREATE TABLE CASINO (GAMES_ID INTEGER PRIMARY KEY , GAMES_NAME VARCHAR(150), ENTRY_COST INTEGER)")
    sql5=("INSERT INTO CASINO (GAMES_ID , GAMES_NAME, ENTRY_COST) VALUES (%s,%s,%s)")
    val5=[("1", "POKER","800"),
          ("2","ROULETTE","700"),
          ("3","BLACKJACK","600"),
          ("4","BACCARAT","500")]
    e.executemany(sql5,val5)
    e.execute("COMMIT")

def guest_reviews():
    e.execute("CREATE TABLE REVIEWS (GUEST_ID INTEGER PRIMARY KEY , GUEST_REVIEW VARCHAR(250))")
    e.execute("COMMIT")


def choice_selection():
    global f
    f=int(input("ENTER YOUR CHOICE: "))
    if f==1:
       ab=str(input("GUEST_ID: ")) 
       ac=str(input("GUEST_NAME: "))
       ad=str(input("ADDRESS: "))
       ae=str(input("CONTACT_NO: "))
       af=str(input("AGE: "))
       ag=str(input("EMAIL: "))
       sql1=("INSERT INTO GUEST VALUES (%s,%s,%s,%s,%s,%s)")
       val1=(ab,ac,ad,ae,af,ag)
       e.execute(sql1,val1)
       e.execute("COMMIT")
       print ("RECORD ENTERED SUCCESSFULLY !!!")
    elif f==2:
       sql3="SELECT * FROM GUEST WHERE GUEST_ID=%s"
       ah=str(input("ENTER THE GUEST_ID:"))
       e.execute(sql3,(ah,))
       abc=e.fetchall()
       if abc:
           print(abc)
       else:
           print("WRONG INPUT !!!")
    elif f==3:
        sql4="DELETE FROM GUEST WHERE GUEST_ID=%s"
        ai=str(input("ENTER THE GUEST_ID TO DELETE:"))
        e.execute(sql4,(ai,))
        e.execute("COMMIT")
    else:
        e.execute("SELECT * FROM GUEST")
        abd=e.fetchall()
        for y in abd:
            print(y)

def loop():
        while (f<10):
            abj=int(input("PRESS 1 FOR MORE SECONDARY CHOICE AND 2 TO EXIT : "))
            if (abj==1):
                secondary_choices()
                choice_selection()
            else:
                break


def choice_selection1():
    global h
    h=int(input("ENTER YOUR CHOICE: "))
    if h==1:
       ab=str(input("BOOING_ID: ")) 
       ac=str(input("ROOM_ID: "))
       ad=str(input("GUEST_ID: "))
       ae=str(input("BOOKING_DATE: "))
       af=str(input("CHECK_IN: "))
       ag=str(input("CHECK_OUT: "))
       sql1=("INSERT INTO BOOKING VALUES (%s,%s,%s,%s,%s,%s)")
       val1=(ab,ac,ad,ae,af,ag)
       e.execute(sql1,val1)
       e.execute("COMMIT")
       print ("RECORD ENTERED SUCCESSFULLY !!!")
    elif h==2:
       sql3="SELECT * FROM BOOKING WHERE GUEST_ID=%s"
       ah=str(input("ENTER THE GUEST_ID:"))
       e.execute(sql3,(ah,))
       abc=e.fetchall()
       if abc:
           print(abc)
       else:
           print("WRONG INPUT !!!")
    elif h==3:
        sql4="DELETE FROM BOOKING WHERE GUEST_ID=%s"
        ai=str(input("ENTER THE GUEST_ID TO DELETE:"))
        e.execute(sql4,(ai,))
        e.execute("COMMIT")
    else:
        e.execute("SELECT * FROM BOOKING")
        abd=e.fetchall()
        for y in abd:
            print(y)


def loop1():
    while (h<10):
        abj=int(input("PRESS 1 FOR MORE SECONDARY CHOICE AND 2 TO EXIT : "))
        if (abj==1):
            secondary_choices()
            choice_selection1()
        else:
            break    


def choice_selection2():
    global h
    h=int(input("ENTER YOUR CHOICE: "))
    if h==1:
       ab=str(input("EMPLOYEE_ID: ")) 
       ac=str(input("EMPLOYEE_NAME: "))
       ad=str(input("EMPLOYEE_TYPE: "))
       sql1=("INSERT INTO EMPLOYEE VALUES (%s,%s,%s)")
       val1=(ab,ac,ad)
       e.execute(sql1,val1)
       e.execute("COMMIT")
       print ("RECORD ENTERED SUCCESSFULLY !!!")
    elif h==2:
       sql3="SELECT * FROM EMPLOYEE WHERE EMPLOYEE_ID=%s"
       ah=str(input("ENTER THE EMPLOYEE_ID:"))
       e.execute(sql3,(ah,))
       abc=e.fetchall()
       if abc:
           print(abc)
       else:
           print("WRONG INPUT !!!")
    elif h==3:
        sql4="DELETE FROM EMPLOYEE WHERE EMPLOYEE_ID=%s"
        ai=str(input("ENTER THE GUEST_ID TO DELETE:"))
        e.execute(sql4,(ai,))
        e.execute("COMMIT")
    else:
        e.execute("SELECT * FROM EMPLOYEE")
        abd=e.fetchall()
        for y in abd:
            print(y)

def loop2():
    while (h<10):
        abj=int(input("PRESS 1 FOR MORE SECONDARY CHOICE AND 2 TO EXIT : "))
        if (abj==1):
            secondary_choices()
            choice_selection2()
        else:
            break    


def choice_selection3():
    global h
    h=int(input("ENTER YOUR CHOICE: "))
    if h==1:
       ab=str(input("ROOM_NUMBER: ")) 
       ac=str(input("STATUS: "))
       sql1=("INSERT INTO ROOM VALUES (%s,%s)")
       val1=(ab,ac)
       e.execute(sql1,val1)
       e.execute("COMMIT")
       print ("RECORD ENTERED SUCCESSFULLY !!!")
    elif h==2:
       sql3="SELECT * FROM ROOM WHERE ROOM_NUMBER=%s"
       ah=str(input("ENTER THE ROOM_NUMBER: "))
       e.execute(sql3,(ah,))
       abc=e.fetchall()
       if abc:
           print(abc)
       else:
           print("WRONG INPUT !!!")
    elif h==3:
        sql4="DELETE FROM ROOM WHERE ROOM_NUMBER=%s"
        ai=str(input("ENTER THE ROOM_NUMBER TO DELETE:"))
        e.execute(sql4,(ai,))
        e.execute("COMMIT")
    else:
        e.execute("SELECT * FROM ROOM")
        abd=e.fetchall()
        for y in abd:
            print(y)


def loop3():
    while (h<10):
        abj=int(input("PRESS 1 FOR MORE SECONDARY CHOICE AND 2 TO EXIT : "))
        if (abj==1):
            secondary_choices()
            choice_selection3()
        else:
            break


def ROOMTPYE_BILL1():
        e.execute("SELECT * FROM ROOMTYPE")
        abd=e.fetchall()
        for y in abd:
            print(y)   
            
def INTERNET_BILL1():
        e.execute("SELECT * FROM INTERNET")
        abd=e.fetchall()
        for y in abd:
            print(y)           
            
def CARS_BILL1():
        e.execute("SELECT * FROM CARS")
        abd=e.fetchall()
        for y in abd:
            print(y)           
    

def FOOD_BILL1():
        e.execute("SELECT * FROM FOOD")
        abd=e.fetchall()
        for y in abd:
            print(y)           

def CASINO_BILL1():
        e.execute("SELECT * FROM CASINO")
        abd=e.fetchall()
        for y in abd:
            print(y)           




guest()
booking()
employee()
room()
roomtype()
internet_bills()
car_bills()
food_bills()
casino_bills()
guest_reviews()

res1=0
res2=0
res3=0
res4=0
res5=0


z=1
while (z<10):
    k=int(input("PRESS 1 FOR MORE OPTIONS AND 2 TO EXIT...: "))
    if (k==1):
        choices()
        if (p==1):
            secondary_choices()
            choice_selection()
            loop()    
        elif (p==2):
            secondary_choices()
            choice_selection1()
            loop1()
        elif (p==3):
            secondary_choices()
            choice_selection2()
            loop2()         
        elif (p==4):
            secondary_choices()
            choice_selection3()
            loop3()    
        elif (p==5):
            ROOMTPYE_BILL1()
            leisure_choices()
            sql3="SELECT COST FROM ROOMTYPE WHERE ROOM_NUMBER=%s"
            e.execute(sql3,(q,))
            abcd=e.fetchone()
            res1=int(''.join(map(str,abcd)))
            hp=int(input("NO. OF DAYS: "))
            res1=res1*hp
        elif (p==6):
            INTERNET_BILL1()
            leisure_choices()
            sql3="SELECT COST FROM INTERNET WHERE INTERNET_ID=%s"
            e.execute(sql3,(q,))
            abce=e.fetchone()
            res2=int(''.join(map(str,abce)))
            hr=int(input("NO. OF HOURS: "))
            res2=res2*hr
        elif (p==7):
            CARS_BILL1()
            leisure_choices()
            sql3="SELECT COST_DAY FROM CARS WHERE CAR_ID=%s"
            e.execute(sql3,(q,))
            abcf=e.fetchone()
            res3=int(''.join(map(str,abcf)))
            hs=int(input("NO. OF DAYS: "))
            res3=res3*hs
        elif (p==8):
            FOOD_BILL1()
            leisure_choices()
            sql3="SELECT COST FROM FOOD WHERE FOOD_ID=%s"
            e.execute(sql3,(q,))
            abcg=e.fetchone()
            res4=int(''.join(map(str,abcg)))
            ht=int(input("NO. OF PLATES: "))
            res4=res4*ht
        elif (p==9):
            CASINO_BILL1()
            leisure_choices()
            sql3="SELECT ENTRY_COST FROM CASINO WHERE GAMES_ID=%s"
            e.execute(sql3,(q,))
            abch=e.fetchone()
            res5=int(''.join(map(str,abch)))
        elif (p==10):
            ua=str(input("GUEST_ID: "))
            ub=str(input("YOUR REVIEW: "))
            sql5=("INSERT INTO REVIEWS (GUEST_ID , GUEST_REVIEW) VALUES (%s,%s)")
            val5=(ua,ub)
            e.execute(sql5,val5)
            e.execute("COMMIT")
    else:
        break

 
S=res1+res2+res3+res4+res5  
print("TO GENERATE THE COMPLETE BILL: ")
sql3="SELECT * FROM GUEST WHERE GUEST_ID=%s"
ah=str(input("ENTER THE GUEST_ID: "))
e.execute(sql3,(ah,))
abc=e.fetchall()
if abc:
    print(abc)
print ("THE TOTAL BILL :", S)    
