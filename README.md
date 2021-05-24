# Advanced-notepad
In this ordinary project i have included some additional features which a windows doesn't provide
import tkinter as tk
from tkinter import ttk
from tkinter import filedialog
from tkinter import font,colorchooser,messagebox
import os

main_application=tk.Tk()
main_application.geometry('1200x800')
main_application.title('Destop Apllication')
# main_application.wm_iconbitmap('icon.ico')

main_menu=tk.Menu()

################################--main menu  ##########################################
file=tk.Menu(main_menu,tearoff=False)#hese are menu and always it must at last position


#file icons
new_icon=tk.PhotoImage(file=r'D:\app_icons\new.png') #this line for saving icons on menu bar
open_icon=tk.PhotoImage(file=r'D:\app_icons\open.png')
save_icon=tk.PhotoImage(file=r'D:\app_icons\save.png')
save_as_icon=tk.PhotoImage(file=r'D:\app_icons\save_as.png')
exit_icon=tk.PhotoImage(file=r'D:\app_icons\exit.png')


# #commands on file
# file.add_command(label='new',image=new_icon,compound=tk.LEFT,accelerator='ctrl+n') 
# #compound is store the commands to left one by one
# file.add_command(label='open',image=open_icon,compound=tk.LEFT,accelerator='ctrl+o')
# file.add_command(label='save',image=save_icon,compound=tk.LEFT,accelerator='ctrl+s')
# file.add_command(label='save_as',image=save_as_icon,compound=tk.LEFT,accelerator='ctrl+shift+s')
# file.add_command(label='exit',image=exit_icon,compound=tk.LEFT)

edit=tk.Menu(main_menu,tearoff=False)#hese are menu 
view=tk.Menu(main_menu,tearoff=False)#hese are menu 
color_theme=tk.Menu(main_menu,tearoff=False)#hese are menu 



# -----------------------------------file menu------------------------------------
edit=tk.Menu(main_menu,tearoff=False)

# edit icons
copy_icon=tk.PhotoImage(file=r'D:\app_icons\copy.png')
paste_icon=tk.PhotoImage(file=r'D:\app_icons\paste.png')
cut_icon=tk.PhotoImage(file=r'D:\app_icons\cut.png')
clear_all_icon=tk.PhotoImage(file=r'D:\app_icons\clear_all.png')
find_icon=tk.PhotoImage(file=r'D:\app_icons\find.png')

# adding command on edit menu
# edit.add_command(label='paste',image=paste_icon,compound=tk.LEFT,accelerator='ctrl+v')
# edit.add_command(label='cut',image=cut_icon,compound=tk.LEFT,accelerator='ctrl+x')
# edit.add_command(label='clear_all',image=clear_all_icon,compound=tk.LEFT)
# edit.add_command(label='find',image=find_icon,compound=tk.LEFT,accelerator='ctrl+f')

    #   ---------------------edit menu------------------------------

#view menu

view=tk.Menu(main_menu,tearoff=False)

toolbar_icon=tk.PhotoImage(file=r'D:\app_icons\tool_bar.png')
statusbar_icon=tk.PhotoImage(file=r'D:\app_icons\status_bar.png')

# view.add_checkbutton(label='Tool_bar',image=toolbar_icon,compound=tk.LEFT)
# view.add_checkbutton(label='status_bar',image=statusbar_icon,compound=tk.LEFT)


    # ----------------------color theme-----------------------
color_theme=tk.Menu(main_menu,tearoff=False) #color theme is radio button

light_default_icon=tk.PhotoImage(file=r'D:\app_icons\light_default.png')
light_plus_icon=tk.PhotoImage(file=r'D:\app_icons\light_plus.png')
dark_icon=tk.PhotoImage(file=r'D:\app_icons\dark.png')
red_icon=tk.PhotoImage(file=r'D:\app_icons\red.png')
monokai_icon=tk.PhotoImage(file=r'D:\app_icons\monokai.png')
night_blue_icon=tk.PhotoImage(file=r'D:\app_icons\night_blue.png')

# color_theme.add_command(label='light_default',image=light_default_icon,compound=tk.LEFT)
# color_theme.add_command(label='light_plus',image=light_plus_icon,compound=tk.LEFT)
# color_theme.add_command(label='light_default',image=dark_icon,compound=tk.LEFT)
# color_theme.add_command(label='light_default',image=red_icon,compound=tk.LEFT)
# color_theme.add_command(label='light_default',image=monokai_icon,compound=tk.LEFT)
# color_theme.add_command(label='light_default',image=night_blue_icon,compound=tk.LEFT)

