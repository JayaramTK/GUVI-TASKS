# GUVI-TASKS

import re

# functions to check validity of email ids / username

def check1(string):
    x = re.findall("[@.]", string)
    y = re.search('[@]', string)
    z = re.search('[.]', string)
    if x == ['@', '.'] and y.start() < z.start() and y.start() != 0:
        return True      
    else:
        print("\nINVALID username, error with symbols'@' and '.'")
        return False

def check2(string):
    x = re.findall("[@][.]", string)
    if x:
        print("\nINVALID username, '@' or '.' is missing")
        return False
    else:
        return True

def check3(string):
    x = re.findall(r"\b\d", string)
    if x:
        print("\nINVALID username, username should not start with a number")
        return False
    else:
        return True

def check4(string):
    x = re.findall("[^a-zA-Z0-9@.]", string)
    if x:
        print("\nINVALID username, special characters not allowed")
        return False
    else:
        return True
  
def emailvalidity():
    if check1(emailid) == True and \
       check2(emailid) == True and \
       check3(emailid) == True and \
       check1(emailid) == True:
       return True
    else:
        print("Given email_ID/username not accepted")
        return False
    

# functions to check validity of passwords

def pcheck1(string):
    x = re.findall("\d", string)
    if x:
        return True
    else:
        print("\nINVALID password, numerical digit missing")
        return False

def pcheck2(string):
    x = re.findall('[A-Z]', string)
    if x:
        return True
    else:
        print("\nINVALID password, capital letter missing")
        return False
    
def pcheck3(string):
    x = re.findall('[a-z]', string)
    if x:
        return True
    else:
        print("\nINVALID password, small letter missing")
        return False  
    
def pcheck4(string):
    x = len(string)
    if x > 5 and x < 16:
        return True
    else:
        print("\nINVALID password, password length should be between 5 and 13")
        return False     
    
def pcheck5(string):
    x = re.findall('[^a-zA-Z0-9]', string)
    if x:
        return True
    else:
        print("\nINVALID password, special character missing")
        return False 

def pwvalidity():
   if pcheck1(password) == True and \
      pcheck2(password) == True and \
      pcheck3(password) == True and \
      pcheck4(password) == True and \
      pcheck5(password) == True:
       return True
   else:
       print("Given password not accepted")
       return False



# registration process, beginning of program

def registration():
    
    global emailid
    global password
    
    print("\nKindly provide the below details for registration")
    emailid = input("Enter the required email-ID/username: ")
    
    if emailvalidity():
        password = input("Enter the required password: ")
        
        if pwvalidity() == False:
            print("Since the password provided is INVALID, redirecting to registration")
            registration()        
    else:
        print("\nSince email-ID provided is INVALID, redirecting to registration")
        registration()
        
    if emailvalidity() == True and \
       pwvalidity() == True:

        f = open("database.txt", "a+")
        database = f"{emailid},{password}"
        
        f.write(f"{database}")
        f.write("\n")
        
        f.close()

    print("\nThe registration is successful")
    print(f"\nYour email-ID is '{emailid}', Your password is '{password}'")


def login():
    entry = input("\nEnter the username/emailid: ")
    f = open("database.txt", "r")

    
    for line in f:

        
        if line != False and line != '\n':

            linesplit = line.split(',')

            e,p = linesplit
            p = p.rstrip("\n")
            
            if entry == e:
                print("\nYour Email-ID is registered")
                
                pw = input("\nPlease enter password: ")
                
                if pw == p:
                    print("\nPassword matched, Entry granted")
                    f.close()
                    break
                
                else:
                    print("\nPassword doesn't match for the given email-ID")
                    f.close()
                    retrievepw()
                    
            else:
                pass
                
        else:
            pass
    
    else:   
        print('\nEmail-ID NOT REGISTERED, you are directed for registration')
        f.close()
        registration()
 
    
# function to retrieve password
# provides password only if emailid exists in database

def retrievepw():
    print("Kindly provide below details to retreive password")
    entry = input("Enter your emailid/username: ")
    f = open("database.txt", "r")
    
    for line in f:
        if line != False and line != '\n': 
            linesplit = line.split(',')

            e, p = linesplit
            p = p.rstrip("\n")
            
            if entry == e:
                print("\nYour email-ID is registered")
                print(f"\nYour password is {p}")
                f.close()
                break
            
            else:
                pass
            
        else:
            pass
        
    else:    
        f.close()


# program starts here

firstin = input('''            To login    press '1'
         To register    press '2'
To retrieve password    press '3'
          press here:   ''')
  
print(f"You have selected {firstin}")

if firstin == '1':
    login()
elif firstin == '2':
    registration()
elif firstin == '3':
    retrievepw()
else:
    print('invalid input')
    registration()








