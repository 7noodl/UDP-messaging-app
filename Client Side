import socket
from threading import Thread
from tkinter import *
from tkinter import ttk

SERVER_CHOICE = input("What server would you like to join? \n 1 = server\n")

if (SERVER_CHOICE == "1"):
    SERVER_HOST = "127.0.0.1"  #<<<<<<<CHANGE TO IP OF SERVER 1>>>>>>>
    SERVER_PORT = 10000
elif (SERVER_CHOICE != "1"):
    print("Invalid Server")
    exit() 
    

s = socket.socket()
print(f"[*] Connecting to {SERVER_HOST}:{SERVER_PORT}...")

s.connect((SERVER_HOST, SERVER_PORT))
print("[+] Connected.")

name = input("Enter your name: ")



def listen_for_messages():
    while True:
        message = s.recv(1024).decode()
        Output.insert(END, message + "\n")
        Output.see("end")
def Take_input(event):
    INPUT = inputtxt.get("1.0", "end-1c")
    to_send =  INPUT
    to_send = f"{name}: {to_send}"
    s.send(to_send.encode())
    Output.see("end")
    inputtxt.delete('1.0', END)
    

t = Thread(target=listen_for_messages)
t.daemon = True
t.start()

root = Tk()
root.geometry("300x300")
root.title("Chat")

l = Label(text = "")
inputtxt = Text(root, height = 1,
                width = 25,
                bg = "light yellow")
  
Output = Text(root, height = 15, 
              width = 25, 
              bg = "light cyan")
  
Display = Button(root, height = 1,
                 width = 3, 
                 text ="Send",
                 command = lambda:Take_input())

root.bind('<Return>', Take_input)

scrollbar = ttk.Scrollbar(root, orient='vertical', command=Output.yview)
scrollbar.grid(row=1, column=2, sticky='ns')
Output['yscrollcommand'] = scrollbar.set

while True:
    
    l.grid()
    Output.grid(row=1,column=1)
    inputtxt.grid(row=2,column=1)
    Display.grid(row=2,column=2)
    
    root.mainloop()
    

s.close()
