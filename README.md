# AVIA Родионов Иван, Вольф Арина
Откройте пайтон код и запустите его
import tkinter as tk
from tkinter import *
from tkinter import messagebox
#cоздание окна интерфейса
window = Tk()
window.title('Интерфейс для дорог')
window.geometry('1000x600')
frame = Frame(
    window,
    padx = 15,
    pady = 15
)
frame.pack(expand=True)
#создание надписей в окне
living_lb = Label(
   frame,
   text="Введите дополнительную площадь жилой застройки  "
)
living_lb.grid(row=3, column=1)
sqware_lb = Label(
   frame,
   text="Введите удельную площадь на человека (25 или 45)  "
)
sqware_lb.grid(row=5, column=1)
working_lb = Label(
   frame,
   text="Введите дополнительную площадь рабочей застройки  "
)
working_lb.grid(row=4, column=1)
#создание ячеек для ввода информации
living_n = Entry(
   frame,
)
living_n.grid(row=3, column=2)
sqware_n = Entry(
   frame,
)
sqware_n.grid(row=5, column=2)
working_n = Entry(
   frame,
)
working_n.grid(row=4, column=2)


def calculate_nag():
   home = int(living_n.get())
   home += 190000
   k = int(sqware_n.get())
   office = int(working_n.get())
   office += 214000
   individual = 0.1 * home / k * 0.57 * 0.3 / 1.2 + 0.35 * office / 35 * 0.57 * 0.3 / 1.2 # ит
   public = 0.1 * home / k * 0.57 * 0.7 + 0.35 * office / 35 * 0.57 * 0.7 # от

   # metro
   Ilyich_square = 8400
   koef_Ilyich_square = Ilyich_square / 14000
   Roman = 4600
   koef_Roman = Roman / 14000
   Serp_i_molot = 1000
   koef_Serp_i_molot = Serp_i_molot / 14000

   # приписка koef - какая часть людей направится именно на этот пункт
   # road
   Gzhel = 0.3 * 150
   koef_Gzhel = 3 / 15
   Sergey_Radonezhsky = 0.7 * 2400
   koef_Sergey_Radonezhsky = 7 / 15
   Zolotorogsky_Val = 0.5 * 300
   koef_Zolotorogsky_Val = 5 / 15

   # новая загруженность metro
   Ilyich_square += koef_Ilyich_square * public
   Roman += koef_Roman * public
   Serp_i_molot += koef_Serp_i_molot * public

   # новая загруженность road
   Gzhel += koef_Gzhel * individual
   Sergey_Radonezhsky += koef_Sergey_Radonezhsky * individual
   Zolotorogsky_Val += koef_Zolotorogsky_Val * individual

   from tkinter import ttk

   if Ilyich_square/1000 < 16:
      if Roman/1000 < 16:
         if Serp_i_molot/1000 < 5:
               if Gzhel/15 < 10:
                  if Sergey_Radonezhsky/240 < 10:
                     if Zolotorogsky_Val/30 < 10:
                           status_Ilyich = "не перегружена"
                           status_Roman = "не перегружена"
                           status_Serp_i_molot = "не перегружена"
                           status_Gzhel = "не перегружен"
                           status_Sergey_Radonezhsky = "не перегружена"
                           status_Zolotorogsky_Val = "не перегружен"
                     else:
                           status_Ilyich = "не перегружена"
                           status_Roman = "не перегружена"
                           status_Serp_i_molot = "не перегружена"
                           status_Gzhel = "не перегружен"
                           status_Sergey_Radonezhsky = "не перегружена"
                           status_Zolotorogsky_Val = "перегружен"
                  else:
                     status_Ilyich = "не перегружена"
                     status_Roman = "не перегружена"
                     status_Serp_i_molot = "не перегружена"
                     status_Gzhel = "не перегружен"
                     status_Sergey_Radonezhsky = "перегружена"
                     status_Zolotorogsky_Val = "перегружен"
               else:
                  status_Ilyich = "не перегружена"
                  status_Roman = "не перегружена"
                  status_Serp_i_molot = "не перегружена"
                  status_Gzhel = "перегружен"
                  status_Sergey_Radonezhsky = "перегружена"
                  status_Zolotorogsky_Val = "перегружен"
         else:
               status_Ilyich = "не перегружена"
               status_Roman = "не перегружена"
               status_Serp_i_molot = "перегружена"
               status_Gzhel = "перегружен"
               status_Sergey_Radonezhsky = "перегружена"
               status_Zolotorogsky_Val = "перегружен"
      else:
         status_Ilyich = "не перегружена"
         status_Roman = "перегружена"
         status_Serp_i_molot = "перегружена"
         status_Gzhel = "перегружен"
         status_Sergey_Radonezhsky = "перегружена"
         status_Zolotorogsky_Val = "перегружен"
   else:
      status_Ilyich = "перегружена"
      status_Roman = "перегружена"
      status_Serp_i_molot = "перегружена"
      status_Gzhel = "перегружен"
      status_Sergey_Radonezhsky = "перегружена"
      status_Zolotorogsky_Val = "перегружен"

   root = tk.Tk()
   root.title("Итоги расчета")

   tree = ttk.Treeview(root)
   tree["columns"] = ("Location", "Status", "Deficit", "Maximum")
   tree.column("#0", width=0, stretch=tk.NO)
   tree.column("Location", anchor=tk.W, width=200)
   tree.column("Status", anchor=tk.W, width=100)
   tree.column("Deficit", anchor=tk.W, width=100)
   tree.column("Maximum", anchor=tk.W, width=100)

   tree.heading("#0", text="", anchor=tk.W)
   tree.heading("Location", text="Location", anchor=tk.W)
   tree.heading("Status", text="Status", anchor=tk.W)
   tree.heading("Deficit", text="Deficit", anchor=tk.W)
   tree.heading("Maximum", text="Maximum", anchor=tk.W)

   tree.insert("", tk.END, values=("Площадь Ильича", status_Ilyich, f"{(-Ilyich_square/1000 + 16):.1f}", '16'))
   tree.insert("", tk.END, values=("Римская", status_Roman, f"{(-Roman/1000 + 16):.1f}", '16'))
   tree.insert("", tk.END, values=("Серп и Молот", status_Serp_i_molot, f"{(-Serp_i_molot/1000 + 5):.1f}", '5'))
   tree.insert("", tk.END, values=("Гжельский переулок", status_Gzhel, f"{(-Gzhel/15 + 10):.1f}", '10'))
   tree.insert("", tk.END, values=("Улица Сергея Радонежского", status_Sergey_Radonezhsky, f"{(-Sergey_Radonezhsky/240 + 10):.1f}", '10'))
   tree.insert("", tk.END, values=("Золоторижский Вал", status_Zolotorogsky_Val, f"{(-Zolotorogsky_Val/30 + 10):.1f}", '10'))

   tree.pack()
   root.mainloop()

#кнопка для начала расчета
cal_btn = Button(
    frame,
    text='Рассчитать нагрузку на транспорт',
    command=calculate_nag
)
cal_btn.grid(row=6, column=2)

window.mainloop()
