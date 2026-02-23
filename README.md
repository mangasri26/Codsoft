import tkinter as tk
import math

root = tk.Tk()
root.title('Scientific Calculator')
root.configure(bg='#ADD8E6')
root.resizable(False, False)

ent_field = tk.Entry(root, bg='#ADD8E6', fg='#000080',
                     font=('Arial', 25), borderwidth=10, justify="right")
ent_field.grid(row=0, columnspan=4, padx=10, pady=10, sticky='nsew')
ent_field.insert(0, '0')

FONT = ('Arial', 12, 'bold')


class SC_Calculator:
    def _init_(self):
        self.current = ""
        self.inp_value = True
        self.result = False

    def Entry(self, value):
        ent_field.delete(0, tk.END)
        ent_field.insert(0, str(value))

    def Enter_Num(self, num):
        self.result = False
        firstnum = ent_field.get()

        if self.inp_value:
            self.current = num
            self.inp_value = False
        else:
            self.current = firstnum + num

        self.Entry(self.current)

    def Standard_Ops(self, val):
        temp_str = ent_field.get()
        try:
            if val == "=":
                ans = eval(temp_str)
                self.Entry(ans)
                self.result = True
                self.inp_value = True
            else:
                self.Entry(temp_str + val)
                self.inp_value = False
        except:
            self.Entry("Error")

    def Clear_Entry(self):
        self.current = "0"
        self.Entry(0)
        self.inp_value = True

    def SQ_Root(self):
        try:
            value = float(ent_field.get())
            self.Entry(math.sqrt(value))
        except:
            self.Entry("Error")

    def Pi(self):
        self.Entry(math.pi)

    def E(self):
        self.Entry(math.e)

    def Sin(self):
        try:
            value = float(ent_field.get())
            self.Entry(math.sin(math.radians(value)))
        except:
            self.Entry("Error")

    def Cos(self):
        try:
            value = float(ent_field.get())
            self.Entry(math.cos(math.radians(value)))
        except:
            self.Entry("Error")

    def Tan(self):
        try:
            value = float(ent_field.get())
            self.Entry(math.tan(math.radians(value)))
        except:
            self.Entry("Error")

    def Log(self):
        try:
            value = float(ent_field.get())
            self.Entry(math.log10(value))
        except:
            self.Entry("Error")

    def Ln(self):
        try:
            value = float(ent_field.get())
            self.Entry(math.log(value))
        except:
            self.Entry("Error")

    def Factorial(self):
        try:
            value = int(float(ent_field.get()))
            self.Entry(math.factorial(value))
        except:
            self.Entry("Error")


sc_app = SC_Calculator()

# -------- Number Buttons --------
numbers = [
    ('7', 1, 0), ('8', 1, 1), ('9', 1, 2),
    ('4', 2, 0), ('5', 2, 1), ('6', 2, 2),
    ('1', 3, 0), ('2', 3, 1), ('3', 3, 2),
    ('0', 4, 0)
]

for (text, row, col) in numbers:
    tk.Button(root, text=text, font=FONT, width=5, height=2,
              command=lambda x=text: sc_app.Enter_Num(x))\
        .grid(row=row, column=col, padx=5, pady=5)

# -------- Operator Buttons --------
ops = [
    ('+', 1, 3), ('-', 2, 3),
    ('*', 3, 3), ('/', 4, 3),
    ('=', 4, 2)
]

for (text, row, col) in ops:
    tk.Button(root, text=text, font=FONT, width=5, height=2,
              command=lambda x=text: sc_app.Standard_Ops(x))\
        .grid(row=row, column=col, padx=5, pady=5)

# -------- Scientific Buttons --------
tk.Button(root, text='CE', font=FONT, width=5, height=2,
          command=sc_app.Clear_Entry).grid(row=4, column=1, padx=5, pady=5)

tk.Button(root, text='√', font=FONT, width=5, height=2,
          command=sc_app.SQ_Root).grid(row=5, column=0, padx=5, pady=5)

tk.Button(root, text='π', font=FONT, width=5, height=2,
          command=sc_app.Pi).grid(row=5, column=1, padx=5, pady=5)

tk.Button(root, text='e', font=FONT, width=5, height=2,
          command=sc_app.E).grid(row=5, column=2, padx=5, pady=5)

tk.Button(root, text='sin', font=FONT, width=5, height=2,
          command=sc_app.Sin).grid(row=6, column=0, padx=5, pady=5)

tk.Button(root, text='cos', font=FONT, width=5, height=2,
          command=sc_app.Cos).grid(row=6, column=1, padx=5, pady=5)

tk.Button(root, text='tan', font=FONT, width=5, height=2,
          command=sc_app.Tan).grid(row=6, column=2, padx=5, pady=5)

tk.Button(root, text='log', font=FONT, width=5, height=2,
          command=sc_app.Log).grid(row=6, column=3, padx=5, pady=5)

tk.Button(root, text='ln', font=FONT, width=5, height=2,
          command=sc_app.Ln).grid(row=7, column=0, padx=5, pady=5)

tk.Button(root, text='x!', font=FONT, width=5, height=2,
          command=sc_app.Factorial).grid(row=7, column=1, padx=5, pady=5)

root.mainloop()