theme_choice=tk.StringVar()
color_icons=(light_default_icon,light_plus_icon,dark_icon,red_icon,monokai_icon,night_blue_icon)
color_dict = {
    'Light Default ' : ('#000000', '#ffffff'),#first one is for text second one is for background
    'Light Plus' : ('#474747', '#e0e0e0'),
    'Dark' : ('#c4c4c4', '#2d2d2d'),
    'Red' : ('#2d2d2d', '#ffe8e8'),
    'Monokai' : ('#d3b774', '#474747'),
    'Night Blue' :('#ededed', '#6b9dc2')
}
# count=0
# for i in color_dict:
#     color_theme.add_radiobutton(label=i,image=color_icons[count],variable=theme_choice,compound=tk.LEFT)
#     count+=1




#cascading
main_menu.add_cascade(label='file',menu=file)
main_menu.add_cascade(label='edit',menu=edit)
main_menu.add_cascade(label='view',menu=view)
main_menu.add_cascade(label='color_theme',menu=color_theme)
# ------------------------------&&&  end main menu &&&&--------------------------------#

################################--tool bar  ##########################################
# there is font families in font class which are we imported 'font'
tool_bar=ttk.Label(main_application)#here we created a label
tool_bar.pack(side=tk.TOP,fill=tk.X)
#font family
font_tuples=tk.font.families()
font_family=tk.StringVar()#ye check karega ki user se konsa font select kiya hai
font_box=ttk.Combobox(tool_bar,width=30,textvariable=font_family,state='readonly')
font_box['values']=font_tuples
font_box.current(font_tuples.index('Arial'))
font_box.grid(row=0,column=0)

#font size
size_var=tk.IntVar()
font_size=ttk.Combobox(tool_bar,width=15,textvariable=size_var,state='readonly') #text variable is used to 
#select karne ke baad combobox me print hoga
font_size['values']=tuple(range(8,80))
font_size.current(4)
font_size.grid(row=0,column=1,padx=3)

#creating bold button
bold_icon=tk.PhotoImage(file=r'D:\app_icons\bold.png')
bold_btn=ttk.Button(tool_bar,image=bold_icon)
bold_btn.grid(row=0,column=2,padx=3)

#creating italic button
italic_icon=tk.PhotoImage(file=r'D:\app_icons\italic.png')
italic_btn=ttk.Button(tool_bar,image=italic_icon)
italic_btn.grid(row=0,column=3,padx=3)

#crearing under line button
under_line_icon=tk.PhotoImage(file=r'D:\app_icons\underline.png')
under_line_btn=ttk.Button(tool_bar,image=under_line_icon)
under_line_btn.grid(row=0,column=4,padx=3)

#creating fint button color button
font_color_icon=tk.PhotoImage(file=r'D:\app_icons\font_color.png')
font_color_btn=ttk.Button(tool_bar,image=font_color_icon)
font_color_btn.grid(row=0,column=5,padx=3)

#creating align left button color button
align_left_icon=tk.PhotoImage(file=r'D:\app_icons\align_left.png')
align_left_btn=ttk.Button(tool_bar,image=align_left_icon)
align_left_btn.grid(row=0,column=6,padx=3)

#creating align center button color button
align_center_icon=tk.PhotoImage(file=r'D:\app_icons\align_center.png')
align_center_btn=ttk.Button(tool_bar,image=align_center_icon)
align_center_btn.grid(row=0,column=7,padx=3)

#creating align right button color button
align_right_icon=tk.PhotoImage(file=r'D:\app_icons\align_right.png')
align_right_btn=ttk.Button(tool_bar,image=align_right_icon)
align_right_btn.grid(row=0,column=8,padx=3)

# ------------------------------&&&  end end tool bar &&&&--------------------------------#

################################--text editing  ##########################################

text_editer=tk.Text(main_application)
text_editer.config(wrap='word',relief=tk.FLAT)

#creating scroll bar means wo baju ka niche lene ka
scroll_bar=tk.Scrollbar(main_application)#this called scroll bar class 
# focusing on text curser / curser creatung
text_editer.focus_set()#in this line we are setting only the curser
scroll_bar.pack(side=tk.RIGHT,fill=tk.Y) #y means top down
text_editer.pack(fill=tk.BOTH,expand=True)#here we are moving the curser value
scroll_bar.config(command=text_editer.yview)#ye batane ke liye ki scroll bar text editer ke liye hai isliye ise istemal kiya hai 
text_editer.config(yscrollcommand=scroll_bar.set)

