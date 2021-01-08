# python
import tkinter as tk
from PIL import ImageTk, Image
from tkinter import filedialog

 
# #Initialize Window
root = tk.Tk()
root.title('Binary Image Classifier')
root.resizable(False, False)

# #Create banner and frames
title = tk.Label(root,bg='violet', text="Binary Image Classifier", padx=25, pady=6, font=("", 12)).pack()
canvas = tk.Canvas(root, height=500, width=500, bg='white')
canvas.pack()
frame = tk.Frame(root, bg='purple')
frame.place(relwidth=0.8, relheight=0.8, relx=0.1, rely=0.1)

def load_img():
    # globally define img and file path (image_data)
    global img,image_data
    for img_display in frame.winfo_children():
        img_display.destroy()
    image_data = filedialog.askopenfilename(initialdir="../images/", title="Choose an image",
                                                filetypes=(("all files", "*.*"), ("png files", "*.png")))

    basewidth = 150 # Processing image for displaying
    img = Image.open(image_data)
    wpercent = (basewidth / float(img.size[0]))
    hsize = int((float(img.size[1]) * float(wpercent)))
    img = img.resize((basewidth, hsize), Image.ANTIALIAS)
    img = ImageTk.PhotoImage(img)
    file_name = image_data.split('/')
    panel = tk.Label(frame, text= str(file_name[len(file_name)-1]).upper()).pack()
    panel_image = tk.Label(frame, image=img).pack()

def classify(file_path):
    return


# #Create Buttons
chose_image = tk.Button(root, text='Choose Image',
                        padx=35, pady=10,
                        fg="white", bg="black", command=load_img)
chose_image.pack(side=tk.LEFT)

class_image = tk.Button(root, text='Classify Image',
                        padx=35, pady=10,
                        fg="white", bg="black", command=lambda:classify(image_data))
class_image.pack(side=tk.RIGHT)

result = tk.Label(root,bg='violet', text="Result", padx=25, pady=6, font=("", 12))
result.pack()

# run the loop for keeping the GUI on
root.mainloop()


# git remote add origin https://github.com/shah9840/worrkshop-ml.git
# git branch -M main
# git push -u origin main
