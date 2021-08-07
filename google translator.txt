from tkinter import * 
from tkinter import ttk
from gtts import gTTS
from playsound import playsound
import os
import googletrans
import textblob
from tkinter import messagebox as msg
from PIL import ImageTk,Image


class gui(Tk):
    def __init__(self):
        super(gui, self).__init__()
        self.title("Google Translate")  #TODO : APLICATION TITLE
        self.geometry("1030x450")   #TODO : APNICATION WIDTH AND HEIGHT
        self.resizable(0,0)     #TODO : SET NOT RESIZABLE SIZE
        self.wm_iconbitmap("google_translate.ico")    #TODO : SET APLICATION ICON

    #TODO : FOR TRANSLATE TEXT
    def trns_txt(self, *args):
        try:
            self.clt_value = self.txt_area.get(1.0,END)
            self.lan_key = googletrans.LANGUAGES.items()

            if self.txt_area.get(1.0,END):

                # Todo :dct language
                self.words = textblob.TextBlob(self.clt_value)
                self.lan = self.words.detect_language()

                #Todo : store language key and translate
                for self.key , self.value in googletrans.LANGUAGES.items():
                    if self.value == self.s_lan_cam_box.get():
                        self.word = self.words.translate(from_lang=self.lan, to=str(self.key))
                        self.output_area.delete(1.0,END)
                        self.output_area.insert(END,self.word)
        except EXCEPTION as e:
            msg.showerror("Error!","Something is wrong\n Chick your inter net and try again")

    #TODO : CLEAR TEXT
    def clr_op(self):
        try:
            self.txt_area.delete(1.0,"end")
            self.output_area.delete(1.0,"end")
        except EXCEPTION as e:
            pass

    #TODO : COPY FUNCTION
    def copy_func(self):
        try:
            self.output_area.clipboard_clear()
            self.output_area.clipboard_append(self.output_area.get(1.0,END))
        except EXCEPTION as e:
            return

    #TODO : TRANSLATE BUTTON
    def trans_btn(self):
        try:
            self.btn = Button(text = "Translate" , font = "lucida 15" , padx = 10 , pady = 5 , activebackground = "black" , activeforeground = "white" , command = self.trns_txt)
            self.btn.place(x = 450 , y =  225)
        except EXCEPTION as e:
            return

    #TODO : CLEAR BUTTON
    def clr_btn(self):
        try:
            self.btn1 = Button(text = "Clear" , font = "lucida 15" , padx = 10 , pady = 5 , activebackground = "black" , activeforeground = "white" , command = self.clr_op)
            self.btn1.place(x = 30 , y =  380)
        except EXCEPTION as e:
            return

    #TODO : SPEAKE TEXT
    def speak_txt(self, *args):
        try:
            self.mytext = self.txt_area.get(1.0 , "end-1c")
            self.words = textblob.TextBlob(self.mytext)
            self.language = self.words.detect_language()
            self.myobj = gTTS(text=self.mytext, lang=self.language, slow=False)
            self.myobj.save("./icon/output.mp3")
            playsound('./icon/output.mp3')
            os.remove("./icon/output.mp3")
        except Exception as e:
            msg.showerror("Error", "Check your internet connection and try angain")

    def speak_txt1(self, *args):
        try:
            self.mytext = self.output_area.get(1.0 , "end-1c")
            self.words = textblob.TextBlob(self.mytext)
            self.language = self.words.detect_language()
            self.myobj = gTTS(text=self.mytext, lang=self.language, slow=False)
            self.myobj.save("./icon/output.mp3")
            playsound('./icon/output.mp3')
            os.remove("./icon/output.mp3")
        except Exception as e:
            msg.showerror("Error", "Check your internet connection and try angain")

        #TODO : Speaker button
    def spk_txt(self):              
        try:
            self.speaker_icon = Image.open("./icon/speaker.png")
            self.re_sz_speaker_icon = self.speaker_icon.resize((60,40), Image.ANTIALIAS)
            self.r_sz_speaker = ImageTk.PhotoImage(self.re_sz_speaker_icon)

            self.spkr_btn = ttk.Button(image = self.r_sz_speaker, command = self.speak_txt)
            self.spkr_btn.place(x = 130 , y = 380)
        except Exception as e:
            msg.showerror("Error", "Check your internet connection and try angain")
    
    def spk_txt1(self):
        try:
            self.speaker_icon1 = Image.open("./icon/speaker1.png")
            self.re_sz_speaker_icon1 = self.speaker_icon1.resize((60,40), Image.ANTIALIAS)
            self.r_sz_speaker1 = ImageTk.PhotoImage(self.re_sz_speaker_icon1)

            self.spkr_btn1 = ttk.Button(image = self.r_sz_speaker1, command = self.speak_txt1)
            self.spkr_btn1.place(x = 815 , y = 380)
        except Exception as e:
            msg.showerror("Error", "Check your internet connection and try angain")


    #TODO : COPY BUTTON
    def copy_btn(self):
        try:
            self.btn2 = Button(text = "Copy" , font = "lucida 15" , padx = 10 , pady = 5 , activebackground = "black" , activeforeground = "white" , command = self.copy_func)
            self.btn2.place(x = 900 , y =  380)
        except EXCEPTION as e:
            return

    # TODO : APPLICATION HEADER
    def hdr_txt(self):
        try:
            self.g_t = Label(text = "Google Translate",font = ("lucida 20 bold") , pady = 15).pack()
        except EXCEPTION as e:
            return

    #TODO : FRAME ONE .
    def main_frm(self):
        try:
            self.main_frmm = Frame(self)
            self.main_frmm.pack(fill = X)
        except EXCEPTION as e:
            return

    def f_lan_com(self):
        self.clt_lan = googletrans.LANGUAGES
        try:
            self.l_lan = list(self.clt_lan.values())
            self.f_lan_cam_box = ttk.Combobox(self.main_frmm , value = self.l_lan , state = "r" , font = ("lucida 12"))
            self.f_lan_cam_box.grid(row = 0 , column = 0 , padx = 120)
            self.f_lan_cam_box.set("english")
        except EXCEPTION as e:
            return


    def s_lan_com(self):
        try:
            self.l_lan1 = list(self.clt_lan.values())
            self.s_lan_cam_box = ttk.Combobox(self.main_frmm, value=self.l_lan, state="r" , font = ("lucida 12"))
            self.s_lan_cam_box.grid(row=0, column=1 , pady = 10 , padx = 250)
            self.s_lan_cam_box.set("bengali")
        except EXCEPTION as e:
            return

    def txt_inpu_frm(self): #TODO : FRAME FOR TEXT AREA
        try:
            self.s_frm = Frame(self, bg= 'black')
            self.s_frm.place(x = 14 , y = 118 , width = 410 , height = 250)
        except EXCEPTION as e:
            return

    def txt_ntry(self):     #TODO : TEXT ENTRY
        try:
            self.txt_var = StringVar()
            self.txt_area = Text(self.s_frm, font = "arial 13", undo = True , width = 405 , height = 245 )
            self.txt_area.grid(row = 1 , column = 0)
            self.txt_area.focus()
        except EXCEPTION as e:
            return

#Todo : other side
    def thrd_frm(self):   #TODO : CREATING A FRAME FOR OUT PUT AREA
        try:
            self.trd_frm = Frame(self, bg= 'black')
            self.trd_frm.place(x = 600 , y = 118 , width = 410 , height = 250)
        except EXCEPTION as e:
            return

    def txt_output(self):# TODO : OUT PUT AREA
        try:
            self.output_area = Text(self.trd_frm, font = "arial 13" , bg = "white")
            self.output_area.grid(row = 1 , column = 0)
        except EXCEPTION as e:
            return

if __name__ == '__main__':
    window = gui()
    window.hdr_txt()
    window.main_frm()
    window.f_lan_com()
    window.s_lan_com()
    window.txt_inpu_frm()
    window.txt_ntry()
    window.thrd_frm()
    window.txt_output()
    window.trans_btn()
    window.clr_btn()
    window.copy_btn()
    window.spk_txt()
    window.spk_txt1()
    # window.speak_txt()

    window.mainloop()
