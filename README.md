#Hotel Management
import random
import datetime
import mysql.connector as m

# Global  Declaration
global cid
room=" "


#MODULE TO ESTABLISHED MYSQL CONNECTION
def MYSQLconnection():
    
    global myConnection
    userName = input("\n ENTER MYSQL SERVER'S USERNAME : ")
    password = input("\n ENTER MYSQL SERVER'S PASSWORD : ")
    myConnection=m.connect(host="localhost",user=userName,passwd=password)
    cursor=myConnection.cursor()
    cursor.execute("CREATE DATABASE IF NOT EXISTS HMS")
    cursor.execute("COMMIT")
    cursor.close()
        

print("ENTER DETAILS FOR CONNECTION")
MYSQLconnection()
print()
print("SUCCESSFULLY CONNECTED")
# Home Function
def Home():
    print()
    print("\t\t\t\t\t\t WELCOME TO HOTEL ANCASA\n")    
    print("\t\t\t 1 Booking\n")
    print("\t\t\t 2 Rooms Info\n")
    print("\t\t\t 3 Room Service(Menu Card)\n")
    print("\t\t\t 4 Gaming\n")
    print("\t\t\t 5 Payment\n")
    print("\t\t\t 6 Record\n")
    print("\t\t\t 0 Exit\n")

    ch=int(input("->"))

    if ch == 1:
        print(" ")
        Booking()
            

    elif ch == 2:
        print(" ")
        Rooms_Info()

    elif ch == 3:
        print(" ")
        restaurant()

    elif ch == 4:
        print(" ")
        Gaming()

    elif ch == 5:
        print(" ")
        Payment()
        
    elif ch == 6:
        print(" ")
        Record()
    
    else:
        exit()

# Function used in booking

def date(c):
    if c[2] >= 2024 and c[2] <= 2025:
            
        if c[1] != 0 and c[1] <= 12:
                    
            if c[1] == 2 and c[0] != 0 and c[0] <= 31:
                    
                if c[2]%4 == 0 and c[0] <= 29:
                    pass
                    
                elif c[0]<29:
                    pass
                    
                else:
                    print("Invalid date\n")
                    Booking()
                    
                    
            # if month is odd & less than equal
            # to 7th month
            elif c[1] <= 7 and c[1]%2 != 0 and c[0] <= 31:
                pass

            # if month is even & less than equal to 7th
            # month and not 2nd month
            elif c[1] <= 7 and c[1]%2 == 0 and c[0] <= 30 and c[1] != 2:
                pass

            # if month is even & greater than equal
            # to 8th month
            elif c[1] >= 8 and c[1]%2 == 0 and c[0] <= 31:
                pass

            # if month is odd & greater than equal
            # to 8th month
            elif c[1]>=8 and c[1]%2!=0 and c[0]<=30:
                pass
                    
            else:
                print("Invalid date\n")
                Booking()
                            
        else:
            print("Invalid date\n")
            Booking()
                    
    else:
        print("Invalid date\n")
        Booking()
