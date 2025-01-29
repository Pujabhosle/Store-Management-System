# Store-Management-System
from tkinter import *
import tkinter as tk
from tkinter import messagebox
import os


root = Tk()
root.title("Shop Management System")
print('welcome to the store application')
print('this store deals with stationery items necessary for students')
stock=[{'item':'glue', 'quantity': 25, 'price':10},{'item':'scissors', 'quantity': 25, 'price': 32}] # change initial products from this dictionary

def show_items():
  m=''
  for i in stock:
    m+=f"{i['item']} - quantity  {i['quantity']}\n"  
  messagebox.showinfo(title='items', message=m)
    

def add_items():
  items=Entry_1.get()
  flag=0
  q=Entry_2.get()
  p=Entry_3.get()
  for i in range(len(stock)):
    if items==stock[i]['item']:
        stock[i]['quantity']=stock[i]['quantity']+q
        flag=1
        break
  if flag==0:  
    itemss={'item': items, 'quantity': q, 'price':p}
    stock.append(itemss)
  Entry_1.delete(0,len(Entry_1.get()))
  Entry_2.delete(0,len(Entry_2.get()))
  Entry_3.delete(0,len(Entry_3.get()))
  messagebox.showinfo(title='items added', message=f"{items} added")
  return(stock)

def sell_items(item_to_sell,Quantity):
  Quantity=int(Quantity)
  items_sold={}
  items_sold[item_to_sell] = Quantity
  for i in stock:
    if item_to_sell in i.values():
      i['quantity']-=Quantity
  for i,j in items_sold.items():
   messagebox.showinfo(title='Bill', message=f"{i} sold, qty: {j}")
  Entry_1.delete(0)
  Entry_2.delete(0)
  Entry_3.delete(0)


def delete_item():
  item_to_delete=Entry_1.get()
  for i in stock:
    for key, value in i.items():
      if item_to_delete == value:
        stock.remove(i)
  Entry_1.delete(0,len(Entry_1.get()))
  Entry_2.delete(0,len(Entry_2.get()))
  Entry_3.delete(0,len(Entry_3.get()))
        
  messagebox.showinfo(title='deleted', message=f'{item_to_delete} deleted successfully')

  return stock

def Clear_Item():
  Entry_1.delete(0,len(Entry_1.get()))
  Entry_2.delete(0,len(Entry_2.get()))
  Entry_3.delete(0,len(Entry_3.get()))
  return 

def Exit():
  root.destroy()
  return

Label_0= Label(root,text="STORE MANAGEMENT SYSTEM",fg="black",font=("Times new roman", 30, 'bold'))
Label_0.grid(columnspan=6)
               
Label_1=Label(root,text="ENTER ITEM NAME",bg="#e8c1c7",fg="black",bd=8,font=("Times new roman", 12, 'bold'),width=25)
Label_1.grid(row=1,column=0)

Entry_1=Entry(root, font=("Times new roman", 14),bd=8,width=25)
Entry_1.grid(row=1,column=1)
 
Label_2=Label(root, text="ENTER ITEM QUANTITY",height="1",bg="#e8c1c7",bd=8,fg="black", font=("Times new roman", 12, 'bold'),width=25)
Label_2.grid(row=2,column=0)

Entry_2= Entry(root, font=("Times new roman", 14),bd=8,width=25)
Entry_2.grid(row=2,column=1)
 
Label_3=Label(root, text="ENTER ITEM PRICE",bg="#e8c1c7",bd=8,fg="black", font=("Times new roman", 12, 'bold'),width=25)
Label_3.grid(row=3,column=0)

Entry_3= Entry(root, font=("Times new roman", 14),bd=8,width=25)
Entry_3.grid(row=3,column=1)
               
Button_1= Button(root,text="ADD ITEM",bd=8, bg="#49D810", fg="black", width=25, font=("Times new roman", 12),command=add_items)
Button_1.grid(row=6,column=0, padx=10, pady=10)

Button_2= Button(root, text="DELETE ITEM",bd=8, bg="#49D810", fg="black", width =25, font=("Times new roman", 12),command=delete_item)
Button_2.grid(row=6,column=1, padx=40, pady=10)

Button_3= Button(root, text="VIEW STOCK",bd=8, bg="#49D810", fg="black", width =25, font=("Times new roman", 12),command=show_items)
Button_3.grid(row=3,column=3, padx=40, pady=10)

Button_4= Button(root, text="SELL ITEM",bd=8, bg="#49D810", fg="black", width =25, font=("Times new roman", 12),command=lambda :sell_items(Entry_1.get(),Entry_2.get()))
Button_4.grid(row=2,column=3, padx=40, pady=10)

Button_5= Button(root, text="CLEAR SCREEN",bd=8, bg="#49D810", fg="black", width=25, font=("Times new roman", 12),command=Clear_Item)
Button_5.grid(row=4,column=3, padx=40, pady=10)

Button_6= Button(root,highlightcolor="blue",activebackground="red", text="Exit",bd=8, bg="#FF0000", fg="#EEEEF1", width=25, font=("Times", 18),command=Exit)
Button_6.grid(row=6,column=3, padx=40, pady=10)


 
root.mainloop()