# font family and font size finctionality
current_font_family='Arial'
current_font_size=12
def change_font(event=None):
    global current_font_family     #uper ka flobal varible yaha inisialize kare 
    current_font_family=font_family.get() #it will change according to the user select family
    text_editer.configure(font=(current_font_family,current_font_size))

def change_font_size(event=None):
    global current_font_size
    current_font_size=size_var.get()
    text_editer.configure(font=(current_font_family,current_font_size))

# binding the size
font_size.bind("<<ComboboxSelected>>",change_font_size)  #change_font_size is for size function                   

# binding means comile hona aur call karna 
font_box.bind("<<ComboboxSelected>>",change_font) #this is bind fuction

###############buttons functionality-----------------

def change_bold():
    text_property=tk.font.Font(font=text_editer['font'])#this is bold function
    #this is propert of obove fuction text_property we have to change according to that property
#{'family': 'Courier New', 'size': 10, 'weight': 'normal', 'slant': 'roman', 'underline': 0, 'overstrike': 0//}
    if text_property.actual()['weight']=='normal':
        text_editer.configure(font=(current_font_family,current_font_size,'bold'))
    if text_property.actual()['weight']=='bold':
        text_editer.configure(font=(current_font_family,current_font_size,'normal'))

bold_btn.configure(command=change_bold)

def change_to_italic():
    text_property=tk.font.Font(font=text_editer['font'])
    if text_property.actual()['slant']=='roman':
        text_editer.configure(font=(current_font_family,current_font_size,'italic'))
    if text_property.actual()['slant']=='italic':
        text_editer.configure(font=(current_font_family,current_font_size,'roman'))

italic_btn.configure(command=change_to_italic)

def underline_text():
    text_property=tk.font.Font(font=text_editer['font'])
    if text_property.actual()['underline']==0:
        text_editer.configure(font=(current_font_family,current_font_size,'underline'))
    if text_property.actual()['underline']==1:
        text_editer.configure(font=(current_font_family,current_font_size,'normal')) 

under_line_btn.configure(command=underline_text)

# -----------functionality of font color -------------------------

def change_font_color():
    color_var=tk.colorchooser.askcolor()
    text_editer.configure(fg=color_var[1])

font_color_btn.configure(command=change_font_color)

# -----------------------align functionality------------------------------
def align_left():
    text_content=text_editer.get(1.0,'end') #this lines means gets the value from starting to end
    text_editer.tag_config('left',justify=tk.LEFT)
    text_editer.delete(1.0,tk.END)#this line delete the from 1 to end position
    text_editer.insert(tk.INSERT,text_content,'left')

align_left_btn.config(command=align_left)

def align_center():
    text_content=text_editer.get(1.0,'end') #this lines means gets the value from starting to end
    text_editer.tag_config('center',justify=tk.CENTER)
    text_editer.delete(1.0,tk.END)#this line delete the from 1 to end position
    text_editer.insert(tk.INSERT,text_content,'center')

align_center_btn.config(command=align_center)

def align_right():
    text_content=text_editer.get(1.0,'end') #this lines means gets the value from starting to end
    text_editer.tag_config('right',justify=tk.RIGHT)
    text_editer.delete(1.0,tk.END)#this line delete the from 1 to end position
    text_editer.insert(tk.INSERT,text_content,'right')

align_right_btn.config(command=align_right)


# setting default as text editer as Arial and 12
text_editer.config(font=('Arial',12))

# ------------------------------&&&  end text editing &&&&--------------------------------#

################################--main status bar  ##########################################
# creating status bar
status_bar=tk.Label(main_application,text='status bar')
status_bar.pack(side=tk.BOTTOM)

# fucntionality of status back
text_changed=False
def status_b(event=None):
    global text_changed
    if text_editer.edit_modified():#it checks wheter the user typed anything
        text_changed=True
        #if typed we need to count words for that
        words=len(text_editer.get(1.0,'end-1c').split())#claculating the lenght by spliting
        characters=len(text_editer.get(1.0,'end-1c'))#ths line is for counting characters
        status_bar.configure(text=f'characters : {characters} words : {words}')
        # u[to the above line it reads only one character and words]
    text_editer.edit_modified(False)


text_editer.bind("<<Modified>>",status_b)




# ------------------------------&&&  end main status bar &&&&--------------------------------#

################################--main menu functionality  ##########################################
# new functionality :->in new just it delete old data in window
url='' #the line is checks wethrt the file is empty or not
def new_file(event=None):
    global url
    url=''
    text_editer.delete(1.0,tk.END)
#after end of this code we need to mention command=new_file on new file 
file.add_command(label='new',image=new_icon,compound=tk.LEFT,accelerator='ctrl+n',command=new_file) 