# Booking function
def Booking():
    global myConnection
    # used global keyword to
    # use global variable 'i'
    global i
    print(" BOOKING ROOMS")
    print(" ")

    
    name = input("Name: ")
    phone_no = input("Phone No.: ")
    cursor=myConnection.cursor()
    cursor.execute("USE HMS")
    # cursor.execute("Create Table IF NOT EXISTS C_DETAILS")
    # sql='SELECT* FROM C_DETAILS'
    # cursor.execute(sql)
    # data=cursor.fetchall()
    # for j in data:
    #     if j[4]==phone_no:
    #         print("\tPhone no. already exists and payment yet not done..!!")
    #         Booking()
    

    address = input("Address: ")
    nationality = input("Enter Customer Country : ")

    email=input("Email: ")
    
        

            
    cii=str(input("Check-In (DD/MM/YYYY):"))
    CI=cii
    cii=cii.split('/')
    
    ci=cii
    ci[0]=int(ci[0])
    ci[1]=int(ci[1])
    ci[2]=int(ci[2])
    date(ci)

    coo=str(input("Check-Out (DD/MM/YYYY): "))
    CO=coo
    coo=coo.split('/')
    co=coo
    co[0]=int(co[0])
    co[1]=int(co[1])
    co[2]=int(co[2])

    # checks if check-out date falls after
    # check-in date
    if co[1]<ci[1] and co[2]<ci[2]:
            
        print("\n\tErr..!!\n\tCheck-Out date must fall after Check-In\n")
        Booking()
    elif co[1]==ci[1] and co[2]>=ci[2] and co[0]<=ci[0]:
            
        print("\n\tErr..!!\n\tCheck-Out date must fall after Check-In\n")
        Booking()
    else:
        pass

    date(co)
    d1 = datetime.datetime(ci[2],ci[1],ci[0])
    d2 = datetime.datetime(co[2],co[1],co[0])
    d = (d2-d1).days
 

    print("----SELECT ROOM TYPE----")
    print(" 1. Standard Non-AC")
    print(" 2. Standard AC")
    print(" 3. 3-Bed Non-AC")
    print(" 4. 3-Bed AC")
    print(("\t\tPress 0 for Room Prices"))

    ch=int(input("->"))

    # if-conditions to display alloted room
    # type and it's price
    if ch==0:
        print(" 1. Standard Non-AC - Rs. 3500")
        print(" 2. Standard AC - Rs. 4000")
        print(" 3. 3-Bed Non-AC - Rs. 4500")
        print(" 4. 3-Bed AC - Rs. 5000")
        ch=int(input("->"))
    if ch==1:
        room='Standard Non-AC'
        print("Room Type- Standard Non-AC")
        price=3500
        print("Price- 3500")
    elif ch==2:
        room='Standard AC'
        print("Room Type- Standard AC")
        price=4000
  
        print("Price- 4000")
    elif ch==3:
        room='3-Bed Non-AC'
        print("Room Type- 3-Bed Non-AC")
        price=4500
        print("Price- 4500")
    elif ch==4:
        room='3-Bed AC'
        price=5000
        print("Room Type- 3-Bed AC")
        print("Price- 5000")
    else:
        print(" Wrong choice..!!")

    # randomly generating room no. and customer
    # id for customer
    rn = random.randrange(40)+300
    cid = random.randrange(40)+10


    # checks if alloted room no. & customer
    # id already not alloted
   
    rn = random.randrange(60)+300
    cid = random.randrange(60)+10
            
    print("")
    print("\t\t\t***ROOM BOOKED SUCCESSFULLY***\n")
    print("Room No. - ",rn)
    print("Customer Id - ",cid)

   
    cursor=myConnection.cursor()
    cursor.execute("USE HMS")
    cursor.execute("CREATE TABLE IF NOT EXISTS C_DETAILS(CID VARCHAR(20),C_NAME VARCHAR(30),C_ADDRESS VARCHAR(30),C_COUNTRY VARCHAR(30) ,P_NO VARCHAR(30),C_EMAIL VARCHAR(30),CHECK_IN VARCHAR(10) ,CHECK_OUT VARCHAR(10),ROOM_CHOICE VARCHAR(30),NO_OF_DAYS INT(10),ROOMNO INT(5) ,ROOM_PRICE INT(10))")
    sql_insert="insert into C_DETAILS values(""'"+str(cid)+"'," "'"+str(name)+"'," "'"+str(address)+"'," "'"+str(nationality)+"'," "'"+str(phone_no)+"'," "'"+str(email)+"'," "'"+str(CI)+"'," "'"+str(CO)+"'," "'"+str(room)+"'," "'"+str(d)+"'," "'"+str(rn)+"'," "'"+str(price)+"'"")"
    cursor.execute(sql_insert)    
    cursor.execute("COMMIT")
    cursor.close()
    n=int(input("0-BACK\n ->"))
    if n==0:
        Home()
    else:
        exit()

# ROOMS INFO
def Rooms_Info():
    print("		 ------ HOTEL ROOMS INFO ------")
    print("")
    print("STANDARD NON-AC")
    print("---------------------------------------------------------------")
    print("Room amenities include: 1 Double Bed, Television, Telephone,")
    print("Double-Door Cupboard, 1 Coffee table with 2 sofa, Balcony and")
    print("an attached washroom with hot/cold water.\n")
    print("STANDARD NON-AC")
    print("---------------------------------------------------------------")
    print("Room amenities include: 1 Double Bed, Television, Telephone,")
    print("Double-Door Cupboard, 1 Coffee table with 2 sofa, Balcony and")
    print("an attached washroom with hot/cold water + Window/Split AC.\n")
    print("3-Bed NON-AC")
    print("---------------------------------------------------------------")
    print("Room amenities include: 1 Double Bed + 1 Single Bed, Television,")
    print("Telephone, a Triple-Door Cupboard, 1 Coffee table with 2 sofa, 1")
    print("Side table, Balcony with an Accent table with 2 Chair and an")
    print("attached washroom with hot/cold water.\n")
    print("3-Bed AC")
    print("---------------------------------------------------------------")
    print("Room amenities include: 1 Double Bed + 1 Single Bed, Television,")
    print("Telephone, a Triple-Door Cupboard, 1 Coffee table with 2 sofa, ")
    print("1 Side table, Balcony with an Accent table with 2 Chair and an")
    print("attached washroom with hot/cold water + Window/Split AC.\n\n")
    print()
    n=int(input("0-BACK\n ->"))
    if n==0:
            Home()
    else:
            exit()

