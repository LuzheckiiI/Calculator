# Calculator
Project
# Калькулятор квадратных уравнений; Лужецкий И. В., группа Р3175, ИТМО, 2016

from tkinter import *
from math import sqrt

def solver(a, b, c):
    """ Решает уравнение """
    D = b * b - 4 * a * c
    if D > 0:
        x1 = (- b - sqrt(D)) / (2 * a)
        x2 = (- b + sqrt(D)) / (2 * a)
        text = "Дискриминант: %s \n D > 0; 2 корня \n x1 = %s \n x2 = %s \n" % (D, x1, x2)
    if D == 0:
        x = - b / (2 * a)
        text = "D = 0; 1 корень \n x = %s \n" % (x)
    if D < 0:
        text = "D < 0; Решений нет"
    return text

def inserter(value):
    """ Вставка заданного значения в текстовый виджет """
    output.delete("0.0","end")
    output.insert("0.0",value)    

def clear(event):
    """ Очистка форм ввода"""
    caller = event.widget
    caller.delete("0", "end")

def handler():
    """ Получает содержимое записи и передает результат в текст """
    try:
        a_val = float(a.get())
        b_val = float(b.get())
        c_val = float(c.get())
        inserter(solver(a_val, b_val, c_val))
    except ValueError: #если возникла ошибка
        inserter("Убедитесь, что вы ввели 3 числа")

root = Tk()

root.title("Калькулятор")  # "Заголовок"
root.minsize(325,230) #размеры поля
#root.resizable(True, True)

frame = Frame(root) #Виджет внутри окна
frame.grid()

a = Entry(frame, width=3) #Entry позволяет ввести пользователю одну строку
a.grid(row=1,column=1) #,padx=(10,0)
a.bind("<FocusIn>", clear) #bind привязывает событие к действию <FocusIn>, очистка
a_lab = Label(frame, text="x^2 + ").grid(row=1,column=2) #текст + патаметры

b = Entry(frame, width=3)
b.bind("<FocusIn>", clear)
b.grid(row=1,column=3)
b_lab = Label(frame, text="x + ").grid(row=1, column=4)

c = Entry(frame, width=3)
c.bind("<FocusIn>", clear)
c.grid(row=1, column=5)
c_lab = Label(frame, text="= 0").grid(row=1, column=6)

but = Button(frame, text="Решить", command=handler).grid(row=1, column=7, padx=(10,0)) #кнопка Решить

output = Text(frame, bg="lightgreen", font="Arial 14", width=35, height=10) #параметры окна вывода (цвет, шрифт ...)
output.grid(row=2, columnspan=8) #

root.mainloop()
