import tkinter as tk 
from tkinter import scrolledtext, messagebox class LoginApplication:     def __init__(self, root):         self.root = root         self.root.title("Login")         self.root.geometry("400x300")         self.root.config(bg="#2c3e50") 
        # Login frame 
        self.login_frame = tk.Frame(root, bg="#2c3e50")         self.login_frame.place(relx=0.5, rely=0.5, anchor=tk.CENTER) 
        # Username label and entry 
        self.username_label = tk.Label(self.login_frame, text="Username:", font=("Arial", 14), bg="#2c3e50", fg="#ecf0f1") 
        self.username_label.grid(row=0, column=0, pady=10, sticky=tk.W)         self.username_entry = tk.Entry(self.login_frame, font=("Arial", 14))         self.username_entry.grid(row=0, column=1, pady=10, padx=10 
        # Password label and entry 
        self.password_label = tk.Label(self.login_frame, text="Password:", font=("Arial", 14), bg="#2c3e50", fg="#ecf0f1") 
        self.password_label.grid(row=1, column=0, pady=10, sticky=tk.W)         self.password_entry = tk.Entry(self.login_frame, font=("Arial", 14), show="*")         self.password_entry.grid(row=1, column=1, pady=10, padx=10) 
        # Login button 
        self.login_button = tk.Button(self.login_frame, text="Login", font=("Arial", 14), bg="#2980b9", fg="#ecf0f1", command=self.login) self.login_button.grid(row=2, columnspan=2, pady=20     def login(self): 
        username = self.username_entry.get()         password = self.password_entry.get() 
        # Simple validation         if username == "user" and password == "password": 
            self.open_charm_chat()         else: 
            messagebox.showerror("Login Error", "Invalid username or password")     def open_charm_chat(self): 
        self.root.withdraw() 
        chat_root = tk.Toplevel(self.root)         ChatApplication(chat_root) class ChatApplication:     def __init__(self, root): 
        self.root = root 
        self.root.title("Chat Application")         self.root.geometry("400x500")         # Set up the gradient background 
        self.gradient_frame = tk.Canvas(root, width=400, height=500, bd=0, highlightthickness=0) 
        self.gradient_frame.pack(fill=tk.BOTH, expand=True)         self.gradient_frame.bind("<Configure>", self.draw_gradient) 
        # Adding a title 
        self.title_frame = tk.Frame(self.gradient_frame, bg="#2c3e50")         self.gradient_frame.create_window(200, 40, window=self.title_frame)         self.title_label = tk.Label(self.title_frame, text="Chat Application", font=("Arial", 20, "bold"), bg="#2c3e50", fg="#ecf0f1") 
         
# Chat display area  self.chat_area=scrolledtext.ScrolledText(self.gradient_frame, wrap=tk.WORD,font=("Arial",12),bg="#ecf0f1",fg="#2c3e50", bd=0, padx=10, pady=10) 
        self.gradient_frame.create_window(200, 250, window=self.chat_area, width=360, height=300)         self.chat_area.config(state=tk.DISABLED)         # Frame for message entry and send button 
        self.entry_frame = tk.Frame(self.gradient_frame, bg="#2c3e50")         self.gradient_frame.create_window(200, 470, window=self.entry_frame, width=360, height=30) 
        # Message entry area 
        self.message_entry = tk.Entry(self.entry_frame, font=("Arial", 12), bg="#ecf0f1", fg="#2c3e50", bd=0, relief=tk.FLAT)         self.message_entry.pack(side=tk.LEFT, fill=tk.X, expand=True, padx=(0, 
10), ipady=5) 
        self.message_entry.bind("<Return>", self.send_message_event)         self.message_entry.focus_set()   
        # Send button 
        self.send_button = tk.Button(self.entry_frame, text="Send", font=("Arial", 
12),bg="#2980b9",fg="#ecf0f1",bd=0,relief=tk.FLAT, command=self.send_message) 
        self.send_button.pack(side=tk.RIGHT, ipadx=10, ipady=5)     def draw_gradient(self, event=None):         self.gradient_frame.delete("gradient")         width = self.gradient_frame.winfo_width()         height = self.gradient_frame.winfo_height()         color1 = "#3498db"         color2 = "#2c3e50"         limit = height 
        (r1, g1, b1) = self.gradient_frame.winfo_rgb(color1) 
(r2, g2, b2) = self.gradient_frame.winfo_rgb(color2)         r_ratio = float(r2 - r1) / limit         g_ratio = float(g2 - g1) / limit         b_ratio = float(b2 - b1) / limit         for i in range(limit): 
            nr = int(r1 + (r_ratio * i))             ng = int(g1 + (g_ratio * i))             nb = int(b1 + (b_ratio * i))             color = f'#{nr:04x}{ng:04x}{nb:04x}' 
            self.gradient_frame.create_line(0,i,width, i, tags=("gradient",), fill=color)     def send_message_event(self, event): 
        self.send_message()     def send_message(self): 
        message = self.message_entry.get().strip()         if message: 
            self.display_message("You", message)             self.message_entry.delete(0, tk.END) 
            self.message_entry.focus_set()  # Set focus back to the message entry after sending 
            # Simulate the "Message Delivered" status             self.display_message("Status", "Message Delivered") 
            # Reply based on the message content             if message.lower() == "hello": 
                self.display_message("Other", "Hii  ")             elif message.lower() == "how are you": 
                self.display_message("Other", "I am fine!! What about you??  ") 
            else: 
                self.display_message("Other", "Received: " + message + "  ")  def display_message(self, sender, message):         self.chat_area.config(state=tk.NORMAL)         if sender == "Status": 
            # Display status messages in a different style             self.chat_area.insert(tk.END, f"*{message}*\n", 'status')         else: 
            self.chat_area.insert(tk.END, f"{sender}: {message}\n") 
        self.chat_area.tag_config('status', foreground='gray', font=('Arial', 10, 
'italic')) 
        self.chat_area.yview(tk.END)         self.chat_area.config(state=tk.DISABLED) if __name__ == "__main__": 
    root = tk.Tk() 
    app = LoginApplication(root)     root.mainloop() 
<!---
VijayaVarsha/VijayaVarsha is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