# RESTAURANT FUNCTION
def restaurant():
    customer=searchCustomer()
    r=0
    if customer:
        
        print("-------------------------------------------------------------------------")
        print("						 Hotel AnCasa")
        print("-------------------------------------------------------------------------")
        print("						 Menu Card")
        print("-------------------------------------------------------------------------")
        print("\n BEVARAGES				             26 Dal Fry................ 140.00")
        print("----------------------------------	 27 Dal Makhani............ 150.00")
        print(" 1 Regular Tea............. 20.00	 28 Dal Tadka.............. 150.00")
        print(" 2 Masala Tea.............. 25.00")
        print(" 3 Coffee.................. 25.00	 ROTI")
        print(" 4 Cold Drink.............. 25.00	----------------------------------")
        print(" 5 Bread Butter............ 30.00	 29 Plain Roti.............. 15.00")
        print(" 6 Bread Jam............... 30.00	 30 Butter Roti............. 15.00")
        print(" 7 Veg. Sandwich........... 50.00	 31 Tandoori Roti........... 20.00")
        print(" 8 Veg. Toast Sandwich..... 50.00	 32 Butter Naan............. 20.00")
        print(" 9 Cheese Toast Sandwich... 70.00")
        print(" 10 Grilled Sandwich........ 70.00	 RICE")
        print("					         ----------------------------------")
        print(" SOUPS				                 33 Plain Rice.............. 90.00")
        print("----------------------------------	 34 Jeera Rice.............. 90.00")
        print(" 11 Tomato Soup............ 110.00	 35 Veg Pulao.............. 110.00")
        print(" 12 Hot & Sour............. 110.00	 36 Peas Pulao............. 110.00")
        print(" 13 Veg. Noodle Soup....... 110.00")
        print(" 14 Sweet Corn............. 110.00	 SOUTH INDIAN")
        print(" 15 Veg. Munchow........... 110.00	 ----------------------------------")
        print("					                     37 Plain Dosa............. 100.00")
        print(" MAIN COURSE				             38 Onion Dosa............. 110.00")
        print("----------------------------------	 39 Masala Dosa............ 130.00")
        print(" 16 Shahi Paneer........... 110.00	 40 Paneer Dosa............ 130.00")
        print(" 17 Kadai Paneer........... 110.00	 41 Rice Idli.............. 130.00")
        print(" 18 Handi Paneer........... 120.00	 42 Sambhar Vada........... 140.00")
        print(" 19 Palak Paneer........... 120.00")
        print(" 20 Chilli Paneer.......... 140.00	 ICE CREAM")
        print(" 21 Matar Mushroom......... 140.00	 ----------------------------------")
        print(" 22 Mix Veg................ 140.00	 43 Vanilla................. 60.00")
        print(" 23 Jeera Aloo............. 140.00	 44 Strawberry.............. 60.00")
        print(" 24 Malai Kofta............ 140.00	 45 Pineapple............... 60.00")
        print(" 25 Aloo Matar............. 140.00	 46 Butter Scotch........... 60.00")
        print("Press 0 -to end ")
        ch=1
        while(ch!=0):
                
            ch=int(input(" -> "))
            
            # if-elif-conditions to assign item
            # prices listed in menu card
            if ch==1 or ch==31 or ch==32:
                rs=20
                r=r+rs
            elif ch<=4 and ch>=2:
                rs=25
                r=r+rs
            elif ch<=6 and ch>=5:
                rs=30
                r=r+rs
            elif ch<=8 and ch>=7:
                rs=50
                r=r+rs
            elif ch<=10 and ch>=9:
                rs=70
                r=r+rs
            elif (ch<=17 and ch>=11) or ch==35 or ch==36 or ch==38:
                rs=110
                r=r+rs
            elif ch<=19 and ch>=18:
                rs=120
                r=r+rs
            elif (ch<=26 and ch>=20) or ch==42:
                rs=140
                r=r+rs
            elif ch<=28 and ch>=27:
                rs=150
                r=r+rs
            elif ch<=30 and ch>=29:
                rs=15
                r=r+rs
            elif ch==33 or ch==34:
                rs=90
                r=r+rs
            elif ch==37:
                rs=100
                r=r+rs
            elif ch<=41 and ch>=39:
                rs=130
                r=r+rs
            elif ch<=46 and ch>=43:
                rs=60
                r=r+rs
            elif ch==0:
                pass
            else:
                print("Wrong Choice..!!")

        cursor=myConnection.cursor()
        cursor.execute("USE HMS")
        cursor.execute("CREATE TABLE IF NOT EXISTS RESTAURENT(CID VARCHAR(20),BILL VARCHAR(30))")                   
        sql= "INSERT INTO RESTAURENT VALUES(""'"+str(cid)+"'," "'"+str(r)+"'"")"
        cursor.execute(sql)
        cursor.execute("COMMIT")

        print("Total Bill: ",r)


    n=int(input("0-BACK\n ->"))
    if n==0:
        Home()
    else:
        exit()