#open functionalty
def open_file(event=None):
    global url #in this line we are url value
    url=filedialog.askopenfilename(initialdir=os.getcwd(),title='select file',filetypes=(('Text File','*.txt')
    ,('All files','*.*')))
    try:
        # here if user selected any data we opening and reaing the data
        with open(url,'r') as fr:
            text_editer.delete(1.0,tk.END)
            text_editer.insert(1.0,fr.read())
    except FileNotFoundError:
        return
    except:
        return
    main_application.title(os.path.basename(url))#after opening this file it will change the file title\
     
file.add_command(label='open',image=open_icon,compound=tk.LEFT,accelerator='Ctrl+O',command=open_file)

# save functionality
def save_file(event=None):
    global url
    try:
        #that below cide is for if our code already exists
        if url: #in this line if the file already exists reading file and converting into str
            content=text_editer.get(1.0,tk.END)
            with open(url ,'w',encoding='utf-8') as fw:
                # whatever we write in window just storing in the window and mivong to folder
                fw.write(content)
        else:
            url=filedialog.asksaveasfilename(mode='w',defaultextension='.txt',filetypes=(('Text File','*.txt')
            ,('All files','*.*')))
            content2=text_editer.get(1.0,tk.END)
            url.write(content2)
            url.close()
    except:
        return
file.add_command(label='save',image=save_icon,compound=tk.LEFT,accelerator='ctrl+s',command=save_file)
# save as fucntionality
def save_as_file(event=None):
    global url
    try:
        content=text_editer.get(1.0,tk.END)
        url=filedialog.asksaveasfile(mode='w',defaultextension='.txt',filetypes=(('Text File','*.txt'),('All files','*.*')))
        url.write(content)
        url.close()
    except:
        return

file.add_command(label='save_as',image=save_as_icon,compound=tk.LEFT,accelerator='Alt+s',command=save_as_file)

#exit functionality
def exit_func(event=None):
    global url,text_changed
    try:   
        if text_changed:
            mbox=messagebox.askyesnocancel('waring','do you want to save file')
            if mbox is True: #true means yes
                if url:
                    content=text_editer.get(1.0,tk.END)
                    with open(url,'w',encoding='utf-8') as fw:
                        fw.write(content)
                        main_application.destroy() #destroy means it exit the window
                        #upto the above line is for existing file
                else:
                    content2=text_editer.get(1.0,tk.END) #here we chamged to string bcuz it shows error sometime
                    #if file does not exist so we need to ask                  
                    url=filedialog.asksaveasfile(mode='w',defaultextension='.txt',filetypes=(('Text File','*.txt')
                    ,('All files','*.*')))
                     #this iis the path where we want to store
                    url.write(content2)#here we write all content
                    url.close()
                    main_application.destroy()
        #upto this is for yes
            elif mbox is False:
                main_application.destroy()
        else:
            main_application.destroy()
    except:
        return

file.add_command(label='exit',image=exit_icon,compound=tk.LEFT,command=exit_func)

#commands on file
#compound is store the commands to left one by one
# file.add_command(label='save',image=save_icon,compound=tk.LEFT,accelerator='ctrl+s',command=save_file)
# file.add_command(label='save_as',image=save_as_icon,compound=tk.LEFT,accelerator='ctrl+shift+s',command=save_as_file)
# file.add_command(label='exit',image=exit_icon,compound=tk.LEFT,command=exit_func)

# copy functionality
def copy_file():
    text_editer.event_generate("<Control c>")
edit.add_command(label='copy',image=copy_icon,compound=tk.LEFT,accelerator='ctrl+c',command=copy_file)


# adding command on edit menu
# edit.add_command(label='copy',image=copy_icon,compound=tk.LEFT,accelerator='ctrl+c',command=lambda : text_editer.event_generate("<Control c>"))
edit.add_command(label='paste',image=paste_icon,compound=tk.LEFT,accelerator='ctrl+v',command=lambda : text_editer.event_generate("<Control v>"))
edit.add_command(label='cut',image=cut_icon,compound=tk.LEFT,accelerator='ctrl+x',command=lambda : text_editer.event_generate("<Control x>"))
edit.add_command(label='clear_all',image=clear_all_icon,compound=tk.LEFT,command=lambda : text_editer.delete(1.0,tk.END))

#_------------------find functioanaity---------------------------------