# GAMING FUNCTION
def Gaming():
    customer=searchCustomer()
    r=0
    if customer:
                
        print("-------------------------------------------------------------------------")
        print("			     HOTEL ANCASA")
        print("-------------------------------------------------------------------------")
        print("			     GAMES AVAILABLE")
        print("-------------------------------------------------------------------------")
        print("""
        1. Table Tennis -----> 150 Rs./HR
        2. Bowling -----> 100 Rs./HR
        3. Snooker -----> 250 Rs./HR
        4. VR World Gaming -----> 400 Rs./HR
        5. Video Games -----> 300 Rs./HR
        6. Swimming Pool Games -----> 350 Rs./HR
        7. Exit
        """)
        game=int(input("Enter What Game You Want To Play : "))
        hour=int(input("Enter No Of Hours You Want To Play : "))
        if game==1:
            print("YOU HAVE SELECTED TO PLAY : Table Tennis")
            gamingbill = hour * 150
        elif game==2:
            print("YOU HAVE SELECTED TO PLAY : Bowling")
            gamingbill = hour * 100
        elif game==3:
            print("YOU HAVE SELECTED TO PLAY : Snooker")
            gamingbill = hour * 250
        elif game==4:
            print("YOU HAVE SELECTED TO PLAY : VR World Gaming")
            gamingbill = hour * 400
        elif game==5:
            print("YOU HAVE SELECTED TO PLAY : Video Games")
            gamingbill = hour * 300
        elif game ==6:
            print("YOU HAVE SELECTED TO PLAY : Swimming Pool Games")
            gamingbill = hour * 350
        else:
            print("Sorry ,May Be You Are Giving Me Wrong Input, Please Try Again !!! ")
        print("Your Total Gaming Bill Is : Rs. ",gamingbill)
        print("FOR : ",hour," HOURS")
        print("WE HOPE YOU WILL ENJOY YOUR GAME")

            
        cursor=myConnection.cursor()
        cursor.execute("USE HMS")
        cursor.execute("CREATE TABLE IF NOT EXISTS GAMING(CID VARCHAR(20),GAMES VARCHAR(30),HOURS VARCHAR(30),GAMING_BILL VARCHAR(30))")                   
        sql= "INSERT INTO GAMING VALUES(""'"+str(cid)+"'," "'"+str(game)+"'," "'"+str(hour)+"'," "'"+str(gamingbill)+"'"")"
        cursor.execute(sql)
        cursor.execute("COMMIT")
    n = int(input("0-BACK\n ->"))
    if n == 0:
            Home()
    else:
            exit()
        
        