def find_func(event=None):

    def find():
        word=find_input.get()#in this line we get what we entered in find entrt box
        text_editer.tag_remove('match','1.0',tk.END)
        matches=0
        # if user enters the word 
        if word:
            start_pos='1.0'
            while True :  #it checks all characters untill it matches
                start_pos=text_editer.search(word,start_pos,stopindex=tk.END)  #it start searching from 1th position
                if not start_pos: #it checks weather the input word is matching
                    break
                end_pos=f'{start_pos}+{len(word)}c'
                text_editer.tag_add('match',start_pos,end_pos)
                matches +=1 # here if match found it go on  increment
                start_pos=end_pos
                text_editer.tag_config('match',foreground='red',background='yellow')

    def replace():
          word=find_input.get() #with this line we get know which word is going to repalce
          replace_text=replace_input.get() #here we getting what user what user is want to replace
          content=text_editer.get(1.0,tk.END) #here is a content get from text editer
          #for replace weare using replace function
          new_content=content.replace(word,replace_text) #
          text_editer.delete(1.0,tk.END) #deleting all old content
          text_editer.insert(1.0,new_content)


    #creating another window
    find_dialogue=tk.Toplevel()
    find_dialogue.geometry('450x250+500+200')
    find_dialogue.title('Find')
    find_dialogue.resizable(0,0) #thsis line is for not resizing

    #creating frame
    find_frame=ttk.LabelFrame(find_dialogue,text='find/replace')
    find_frame.pack(pady=20)

    #creating labels
    text_find_label=ttk.Label(find_frame,text='Find :')
    text_replace_label=ttk.Label(find_frame,text='Replace')
    
    #creating entry boxes
    find_input=ttk.Entry(find_frame,width=30)
    replace_input=ttk.Entry(find_frame,width=30)

    #creating button
    find_btn=ttk.Button(find_frame,text='find',command=find)
    replace_btn=ttk.Button(find_frame,text='replace',command=replace)

    #label griding
    text_find_label.grid(row=0,column=0,padx=4,pady=4)
    text_replace_label.grid(row=1,column=0,padx=4,pady=4)

    #entry box griding
    find_input.grid(row=0,column=1,padx=4,pady=4)
    replace_input.grid(row=1,column=1,padx=4,pady=4)

    #button grid
    find_btn.grid(row=2,column=0,padx=4,pady=4)
    replace_btn.grid(row=2,column=1,padx=8,pady=4)
edit.add_command(label='find',image=find_icon,compound=tk.LEFT,accelerator='ctrl+f',command=find_func)

# ------------------funtionality of toolbar--------------------------------

show_toolbar=tk.BooleanVar()
show_toolbar.set(True)
show_statusbar=tk.BooleanVar()
show_statusbar.set(True)

def hide_toolbar():
    global show_toolbar
    if show_toolbar: #if it true than we need hide
        tool_bar.pack_forget() #this pack_forget fucntion will hide toolbar
        show_toolbar=False 
        #upto this it will hide permanently
    else:
        text_editer.pack_forget()
        status_bar.pack_forget()
        tool_bar.pack(side=tk.TOP,fill=tk.X)
        text_editer.pack(fill=tk.BOTH,expand=True)
        status_bar.pack(side=tk.BOTTOM)
        show_toolbar=True

def hide_statusbar():
    global show_statusbar
    if show_statusbar:
        status_bar.pack_forget()
        show_statusbar=False
    else:
        status_bar.pack(side=tk.BOTTOM)
        show_statusbar=True

# view check button
view.add_checkbutton(label='Tool_bar',onvalue=True,offvalue=0,variable=show_toolbar,image=toolbar_icon
,compound=tk.LEFT,command=hide_toolbar)#onvalue shows whether its on or not
#the variable is created because for to get know wether clickes on button or not
view.add_checkbutton(label='status_bar',onvalue=False,offvalue=1,variable=show_statusbar,image=statusbar_icon,
compound=tk.LEFT,command=hide_statusbar)

#color theme
def change_theme():
    choose_theme=theme_choice.get() #gettng theme from line 86
    color_tuple=color_dict.get(choose_theme)
    fg_color,bg_color=color_tuple[0],color_tuple[1]
    text_editer.config(background=bg_color,fg=fg_color)

count=0
for i in color_dict:
    color_theme.add_radiobutton(label=i,image=color_icons[count],variable=theme_choice,compound=tk.LEFT,command=change_theme)
    count+=1

# ------------------------------&&&  end main menu functionality &&&&--------------------------------#


main_application.config(menu=main_menu)#config is used to create main menu

#-----------------adding shortcut key---------------------------

main_application.bind("<Control-n>",new_file)
main_application.bind("<Control-o>",open_file)
main_application.bind("<Control-s>",save_file)
main_application.bind("<Alt-s>",save_as_file)
main_application.bind("<Control-q>",exit_func)
main_application.bind("<Control-f>",find_func)

main_application.mainloop()