# PAYMENT FUNCTION			
def Payment():
    customer=searchCustomer()
    if customer:
        cursor=myConnection.cursor()
        cursor.execute("USE HMS")
        sql='SELECT A.CID, A.C_NAME, A.C_ADDRESS, A.C_COUNTRY , A.P_NO , A.C_EMAIL, A.CHECK_IN , A.CHECK_OUT , A.ROOM_CHOICE, A.NO_OF_DAYS, A.ROOMNO, A.ROOM_PRICE, SUM(B.BILL), SUM(C.GAMING_BILL) FROM C_DETAILS A LEFT JOIN RESTAURENT B ON A.CID=B.CID LEFT JOIN GAMING C ON A.CID=C.CID WHERE A.CID={} GROUP BY A.CID, A.C_NAME, A.C_ADDRESS, A.C_COUNTRY , A.P_NO , A.C_EMAIL, A.CHECK_IN , A.CHECK_OUT , A.ROOM_CHOICE, A.NO_OF_DAYS, A.ROOMNO, A.ROOM_PRICE'.format(cid)
        cursor.execute(sql)
        data=cursor.fetchall()
        if data!=[]:
            for n in data:
                print(" Payment")
                print(" --------------------------------")
                print(" MODE OF PAYMENT")
                
                print(" 1- Credit/Debit Card")
                print(" 2- Paytm/PhonePe")
                print(" 3- Using UPI")
                print(" 4- Cash")
                x=int(input("-> "))
                print("\n		 Pay For AnCasa")
                print(" (y/n)")
                ch=str(input("->"))
                
                if ch=='y' or ch=='Y':
                    print("\n\n --------------------------------")
                    print("	 Hotel AnCasa")
                    print(" --------------------------------")
                    print("	  Bill")
                    print(" --------------------------------")
                    print(" Name: ",n[1],"\t\n Phone No.: ",n[4],"\t\n Address: ",n[2],"\t")
                    print("\n Check-In: ",n[6],"\t\n Check-Out: ",n[7],"\t")
                    print("\n Room Type: ",n[8],"\t\n Room Charges: ",(int(n[11])*int(n[9])),"\t")
                    print(" Restaurant Charges: \t",n[12])
                    print(" Gaming Charges: \t",n[13])
                    print(" --------------------------------")
                    if n[12]==None and n[13]==None:
                        print("\n Total Amount: ",(int(n[11])*int(n[9])),"\t")
                    elif n[13]==None:
                        print("\n Total Amount: ",(int(n[11])*int(n[9]))+int(n[12]),"\t")
                    elif n[12]==None:
                        print("\n Total Amount: ",(int(n[11])*int(n[9]))+int(n[13]),"\t")
                    else:
                        print("\n Total Amount: ",(int(n[11])*int(n[9]))+int(n[13])+int(n[12]),"\t")
                        
                    print(" --------------------------------")
                    print("		 Thank You")
                    print("		 Visit Again :)")
                    print(" --------------------------------\n")

                    sql='DELETE FROM C_DETAILS WHERE CID=("{}")'.format(cid)
                    cursor.execute(sql)
                    sql='DELETE FROM RESTAURENT WHERE CID=("{}")'.format(cid)
                    cursor.execute(sql)
                    cursor.execute("COMMIT")
                    

    n = int(input("0-BACK\n ->"))
    if n == 0:
            Home()
    else:
            exit()

#Add data to file

# RECORD FUNCTION
def Record():
    cursor=myConnection.cursor()
    cursor.execute("USE HMS")
    sql="SELECT CID, C_NAME, C_ADDRESS, C_COUNTRY , P_NO , C_EMAIL, CHECK_IN , CHECK_OUT , ROOM_CHOICE, NO_OF_DAYS, ROOMNO, ROOM_PRICE  FROM C_DETAILS  "
    cursor.execute(sql)
    data=cursor.fetchall()
    if data!=[]:
        print("\t\t***HOTEL RECORD ***\n")
        print("| Name       | Phone No.    | Address    | Check-In      | Check-Out	| Room Type   | Price	|")
        print("----------------------------------------------------------------------------------------------------------------------")
        for n in data:
        # checks if any record exists or not
            
            print("|",n[1],"\t |",n[4],"\t|",n[2],"\t|",n[6],"\t|",n[7],"\t|",n[8],"\t|",n[11],"\t|")
            print("----------------------------------------------------------------------------------------------------------------------")
    else:
        print("No Record Found")
    n = int(input("0-BACK\n ->"))
    if n == 0:
            Home()
    else:
            exit()        


def searchCustomer():
    global myConnection
    global cid
    cursor=myConnection.cursor()
    cursor.execute("USE HMS")
    cid=input("ENTER CUSTOMER ID : ")
    sql='SELECT * FROM C_DETAILS WHERE CID=("{}")'.format(cid)
    cursor.execute(sql)
    data=cursor.fetchall()
    if data:
        return True
        
    else:
        print("Record Not Found Try Again !")
        
        searchCustomer()
        
    cursor.close()
 

# Driver Code
Home()
